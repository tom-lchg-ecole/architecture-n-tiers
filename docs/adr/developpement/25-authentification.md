# ADR : Authentification

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application de gestion de factures doit proteger l'acces aux donnees sensibles et limiter les actions selon le profil utilisateur.

Le mecanisme d'authentification doit assurer :

- l'identification fiable des utilisateurs
- la securisation des sessions
- la gestion des autorisations par role
- une integration simple avec l'API Express

## Options considerées pour l'authentification

### Option 1 : Session serveur (cookie + stockage serveur)

**Avantages** :

- Revocation de session simple cote serveur
- Bon controle de la duree de vie des sessions
- Pattern adapte aux applications web classiques

**Inconvenients** :

- Besoin d'un stockage de session partage en cas de scalabilite horizontale
- Gestion CSRF a traiter explicitement

### Option 2 : JWT (token signe)

**Avantages** :

- Statelesse cote serveur pour l'authentification
- Integration simple avec API REST et clients multiples
- Bonne compatibilite avec architecture n-tiers

**Inconvenients** :

- Revocation des tokens plus complexe
- Exposition au risque en cas de fuite de token non expire

## Decision

**Utilisation de JWT avec refresh token et controle d'acces par role**

Raisons principales :

- integration fluide avec le back-end Express et les APIs REST
- support des clients web, mobile et tablette
- separation claire entre authentification et autorisation
- evolution simple vers des besoins de scalabilite
