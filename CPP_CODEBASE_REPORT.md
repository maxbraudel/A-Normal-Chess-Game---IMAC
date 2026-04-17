# Rapport d'analyse complet de la codebase C++

Ce document couvre l'ensemble des fichiers `.cpp` du projet (89 fichiers) et décrit, pour chacun, ce qu'il fait et son role dans l'architecture du jeu.

## 1) Point d'entree

### `src/main.cpp`
- Ce que le fichier fait: initialise l'application et lance la boucle principale de jeu via la classe principale.
- A quoi il sert: c'est le point d'entree executable qui demarre toute l'architecture runtime.

## 2) Assets

### `src/Assets/AssetManager.cpp`
- Ce que le fichier fait: charge et met en cache les ressources visuelles (textures, spritesheets, etc.) depuis `assets/`.
- A quoi il sert: fournit une source centralisee d'assets pour le rendu et evite les rechargements couteux.

## 3) Board

### `src/Board/Board.cpp`
- Ce que le fichier fait: implemente la representation du plateau (cellules, acces aux positions, etat des cases).
- A quoi il sert: sert de fondation spatiale a tous les systemes (mouvement, construction, rendu, occupation).

### `src/Board/BoardGenerator.cpp`
- Ce que le fichier fait: genere l'etat initial du plateau (terrain, dispositions de depart, placements structurels initiaux).
- A quoi il sert: encapsule la logique de creation de partie pour produire un monde cohérent.

### `src/Board/CellTraversal.cpp`
- Ce que le fichier fait: calcule les regles de traversabilite des cellules selon le contexte (terrain, obstacles, structures).
- A quoi il sert: supporte les systemes de deplacement, de validation de coup et de projection.

## 4) Buildings

### `src/Buildings/Building.cpp`
- Ce que le fichier fait: implemente l'entite batiment (etat, proprietaire, position, progression, integrite).
- A quoi il sert: modele les structures construites et leur cycle de vie dans le jeu.

### `src/Buildings/BuildingFactory.cpp`
- Ce que le fichier fait: cree les instances de batiments avec leurs parametres et identifiants coherents.
- A quoi il sert: centralise l'instanciation pour garantir des creations uniformes et valides.

### `src/Buildings/StructureChunkRegistry.cpp`
- Ce que le fichier fait: maintient le registre des chunks/segments graphiques et metadonnees lies aux structures.
- A quoi il sert: permet au rendu et a la logique de placement de retrouver les definitions structurelles.

### `src/Buildings/StructurePlacementProfile.cpp`
- Ce que le fichier fait: encode les profils de placement (empreinte, ancrage, orientation) des structures.
- A quoi il sert: aligne la logique de build avec la geometrie effective des batiments.

## 5) Config

### `src/Config/GameConfig.cpp`
- Ce que le fichier fait: charge et valide la configuration de jeu (JSON, parametres globaux, contraintes).
- A quoi il sert: fournit un point de configuration unique pour equilibrage, generation et regles parametrees.

## 6) Core

### `src/Core/Game.cpp`
- Ce que le fichier fait: pilote le cycle de haut niveau de l'application (fenetre, boucle, orchestration globale).
- A quoi il sert: relie l'execution runtime aux sous-systemes (input, update, render, UI).

### `src/Core/GameClock.cpp`
- Ce que le fichier fait: gere la mesure du temps (delta-time, cadencement) pour les mises a jour.
- A quoi il sert: stabilise la boucle de jeu et la coherence temporelle des systemes.

### `src/Core/GameEngine.cpp`
- Ce que le fichier fait: porte le coeur logique (etat courant, commandes, transitions de tour, coordination metier).
- A quoi il sert: constitue le noyau d'execution des regles du jeu et des interactions.

### `src/Core/GameStateValidator.cpp`
- Ce que le fichier fait: verifie la coherence de l'etat de jeu apres actions ou transitions.
- A quoi il sert: detecte les incoherences metier et protege l'integrite du modele.

### `src/Core/InteractionPermissions.cpp`
- Ce que le fichier fait: calcule les permissions d'interaction selon contexte, phase et role joueur.
- A quoi il sert: garantit que UI/input respectent les contraintes de gameplay.

### `src/Core/TurnDraft.cpp`
- Ce que le fichier fait: represente et met a jour le brouillon d'actions d'un tour avant validation finale.
- A quoi il sert: supporte la planification de commandes et les previsualisations non destructives.

## 7) Debug

