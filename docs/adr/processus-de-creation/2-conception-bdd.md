# ADR-2 : Conception

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Réflexion sur tout ce que nous devons faire pour réaliser l'application.

Notre application doit gérer une partie front-end et back-end, ainsi qu'une partie stockage, pour accéder plus tard aux fichiers .pdf, dans le cas où nous voudrions les visualiser ou les télécharger.

La base de données doit gérer :

- le stockage des données extraites des fichiers PDF
- le stockage du lien d'accès aux fichiers
- la sauvegarde de la catégorisation des fichiers

## Options considérées pour la base de données

### Option 1 : MySQL

**Avantages** :

- Large communauté

**Inconvénients** :

- Support JSON moins mature que PostgreSQL
- Performances JSON inférieures dans nos benchmarks

### Option 2 : NoSQL

**Avantages** :

- Flexibilité
- Support JSON

**Inconvénients** :

- Coût plus élevé à grande échelle

## Décision

**Utilisation de MongoDB**

Raisons principales :

- Support JSON
- Schéma flexible
- Développement plus rapide
- Données imbroquées
- Scalabilité
