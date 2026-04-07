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

**Le deploiement est automatise avec GitHub Actions via le workflow `deploy.yml`.**

Choix retenu de maniere explicite :

- outil CI/CD : GitHub Actions
- fichier de workflow : `.github/workflows/deploy.yml`
- etapes minimales : build, tests, puis deploiement cible
- securite : secrets de deploiement geres dans GitHub Secrets

## Consequences

- Les deploiements deviennent plus reproductibles et moins dependants des operations manuelles.
- Une panne du pipeline ou une mauvaise configuration peut bloquer les livraisons.
- La gestion des secrets et des permissions GitHub devient un point de securite majeur.
- Les modifications d'infrastructure doivent etre synchronisees avec les workflows CI/CD.
