# ADR-5 : Stockage des fichiers PDF sur AWS S3

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit conserver les fichiers PDF de factures de manière fiable, sécurisée et accessible depuis l'interface.

Le système de stockage doit gérer :

- l'upload des fichiers PDF
- la conservation à long terme
- la récupération rapide pour téléchargement et visualisation
- la gestion des droits d'accès

## Options considérées pour le stockage des fichiers PDF

### Option 1 : Stockage local sur le serveur applicatif

**Avantages** :

- Mise en place simple
- Coût initial faible

**Inconvénients** :

- Risque de perte de données en cas de panne
- Scalabilité limitée
- Gestion des sauvegardes plus complexe

### Option 2 : AWS S3 Bucket

**Avantages** :

- Haute durabilité des données
- Scalabilité automatique
- Intégration simple avec une application web
- Gestion fine des permissions

**Inconvénients** :

- Dépendance à un service cloud externe
- Coût variable selon usage et volume

## Décision

**Utilisation d'un bucket AWS S3 pour le stockage des fichiers PDF**

Raisons principales :

- meilleure fiabilité du stockage
- accès simplifié aux fichiers depuis l'application
- scalabilité adaptée à l'augmentation des volumes
- sécurité et contrôle d'accès robustes
