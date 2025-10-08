# Alternative Hackathon Structure: The Two Squads

This document outlines a complete and self-contained alternative structure for the "Leaders" hackathon. In this scenario, participants are divided into two parallel squads, each tasked with building a full version of the project from the ground up.

---

## Squad 1 (36 Étudiants)

*   **Total d'étudiants :** 36
*   **Équipes :** 12 équipes de 3 étudiants chacune.
*   **Fusions de domaines :**
    *   `service-players` and `service-lobby` are merged.
    *   `service-persistence` and `database` are merged.

### 5. Structure du Projet (Squad 1)

```
/Leaders_Squad1/
├── backend/
│   ├── api-gateway/        # Équipe 11
│   ├── service-actions/    # Équipe 4
│   ├── service-characters/ # Équipe 3
│   ├── service-gamestate/  # Équipe 2
│   ├── service-players-lobby/ # Équipe 1 (Fusion)
│   └── service-persistence-db/ # Équipe 5 (Fusion)
├── frontend/
│   ├── ui-board/           # Équipe 7
│   ├── ui-controls/        # Équipe 9
│   ├── ui-hud/             # Équipe 8
│   ├── ui-lobby/           # Équipe 6
│   └── ui-recruitment/     # Équipe 10
├── platform/
│   └── build-integration/  # Équipe 12
├── docker-compose.yml      # Géré par l'Équipe 12
└── README.md
```

### 10. Backlog Quotidien par Équipe (Squad 1)

#### PÔLE BACK-END

**Équipe 1: Service Joueurs & Lobby (Fusion)**
*   **J1:** Définir les API pour `GET /api/players/{id}`, `POST /api/players`, `GET /api/games`, `POST /api/games`, `POST /api/games/{id}/join`.
*   **J2:** Initialiser le projet Spring Boot, créer les Controllers et Services avec des données en dur.
*   **J3:** Implémenter la logique métier pour créer/récupérer des joueurs et créer/lister les parties.
*   **J4:** Implémenter la logique pour rejoindre une partie. Intégrer avec le Service de Persistance & DB pour sauvegarder et charger les données.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 2: Service d'État du Jeu**
*   **J1:** Définir le contrat du message WebSocket `gameStateUpdate`.
*   **J2:** Mettre en place le serveur WebSocket et diffuser un état de jeu simulé.
*   **J3:** Implémenter la logique de mise à jour de l'état du jeu (tour suivant, etc.).
*   **J4:** Intégrer avec le Service de Persistance pour charger/sauvegarder l'état d'une partie.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 3: Service des Personnages**
*   **J1:** Définir l'API pour `GET /api/characters` et `POST /api/abilities/validate`.
*   **J2:** Initialiser le projet. Implémenter `GET /api/characters` avec les données des 19 personnages en dur.
*   **J3:** Modéliser la logique de toutes les compétences des personnages.
*   **J4:** Implémenter la logique de validation pour `POST /api/abilities/validate`.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 4: Service d'Actions**
*   **J1:** Définir l'API pour `POST /api/games/{id}/action` et l'objet `PlayerAction`.
*   **J2:** Initialiser le projet et le controller.
*   **J3:** Implémenter la logique de validation pour les actions "MOVE".
*   **J4:** Implémenter la logique pour les actions "RECRUIT" et "ABILITY". Orchestrer les appels aux autres services.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 5: Service de Persistance & Base de Données (Fusion)**
*   **J1:** Définir le schéma complet de la base de données en collaboration avec les équipes back-end. Définir l'API interne (méthodes Java) pour les autres services.
*   **J2:** Mettre en place le projet Supabase, créer les tables. Initialiser le projet Spring Boot (service de persistance) et configurer la connexion.
*   **J3:** Écrire un script de "seeding" pour les données initiales (personnages). Implémenter les méthodes pour sauvegarder/charger les `Player` et `Game`.
*   **J4:** Implémenter les méthodes pour sauvegarder/charger le `GameState` complet. Optimiser les requêtes et la structure des tables si nécessaire.
*   **J5:** Tests d'intégration et support aux autres équipes.

#### PÔLE FRONT-END

**Équipe 6: UI - Connexion & Lobby**
*   **J1:** Maquettes et structure des composants Vue.js.
*   **J2:** Développer l'UI statique.
*   **J3:** Appeler l'API du Service de Lobby pour afficher la liste des parties.
*   **J4:** Implémenter la création et la jonction d'une partie.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 7: UI - Plateau de Jeu**
*   **J1:** Maquettes et structure des composants `GameBoard`, `HexTile`, `GamePiece`.
*   **J2:** Développer l'affichage statique du plateau avec des données simulées.
*   **J3:** Se connecter au WebSocket pour afficher l'état du jeu en temps réel.
*   **J4:** Implémenter les interactions utilisateur (sélection, etc.).
*   **J5:** Finalisation du style, tests et préparation de la démo.

