# ADR-9 : Modele IA pour nettoyer, organiser et restructurer le JSON OCR

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Les donnees OCR brutes peuvent contenir du bruit, des champs incoherents et une structure variable selon les types de documents PDF.

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

**Le post-traitement OCR est assure par un modele IA dedie au nettoyage et a la normalisation JSON.**

Choix retenu de maniere explicite :

- composant : modele IA de transformation de donnees OCR
- entrees : JSON brut issu de Tesseract OCR
- sorties : JSON normalise selon un schema metier unique (dates, montants, devise, champs obligatoires)
- role : preparation des donnees avant categorisation, stockage et affichage applicatif

## Consequences

- La qualite des donnees aval s'ameliore grace a une normalisation uniforme.
- Une etape de validation metier reste necessaire pour detecter les erreurs de transformation.
- Le composant IA ajoute un point de complexite et de supervision supplementaire.
- Les schemas cibles doivent etre versionnes pour eviter les ruptures entre services.
