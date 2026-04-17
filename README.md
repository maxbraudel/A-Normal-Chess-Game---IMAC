# A Normal Chess Game

Jeu de strategie au tour par tour inspire des echecs, avec carte, economie, constructions, meteo, progression des pieces et mode multijoueur LAN.

## Ce que fait l'application

L'application lance une partie sur un plateau tactique et combine:
- Deplacement et combat de pieces de type echecs (avec regles et variantes gameplay)
- Gestion de royaumes (or, production, controle de batiments publics)
- Construction de structures (murs, baraquements, etc.)
- Systeme de tours avec actions planifiees avant validation
- UI complete (HUD, panneaux contextuels, journal d'evenements)
- Sauvegarde/chargement de partie
- Multijoueur client/serveur en LAN

## Ce qu'on peut y faire

- Demarrer une nouvelle partie ou charger une sauvegarde
- Selectionner pieces/batiments/cellules et planifier des actions
- Deplacer les pieces, capturer, produire des unites, construire des structures
- Suivre l'economie, l'etat des royaumes et le journal d'evenements
- Jouer en local ou rejoindre/heberger une session multijoueur

## Stack technique

- C++17
- CMake 3.20+
- SFML 2.6 (`graphics`, `window`, `system`, `network`)
- TGUI 1.10.0 (recupere automatiquement via CMake FetchContent)

## Prerequis build

### Generaux

- Un compilateur C++17 (MSVC, clang++, g++)
- CMake >= 3.20
- Git + acces internet (pour telecharger TGUI a la configuration)
- SFML 2.6 installe et trouvable par CMake

### Windows (recommande pour ce depot)

Le `CMakeLists.txt` est configure avec des chemins MSYS2 UCRT64 (`C:/msys64/ucrt64`) et copie des DLL runtime depuis cet emplacement.

Prerequis recommandes:
- MSYS2 installe dans `C:/msys64`
- Ouvrir un shell `MSYS2 UCRT64`
- Installer paquets:

```bash
pacman -S --needed mingw-w64-ucrt-x86_64-toolchain mingw-w64-ucrt-x86_64-cmake mingw-w64-ucrt-x86_64-ninja mingw-w64-ucrt-x86_64-sfml git
```

### macOS

- Installer SFML 2.x via Homebrew (`sfml@2`) si necessaire
- Le projet detecte automatiquement `/opt/homebrew/opt/sfml@2` ou `/usr/local/opt/sfml@2`
- Cocoa est requis (gere par CMake)

### Linux

- Installer CMake, compilateur C++17, SFML dev et Git
- Selon distribution, il peut etre necessaire d'indiquer `CMAKE_PREFIX_PATH` pour SFML

## Build et execution

## Windows (MSYS2 UCRT64, Ninja)

Depuis la racine du projet:

```bash
cmake -S . -B build -G Ninja -DCMAKE_BUILD_TYPE=Release -DCMAKE_PREFIX_PATH=C:/msys64/ucrt64
cmake --build build -j
./build/ANormalChessGame.exe
```

## Windows (Visual Studio generator)

```powershell
cmake -S . -B build -G "Visual Studio 17 2022" -A x64 -DCMAKE_PREFIX_PATH="C:/msys64/ucrt64"
cmake --build build --config Release
.\build\Release\ANormalChessGame.exe
```

## macOS / Linux

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build -j
./build/ANormalChessGame
```

## Notes importantes de runtime

- Les assets sont copies automatiquement vers `build/assets` lors du build.
- Un dossier `saves` est cree automatiquement a cote de l'executable.
- Sur Windows, le script CMake copie aussi les DLL runtime SFML/MSYS2 necessaires si elles sont presentes.

## Structure du projet (resume)

- `src/Core`: boucle de jeu, moteur, validation d'etat
- `src/Systems`: regles metier (tour, combat, economie, meteo, etc.)
- `src/Runtime`: coordinateurs entre moteur, UI, rendu, multijoueur
- `src/Render`: camera, rendu principal, overlays
- `src/UI`: menus, HUD, panneaux contextuels
- `src/Multiplayer`: protocole, client, serveur, runtime reseau
- `src/Save`: sauvegarde/chargement
- `assets`: configurations, textures, fonts, UI

## Documentation interne

- Rapport complet d'analyse C++: `CPP_CODEBASE_REPORT.md`
