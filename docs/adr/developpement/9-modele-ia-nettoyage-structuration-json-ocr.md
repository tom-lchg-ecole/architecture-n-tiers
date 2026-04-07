# ADR-9 : Modele IA pour nettoyer, organiser et restructurer le JSON OCR

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Les donnees OCR brutes peuvent contenir du bruit, des champs incoherents et une structure variable selon les factures.

Le composant de post-traitement doit gerer :

- le nettoyage des valeurs invalides ou ambiguës
- la normalisation des formats (dates, montants, devise)
- la reorganisation des champs dans un schema JSON unique
- la preparation des donnees pour la categorisation et le stockage

## Options considerees pour le post-traitement des donnees OCR

### Option 1 : Pipeline de regles statiques

**Avantages** :

- Resultats predictibles
- Mise en oeuvre simple au demarrage

**Inconvenients** :

- Difficile a maintenir avec des formats varies
- Faible capacite d'adaptation aux nouveaux cas

### Option 2 : Modele IA de transformation de donnees

**Avantages** :

- Meilleure adaptation aux variations de structure
- Normalisation plus robuste des champs
- Evolution continue possible avec des exemples reels

**Inconvenients** :

- Besoin de validation des sorties
- Cout de mise au point initial

## Decision

**Utilisation d'un modele IA pour nettoyer et restructurer le JSON OCR**

Raisons principales :

- meilleure qualite de donnees en sortie
- schema JSON plus coherent pour les services en aval
- reduction des corrections manuelles
- adaptation plus rapide a de nouveaux formats de factures
