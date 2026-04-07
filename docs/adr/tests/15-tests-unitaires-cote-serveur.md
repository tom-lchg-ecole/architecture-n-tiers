# ADR-15 : Tests unitaires cote serveur

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Le serveur doit rester fiable a chaque changement de logique metier, en particulier sur le traitement des donnees facture, les validations et les integrations techniques.

La strategie de tests unitaires doit gerer :

- la validation de la logique metier independamment des dependances externes
- la prevention des regressions sur les services et utilitaires
- une execution rapide pour feedback developpeur
- une base de qualite avant les tests d'integration et E2E

## Options considerees pour les tests unitaires serveur

### Option 1 : Peu de tests unitaires, priorite aux tests d'integration

**Avantages** :

- Moins d'effort initial de mise en place
- Verification proche des cas reels

**Inconvenients** :

- Diagnostic des bugs plus lent
- Couverture fine de la logique metier insuffisante

### Option 2 : Suite de tests unitaires dediée cote serveur

**Avantages** :

- Detection rapide des regressions
- Validation precise des regles metier
- Execution rapide dans le cycle de developpement

**Inconvenients** :

- Besoin de maintenir les mocks et fixtures
- Temps de redaction supplementaire au debut

## Decision

**Mise en place de tests unitaires dedies cote serveur**

Raisons principales :

- fiabiliser la logique metier avant integration complete
- reduire le cout de correction des regressions
- accelerer le feedback pendant le developpement
- completer efficacement la pyramide de tests du projet
