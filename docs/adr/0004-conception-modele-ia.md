# ADR-4 : Conception d'un modele d'IA

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit catégoriser automatiquement les documents PDF (factures, devis, etc.) à partir de leur contenu pour réduire le traitement manuel.

Le modèle d'IA doit gérer :

- l'analyse du texte extrait des documents PDF
- la proposition d'une catégorie pertinente pour identifier le type de document
- l'adaptation aux nouveaux types de documents
- une précision suffisante pour être utile en production

## Options considérées pour le modèle d'IA

### Option 1 : Règles métier statiques (sans apprentissage)

**Avantages** :

- Facile à mettre en place
- Résultats explicables

**Inconvénients** :

- Peu flexible
- Maintenance importante quand les cas évoluent

### Option 2 : Modèle de machine learning supervisé

**Avantages** :

- Meilleure adaptation aux variations de documents
- Précision plus élevée avec des données d'entraînement
- Amélioration continue possible

**Inconvénients** :

- Besoin de données annotées
- Coût initial d'entraînement

## Décision

**La catégorisation est réalisée avec un modèle de machine learning supervisé, entraîné sur des documents PDF annotés (factures, devis, etc.).**

Choix retenu de manière explicite :

- type de modèle : classification supervisée
- entrée : texte extrait des documents PDF (pipeline OCR)
- sortie : type de document prédit (facture, devis, etc.) puis catégorie métier associée
- cycle de vie : entraînement initial + réentraînements sur données internes validées

## Conséquences

- La performance du modèle dépend directement de la qualité et de la représentativité des données annotées.
- Un processus MLOps est nécessaire pour suivre les versions, métriques et réentraînements.
- Les erreurs de classification restent possibles et imposent un mécanisme de correction métier.
- Le coût d'exploitation augmente avec les besoins d'entraînement et de validation continue.
