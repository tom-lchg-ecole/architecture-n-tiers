# ADR-16 : GitHub pipeline avec deploy.yml

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Le projet doit automatiser le deploiement pour reduire les erreurs manuelles et accelerer la mise en ligne des evolutions.

Le pipeline de deploiement doit gerer :

- le declenchement automatique sur des evenements GitHub
- la verification prealable (build, tests, qualite)
- le deploiement sur les environnements cibles
- la tracabilite des executions et des echecs

## Options considerees pour le pipeline de deploiement

### Option 1 : Deploiement manuel

**Avantages** :

- Mise en place initiale simple
- Controle humain direct

**Inconvenients** :

- Risque d'erreurs humaines
- Processus lent et non reproductible
- Difficile a scaler avec l'equipe

### Option 2 : GitHub Actions avec workflow deploy.yml

**Avantages** :

- Automatisation reproductible
- Integration native avec le repository
- Historique clair des executions

**Inconvenients** :

- Configuration initiale a cadrer
- Gestion securisee des secrets necessaire

## Decision

**Utilisation d'un pipeline GitHub Actions avec deploy.yml**

Raisons principales :

- fiabiliser le deploiement
- reduire les interventions manuelles
- accelerer la mise en production
- garantir la tracabilite complete des livraisons
