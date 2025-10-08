# Hackathon "Leaders" - ESIEA 2025

Bienvenue dans ce hackathon de 5 jours ! L'objectif est de construire une version web complète et fonctionnelle du jeu de société "Leaders". Ce projet n'est pas seulement un défi de programmation, mais aussi un exercice de collaboration à grande échelle, simulant un environnement de travail professionnel avec une architecture microservices.

## 1. Le Jeu "Leaders"

*   **But du jeu :** Vaincre le Leader adverse de l'une des deux manières suivantes :
    1.  **Capture :** Amener 2 de vos personnages sur des cases adjacentes au Leader adverse.
    2.  **Encerclement :** Le Leader adverse se retrouve sans aucune case libre autour de lui.
*   **Déroulement :** À tour de rôle, les joueurs effectuent une action avec chacun de leurs personnages (déplacement ou utilisation de compétence). Ensuite, le joueur recrute un nouveau personnage parmi ceux disponibles, jusqu'à ce que chaque joueur ait une équipe de 5 (1 Leader + 4 personnages recrutés). Une fois les équipes complètes, la phase de recrutement est sautée.

## 2. Le Défi : Architecture par Domaines

Vous n'allez pas construire le jeu seul dans votre équipe. Les 73 étudiants sont répartis en 14 équipes, et toutes les équipes collaborent sur un **unique produit**. Chaque équipe est propriétaire d'un ou plusieurs **domaines fonctionnels**.

**Le succès de ce hackathon repose sur votre capacité à communiquer, à définir des contrats clairs (API), et à intégrer votre travail avec celui des autres.**

## 3. Compétences Développées

Ce hackathon est conçu pour être une expérience d'apprentissage intensive et intégrée. Au-delà de la réalisation du jeu, il vous permettra de développer un large éventail de compétences clés, notamment :

*   **Techniques :** Maîtrise d'une architecture microservices moderne (Java, Spring Boot), développement d'interfaces réactives (Vue.js), gestion de bases de données relationnelles (PostgreSQL), communication en temps réel (WebSockets), et orchestration d'applications conteneurisées (Docker, Docker Compose). Vous pratiquerez également les principes de l'API-first et de l'intégration continue.

*   **Managériales :** Gestion de projet en mode Agile, planification et suivi de backlog, négociation de contrats d'interface (API) entre les équipes, gestion des dépendances, et élaboration de stratégies d'intégration et de tests dans un environnement complexe.

*   **Humaines :** Communication technique efficace, travail et prise de décision en équipe, résolution de problèmes collectifs, et leadership. Vous apprendrez à faire des compromis et à vous synchroniser avec d'autres équipes pour atteindre un objectif commun.

## 4. La Pile Technologique

*   **Front-End :** Vue.js
*   **Back-End :** Java 17+ avec Spring Boot 3+
*   **Base de Données :** Supabase (PostgreSQL)
*   **Communication Temps Réel :** WebSockets (via Spring Boot)
*   **Orchestration & Environnement :** Docker et Docker Compose

## 5. Structure du Projet (Monorepo)

```
/Leaders/
├── backend/
│   ├── api-gateway/        # Équipe 12
│   ├── service-actions/    # Équipe 5
│   ├── service-characters/ # Équipe 4
│   ├── service-gamestate/  # Équipe 3
│   ├── service-lobby/      # Équipe 2
│   ├── service-persistence/ # Équipe 6
│   └── service-players/    # Équipe 1
├── frontend/
│   ├── ui-board/           # Équipe 8
│   ├── ui-controls/        # Équipe 10
│   ├── ui-hud/             # Équipe 9
│   ├── ui-lobby/           # Équipe 7
│   └── ui-recruitment/     # Équipe 11
├── platform/
│   ├── build-integration/  # Équipe 14
│   └── database/           # Équipe 13
├── docker-compose.yml      # Fichier principal d'orchestration (géré par l'Équipe 14)
└── README.md               # Ce fichier
```

## 6. Architecture Générale

