# ADR-14 : Utilisation de Playwright pour les tests E2E de l'interface utilisateur

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

L'application doit garantir que les parcours utilisateurs critiques fonctionnent correctement de bout en bout dans l'interface web.

La strategie de test E2E doit gerer :

- la validation des parcours principaux (upload, consultation, telechargement)
- la detection des regressions apres chaque evolution front-end
- l'execution automatisee dans un pipeline CI
- des resultats lisibles pour faciliter le diagnostic des echecs

## Options considerees pour les tests E2E

### Option 1 : Cypress

**Avantages** :

- Bonne experience developpeur
- Ecosysteme mature pour les tests front-end

**Inconvenients** :

- Capacites multi-navigateurs moins completes selon le contexte
- Moins adapte a certains scenarios complexes de navigation multi-onglets

### Option 2 : Playwright

**Avantages** :

- Support multi-navigateurs robuste
- Bonne stabilite des tests E2E
- Outils integres utiles (traces, screenshots, videos)

**Inconvenients** :

- Configuration initiale a cadrer
- Besoin de bonnes pratiques pour eviter les tests instables

## Decision

**Les tests E2E de l'interface sont implementes avec Playwright.**

Choix retenu de maniere explicite :

- framework de tests E2E : Playwright
- parcours couverts : upload de document PDF, consultation, recherche, telechargement
- execution : automatique dans GitHub Actions
- diagnostic : traces, captures d'ecran et videos en cas d'echec

## Consequences

- Les parcours critiques sont verifies automatiquement avant livraison.
- Le temps d'execution CI augmente et doit etre optimise pour garder un feedback rapide.
- La fiabilite des tests depend de bonnes pratiques anti-flaky.
- Les artefacts Playwright facilitent fortement le diagnostic des regressions UI.
