# ADR-1 : Définition de l'application

## Date

07/04/2026

## Status

Approuvé

## Contexte

Créer une application de gestion de factures avec catégorisation automatique par IA et remplissage des champs.

## Options considérées

### Option 1 : Outil de stockage documentaire sans intelligence

**Avantages** :

- Mise en place rapide
- Faible complexité technique

**Inconvénients** :

- Forte charge manuelle de saisie et de classement
- Peu de valeur métier sur l'automatisation

### Option 2 : Application de gestion de factures avec OCR, IA et contrôle d'accès

**Avantages** :

- Réduction du temps de traitement des factures
- Standardisation des données extraites
- Sécurisation de l'accès aux informations financières

**Inconvénients** :

- Architecture plus complexe (OCR, IA, stockage, sécurité)
- Besoin de gouvernance des modèles et des données

## Décision

**Le projet met en place une application de gestion de factures avec extraction OCR, catégorisation IA et authentification par rôles.**

Choix retenu de manière explicite :

- périmètre : import, consultation, recherche, téléchargement et gestion des factures
- automatisation : extraction des données PDF et catégorisation automatique
- sécurité : authentification et contrôle d'accès selon les rôles
- architecture : séparation front-end, backend, stockage documentaire et traitement IA

## Conséquences

- Le système nécessite une architecture n-tiers pour isoler les responsabilités front, API, données et IA.
- La qualité globale dépend du pipeline OCR/IA et impose une stratégie de tests et d'amélioration continue.
- La gestion des données sensibles impose des contraintes de sécurité, traçabilité et gouvernance.
- Le périmètre fonctionnel est clair et sert de base aux ADR techniques suivants.

## Objectif

Améliorer, simplifier et faire gagner du temps sur l'organisation des factures d'une entreprise.

## Fonctionnalités attendues

### Gestion des factures

- Envoi de factures multiples
- Glisser-déposer
- Téléchargement des factures
- CRUD des factures

### Catégorisation

- Factures automatiquement catégorisées en fonction de leur contenu

### Authentification

- Connexion sécurisée des utilisateurs
- Gestion des sessions et déconnexion
- Contrôle d'accès selon les rôles (administrateur, utilisateur)
