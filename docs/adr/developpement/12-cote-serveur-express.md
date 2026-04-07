# ADR-12 : Cote serveur Express

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Le back-end doit exposer des APIs pour gerer les factures, orchestrer les traitements OCR/IA et communiquer avec la base de donnees et le stockage des fichiers.

Le framework serveur doit gerer :

- la creation d'APIs REST
- la gestion des middlewares (authentification, validation, erreurs)
- la performance des traitements asynchrones
- une structure simple a maintenir

## Options considerees pour le cote serveur

### Option 1 : NestJS

**Avantages** :

- Architecture tres structuree
- Bonne integration TypeScript

**Inconvenients** :

- Plus de conventions a assimiler au demarrage
- Surcout initial pour un perimetre fonctionnel simple

### Option 2 : Express

**Avantages** :

- Leger et rapide a mettre en place
- Ecosysteme large et mature
- Grande flexibilite d'implementation

**Inconvenients** :

- Architecture a structurer manuellement
- Risque d'heterogeneite sans conventions internes

## Decision

**Utilisation d'Express pour le cote serveur**

Raisons principales :

- mise en place rapide des APIs metier
- flexibilite adaptee au projet
- ecosysteme mature pour les integrations necessaires
- maintenance simple avec une convention de structure claire
