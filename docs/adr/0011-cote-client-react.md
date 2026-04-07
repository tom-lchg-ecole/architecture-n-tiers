# ADR-11 : Cote client React

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application necessite une interface web dynamique pour gerer l'import des factures, la consultation des donnees et les interactions utilisateur en temps reel.

Le framework front-end doit gerer :

- la construction d'une interface modulaire
- la gestion des etats de l'application
- la navigation fluide entre les ecrans
- l'integration simple avec les APIs serveur

## Options considerees pour le cote client

### Option 1 : Vue.js

**Avantages** :

- Prise en main rapide
- Structure claire pour des interfaces modernes

**Inconvenients** :

- Ecosysteme interne moins aligne avec les choix de l'equipe
- Reutilisation de composants existants plus limitee

### Option 2 : React

**Avantages** :

- Architecture orientee composants tres flexible
- Ecosysteme mature et largement adopte
- Integration efficace avec TypeScript

**Inconvenients** :

- Besoin de choix supplementaires (routing, state management)
- Courbe d'apprentissage sur les bonnes pratiques d'architecture

## Decision

**Le client web est developpe avec React et TypeScript.**

Choix retenu de maniere explicite :

- framework front-end : React
- langage : TypeScript
- cible : application web responsive (mobile, tablette, desktop)
- integration : consommation des APIs REST exposees par Express

## Consequences

- Le front-end beneficie d'une forte reutilisabilite via les composants React.
- Le projet doit fixer des conventions de structure pour limiter l'heterogeneite.
- L'ecosysteme React impose des choix complementaires (routing, etat, formulaires).
- Les evolutions UI sont plus rapides une fois le socle de composants stabilise.
