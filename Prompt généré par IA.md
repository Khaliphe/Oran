Modification du jeu de l’oie existant à l’aide d’une IA générative

1. Contexte et fichiers fournis
    

Tu disposes des ressources suivantes :

Le code HTML du jeu de l’oie existant, comprenant éventuellement du CSS et du JavaScript intégrés ou associés.

Le fichier README.md, qui décrit le fonctionnement du jeu, son architecture technique, ses dépendances et les éléments qui peuvent ou ne peuvent pas être modifiés.

Une image de référence du plateau de jeu, qui sert de modèle visuel pour la conception du plateau final.

Des éventuels fichiers complémentaires nécessaires au fonctionnement du projet.

Ta mission est de modifier le jeu existant en respectant son architecture, tout en intégrant les nouvelles règles décrites ci-dessous.

Avant de commencer les modifications, analyse attentivement tous les fichiers fournis. Consulte en priorité le README.md afin de comprendre le fonctionnement du projet, les contraintes techniques et les limites à respecter.

2. Objectif général
    

Faire évoluer le jeu de l’oie existant en conservant ses fonctionnalités essentielles et son identité visuelle, tout en supprimant le système de cartes et en appliquant de nouvelles règles de déplacement.

Le résultat doit être un jeu fonctionnel, cohérent, jouable et fidèle aux contraintes décrites dans ce prompt.

Il ne s’agit pas de recréer intégralement le projet sans raison, mais de modifier le code existant de la manière la plus ciblée, propre et fiable possible.

3. Modifications obligatoires des règles du jeu
    

Règle 1 — Suppression complète du système de cartes

Le concept des cartes doit être entièrement supprimé du jeu.

Cela comprend notamment, si ces éléments existent dans le projet :

Les paquets de cartes, leur tirage et leur affichage.

Les interfaces, boutons, fenêtres ou animations associés aux cartes.

Les événements et fonctions JavaScript dédiés à la gestion des cartes.

Les effets sur le déplacement ou la progression des joueurs déclenchés par les cartes.

Les références inutiles aux cartes dans l’interface et dans le code.

Toutes les mécaniques qui dépendaient exclusivement des cartes doivent être retirées ou adaptées, sans casser les autres fonctionnalités du jeu.

Ne conserve aucun système de cartes résiduel, sauf si une dépendance technique explicitement documentée impose une adaptation particulière. Dans ce cas, explique clairement la contrainte avant de procéder.

Règle 2 — Utilisation d’un seul dé

Le jeu doit utiliser un seul dé pour déterminer les déplacements des joueurs.

Chaque lancer produit un résultat compris entre 1 et 6 inclus.

Le déplacement normal d’un joueur correspond au résultat obtenu.

L’interface doit représenter clairement le résultat du lancer.

Si le jeu possède déjà une animation de lancer ou une représentation visuelle du dé, conserve-la et adapte-la plutôt que de la remplacer inutilement.

Toute ancienne logique utilisant deux dés doit être supprimée ou adaptée.

Le résultat affiché doit toujours correspondre au résultat réellement utilisé par la logique de déplacement.

Règle 3 — Gestion des collisions entre joueurs sur une même case

Si un joueur termine son déplacement sur une case déjà occupée par un autre joueur, un lancer de dé supplémentaire doit être effectué pour déterminer lequel des deux joueurs conserve la case.

Le fonctionnement doit être le suivant :

Le joueur actif effectue son lancer normal et se déplace.

Si sa case d’arrivée est déjà occupée par un autre joueur, un lancer de dé supplémentaire est déclenché.

Ce lancer supplémentaire détermine lequel des deux joueurs conserve la case contestée.

Le gagnant reste sur la case contestée.

Le perdant est déplacé sur la case que le gagnant occupait avant son lancer normal, c’est-à-dire sa position précédente.

Déroulement précis du duel :

Chaque joueur impliqué dans le duel effectue un lancer avec le même dé, soit deux lancers individuels au total.

Le joueur qui obtient le résultat le plus élevé remporte le duel et conserve la case contestée.

En cas d’égalité, les deux joueurs relancent le dé jusqu’à ce qu’un résultat différent permette de les départager.

Le perdant est déplacé sur la position que le joueur actif occupait avant son déplacement normal.

Si plusieurs joueurs occupent la case contestée, les duels sont résolus successivement, en respectant une règle d’ordre déterministe.

Les lancers du duel ne constituent pas des tours de jeu normaux et ne modifient pas l’ordre habituel des joueurs.

Exemple concret :

Le joueur A se trouve sur la case 20.

Le joueur B se trouve sur la case 24.

Le joueur A lance le dé et obtient 4 : il arrive sur la case 24.

Les deux joueurs se retrouvent donc sur la case 24.

Un lancer supplémentaire est effectué pour départager les joueurs.

Le joueur qui gagne ce duel reste sur la case 24.

Le joueur perdant est placé sur la case 20, qui correspond à la position du joueur A avant son déplacement initial.

