# ADR-1 : Définition de l'application

## Date

07/04/2026

## Status

Approuvé

## Contexte

Créer une application de gestion de documents PDF (factures, devis, etc.) avec catégorisation automatique par IA et remplissage des champs.

## Options considérées

### Option 1 : Outil de stockage documentaire sans intelligence

**Avantages** :

- Mise en place rapide
- Faible complexité technique

**Inconvénients** :

- Forte charge manuelle de saisie et de classement
- Peu de valeur métier sur l'automatisation

### Option 2 : Application de gestion de documents PDF avec OCR, IA et contrôle d'accès

**Avantages** :

- Réduction du temps de traitement des documents PDF
- Standardisation des données extraites
- Sécurisation de l'accès aux informations financières

**Inconvénients** :

- Architecture plus complexe (OCR, IA, stockage, sécurité)
- Besoin de gouvernance des modèles et des données

## Décision

**Le projet met en place une application de gestion de documents PDF avec extraction OCR, catégorisation IA et authentification par rôles.**

Choix retenu de manière explicite :

- périmètre : import, consultation, recherche, téléchargement et gestion de documents PDF variés (factures, devis, etc.)
- automatisation : extraction des données PDF et catégorisation automatique pour identifier le type de document traité
- sécurité : authentification et contrôle d'accès selon les rôles
- architecture : séparation front-end, backend, stockage documentaire et traitement IA

## Conséquences

- Le système nécessite une architecture n-tiers pour isoler les responsabilités front, API, données et IA.
- La qualité globale dépend du pipeline OCR/IA et impose une stratégie de tests et d'amélioration continue.
- La gestion des données sensibles impose des contraintes de sécurité, traçabilité et gouvernance.
- Le périmètre fonctionnel est clair et sert de base aux ADR techniques suivants.

## Objectif

Améliorer, simplifier et faire gagner du temps sur l'organisation des documents d'une entreprise.

## Fonctionnalités attendues

### Gestion des documents PDF

- Envoi de documents PDF multiples
- Glisser-déposer
- Téléchargement des documents PDF
- CRUD des documents PDF

### Catégorisation

- Documents PDF automatiquement catégorisés en fonction de leur contenu (facture, devis, etc.)

### Authentification

- Connexion sécurisée des utilisateurs
- Gestion des sessions et déconnexion
- Contrôle d'accès selon les rôles (administrateur, utilisateur)