```
+-----------------------------------------------------------------+
|                                                                 |
|                    +------------------+                         |
|                    |   Utilisateurs   |                         |
|                    +--------+---------+                         |
|                             |                                   |
|                             v                                   |
|      +---------------------------------------------+            |
|      |         FRONTEND (Vue.js / Docker)          |            |
|      | (Équipes 7-11: UI-Lobby, UI-Board, etc.)    |            |
|      +----------------------+----------------------+            |
|                             |                                   |
|                             v (Requêtes HTTP/S)                 |
|      +----------------------+----------------------+            |
|      |   API GATEWAY (Spring Cloud / Docker)       |            |
|      | (Équipe 12)                                 |            |
|      +----------------------+----------------------+            |
|                             | (Routage interne)                 |
|                             v                                   |
|      +---------------------------------------------+            |
|      |         BACKEND (Spring Boot / Docker)      |            |
|      | (Équipes 1-6: Services Joueurs, Lobby, etc.)|            |
|      +--+-----------------+--------------------+--+            |
|         |                 |                    |                |
|         +-----------------v--------------------+                |
|                           | (Appels de service)                 |
|                           v                                   |
|      +--------------------+-----------------------+            |
|      |   SERVICE PERSISTANCE (Spring / Docker)    |            |
|      |   (Équipe 6)                               |            |
|      +--------------------+-----------------------+            |
|                           | (JDBC)                            |
|                           v                                   |
|                    +------+-----------+                        |
|                    |  SUPABASE DB     |                        |
|                    |  (PostgreSQL)    |                        |
|                    |  (Équipe 13)     |                        |
|                    +------------------+                        |
|                                                                 |
+-----------------------------------------------------------------+
|                                                                 |
|   GIT / GITHUB : Code source unique pour toutes les équipes     |
|                                                                 |
|   DOCKER COMPOSE : Orchestration de tous les services (Éq. 14)  |
|                                                                 |
+-----------------------------------------------------------------+
```

## 7. Le Principe Clé : Le Contrat d'API d'Abord

**Le livrable du Jour 1 n'est PAS du code.** C'est un **contrat d'API**. Les équipes back-end doivent définir les points d'entrée (endpoints) de leur service, les données attendues en entrée et les données retournées en sortie en utilisant le format **OpenAPI (Swagger)**. Ce contrat est la promesse que vous faites aux autres équipes.

## 8. Jalons du Hackathon

*   **Jour 1 : Définition des Contrats.** Validation en fin de journée.
*   **Jour 2 : Développement Initial.** Implémentation des squelettes de services et des UI avec données simulées.
*   **Jour 3 & 4 : Développement et Intégration.** Développement des fonctionnalités et premiers tests d'intégration.
*   **Jour 5 : Finalisation et Démonstration.** Matin : Intégration finale. 12h00 : **CODE FREEZE**. Après-midi : **Démonstrations Finales**.

## 9. Grille d'Évaluation (sur 100 points)

| Catégorie | Points | Description |
| :--- | :--- | :--- |
| **Travail d'Équipe** | 50 | Qualité de la livraison du domaine spécifique à l'équipe. |
| **Projet Global** | 30 | Succès de l'intégration finale et qualité de la démo. Note commune à tous. |
| **Processus** | 20 | Qualité des pratiques de collaboration (Git, etc.) et évaluation par les pairs. |

---
## 10. Backlog Quotidien par Équipe

### PÔLE BACK-END

#### Équipe 1: Service Joueurs
*   **J1:** Définir l'API pour `GET /api/players/{id}` et `POST /api/players`.
*   **J2:** Initialiser le projet Spring Boot, créer le Controller et le Service avec des données en dur.
*   **J3:** Implémenter la logique métier pour créer et récupérer des joueurs.
*   **J4:** Intégrer avec le Service de Persistance pour sauvegarder et charger les joueurs.
*   **J5:** Tests d'intégration et préparation de la démo.

#### Équipe 2: Service de Lobby
*   **J1:** Définir l'API pour `GET /api/games`, `POST /api/games`, `POST /api/games/{id}/join`.
*   **J2:** Initialiser le projet, créer les controllers et services avec des données en dur.
*   **J3:** Implémenter la logique pour créer et lister les parties.
*   **J4:** Implémenter la logique pour rejoindre une partie. Intégrer avec le Service de Persistance.
*   **J5:** Tests d'intégration et préparation de la démo.

#### Équipe 3: Service d'État du Jeu
*   **J1:** Définir le contrat du message WebSocket `gameStateUpdate`.
*   **J2:** Mettre en place le serveur WebSocket et diffuser un état de jeu simulé.
*   **J3:** Implémenter la logique de mise à jour de l'état du jeu (tour suivant, etc.).
*   **J4:** Intégrer avec le Service de Persistance pour charger/sauvegarder l'état d'une partie.
*   **J5:** Tests d'intégration et préparation de la démo.

#### Équipe 4: Service des Personnages
*   **J1:** Définir l'API pour `GET /api/characters` et `POST /api/abilities/validate`.
*   **J2:** Initialiser le projet. Implémenter `GET /api/characters` avec les données des 19 personnages en dur.
*   **J3:** Modéliser la logique de toutes les compétences des personnages.
*   **J4:** Implémenter la logique de validation pour `POST /api/abilities/validate`.
*   **J5:** Tests d'intégration et préparation de la démo.

