# ADR-10 : Recuperation d'un data-set pour l'entrainement et les tests du modele

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Le modele IA de traitement des factures doit etre entraine et evalue sur des donnees representatives pour garantir des resultats fiables en production.

La strategie data doit gerer :

- la source du data-set d'entrainement
- la creation d'un data-set si les sources publiques sont insuffisantes
- la separation claire entre entrainement, validation et test
- des criteres de test mesurables pour valider la qualite du modele

## Options considerees pour constituer le data-set

### Option 1 : Data-sets publics uniquement

**Avantages** :

- Demarrage rapide
- Cout de collecte limite

**Inconvenients** :

- Donnees parfois eloignees du contexte metier reel
- Qualite et schema variables selon les sources

### Option 2 : Approche hybride (public + data-set interne annote)

**Avantages** :

- Base initiale rapide grace aux sources publiques
- Meilleure representativite via des factures reelles anonymisees
- Qualite controlee avec un schema cible unique

**Inconvenients** :

- Besoin d'un processus d'anonymisation
- Effort d'annotation et de validation humaine

## Decision

**Le data-set du modele IA est construit avec une approche hybride : jeux publics + jeu interne annote.**

Choix retenu de maniere explicite :

- source 1 : data-sets publics pour initialiser l'entrainement
- source 2 : factures internes anonymisees, annotees selon le schema JSON cible
- gouvernance data : separation obligatoire entrainement/validation/test
- qualite : validation du modele sur un jeu de test gele representatif du contexte metier

## Mise en oeuvre retenue

Sources de data-set :

- Sources publiques de documents OCR/factures pour initialiser les experiments
- Factures internes anonymisees pour couvrir les cas metiers cibles

Si aucun data-set adequat n'est disponible :

- Collecter un lot de factures reelles representatif
- Anonymiser toutes les donnees sensibles
- Definir un guide d'annotation (champs obligatoires, formats, regles)
- Annoter manuellement puis faire une revue qualite par echantillonnage

Strategie de test du modele :

- Split des donnees : entrainement (70%), validation (15%), test (15%)
- Jeu de test gele (jamais utilise pour l'entrainement)
- Metriques principales : precision, rappel, F1-score par champ extrait
- Tests de robustesse sur PDF bruites, scans de faible qualite, formats heterogenes
- Critere de validation avant production : seuil minimal de F1 global et par champ critique
