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

**Utilisation de Playwright pour les tests E2E de l'interface utilisateur**

Raisons principales :

- couverture fiable des parcours critiques
- execution efficace en CI sur plusieurs navigateurs
- outillage de diagnostic tres utile en cas d'echec
- bonne maintenabilite de la suite de tests sur le long terme
