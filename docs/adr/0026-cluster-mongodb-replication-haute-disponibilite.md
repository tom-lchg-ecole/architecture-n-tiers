# ADR-26 : Cluster MongoDB — Réplication et Haute Disponibilité

## Date

09/04/2026

## Status

Approuvé

---

## 1. Contexte et problème

L'application gère des documents PDF critiques (factures, devis) avec un pipeline OCR/IA qui produit des données structurées stockées dans MongoDB. Ces données représentent une valeur métier forte : perte ou indisponibilité = impact direct sur les utilisateurs.

Le système doit garantir :

- la continuité de service en cas de défaillance d'un nœud
- l'intégrité des données malgré des écritures concurrentes
- une reprise automatique sans intervention manuelle
- des performances acceptables en lecture pour un usage concurrent

---

## 2. Choix de la technique de réplication

### Options considérées

#### Option 1 : Réplication synchrone

Chaque écriture est validée sur **tous les nœuds avant d'être confirmée** à l'application.

**Avantages** :
- Cohérence stricte des données (pas de perte possible)
- Tous les nœuds sont toujours à jour

**Inconvénients** :
- Latence d'écriture élevée (attente de tous les nœuds)
- Disponibilité réduite si un nœud est lent ou injoignable
- Non supporté nativement par MongoDB

#### Option 2 : Réplication asynchrone (Replica Set MongoDB natif)

Le nœud primaire confirme l'écriture **immédiatement**, les secondaires répliquent en arrière-plan via l'oplog.

