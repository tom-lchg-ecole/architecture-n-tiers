# ADR-13 : Creation d'une base de donnees NoSQL (MongoDB)

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit stocker des donnees facture heterogenes issues de l'OCR et des traitements IA, avec des champs pouvant evoluer dans le temps.

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

**Utilisation de MongoDB comme base NoSQL principale**

Raisons principales :

- adaptation naturelle aux donnees JSON evolutives
- rapidite de developpement et d'evolution du schema
- performances adaptees au cas d'usage documentaire
- coherence avec l'architecture orientee services du projet
