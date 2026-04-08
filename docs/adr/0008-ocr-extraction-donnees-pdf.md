# ADR-8 : OCR pour l'extraction des donnees d'un fichier PDF

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit extraire automatiquement les informations utiles des documents PDF (factures, devis, etc.), y compris lorsque le document est scanné et non directement exploitable en texte.

La solution OCR doit gérer :

- la reconnaissance du texte dans différents formats de PDF
- l'extraction de champs clés adaptés au type de document (ex : date, montant, fournisseur)
- une qualité de lecture suffisante pour limiter les corrections manuelles
- l'intégration simple avec le pipeline de traitement

## Options considérées pour l'OCR

### Option 1 : Tesseract OCR (open source)

**Avantages** :

- Gratuit et open source
- Facile à intégrer en local

**Inconvénients** :

- Précision variable selon la qualité des documents
- Configuration et entraînement parfois nécessaires

### Option 2 : AWS Textract

**Avantages** :

- Bonne précision sur plusieurs types de documents PDF
- Extraction structurée de champs
- Intégration naturelle avec l'écosystème AWS

**Inconvénients** :

- Coût à l'usage
- Dépendance à un service cloud externe

## Décision

**L'OCR des documents PDF (factures, devis, etc.) est réalisé avec Tesseract OCR.**

Choix retenu de manière explicite :

- service OCR : Tesseract OCR
- périmètre : extraction texte et champs depuis PDF natifs ou scannés
- sortie : données OCR structurées au format JSON
- intégration :
  - Tesseract n'accède jamais directement au bucket S3
  - l'API orchestre l'extraction OCR depuis le PDF puis la communication avec S3
  - traitement en entrée du pipeline IA après extraction

## Conséquences

- Le composant OCR reste découplé du stockage objet S3.
- L'API devient le point unique de communication avec S3 pour le flux OCR.
- La qualité d'extraction dépend de la configuration Tesseract et de la qualité des scans.
- Un contrôle qualité des sorties OCR reste nécessaire sur les cas ambigus.
- Le pipeline doit gérer les erreurs OCR et les documents non exploitables.
