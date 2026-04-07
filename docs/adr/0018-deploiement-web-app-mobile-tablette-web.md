# ADR-18 : Deploiement de la web app compatible mobile, tablette et web

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

La web app doit offrir une experience utilisateur coherente sur mobile, tablette et ordinateur sans multiplier les applications a maintenir.

La strategie de deploiement front-end doit gerer :

- la compatibilite multi-formats d'ecran
- la diffusion rapide des mises a jour
- les performances d'affichage sur differents terminaux
- la simplification de la maintenance de l'interface

## Options considerees pour la diffusion multi-support

### Option 1 : Applications separees par support

**Avantages** :

- Optimisation fine par plateforme
- Controle specifique des parcours utilisateur

**Inconvenients** :

- Cout de developpement et maintenance eleve
- Risque de divergence fonctionnelle entre supports

### Option 2 : Web app responsive unique

**Avantages** :

- Base de code unique
- Deploiement centralise et rapide
- Maintenance simplifiee

**Inconvenients** :

- Besoin d'un travail UI/UX rigoureux sur les breakpoints
- Ajustements necessaires pour certains usages mobiles

## Decision

**Le front-end est deploye sous forme d'une seule web app responsive pour mobile, tablette et desktop.**

Choix retenu de maniere explicite :

- application : une base de code React unique
- adaptation ecran : responsive design avec breakpoints
- diffusion : meme artefact front-end pour tous les supports web
- maintenance : une seule chaine de build et de deploiement

## Consequences

- La maintenance front-end est simplifiee avec une seule base de code.
- L'experience mobile depend fortement de la qualite du responsive design.
- Les mises a jour sont diffusees plus vite sur tous les supports web.
- Certains usages mobiles avances peuvent necessiter des adaptations specifiques.
