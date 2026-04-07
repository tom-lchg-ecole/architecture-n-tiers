# ADR-21 : Strategie de sauvegarde et restauration

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Les donnees metier (MongoDB, fichiers PDF, metadonnees OCR/IA) doivent etre protegees contre la perte, la corruption ou une erreur de manipulation.

La strategie de backup doit gerer :

- la sauvegarde periodique des donnees critiques
- la restauration testee et reproductible
- des objectifs RPO/RTO adaptes au projet
- la conservation securisee des sauvegardes

## Options considerees pour la protection des donnees

### Option 1 : Sauvegardes manuelles ponctuelles

**Avantages** :

- Mise en place simple
- Cout operationnel initial faible

**Inconvenients** :

- Risque d'oubli et d'incoherence
- Faible garantie de restauration rapide
- Processus non fiable en situation de crise

### Option 2 : Sauvegardes automatisees avec tests de restauration

**Avantages** :

- Processus fiable et repetable
- Reduction du risque de perte de donnees
- Verification reguliere de la capacite de reprise

**Inconvenients** :

- Besoin d'automatisation et de suivi
- Cout de stockage supplementaire

## Decision

**La protection des donnees repose sur des sauvegardes automatisees et des tests de restauration planifies.**

Choix retenu de maniere explicite :

- sauvegardes : automatisation reguliere pour MongoDB et fichiers PDF sur S3
- restauration : exercices periodiques documentes avec verification de bout en bout
- objectifs : respecter les contraintes RPO/RTO definies pour le projet
- retention : conservation securisee des sauvegardes selon une politique formelle

## Consequences

- Le risque de perte de donnees est reduit avec une reprise testee.
- Le projet doit assumer des couts de stockage et d'automatisation supplementaires.
- Les exercices de restauration deviennent obligatoires pour valider le dispositif.
- Les objectifs RPO/RTO doivent etre suivis et reevalues avec la croissance du systeme.
