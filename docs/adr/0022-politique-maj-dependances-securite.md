# ADR-22 : Politique de mise a jour des dependances et securite

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Le projet utilise de nombreuses dependances (front-end, back-end, outils CI/CD, bibliotheques IA) qui evoluent et peuvent introduire des vulnerabilites.

La politique de maintenance securite doit gerer :

- la veille des vulnerabilites connues
- la mise a jour reguliere des dependances
- la priorisation des correctifs critiques
- la verification de non regression apres mise a jour

## Options considerees pour les mises a jour

### Option 1 : Mises a jour ad hoc uniquement en cas de probleme

**Avantages** :

- Effort limite a court terme
- Moins de changements frequents

**Inconvenients** :

- Accumulation de dette technique
- Exposition prolongee aux vulnerabilites
- Migrations plus risquées a long terme

### Option 2 : Politique de mises a jour planifiees avec scans securite

**Avantages** :

- Reduction du risque securite
- Evolutions plus progressives et maitrisables
- Meilleure stabilite globale du systeme

**Inconvenients** :

- Charge de maintenance recurrente
- Besoin d'automatiser une partie du suivi

## Decision

**Les dependances sont gerees avec une politique de mise a jour planifiee et controle securite systematique.**

Choix retenu de maniere explicite :

- frequence : revues periodiques des dependances front-end, backend et CI/CD
- securite : scans automatiques de vulnerabilites (npm audit / outils GitHub)
- priorisation : correctifs critiques traites en priorite
- validation : execution des tests avant fusion de toute mise a jour
