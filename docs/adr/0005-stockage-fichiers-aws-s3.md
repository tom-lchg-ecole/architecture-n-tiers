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

**Les factures PDF sont stockées dans un bucket Amazon S3 dédié au projet.**

Choix retenu de manière explicite :

- service de stockage : Amazon S3
- objet stocké : fichiers PDF originaux des factures
- sécurité : accès via IAM et URLs signées pour téléchargement/visualisation
- application : seules les métadonnées et la clé S3 sont conservées en base MongoDB

## Conséquences

- La durabilité et la scalabilité du stockage sont renforcées pour accompagner la croissance.
- Le système dépend d'AWS et des coûts variables associés au volume et aux accès.
- La sécurité des accès impose une gestion stricte des permissions IAM et des URLs signées.
- Les workflows applicatifs doivent gérer explicitement la relation MongoDB (métadonnées) / S3 (fichier).
