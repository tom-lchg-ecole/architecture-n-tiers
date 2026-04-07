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

**Utilisation d'une web app responsive unique pour mobile, tablette et web**

Raisons principales :

- reduire la complexite de maintenance
- accelerer la livraison des evolutions
- garantir une experience coherente sur tous les ecrans
- optimiser le cout global de deploiement front-end
