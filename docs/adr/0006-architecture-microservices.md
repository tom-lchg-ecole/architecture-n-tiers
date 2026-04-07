# ADR-6 : Architecture microservices

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit couvrir plusieurs domaines fonctionnels (gestion des factures, catégorisation IA, stockage des fichiers) avec des besoins d'évolution différents.

L'architecture doit gérer :

- la séparation des responsabilités entre modules
- la scalabilité de chaque domaine indépendamment
- la maintenance et l'évolution continue
- la communication entre services

## Options considérées pour l'architecture applicative

### Option 1 : Monolithe

**Avantages** :

- Développement initial plus rapide
- Déploiement plus simple au démarrage

**Inconvénients** :

- Couplage fort entre les modules
- Scalabilité globale moins flexible
- Maintenance plus complexe à long terme

### Option 2 : Architecture microservices

**Avantages** :

- Services indépendants et spécialisés
- Scalabilité par domaine fonctionnel
- Déploiement et évolution plus flexibles

**Inconvénients** :

- Complexité d'orchestration plus élevée
- Communication inter-services à gérer

## Décision

**L'architecture retenue est une architecture microservices, avec services déployables indépendamment.**

Choix retenu de manière explicite :

- découpage : service API métier, service OCR/IA, service de gestion documentaire
- communication : API HTTP internes entre services
- déploiement : chaque service versionné et déployé séparément
- données : MongoDB et S3 partagés via contrats d'accès définis

## Conséquences

- Les services peuvent évoluer et se déployer indépendamment selon les besoins métier.
- La complexité opérationnelle augmente (observabilité, orchestration, contrats inter-services).
- La robustesse dépend de la qualité des interfaces et de la gestion des erreurs réseau.
- L'équipe doit maintenir des standards transverses (auth, logs, tracing, versioning API).