Cette règle doit être implémentée de manière cohérente avec l’ordre des joueurs, leurs positions précédentes et la gestion des tours.

Précisions importantes :

La position de référence pour le déplacement du perdant doit être enregistrée avant le lancer normal du joueur actif.

Le résultat du lancer supplémentaire doit être exploité par une règle de victoire et de défaite clairement définie.

Si le résultat du duel est identique pour les deux joueurs, applique une règle de départage cohérente et documentée, sans créer de boucle infinie.

Évite que le traitement d’une collision déclenche involontairement une nouvelle collision en cascade.

Le joueur déplacé à la suite du duel ne doit pas effectuer un nouveau déplacement normal ni rejouer automatiquement, sauf si une règle existante et explicitement conservée le prévoit.

Si plusieurs joueurs peuvent se retrouver sur la même case, prévois un traitement cohérent de cette situation, compatible avec le principe de duel décrit ci-dessus.

La position de référence doit être enregistrée une seule fois, avant le déplacement normal du joueur actif, et conservée jusqu'à la résolution complète du duel. Elle ne doit jamais être recalculée après un déplacement intermédiaire.

Le traitement des collisions ne doit pas modifier accidentellement cette position de référence. Si le déplacement du perdant provoque une nouvelle collision, applique une procédure déterministe et sans récursion infinie, tout en conservant les positions de référence nécessaires au duel initial.

Phase d'analyse préalable :

Avant toute modification, identifie :

Les fichiers qui constituent le jeu et leurs dépendances.

La fonction responsable des lancers de dés.

La fonction responsable du déplacement des joueurs.

La fonction responsable de la gestion des tours.

Le système de cartes et toutes ses dépendances.

La représentation du plateau et la logique de numérotation des cases.

Le mécanisme de détection de victoire.

Le système de gestion des joueurs, des pions et des collisions.

Établis un plan de modification concis indiquant les fichiers et fonctions concernés. Puis effectue les changements nécessaires en évitant de modifier les parties indépendantes des nouvelles règles.

Règle 4 — Plateau de 100 cases et arrivée exacte

Avant de modifier le code, identifie les cases spéciales et les effets de jeu déjà présents.

Supprime les effets qui dépendent exclusivement du système de cartes.

Conserve les autres règles et effets de cases s'ils sont compatibles avec les nouvelles contraintes.

Ne crée aucune nouvelle règle de case spéciale sans instruction explicite.

Vérifie que les effets conservés ne permettent pas de dépasser la case 100 ni de déclencher une victoire incorrecte.

Si une règle existante est incompatible avec les nouvelles règles, explique le conflit et propose une adaptation minimale.

Le plateau doit comporter exactement 100 cases numérotées de 1 à 100.

La case 100 représente la case d’arrivée.

Pour gagner, un joueur doit atteindre exactement la case 100. Il ne peut pas dépasser cette case.

Les règles de déplacement sont les suivantes :

Si le résultat du dé permet d’atteindre la case 100 exactement, le joueur y arrive et remporte la partie, sous réserve des autres règles de victoire éventuellement conservées.

Si le résultat du dé dépasse la distance restante jusqu’à la case 100, le joueur ne doit pas dépasser la case d’arrivée.

Dans ce dernier cas, le joueur avance uniquement du nombre de cases qui le sépare de la case 100 moins une, si nécessaire pour respecter la règle d’arrivée exacte, ou reste à sa position si la règle de déplacement retenue l’exige.

Aucun déplacement ne doit placer un joueur au-delà de la case 100.

Règle de déplacement vers l'arrivée :

La position d'arrivée est calculée en additionnant la position actuelle du joueur et le résultat du dé.

Si le résultat est inférieur ou égal à la distance restante jusqu'à la case 100, le joueur avance normalement.

Si le résultat est supérieur à cette distance, le joueur reste sur sa case de départ.

Un joueur ne peut jamais dépasser la case 100.

La victoire est déclenchée uniquement lorsque le joueur atteint effectivement la case 100.

La logique de déplacement doit donc être adaptée pour empêcher tout dépassement de la case 100. Dans cette version, un joueur qui dépasse virtuellement la case d’arrivée avec son lancer reste sur sa case de départ.

La vérification de la victoire doit être effectuée au bon moment afin d'éviter qu'un joueur soit déclaré gagnant avant que les règles de déplacement et les éventuels effets de collision aient été correctement traités.

4. Contraintes techniques et préservation du projet
    

Le fichier README.md constitue la référence prioritaire pour comprendre l’architecture et les limites du projet.

Tu dois donc :

Respecter les technologies, bibliothèques, conventions et dépendances déjà utilisées.

Préserver les fonctionnalités existantes qui ne sont pas incompatibles avec les nouvelles règles.

Conserver autant que possible la structure HTML, les styles CSS, les fonctions JavaScript et les composants existants.

Ne pas supprimer de fonctionnalité sans justification.

Éviter de réécrire entièrement le projet si des modifications ciblées suffisent.

