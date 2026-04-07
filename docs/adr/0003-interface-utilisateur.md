# ADR-3 : Conception de l'interface utilisateur

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit proposer une interface simple pour permettre aux utilisateurs d'importer, classer et consulter leurs documents PDF (factures, devis, etc.) sans complexité technique.

L'interface doit gérer :

- l'envoi de documents PDF en lot ou unitaire
- la visualisation des informations extraites
- la recherche et le filtrage des documents selon leur type
- l'accès au téléchargement des fichiers

## Options considérées

### Option 1 : Interface multi-pages classique

**Avantages** :

- Structure claire
- Mise en place rapide

**Inconvénients** :

- Navigation moins fluide
- Expérience utilisateur plus fragmentée

### Option 2 : Interface web moderne orientée composants

**Avantages** :

- Navigation fluide
- Réutilisation des composants
- Maintenance facilitée

**Inconvénients** :

- Mise en place initiale plus longue
- Besoin d'une organisation stricte des composants

## Décision

**L'interface utilisateur est réalisée en React.**

Choix retenu de manière explicite :

- framework front-end : React
- approche UI : single-page application (SPA) responsive
- structuration : composants partagés (écrans, formulaires, tableaux, filtres)
- intégration : appels API REST vers le backend Express

## Conséquences

- La navigation est plus fluide, avec une meilleure continuité des parcours utilisateur.
- La qualité de code dépend d'une architecture de composants claire et partagée.
- Le référencement SEO natif est moins favorable qu'avec un rendu côté serveur.
- La dette front-end peut croître vite sans conventions de structure et de state management.
