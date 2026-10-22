# VibeOie
jeu de l'oie de base pour TP vibecoding

L'ensemble du jeu est dans le fichier jeu_de_l_oie_le_jardin_des_oies.html
le graphique du plateau est donné dans le fichier plateau jeu oie.png

Version modifiée (règles simplifiées) :

- **Plateau de 100 cases** (spirale 14×10), arrivée **exacte** sur la case 100 : si le dé dépasse, le joueur reste sur sa case.
- **Un seul dé** (1 à 6).
- **Plus aucune carte** (ni Chance, ni Action en main). Les actions n'existent que sur les cases du plateau.
- **Collision** : si un joueur termine son déplacement normal sur une case occupée, duel au dé (égalité = relance, départage déterministe après 20 égalités). Le gagnant garde la case, le perdant retourne sur la case que le joueur actif occupait avant son lancer. Plusieurs occupants : duels successifs dans l'ordre de jeu. Aucun duel en cascade.
- **2 à 5 joueurs.**

De nouvelles actions de case peuvent être ajoutées avec `registerGooseAction(actionObject)` (ou via le bouton **« API Actions (IA / Dev) »**).

#### Format de l'objet Action :

- `id` *(String)* : identifiant unique en `snake_case`.
- `name`, `description`, `icon` *(String)* : affichage.
- `theme` *(String)* : `'green'`, `'blue'`, `'yellow'`, `'purple'`, `'red'`.
- `defaultWeight` *(Number)* : poids relatif (0 à 100).
- `canBeOnBoard` *(Boolean)* : peut apparaître sur une case. (`canBeChanceCard` / `canBePlayerCard` sont obsolètes et ignorés.)
- `execute(gameState, playerId, context)` :
  - `gameState` : `players` (`{ id, name, position (1 à 100), skipTurns }`), `board` (100 cases `{ number, actionId }`), `turnIndex`, `round`, `maxCell` (`100`).
  - `context` : `{ source: 'CELL', cellNumber, lastRoll }`.
  - Pour avancer, utiliser `moveForwardCapped(gameState, player, n)` (retourne `false` sans déplacer si la case 100 serait dépassée).
  - Retour : `{ gameState, message: String, extraTurn: Boolean }`.