**Équipe 8: UI - HUD Joueur**
*   **J1:** Maquettes et structure des composants.
*   **J2:** Développer l'affichage statique avec des données simulées.
*   **J3:** Se connecter au WebSocket pour afficher le joueur actuel et les infos du tour.
*   **J4:** Afficher les cartes des personnages recrutés par le joueur.
*   **J5:** Finalisation du style, tests et préparation de la démo.

**Équipe 9: UI - Contrôles & Actions**
*   **J1:** Maquettes et structure des composants.
*   **J2:** Développer les boutons d'action statiques.
*   **J3:** Activer/désactiver les contrôles en fonction des données du WebSocket (tour du joueur).
*   **J4:** Appeler l'API du Service d'Actions lors d'un clic sur un bouton d'action.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 10: UI - Recrutement & Info**
*   **J1:** Maquettes et structure des composants.
*   **J2:** Développer l'UI statique avec des données simulées.
*   **J3:** Appeler l'API du Service des Personnages pour afficher la liste des personnages à recruter.
*   **J4:** Implémenter l'action de recrutement.
*   **J5:** Tests d'intégration et préparation de la démo.

#### PÔLE PLATEFORME

**Équipe 11: API Gateway**
*   **J1:** Étudier Spring Cloud Gateway et définir la carte de routage.
*   **J2:** Initialiser le projet et configurer les routes pour 2 services.
*   **J3:** Configurer les routes pour tous les services back-end.
*   **J4:** Mettre en place la gestion des CORS et la journalisation (logging).
*   **J5:** Tests de charge (stretch goal) et support à l'intégration.

**Équipe 12: Intégration & Build**
*   **J1:** Mettre en place le monorepo Git avec les politiques de branches.
*   **J2:** Créer le `docker-compose.yml` et les `Dockerfile` initiaux pour tous les services.
*   **J3:** Mettre en place les scripts de build pour chaque service.
*   **J4:** Mettre en place un workflow d'intégration continue simple (ex: GitHub Actions) qui build le projet.
*   **J5:** Gérer le "Code Freeze", le merge final et la préparation de l'environnement de démo.

---

## Squad 2 (37 Étudiants)

*   **Total d'étudiants :** 37
*   **Équipes :** 10 équipes (sept équipes de 4 étudiants et trois équipes de 3).
*   **Fusions de domaines :**
    *   `service-players` et `service-lobby` sont fusionnés.
    *   `service-persistence` et `database` sont fusionnés.
    *   `ui-hud` et `ui-controls` sont fusionnés.
    *   `api-gateway` et `build-integration` sont fusionnés.

### 5. Structure du Projet (Squad 2)

```
/Leaders_Squad2/
├── backend/
│   ├── service-actions/    # Équipe 4
│   ├── service-characters/ # Équipe 3
│   ├── service-gamestate/  # Équipe 2
│   ├── service-session/    # Équipe 1 (Fusion)
│   └── service-persistence-db/ # Équipe 5 (Fusion)
├── frontend/
│   ├── ui-board/           # Équipe 7
│   ├── ui-lobby/           # Équipe 6
│   ├── ui-player-interface/ # Équipe 8 (Fusion)
│   └── ui-recruitment/     # Équipe 9
├── platform/
│   └── platform-services/  # Équipe 10 (Fusion)
├── docker-compose.yml      # Géré par l'Équipe 10
└── README.md
```

### 10. Backlog Quotidien par Équipe (Squad 2)

#### PÔLE BACK-END

