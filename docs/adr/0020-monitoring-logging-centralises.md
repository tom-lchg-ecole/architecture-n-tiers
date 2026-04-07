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

**Le projet adopte une plateforme centralisee pour le monitoring et le logging de tous les services.**

Choix retenu de maniere explicite :

- perimetre : front-end, backend, pipeline OCR/IA et integrations stockage
- donnees collectees : logs applicatifs, metriques techniques, erreurs
- exploitation : tableaux de bord et alertes centralises
- objectif operationnel : detection rapide des incidents et diagnostic unifie

## Consequences

- La detection d'incidents et le diagnostic deviennent plus rapides.
- Les couts et la complexite de la plateforme d'observabilite augmentent.
- Les equipes doivent definir des standards de logs, metriques et alertes.
- La qualite de supervision depend de la couverture effective des instrumentations.
