# ADR-13 : Creation d'une base de donnees NoSQL (MongoDB)

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit stocker des donnees documentaires heterogenes issues de l'OCR et des traitements IA, avec des champs pouvant evoluer dans le temps.

La base de donnees doit gerer :

- un schema flexible pour les donnees JSON
- de bonnes performances en lecture et ecriture
- la scalabilite pour la croissance du volume de documents
- une integration simple avec le serveur applicatif

## Options considerees pour la base de donnees

### Option 1 : PostgreSQL

**Avantages** :

- Robustesse relationnelle
- Support SQL puissant

**Inconvenients** :

- Evolution du schema plus contraignante
- Moins naturel pour des donnees tres variables

### Option 2 : MongoDB

**Avantages** :

- Stockage natif de documents JSON
- Schema flexible pour les donnees OCR/IA
- Bonne scalabilite horizontale

**Inconvenients** :

- Normalisation relationnelle moins stricte
- Vigilance necessaire sur la modelisation des collections

## Decision

**La base de donnees principale est MongoDB, utilisee comme base NoSQL documentaire.**

Choix retenu de maniere explicite :

- SGBD : MongoDB
- format de stockage : documents BSON (JSON)
- perimetre : metadonnees des documents PDF, resultats OCR/IA, references de fichiers S3
- schema : flexible mais contraint par des validations applicatives cote backend

## Consequences

- Les donnees variables OCR/IA sont mieux prises en charge grace au schema flexible.
- Le controle de qualite des donnees repose davantage sur l'application que sur le SGBD.
- Les performances exigent une strategie d'indexation adaptee aux requetes reelles.
- Les evolutions de modelisation sont plus rapides mais doivent rester gouvernees.