**Équipe 1: Service Session (Joueurs & Lobby)**
*   **J1:** Définir les API pour `GET /api/players/{id}`, `POST /api/players`, `GET /api/games`, `POST /api/games`, `POST /api/games/{id}/join`.
*   **J2:** Initialiser le projet Spring Boot, créer les Controllers et Services avec des données en dur.
*   **J3:** Implémenter la logique métier pour créer/récupérer des joueurs et créer/lister les parties.
*   **J4:** Implémenter la logique pour rejoindre une partie. Intégrer avec le Service de Persistance & DB pour sauvegarder et charger les données.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 2: Service d'État du Jeu**
*   **J1:** Définir le contrat du message WebSocket `gameStateUpdate`.
*   **J2:** Mettre en place le serveur WebSocket et diffuser un état de jeu simulé.
*   **J3:** Implémenter la logique de mise à jour de l'état du jeu (tour suivant, etc.).
*   **J4:** Intégrer avec le Service de Persistance pour charger/sauvegarder l'état d'une partie.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 3: Service des Personnages**
*   **J1:** Définir l'API pour `GET /api/characters` et `POST /api/abilities/validate`.
*   **J2:** Initialiser le projet. Implémenter `GET /api/characters` avec les données des 19 personnages en dur.
*   **J3:** Modéliser la logique de toutes les compétences des personnages.
*   **J4:** Implémenter la logique de validation pour `POST /api/abilities/validate`.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 4: Service d'Actions**
*   **J1:** Définir l'API pour `POST /api/games/{id}/action` et l'objet `PlayerAction`.
*   **J2:** Initialiser le projet et le controller.
*   **J3:** Implémenter la logique de validation pour les actions "MOVE".
*   **J4:** Implémenter la logique pour les actions "RECRUIT" et "ABILITY". Orchestrer les appels aux autres services.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 5: Service de Persistance & Base de Données**
*   **J1:** Définir le schéma complet de la base de données en collaboration avec les équipes back-end. Définir l'API interne (méthodes Java) pour les autres services.
*   **J2:** Mettre en place le projet Supabase, créer les tables. Initialiser le projet Spring Boot (service de persistance) et configurer la connexion.
*   **J3:** Écrire un script de "seeding" pour les données initiales (personnages). Implémenter les méthodes pour sauvegarder/charger les `Player` et `Game`.
*   **J4:** Implémenter les méthodes pour sauvegarder/charger le `GameState` complet. Optimiser les requêtes et la structure des tables si nécessaire.
*   **J5:** Tests d'intégration et support aux autres équipes.

#### PÔLE FRONT-END

**Équipe 6: UI - Connexion & Lobby**
*   **J1:** Maquettes et structure des composants Vue.js.
*   **J2:** Développer l'UI statique.
*   **J3:** Appeler l'API du Service de Lobby pour afficher la liste des parties.
*   **J4:** Implémenter la création et la jonction d'une partie.
*   **J5:** Tests d'intégration et préparation de la démo.

**Équipe 7: UI - Plateau de Jeu**
*   **J1:** Maquettes et structure des composants `GameBoard`, `HexTile`, `GamePiece`.
*   **J2:** Développer l'affichage statique du plateau avec des données simulées.
*   **J3:** Se connecter au WebSocket pour afficher l'état du jeu en temps réel.
*   **J4:** Implémenter les interactions utilisateur (sélection, etc.).
*   **J5:** Finalisation du style, tests et préparation de la démo.

**Équipe 8: UI - Interface Joueur (HUD & Contrôles)**
*   **J1:** Maquettes et structure des composants.
*   **J2:** Développer l'affichage statique du HUD et les boutons d'action avec des données simulées.
*   **J3:** Se connecter au WebSocket pour afficher le joueur actuel, les infos du tour et activer/désactiver les contrôles en fonction des données.
*   **J4:** Afficher les cartes des personnages recrutés. Appeler l'API du Service d'Actions lors d'un clic sur un bouton d'action.
*   **J5:** Finalisation du style, tests d'intégration et préparation de la démo.

**Équipe 9: UI - Recrutement & Info**
*   **J1:** Maquettes et structure des composants.
*   **J2:** Développer l'UI statique avec des données simulées.
*   **J3:** Appeler l'API du Service des Personnages pour afficher la liste des personnages à recruter.
*   **J4:** Implémenter l'action de recrutement.
*   **J5:** Tests d'intégration et préparation de la démo.

#### PÔLE PLATEFORME

**Équipe 10: Services de Plateforme (API Gateway & Intégration)**
*   **J1:** Mettre en place le monorepo Git avec les politiques de branches. Étudier Spring Cloud Gateway et définir la carte de routage.
*   **J2:** Créer le `docker-compose.yml` et les `Dockerfile` initiaux pour tous les services. Configurer les routes pour 2 services.
*   **J3:** Mettre en place les scripts de build pour chaque service. Configurer les routes pour tous les services back-end.
*   **J4:** Mettre en place un workflow d'intégration continue simple (ex: GitHub Actions). Mettre en place la gestion des CORS et la journalisation (logging).
*   **J5:** Gérer le "Code Freeze", le merge final et la préparation de l'environnement de démo.

---

### 8. Jalons du Hackathon (Applicable aux deux Squads)

*   **Jour 1 : Définition des Contrats.** Validation en fin de journée.
*   **Jour 2 : Développement Initial.** Implémentation des squelettes de services et des UI avec données simulées.
*   **Jour 3 & 4 : Développement et Intégration.** Développement des fonctionnalités et premiers tests d'intégration.
*   **Jour 5 : Finalisation et Démonstration.** Matin : Intégration finale. 12h00 : **CODE FREEZE**. Après-midi : **Démonstrations Finales**.
