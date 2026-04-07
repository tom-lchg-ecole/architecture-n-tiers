# ADR-17 : GitHub pipeline release.yml pour la creation de release

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Le projet doit standardiser la creation des releases pour securiser le versioning et simplifier la distribution des versions applicatives.

Le pipeline release doit gerer :

- la generation d'une release depuis un tag/version
- la publication automatisee des artefacts
- la tracabilite des versions diffusees
- la reduction des operations manuelles repetitives

## Options considerees pour la creation de release

### Option 1 : Creation manuelle des releases

**Avantages** :

- Processus simple au depart
- Flexibilite complete sur chaque publication

**Inconvenients** :

- Forte dependance aux actions humaines
- Risque d'incoherence entre versions et contenus publies

### Option 2 : GitHub Actions avec workflow release.yml

**Avantages** :

- Processus de release standardise
- Publication plus rapide et reproductible
- Historique clair des versions

**Inconvenients** :

- Besoin de conventions strictes de versioning
- Configuration initiale des etapes de publication

## Decision

**La creation des releases est automatisee avec GitHub Actions via le workflow `release.yml`.**

Choix retenu de maniere explicite :

- outil : GitHub Actions
- fichier de workflow : `.github/workflows/release.yml`
- declenchement : publication depuis un tag/version Git
- resultat : creation de release GitHub et publication des artefacts associes

## Consequences

- Le versioning et la publication deviennent coherents et auditables.
- L'equipe doit respecter une discipline stricte sur les tags et conventions de release.
- Les erreurs de configuration du workflow impactent directement la diffusion des versions.
- La production des artefacts est standardisee et plus fiable dans le temps.