### `src/Debug/GameStateDebugRecorder.cpp`
- Ce que le fichier fait: enregistre des snapshots/exports de l'etat de jeu pour diagnostic.
- A quoi il sert: facilite le debogage, l'analyse post-mortem et la reproductibilite.

## 8) Input

### `src/Input/InputHandler.cpp`
- Ce que le fichier fait: traite les evenements de saisie (souris/clavier), selection et intentions de commande.
- A quoi il sert: traduit l'input utilisateur en actions metier exploitables par le moteur.

### `src/Input/LayeredSelection.cpp`
- Ce que le fichier fait: implemente une selection multicouche (piece, batiment, objet, cellule) avec priorites.
- A quoi il sert: clarifie les interactions sur une meme zone et rend la selection robuste.

## 9) Kingdom

### `src/Kingdom/Kingdom.cpp`
- Ce que le fichier fait: implemente le modele de royaume (ressources, inventaire d'unites/structures, etat faction).
- A quoi il sert: centralise les donnees de camp et leur evolution tour par tour.

## 10) Multiplayer

### `src/Multiplayer/MultiplayerClient.cpp`
- Ce que le fichier fait: gere la connexion client, l'echange reseau et la reception des messages de session.
- A quoi il sert: permet a un joueur distant de rejoindre et de synchroniser une partie.

### `src/Multiplayer/MultiplayerRuntime.cpp`
- Ce que le fichier fait: orchestre le runtime multijoueur (etat connexion, synchro, transitions).
- A quoi il sert: fait le lien entre couche reseau et logique de partie en cours.

### `src/Multiplayer/MultiplayerServer.cpp`
- Ce que le fichier fait: implemente le serveur de partie (ecoute, gestion clients, diffusion et autorite).
- A quoi il sert: heberge l'etat de reference et arbitre les interactions en mode multijoueur.

### `src/Multiplayer/Protocol.cpp`
- Ce que le fichier fait: definit serialisation/deserialisation et types de messages reseau.
- A quoi il sert: garantit une communication stable et interoperable client/serveur.

## 11) Projection

### `src/Projection/ForwardModel.cpp`
- Ce que le fichier fait: simule les consequences de commandes a venir sans modifier l'etat canonique.
- A quoi il sert: alimente la previsualisation de coups et l'aide a la decision utilisateur.

## 12) Render

### `src/Render/Camera.cpp`
- Ce que le fichier fait: gere la camera (position, zoom, transformations de vue).
- A quoi il sert: controle le cadrage du monde et la navigation visuelle du joueur.

### `src/Render/OverlayRenderer.cpp`
- Ce que le fichier fait: dessine les overlays de gameplay (selection, portee, highlights contextuels).
- A quoi il sert: expose visuellement l'etat tactique et les intentions de commande.

### `src/Render/Renderer.cpp`
- Ce que le fichier fait: realise le rendu principal du plateau, pieces, structures et couches de scene.
- A quoi il sert: produit l'image finale du monde de jeu a chaque frame.

### `src/Render/StructureOverlay.cpp`
- Ce que le fichier fait: calcule et prepare les informations overlay dediees aux structures.
- A quoi il sert: specialise l'affichage contextuel autour des batiments.

## 13) Runtime

### `src/Runtime/BuildOverlayCoordinator.cpp`
- Ce que le fichier fait: coordonne la generation/mise a jour des overlays de construction.
- A quoi il sert: synchronise etat de build, preview et rendu d'aide au placement.

### `src/Runtime/FrontendCoordinator.cpp`
- Ce que le fichier fait: orchestre la couche frontend en fonction de l'etat runtime.
- A quoi il sert: relie moteur et presentation pour maintenir une UI coherente.

### `src/Runtime/InGamePresentationCoordinator.cpp`
- Ce que le fichier fait: met a jour la presentation in-game (HUD, panneaux, infos de contexte).
- A quoi il sert: centralise la composition visuelle pendant la partie.

### `src/Runtime/InputCoordinator.cpp`
- Ce que le fichier fait: distribue et ordonne le traitement des entrees entre gameplay et UI.
- A quoi il sert: evite les conflits d'input et harmonise les priorites d'interaction.

### `src/Runtime/MultiplayerJoinCoordinator.cpp`
- Ce que le fichier fait: pilote le flux de jonction a une partie multijoueur (handshake, etat initial).
- A quoi il sert: securise l'entree en session distante.

### `src/Runtime/MultiplayerEventCoordinator.cpp`
- Ce que le fichier fait: traite les evenements reseau entrants et leurs effets runtime.
- A quoi il sert: convertit les messages protocolaires en transitions de jeu.

### `src/Runtime/MultiplayerRuntimeCoordinator.cpp`
- Ce que le fichier fait: coordonne les aspects runtime specifiques au multijoueur.
- A quoi il sert: maintient la synchronisation entre simulation locale et autorite reseau.

### `src/Runtime/PanelActionCoordinator.cpp`
- Ce que le fichier fait: gere les actions declenchees depuis les panneaux UI.
- A quoi il sert: mappe les intentions d'interface vers les commandes metier.

### `src/Runtime/RenderCoordinator.cpp`
- Ce que le fichier fait: ordonnance les passes de rendu (scene, overlays, UI).
- A quoi il sert: structure proprement le pipeline visuel de chaque frame.

### `src/Runtime/SelectionQueryCoordinator.cpp`
- Ce que le fichier fait: centralise les requetes de selection et resolutions de cibles.
- A quoi il sert: fournit une API de selection coherente aux autres coordinateurs.

### `src/Runtime/SessionFlow.cpp`
- Ce que le fichier fait: pilote le flux global de session (menu -> partie -> transitions).
- A quoi il sert: formalise le cycle de vie de session utilisateur.

### `src/Runtime/SessionPresentationCoordinator.cpp`
- Ce que le fichier fait: gere la presentation associee a l'etat de session (menus, ecrans de transition).
- A quoi il sert: rend lisible l'etat de session cote joueur.

### `src/Runtime/SessionRuntimeCoordinator.cpp`
- Ce que le fichier fait: coordonne les composantes runtime durant la session active.
- A quoi il sert: maintient un comportement stable entre les sous-systemes en jeu.

### `src/Runtime/TurnCoordinator.cpp`
- Ce que le fichier fait: orchestre progression et validation des tours.
- A quoi il sert: garantit un enchainement de tour deterministe et conforme aux regles.

### `src/Runtime/TurnDraftCoordinator.cpp`
- Ce que le fichier fait: synchronise le brouillon de tour avec UI/projections/runtime.
- A quoi il sert: permet l'edition d'actions avant commit tout en restant coherent visuellement.

### `src/Runtime/TurnLifecycleCoordinator.cpp`
- Ce que le fichier fait: gere les etapes de vie d'un tour (preparation, execution, finalisation).
- A quoi il sert: structure les transitions et side-effects autour d'un tour.

### `src/Runtime/UICallbackBinder.cpp`
- Ce que le fichier fait: relie les callbacks widgets UI aux handlers applicatifs.
- A quoi il sert: standardise la connexion entre interface et logique.

### `src/Runtime/UICallbackCoordinator.cpp`
- Ce que le fichier fait: centralise l'execution des callbacks UI et leurs consequences runtime.
- A quoi il sert: evite la dispersion de logique evenementielle dans les panneaux.

### `src/Runtime/UpdateCoordinator.cpp`
- Ce que le fichier fait: pilote la phase update de frame en ordonnant les sous-systemes.
- A quoi il sert: impose un ordre de mise a jour reproductible.

### `src/Runtime/WeatherVisibility.cpp`
- Ce que le fichier fait: calcule la visibilite liee aux conditions meteo.
- A quoi il sert: influence perception tactique et informations affichees.

## 14) Save

### `src/Save/SaveManager.cpp`
- Ce que le fichier fait: serialise et deserialise l'etat de jeu complet.
- A quoi il sert: permet sauvegarde/chargement de parties et reprise de progression.

## 15) Systems

### `src/Systems/BuildReachRules.cpp`
- Ce que le fichier fait: evalue les regles de portee applicables aux actions de construction.
- A quoi il sert: encadre legalement ou un joueur peut construire.

### `src/Systems/BuildSystem.cpp`
- Ce que le fichier fait: applique les commandes de construction (validation, cout, pose, progression).
- A quoi il sert: execute la mecanique de build dans le moteur.

### `src/Systems/ChestSystem.cpp`
- Ce que le fichier fait: gere la logique des coffres/objets de recompense et leurs interactions.
- A quoi il sert: ajoute une boucle de loot et d'objectifs secondaires.

### `src/Systems/CheckResponseRules.cpp`
- Ce que le fichier fait: verifie les reponses autorisees lorsqu'un roi est en echec.
- A quoi il sert: enforce les contraintes d'echecs pour les coups legaux.

### `src/Systems/CheckSystem.cpp`
- Ce que le fichier fait: detecte les situations d'echec (et selon contexte, etats relies).
- A quoi il sert: constitue le noyau des regles strategiques de survie du roi.

### `src/Systems/CombatSystem.cpp`
- Ce que le fichier fait: resout affrontements/captures et effets associes.
- A quoi il sert: applique les consequences de combat dans l'etat de jeu.

### `src/Systems/EconomySystem.cpp`
- Ce que le fichier fait: calcule revenus, depenses, upkeep et flux economiques de royaume.
- A quoi il sert: impose les contraintes de ressources pour les decisions tactiques.

### `src/Systems/EventLog.cpp`
- Ce que le fichier fait: enregistre les evenements de gameplay dans un journal structuré.
- A quoi il sert: alimente l'historique joueur, la lisibilite et le debug.

### `src/Systems/FormationSystem.cpp`
- Ce que le fichier fait: gere les mecaniques de formation/groupement d'unites.
- A quoi il sert: apporte des regles collectives de deplacement/positionnement.

### `src/Systems/InfernalSystem.cpp`
- Ce que le fichier fait: implemente les regles du sous-systeme infernal (spawns/effets speciaux).
- A quoi il sert: introduit une couche de gameplay asymetrique et evenementielle.

### `src/Systems/MarriageSystem.cpp`
- Ce que le fichier fait: traite les regles et transitions associees au mecanisme de mariage/couronnement.
- A quoi il sert: gere cette mecanique speciale de progression de faction.

### `src/Systems/PendingTurnProjection.cpp`
- Ce que le fichier fait: projette l'etat attendu en tenant compte des actions de tour en attente.
- A quoi il sert: donne une vue previsionnelle pour UI et validation.

### `src/Systems/ProductionSpawnRules.cpp`
- Ce que le fichier fait: determine les regles de spawn d'unites produites.
- A quoi il sert: choisit legalement ou apparait une nouvelle unite.

### `src/Systems/ProductionSystem.cpp`
- Ce que le fichier fait: gere les files de production, progression et finalisation des creations.
- A quoi il sert: materialise le recrutement/production au fil des tours.

### `src/Systems/PublicBuildingOccupation.cpp`
- Ce que le fichier fait: calcule l'occupation/controle des batiments publics.
- A quoi il sert: impacte ressources, map control et dynamique strategique.

### `src/Systems/SelectionMoveRules.cpp`
- Ce que le fichier fait: calcule les deplacements valides selon la selection courante.
- A quoi il sert: fournit les cases atteignables et securise les commandes de move.

### `src/Systems/StructureIntegrityRules.cpp`
- Ce que le fichier fait: applique les regles d'integrite/dommages/reparation des structures.
- A quoi il sert: gere la durabilite des batiments et murs sur la duree.

### `src/Systems/TurnPointRules.cpp`
- Ce que le fichier fait: gere les points de tour et leur consommation par action.
- A quoi il sert: impose un budget d'actions et cadence la prise de decision.

### `src/Systems/TurnSystem.cpp`
- Ce que le fichier fait: execute les commandes de tour, transitions et resolutions globales.
- A quoi il sert: constitue le coeur transactionnel du gameplay tour par tour.

### `src/Systems/WeatherSystem.cpp`
- Ce que le fichier fait: simule meteo et effets associes sur la partie.
- A quoi il sert: modifie le contexte tactique (visibilite, ambiance, contraintes).

### `src/Systems/XPSystem.cpp`
- Ce que le fichier fait: gere gain d'experience, progression et ameliorations d'unites.
- A quoi il sert: introduit une progression persistante intra-partie.

## 16) UI

### `src/UI/BarracksPanel.cpp`
- Ce que le fichier fait: implemente le panneau de baraquement (production, options contextuelles).
- A quoi il sert: expose les actions de production au joueur.

### `src/UI/BuildingPanel.cpp`
- Ce que le fichier fait: affiche les informations et actions d'un batiment selectionne.
- A quoi il sert: fournit l'interface de gestion structurelle.

### `src/UI/BuildToolPanel.cpp`
- Ce que le fichier fait: implemente l'outil UI de construction (choix de structure, mode de pose).
- A quoi il sert: permet d'entrer/sortir du workflow de build.

### `src/UI/CellPanel.cpp`
- Ce que le fichier fait: affiche le detail de la cellule selectionnee.
- A quoi il sert: donne une lecture fine du terrain et de son etat.

### `src/UI/EventLogPanel.cpp`
- Ce que le fichier fait: rend le journal d'evenements de partie.
- A quoi il sert: augmente la lisibilite historique et decisionnelle.

### `src/UI/GameMenuUI.cpp`
- Ce que le fichier fait: gere le menu en partie (pause, options contextuelles, navigation).
- A quoi il sert: structure les commandes meta durant le gameplay.

### `src/UI/HUD.cpp`
- Ce que le fichier fait: dessine et met a jour la couche HUD (infos rapides de partie).
- A quoi il sert: maintient l'etat tactique visible en permanence.

### `src/UI/InGameViewModelBuilder.cpp`
- Ce que le fichier fait: construit les view-models UI a partir des donnees metier.
- A quoi il sert: decouple presentation et structures internes du moteur.

### `src/UI/KingdomBalancePanel.cpp`
- Ce que le fichier fait: presente un recapitulatif des equilibres de royaume (economiques/etat global).
- A quoi il sert: aide a comparer rapidement les camps.

### `src/UI/MainMenuUI.cpp`
- Ce que le fichier fait: implemente le menu principal (nouvelle partie, chargement, multi, sortie).
- A quoi il sert: point d'acces UX aux flux de session.

### `src/UI/MapObjectPanel.cpp`
- Ce que le fichier fait: affiche les details/actions des objets de carte selectionnes.
- A quoi il sert: rend utilisables les interactions hors pieces/batiments.

### `src/UI/PiecePanel.cpp`
- Ce que le fichier fait: gere le panneau d'information et d'actions d'une piece.
- A quoi il sert: supporte les commandes unitaires depuis l'interface.

### `src/UI/PlannedActionsPanel.cpp`
- Ce que le fichier fait: liste les actions planifiees pour le tour courant.
- A quoi il sert: donne une vue consolidée avant validation du tour.

### `src/UI/ToolBar.cpp`
- Ce que le fichier fait: implemente la barre d'outils principale (modes, toggles, acces rapides).
- A quoi il sert: accelere l'acces aux interactions frequentes.

### `src/UI/UIManager.cpp`
- Ce que le fichier fait: centralise creation, cycle de vie et mise a jour des composants UI.
- A quoi il sert: constitue le hub de la presentation utilisateur.

## 17) Units

### `src/Units/MovementRules.cpp`
- Ce que le fichier fait: implemente les regles de deplacement des pieces (avec variantes/metacontraintes du jeu).
- A quoi il sert: definit la legalite cinematique de base du gameplay.

### `src/Units/Piece.cpp`
- Ce que le fichier fait: implemente le modele d'une piece (identite, etat, stats, progression).
- A quoi il sert: represente l'unite jouable fondamentale manipulee par tous les systemes.

### `src/Units/PieceFactory.cpp`
- Ce que le fichier fait: cree les pieces avec initialisation consistente et ids appropries.
- A quoi il sert: fiabilise le pipeline d'apparition d'unites.

---

# Synthese de la structure du jeu

## Architecture generale
Le projet suit une architecture modulaire en couches:
1. **Modele et etat**: `Board`, `Kingdom`, `Piece`, `Building`, configuration.
2. **Moteur metier**: `GameEngine` + systemes de regles (`src/Systems`).
3. **Orchestration runtime**: coordinateurs (`src/Runtime`) qui pilotent le flux frame/tour/session.
4. **Presentation**: rendu (`src/Render`) + UI (`src/UI`) + input (`src/Input`).
5. **Peripheriques fonctionnels**: sauvegarde (`src/Save`), multijoueur (`src/Multiplayer`), debug (`src/Debug`).

## Flux principal
- Demarrage via `main.cpp`, puis initialisation de `Game` et du moteur.
- Boucle frame: collecte input -> update runtime -> rendu scene/overlays/UI.
- Boucle tour: edition de commandes (draft/projection), validation regles, application transactionnelle dans `TurnSystem`.

## Role des coordinateurs Runtime
Les coordinateurs servent de couche anti-couplage: ils relient UI/input/rendu au moteur sans disperser les responsabilites. Cette strate clarifie les transitions de session, de tour, et de mode multijoueur.

## Separation logique / presentation
- Les systemes metier restent majoritairement centres sur les regles du jeu.
- La presentation (HUD/panneaux/overlays) lit des view-models et projections.
- Cette separation favorise maintenabilite, testabilite et evolution des interfaces.

## Multiplayer et persistence
- **Multiplayer**: protocole dedie + client/serveur + coordinateurs runtime pour la synchronisation.
- **Save**: serialisation complete de l'etat, permettant reprise de partie et workflows de debug.

## Conclusion
La codebase est construite pour un jeu tactique tour par tour enrichi, avec une forte granularite de systemes et une orchestration runtime explicite. La structure actuelle privilegie l'evolutivite (ajout de regles), la lisibilite des responsabilites et la coherence entre simulation, interface et reseau.