#### Équipe 5: Service d'Actions
*   **J1:** Définir l'API pour `POST /api/games/{id}/action` et l'objet `PlayerAction`.
*   **J2:** Initialiser le projet et le controller.
*   **J3:** Implémenter la logique de validation pour les actions "MOVE".
*   **J4:** Implémenter la logique pour les actions "RECRUIT" et "ABILITY". Orchestrer les appels aux autres services.
*   **J5:** Tests d'intégration et préparation de la démo.

#### Équipe 6: Service de Persistance
*   **J1:** Définir l'API interne (méthodes Java) pour les autres services.
*   **J2:** Initialiser le projet, configurer la connexion à Supabase.
*   **J3:** Implémenter les méthodes pour sauvegarder/charger les `Player` et `Game`.
*   **J4:** Implémenter les méthodes pour sauvegarder/charger le `GameState` complet.
*   **J5:** Tests d'intégration et support aux autres équipes.

### PÔLE FRONT-END

#### Équipe 7: UI - Connexion & Lobby
*   **J1:** Maquettes et structure des composants Vue.js.
*   **J2:** Développer l'UI statique.
*   **J3:** Appeler l'API du Service de Lobby pour afficher la liste des parties.
*   **J4:** Implémenter la création et la jonction d'une partie.
*   **J5:** Tests d'intégration et préparation de la démo.

#### Équipe 8: UI - Plateau de Jeu
*   **J1:** Maquettes et structure des composants `GameBoard`, `HexTile`, `GamePiece`.
*   **J2:** Développer l'affichage statique du plateau avec des données simulées.
*   **J3:** Se connecter au WebSocket pour afficher l'état du jeu en temps réel.
*   **J4:** Implémenter les interactions utilisateur (sélection, etc.).
*   **J5:** Finalisation du style, tests et préparation de la démo.

#### Équipe 9: UI - HUD Joueur
*   **J1:** Maquettes et structure des composants.
*   **J2:** Développer l'affichage statique avec des données simulées.
*   **J3:** Se connecter au WebSocket pour afficher le joueur actuel et les infos du tour.
*   **J4:** Afficher les cartes des personnages recrutés par le joueur.
*   **J5:** Finalisation du style, tests et préparation de la démo.

#### Équipe 10: UI - Contrôles & Actions
*   **J1:** Maquettes et structure des composants.
*   **J2:** Développer les boutons d'action statiques.
*   **J3:** Activer/désactiver les contrôles en fonction des données du WebSocket (tour du joueur).
*   **J4:** Appeler l'API du Service d'Actions lors d'un clic sur un bouton d'action.
*   **J5:** Tests d'intégration et préparation de la démo.

#### Équipe 11: UI - Recrutement & Info
*   **J1:** Maquettes et structure des composants.
*   **J2:** Développer l'UI statique avec des données simulées.
*   **J3:** Appeler l'API du Service des Personnages pour afficher la liste des personnages à recruter.
*   **J4:** Implémenter l'action de recrutement.
*   **J5:** Tests d'intégration et préparation de la démo.

### PÔLE PLATEFORME

#### Équipe 12: API Gateway
*   **J1:** Étudier Spring Cloud Gateway et définir la carte de routage.
*   **J2:** Initialiser le projet et configurer les routes pour 2 services.
*   **J3:** Configurer les routes pour tous les services back-end.
*   **J4:** Mettre en place la gestion des CORS et la journalisation (logging).
*   **J5:** Tests de charge (stretch goal) et support à l'intégration.

#### Équipe 13: Base de Données
*   **J1:** Définir le schéma complet de la base de données en collaboration avec les équipes back-end.
*   **J2:** Mettre en place le projet Supabase et créer les tables.
*   **J3:** Écrire un script de "seeding" pour les données initiales (ex: les 19 personnages).
*   **J4:** Optimiser les requêtes et la structure des tables si nécessaire.
*   **J5:** Support et supervision de la base de données.

#### Équipe 14: Intégration & Build
*   **J1:** Mettre en place le monorepo Git avec les politiques de branches.
*   **J2:** Créer le `docker-compose.yml` et les `Dockerfile` initiaux pour tous les services.
*   **J3:** Mettre en place les scripts de build pour chaque service.
*   **J4:** Mettre en place un workflow d'intégration continue simple (ex: GitHub Actions) qui build le projet.
*   **J5:** Gérer le "Code Freeze", le merge final et la préparation de l'environnement de démo.
