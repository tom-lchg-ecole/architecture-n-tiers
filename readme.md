# Application de gestion de factures (OCR + IA)

L'objectif est de reduire le travail manuel sur la saisie et le classement des factures grace a un pipeline :

- import des PDF
- extraction OCR
- nettoyage/normalisation des donnees
- categorisation automatique par IA
- stockage et consultation via une interface web

## Ce que fait le projet

Fonctionnalites metier visees :

- import unitaire ou en lot de factures PDF (drag-and-drop inclus)
- extraction automatique des informations utiles (date, montant, fournisseur, etc.)
- categorisation automatique des factures selon leur contenu
- CRUD des factures et recherche/filtrage
- telechargement/visualisation des PDF

## Fonctionnement global

Flux simplifie du traitement :

1. L'utilisateur depose une ou plusieurs factures PDF dans l'interface web
2. Les fichiers sont stockes dans AWS S3
3. Un service OCR (AWS Textract) extrait les donnees brutes
4. Un composant IA nettoie et restructure le JSON OCR vers un schema commun
5. Un modele de categorisation attribue automatiquement une categorie
6. Les metadonnees et resultats sont stockes dans MongoDB
7. L'interface React permet de consulter, filtrer, corriger et telecharger les factures

## Architecture cible

- **Front-end** : React (web app responsive mobile/tablette/desktop)
- **Back-end** : Express (APIs REST, orchestration des traitements)
- **Base de donnees** : MongoDB (schema flexible adapte aux donnees OCR/IA)
- **Stockage fichiers** : AWS S3 (durable et scalable)
- **OCR** : AWS Textract
- **IA** :
  - post-traitement des donnees OCR (nettoyage + normalisation + restructuration JSON)
  - categorisation automatique supervisee
- **Style d'architecture** : microservices pour separer les responsabilites et scaler independamment.

## Qualite, tests et exploitation

- **Tests** :
  - tests unitaires cote serveur pour la logique metier
  - tests E2E Playwright pour les parcours critiques interface
- **CI/CD** :
  - pipeline `deploy.yml` pour automatiser les deploiements
  - pipeline `release.yml` pour standardiser les releases
- **Run/ops** :
  - monitoring et logging centralises
  - sauvegardes automatisees + tests de restauration
  - politique de mises a jour de dependances avec controle securite
  - gestion d'incidents formalisee via runbooks et post-mortems

## Stack et outils retenus

- TypeScript sur la stack applicative
- React cote client, Express cote serveur
- MongoDB et Mongo Compass
- Docker Desktop
- Visual Studio Code
- Figma (conception UI)

## Sources de reference

Le detail des choix d'architecture et d'implementation est documente dans `docs/adr/`.
