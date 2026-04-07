# ADR-19 : Deploiement du backend separe

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Le backend a des contraintes techniques differentes du front-end (charge, securite, traitements asynchrones) et doit pouvoir evoluer independamment.

La strategie de deploiement serveur doit gerer :

- la scalabilite des APIs et traitements metier
- l'isolation des risques entre front-end et back-end
- le deploiement independant des composants
- la supervision specifique des services serveur

## Options considerees pour l'architecture de deploiement

### Option 1 : Deploiement front-end et back-end sur la meme unite

**Avantages** :

- Mise en place initiale simple
- Moins d'elements d'infrastructure a gerer

**Inconvenients** :

- Couplage fort des cycles de livraison
- Scalabilite limitee et moins fine
- Impact global en cas d'incident sur un composant

### Option 2 : Deploiement backend separe

**Avantages** :

- Evolution et scaling independants
- Meilleure isolation des incidents
- Gouvernance securite plus adaptee aux APIs

**Inconvenients** :

- Infrastructure plus complexe a orchestrer
- Besoin de gerer la communication reseau entre composants

## Decision

**Le backend est deploye separement du front-end, avec son propre cycle de livraison.**

Choix retenu de maniere explicite :

- unites de deploiement distinctes : front-end React et API Express
- scalabilite : backend ajustable independamment selon la charge API/OCR/IA
- exploitation : supervision backend dediee (logs, metriques, alertes)
- securite : configuration reseau et secrets backend isoles du front-end