**Avantages** :
- Latence d'écriture faible
- Disponibilité élevée (le primaire n'attend pas les secondaires)
- Support natif MongoDB avec failover automatique

**Inconvénients** :
- Risque de perte de quelques opérations en cas de crash du primaire avant réplication

#### Option 3 : Réplication semi-synchrone (write concern `majority`)

L'écriture est confirmée dès qu'une **majorité de nœuds** (primaire + au moins 1 secondaire) a persiste l'opération.

**Avantages** :
- Compromis performance / durabilité
- Élimine le risque de perte de données sur les écritures critiques
- Supporté nativement par MongoDB via le paramètre `writeConcern`

**Inconvénients** :
- Légère latence supplémentaire sur les écritures critiques
- Nécessite au moins 3 nœuds pour que la majorité ait du sens

### Décision

**La technique retenue est la réplication asynchrone via MongoDB Replica Set, avec write concern `majority` sur les opérations critiques.**

| Type d'opération | Write Concern | Justification |
|---|---|---|
| Upload document (création) | `majority` | Donnée critique, pas de perte acceptable |
| Mise à jour statut (pending → processing) | `majority` | Cohérence du pipeline OCR/IA |
| Stockage résultats OCR/IA | `majority` | Résultat du traitement, non reproductible |
| Logs applicatifs | `w: 1` (défaut) | Tolérance à la perte acceptable |

Cette approche combine la **performance** de l'asynchrone pour les opérations non critiques et la **durabilité** du semi-synchrone pour les données métier.

---

## 3. Configuration du cluster

### Options considérées

#### Option 1 : Actif-Actif (sharding)

Plusieurs nœuds acceptent des lectures **et des écritures** simultanément, les données sont partitionnées entre eux.

**Avantages** :
- Scalabilité horizontale des écritures
- Aucun SPOF pour les écritures

**Inconvénients** :
- Complexité opérationnelle élevée (config servers, mongos routers)
- Transactions cross-shard coûteuses
- Inadapté au volume actuel du projet
- Cohérence plus difficile à garantir

#### Option 2 : Actif-Passif (Replica Set 1 Primary + 2 Secondaries)

Un seul nœud primaire accepte les écritures. Les secondaires répliquent et peuvent servir les lectures non critiques. En cas de panne du primaire, élection automatique d'un nouveau primaire.

**Avantages** :
- Modèle natif et recommandé MongoDB
- Failover automatique (< 30 secondes)
- Secondaires utilisables pour les lectures (dashboard admin, reporting)
- Simplicité opérationnelle

**Inconvénients** :
- Un seul point d'écriture (goulot si charge très élevée)
- Fenêtre de quelques secondes d'indisponibilité lors d'une élection

### Décision

**Le cluster fonctionne en mode Actif-Passif avec un MongoDB Replica Set à 3 nœuds : 1 Primary + 2 Secondaries.**

Configuration retenue :

| Nœud | Rôle | Votes | Priority | Lectures |
|---|---|---|---|---|
| mongo-primary | Primary | 1 | 2 | Oui (écritures + lectures critiques) |
| mongo-secondary-1 | Secondary | 1 | 1 | Oui (lectures non critiques, reporting) |
| mongo-secondary-2 | Secondary | 1 | 1 | Oui (lectures non critiques, backup) |

- **Priority** : le primaire a une priorité plus haute pour redevenir primaire après redémarrage
- **3 nœuds** : garantit qu'une majorité (2/3) est toujours atteignable même si un nœud tombe

---

## 4. Stratégies de haute disponibilité

### 4.1 Failover automatique

MongoDB Replica Set intègre un mécanisme d'élection automatique :

1. Chaque nœud envoie un **heartbeat** toutes les 2 secondes aux autres
2. Si le primaire ne répond plus après **10 secondes** (electionTimeoutMillis), les secondaires déclenchent une élection
3. Le secondaire avec la priority la plus haute et l'oplog le plus à jour est élu primaire
4. Le basculement est transparent pour l'application via le **driver MongoDB** qui gère le retry automatique

**Temps de basculement estimé** : 10–30 secondes

### 4.2 Read preference

Configuration de la lecture selon les cas d'usage :

| Cas d'usage | Read Preference | Justification |
|---|---|---|
| Consultation d'un document après upload | `primary` | Cohérence forte requise |
| Recherche / filtrage (liste) | `secondaryPreferred` | Lecture tolérante au léger décalage |
| Dashboard admin / reporting | `secondary` | Décharge le primaire |
| Pipeline OCR/IA (lecture avant traitement) | `primary` | Données critiques, cohérence stricte |

### 4.3 Gestion des défaillances

| Scénario | Comportement attendu |
|---|---|
| Panne du nœud Secondary | Cluster continue normalement (2 nœuds restants, majorité conservée) |
| Panne du nœud Primary | Élection automatique du nouveau Primary en < 30 s, driver reconnecte |
| Panne de 2 nœuds sur 3 | Cluster passe en lecture seule (pas de majorité pour élire un Primary) |
| Split-brain réseau | Seule la partition avec majorité reste opérationnelle en écriture |
| Corruption de données | Restauration depuis backup S3 ou resync depuis un Secondary sain |

### 4.4 Sauvegardes (complément ADR-21)

- **mongodump** planifié toutes les 24h sur le Secondary (sans impacter le Primary)
- Résultat archivé dans **AWS S3 (zone dédiée backup)**
- Test de restauration mensuel documenté
- Retention : 30 jours glissants

### 4.5 Monitoring du cluster

Métriques à surveiller en priorité :

- **replication lag** : délai de réplication entre Primary et Secondaries (alerte si > 10 s)
- **oplog window** : durée couverte par l'oplog (alerte si < 24 h)
- **election count** : nombre d'élections déclenchées (indicateur d'instabilité réseau)
- **connections** : nombre de connexions actives par nœud
- **write concern failures** : échecs de `majority` (réseau ou nœud lent)

---

## 5. Conséquences

- La disponibilité est assurée même en cas de panne d'un nœud, sans intervention manuelle.
- Les écritures critiques (documents, résultats OCR/IA) ne sont jamais perdues grâce au write concern `majority`.
- La charge de lecture est distribuable sur les Secondaries pour les cas non critiques.
- L'opérabilité reste simple avec 3 nœuds : pas besoin de config servers ni de mongos.
- Une panne simultanée de 2 nœuds bloque les écritures (cas rare mais à documenter dans le runbook).
- Le monitoring du replication lag devient un indicateur opérationnel critique à surveiller.
