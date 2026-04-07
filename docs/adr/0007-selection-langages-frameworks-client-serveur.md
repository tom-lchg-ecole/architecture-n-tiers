# ADR-7 : Selection des langages et frameworks cote client et serveur

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application nécessite un socle technique cohérent entre le front-end et le back-end pour accélérer le développement et faciliter la maintenance.

Le choix des technologies doit gérer :

- la productivité de l'équipe de développement
- la maintenabilité du code sur le long terme
- la performance côté client et serveur
- l'intégration avec les services prévus (IA, base de données, stockage)

## Options considérées pour les langages et frameworks

### Option 1 : JavaScript (React + Express)

**Avantages** :

- Écosystème large
- Développement rapide
- Même langage côté client et serveur
- Équipe déjà formé

**Inconvénients** :

- Typage faible sans couche supplémentaire
- Risque d'erreurs détectées tardivement

### Option 2 : TypeScript (React + NestJS)

**Avantages** :

- Typage statique
- Meilleure robustesse du code
- Architecture back-end structurée
- Réutilisation des types entre client et serveur

**Inconvénients** :

- Courbe d'apprentissage plus élevée
- Temps de configuration initial plus important
- L'équipe ne connaît pas

## Décision

**La stack applicative retenue est TypeScript + React pour le client et TypeScript + Express pour le serveur.**

Choix retenu de manière explicite :

- langage principal : TypeScript (front-end et back-end)
- framework client : React
- framework serveur : Express
- objectif : partage des types et cohérence de la base de code sur toute la stack

## Conséquences

- Le typage statique réduit les erreurs d'intégration entre client et serveur.
- La vitesse de développement initiale est impactée par la configuration TypeScript.
- Le maintien d'un contrat de types partagé devient un actif central du projet.
- La montée en compétence TypeScript est nécessaire pour toute l'équipe.
