# ADR-4 : Conception d'un modele d'IA

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit catégoriser automatiquement les factures à partir de leur contenu pour réduire le traitement manuel.

Le modèle d'IA doit gérer :

- l'analyse du texte extrait des factures
- la proposition d'une catégorie pertinente
- l'adaptation aux nouveaux types de factures
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

**Utilisation d'un modèle de machine learning supervisé**

Raisons principales :

- meilleure qualité de catégorisation
- capacité d'apprentissage sur les données réelles
- adaptation plus simple à l'évolution des formats de factures
- réduction des corrections manuelles dans le temps
