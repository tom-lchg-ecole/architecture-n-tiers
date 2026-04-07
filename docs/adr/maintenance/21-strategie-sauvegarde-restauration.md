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

**Utilisation de sauvegardes automatisees avec tests periodiques de restauration**

Raisons principales :

- securiser les donnees critiques du projet
- garantir la reprise en cas d'incident
- reduire les erreurs humaines
- augmenter la confiance en production
