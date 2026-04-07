# ADR-20 : Monitoring et logging centralises

## Date

07/04/2026

## Status

Approuvé

## Contexte et problème

Le projet repose sur plusieurs composants (front-end, backend, OCR, IA, stockage) qui doivent etre supervises en continu pour detecter rapidement les anomalies.

La strategie de supervision doit gerer :

- la collecte des logs applicatifs et techniques
- le suivi des metriques critiques (latence, erreurs, disponibilite)
- l'alerte proactive en cas d'incident
- l'aide au diagnostic et au debug en production

## Options considerees pour la supervision

### Option 1 : Logs locaux par service sans centralisation

**Avantages** :

- Mise en place rapide
- Faible cout initial

**Inconvenients** :

- Vision globale limitee
- Diagnostic lent en cas d'incident transverse
- Difficile a exploiter a mesure que le projet grandit

### Option 2 : Monitoring et logging centralises

**Avantages** :

- Vue unifiee de l'etat du systeme
- Alerting plus fiable
- Analyse plus rapide des causes racines

**Inconvenients** :

- Configuration initiale plus importante
- Cout d'exploitation potentiellement plus eleve

## Decision

**Utilisation d'une solution de monitoring et logging centralises**

Raisons principales :

- accelerer la detection des incidents
- reduire le temps moyen de resolution
- fiabiliser le suivi de la qualite de service
- faciliter la maintenance de l'architecture distribuee