Ne pas ajouter de dépendance externe sans nécessité réelle.

Maintenir la compatibilité entre les fichiers HTML, CSS et JavaScript du projet.

Préserver l'accessibilité et la lisibilité de l'interface.

Éviter les duplications de code et les effets de bord.

Si une fonctionnalité existante entre en conflit avec les nouvelles règles, donne la priorité aux règles explicitement définies dans ce prompt, tout en limitant les modifications aux parties concernées.

Si une instruction est incompatible avec une contrainte technique décrite dans le README.md, identifie le problème et propose une solution compatible avant de procéder.

5. Respect de l’image de référence du plateau
    

Utilise l’image fournie comme référence visuelle pour le plateau de jeu.

Respecte autant que possible sa disposition, son organisation, ses couleurs et son style graphique.

Assure-toi que le plateau représente exactement 100 cases.

Vérifie que la numérotation des cases est cohérente et que la case 100 est clairement identifiable.

Adapte l’affichage si nécessaire pour garantir que tous les joueurs, leurs pions et les numéros des cases restent lisibles.

Préserve l’identité visuelle du jeu existant lorsque cela est compatible avec l’image de référence et les nouvelles règles.

Ne modifie pas arbitrairement le design du plateau si aucune modification n’est nécessaire au fonctionnement du jeu.

6. Gestion des tours et de l’interface
    

Adapte l’interface et la logique de jeu aux nouvelles règles.

Le joueur actif doit être clairement identifiable.

Le résultat de chaque lancer doit être visible.

Le lancer supplémentaire lié à une collision doit être identifiable comme un duel entre joueurs.

Le résultat du duel et le déplacement du perdant doivent être compréhensibles pour les joueurs.

La victoire doit être annoncée clairement lorsque la case 100 est atteinte exactement.

Les boutons et interactions doivent rester cohérents avec l’état réel du jeu.

Aucun lancer ne doit être effectué au mauvais moment ou en double à cause d’un problème de gestion des événements.

Conserve les mécanismes de gestion des tours déjà présents lorsqu’ils restent compatibles avec les nouvelles règles.

7. Vérifications et tests obligatoires
    

Après les modifications, vérifie le fonctionnement du jeu et teste au minimum les cas suivants :

Un lancer normal avec un seul dé produit un résultat compris entre 1 et 6.

Le déplacement normal correspond au résultat du dé.

Aucun tirage de carte ni aucune interface liée aux cartes ne subsiste.

Une collision déclenche bien un lancer supplémentaire.

Le gagnant du duel reste sur la case contestée.

Le perdant du duel revient sur la position que le joueur A occupait avant son déplacement initial, conformément à la règle définie.

Un résultat de duel identique est correctement géré.

Un joueur sur la case 97 qui obtient 3 atteint la case 100 et gagne.

Un joueur sur la case 97 qui obtient 5 reste sur la case 97.

Un joueur sur la case 95 qui obtient 5 atteint la case 100 et gagne.

Aucun joueur ne peut dépasser la case 100.

Le plateau affiche exactement 100 cases numérotées correctement.

La gestion des tours, des pions et des états de victoire reste fonctionnelle.

Si des tests automatisés existent déjà, adapte-les et exécute-les. Sinon, effectue des vérifications ciblées dans le code et, si possible, dans le jeu en fonctionnement.

Ne prétends pas avoir exécuté un test ou vérifié visuellement un résultat si tu ne disposes pas des moyens nécessaires pour le faire.

8. Idées et contraintes additionnelles
    

Cette section est réservée aux demandes complémentaires que je pourrais ajouter par la suite.

Instructions additionnelles à prendre en compte :

Les graphismes n’ont pas besoin de changer nécessairement, le nombre de joueurs est compris entre 2 et 5,

Ces instructions devront être intégrées au projet dans la mesure où elles sont compatibles avec les contraintes techniques du README.md et les règles obligatoires précédentes.

En cas de conflit, signale précisément le problème et propose une solution plutôt que de modifier silencieusement une règle obligatoire.

9. Résultat attendu
    

À la fin de ton travail, fournis :

Le code complet des fichiers modifiés, dans leur intégralité lorsque cela est possible.

La liste des fichiers créés, modifiés ou supprimés.

Un résumé des principales modifications effectuées.

Une explication concise de la manière dont les quatre nouvelles règles ont été implémentées.

Les tests réalisés et leurs résultats.

Les éventuels problèmes non résolus, limitations techniques ou points nécessitant une validation manuelle.

Ne fournis pas uniquement des extraits de code ou des conseils généraux : réalise les modifications directement dans les fichiers du projet lorsque ton environnement le permet. Si tu ne peux pas modifier directement les fichiers, fournis le contenu complet des fichiers modifiés et indique clairement où les placer.

Priorité absolue : respecter les quatre nouvelles règles du jeu, préserver l’architecture existante autant que possible et obtenir un jeu fonctionnel sans régression des fonctionnalités conservées.

**