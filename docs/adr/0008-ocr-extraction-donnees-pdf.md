# ADR-8 : OCR pour l'extraction des donnees d'un fichier PDF

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit extraire automatiquement les informations utiles des factures PDF, y compris lorsque le document est scanné et non directement exploitable en texte.

La solution OCR doit gérer :

- la reconnaissance du texte dans différents formats de PDF
- l'extraction de champs clés (date, montant, fournisseur)
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

- Bonne précision sur les documents de type facture
- Extraction structurée de champs
- Intégration naturelle avec l'écosystème AWS

**Inconvénients** :

- Coût à l'usage
- Dépendance à un service cloud externe

## Décision

**L'OCR des factures PDF est réalisé avec Amazon Textract.**

Choix retenu de manière explicite :

- service OCR : Amazon Textract
- périmètre : extraction texte et champs depuis PDF natifs ou scannés
- sortie : données OCR structurées au format JSON
- intégration : traitement en entrée du pipeline IA et stockage des PDF sur S3
