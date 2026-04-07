# ADR-6 : Architecture microservices

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit couvrir plusieurs domaines fonctionnels (gestion des factures, catégorisation IA, stockage des fichiers) avec des besoins d'évolution différents.

L'architecture doit gérer :

- la séparation des responsabilités entre modules
- la scalabilité de chaque domaine indépendamment
- la maintenance et l'évolution continue
- la communication entre services

## Options considérées pour l'architecture applicative

### Option 1 : Monolithe

**Avantages** :

- Développement initial plus rapide
- Déploiement plus simple au démarrage

**Inconvénients** :

- Couplage fort entre les modules
- Scalabilité globale moins flexible
- Maintenance plus complexe à long terme

### Option 2 : Architecture microservices

**Avantages** :

- Services indépendants et spécialisés
- Scalabilité par domaine fonctionnel
- Déploiement et évolution plus flexibles

**Inconvénients** :

- Complexité d'orchestration plus élevée
- Communication inter-services à gérer

## Décision

**Utilisation d'une architecture microservices**

Raisons principales :

- meilleure séparation des responsabilités
- évolution indépendante des services
- scalabilité adaptée aux besoins réels de chaque composant
- meilleure maintenabilité sur le long terme
