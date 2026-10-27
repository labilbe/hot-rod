# Hot Rod '88

Un jeu de course en vue de dessus, dans l'esprit du *Hot Rod* que Sega sortait en 1988 sur
System 16 : <https://labilbe.github.io/hot-rod/>

Le chrono est l'adversaire. On part avec quarante secondes, chaque banderole **CHECK POINT**
en rend vingt-deux, et la manche s'arrête là où le compteur tombe à zéro. Entre deux manches,
l'argent ramassé sur la route passe au garage.

## Jouer

| Touche | Effet |
| --- | --- |
| `↑` `W` | Accélérer |
| `↓` `S` | Freiner, puis reculer une fois à l'arrêt |
| `←` `→` | Braquer |
| `Espace` | Coup de nitro |
| `P` · `M` | Pause · couper le son |

La manette est reconnue : stick gauche pour un braquage proportionnel, `RT` et `LT` en
gâchettes analogiques, `X` ou `LB` pour la nitro, `START` pour valider et mettre en pause.
Elle vibre aux chocs, au nitro et au passage des checkpoints. Un navigateur n'annonce une
manette qu'après une première pression sur un bouton : la fiche d'instructions affiche son
état. Sur mobile, quatre touches tactiles apparaissent sous l'écran.

## Ce qu'il y a dedans

- **Cinq manches** — Coastal Highway, Desert Run, Night City et ses phares, Mountain Pass,
  Final Circuit. Chaque tracé est engendré à la volée depuis une graine fixe : il est donc
  toujours le même, sans qu'aucune carte soit stockée.
- **Trois rivaux** qui suivent la trajectoire, lèvent le pied dans les courbes selon la
  courbure à venir, évitent les obstacles, ramassent les billets, et qu'un léger élastique
  garde à portée.
- **Une conduite arcade** : vitesses longitudinale et latérale tenues séparément, ce dont le
  dérapage découle tout seul. L'herbe plafonne à la moitié de la vitesse, l'huile annule
  l'adhérence, les barils et les blocs cassent l'élan.
- **Un garage** — moteur, pneus, freins, nitro, blindage, cinq niveaux chacun, à des prix
  qui montent. C'est là que part la recette : $4 000 pour une victoire, $250 le sac de
  billets, $60 la seconde restante.
- **Du son synthétisé de bout en bout**, sans un seul fichier audio : le moteur suit le
  régime, et trois boucles de musique originales dans l'idiome YM2151 — attract, course,
  garage — transposées à chaque manche. Sous dix secondes, le tempo monte de 18 %, comme le
  faisaient les bornes.

## Sous le capot

Une page, sans dépendance ni étape de construction : `index.html` porte la feuille de style,
le balisage de la borne et le moteur de jeu. Tout le rendu passe par un canevas en
960 × 720 unités logiques, redimensionné selon la densité de l'écran ; la physique tourne à
pas fixe de 1/60 s avec un accumulateur, indépendamment de la fréquence d'affichage.

Le son est entièrement bâti sur l'API Web Audio : oscillateurs, filtres et un tampon de bruit
partagé. Le séquenceur musical planifie les notes en avance sur l'horloge audio plutôt que
sur `setInterval`, seule façon d'obtenir un tempo qui ne flotte pas.

Les meilleurs gains sont gardés dans `localStorage`, dans un `try` : un navigateur qui refuse
le stockage fait perdre le score, pas la partie.
