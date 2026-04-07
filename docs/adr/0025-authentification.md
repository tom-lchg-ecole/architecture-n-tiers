# ADR-25 : Authentification

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application de gestion de documents PDF doit proteger l'acces aux donnees sensibles et limiter les actions selon le profil utilisateur.

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

**Le mecanisme d'authentification retenu est JWT (access token) avec refresh token, et autorisation par roles (RBAC).**

Choix retenu de maniere explicite :

- authentification : JSON Web Token signe cote backend Express
- gestion de session : refresh token pour renouveler les access tokens
- autorisation : controle d'acces par role (administrateur, utilisateur)
- transport : token transmis dans les appels API REST securises

## Consequences

- L'authentification s'aligne bien avec une API REST et des clients multiplateformes.
- La revocation et la rotation des tokens doivent etre traitees explicitement.
- La surface de risque impose une gestion stricte des secrets de signature et des durees de vie.
- Les controles RBAC doivent etre testes et appliques sur tous les endpoints sensibles.
