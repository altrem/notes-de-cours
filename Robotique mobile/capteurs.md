# Capteurs

Reposent sur un transducteur qui convertit une grandeur physique $A$ en une autre $B$. Cette grandeur physique $B$ est généralement facile à mesurer.

- Voltage
- Résistance
- Courant

## Catégories

### Actif

Émet de l'énergie dans l'environnement.
Exemples:

- Radar
- Laser
- Caméra avec flash
- Sonar

| Points positifs (+) | Points négatifs (-) |
| --------------- | --------------- |
| Robuste car + indépendant de l'environnement | Interférence entre capteurs |
| Bonne qualité d'information | Énergivore |
| Moins bruité | Détectable par autrui |

### Passif

Se base sur l'énergie de l'environnement.
Exemples:

- Caméra sans flash
- Microphone

| Points positifs (+) | Points négatifs (-) |
| --------------- | --------------- |
| Moins intrusif | Dépend de l'environnement |
| Difficile à détecter | Moins précis/plus bruité |
| Possiblement moins énergivore | |

### Proprioceptif

Donne de l'information sur l'état interne du robot.
Par exemple, si je suis téléporté dans le vide intersidéral, j'aurais encore des mesures.

### Extéroceptif

Donne de l'information sur l'environnement.
Lorsqu'un blackout de ces capteurs se produit, les capteurs *propriceptifs* peuvent continuer à donner un estimé, qui diverge de plus en plus avec le temps.

## Caractéristiques

### Plage dynamique

Différence entre min et max senti. Important pour des capteurs comme microphone et caméra.

- **Oreille**: facteur 10 000 000 000
- **Oeil**: facteur 1 000 000 000
- **Caméra CCD 16 bits**: facteur 65 536

### Sensibilité

Essentiellement le ratio $\frac{\Delta sortie}{\Delta entrée}$.

### Linéarité

On préfère les capteurs ayant une relation la plus linéaire possible avec une grandeur physique.

### Temps de réponse

Temps requis pour changement entre entrée et sortie. Important pour un véhicule routier, par exemple.

### Résolution

Plus petit incrément observable. Souvent dicté par le nombre de bits du convertisseur.

### Répétabilité

Différence entre mesures consécutives quand on ne change rien. Variance sur le bruit, en bref. Peut se régler par une meilleure calibration.

### Précision

Différence entre mesuré et actuel.

### Bande passante

Quantité d'information par seconde.

## Problèmes associés

Donne une information incomplète et de bas niveau.
Par exemple:

- Perte de la 3ème dimension dans une photo;
- Pas de numéro de local, mais un scan de la pièce.

Il y a aussi le fait que les mesures sont bruitées. Il y a donc des fluctuations aléatoires du signal. Elles sont souvent modéllisées par une distribution gaussienne (normale). Pour *Python*, il y a ***numpy.random.normal***.
La qualité est souvent proportionnel au prix du capteur.

### Modèle de capteur

Pour beaucoup de méthodes, il faut avoir un modèle du capteur.

$z = f_{capteur}(monde)$

Plus le modèle $f_{capteur}$ colle à la réalité, meilleure sera l'estimation. Impossible de modéliser toute la physique sousjacente, donc on approxime.

### Inverse de la fonction capteur

Si j'ai un bon modèle $z = f_{capteur}(monde)$, je devrais pouvoir retrouver un l'état du monde?

$monde = f_{capteur}^{-1}(z)$

Réponse: NOPE. Il y a problème de perception due à la reconstruction incomplète du capteur.

## Problème bien posé: définition

Un modèle mathématique des phénomères physiques devrait avoir ces propriétés:

1. Une solution **existe**
1. La solution est **unique**
1. La solution dépend de façon continue des données (**stable**)

Lorsque ces trois critères sont remplies, on a un problème **bien posé**.

Dans ce cas, la fonction inverse

$monde = f_{capteur}^{-1}(z)$

est un problème **mal posé**.

## Convertisseurs analogue-numérique

Échantillonne un signal à intervelle régulier à une fréquence d'échantillonnage $f_e$ (Hz). Cela permet à un ordinateur de lire le monde extérieur.

Critère de Nyquist: $f_e > 2f_{max}$

En bref, il faut que la fréquence d'échantillonnage soit au moins deux fois plus élevée que la fréquence maximale des variations aléatoires de la mesure (bruit).

### Capteurs de position angulaire

#### Potentiomètre

On utilise un *potentiomètre*. Il s'agit d'une résistance électrique variable. La résistance est fonction **linéaire** de l'angle de rotation.

Problèmes associés:

- Friction
- Bruit si poussière
- Usure

#### Encodeurs optiques

On peut aussi utiliser des *codeurs optiques*, tant relatifs (encodeur incrémental) qu'absolus. Dans le cas de l'encodeur absolu, un seul bit change par déplacement (Code Grey). Il est moins sensible aux erreurs que l'encodeur relatif.

#### Capteurs magnétiques interrupteur

Détection de l'angle de référence. On a un capture magnétique face à un disque rotatif contenant des aimants.

### Capteurs de proximité

#### Capacitance

Capacitance: capacité à enmmagasiner une charger électrique. Ce n'est **pas** un capteur linéaire.

Un tel capteur mesure le changement de capacitance.
Utilisé par exemple dans les écrans tactiles.

#### Infrarouge

Capteur proximité très simple, assez répandu en robotique.
Fonctionne par émission IR modulée, afin de la distinguer de sources ambiantes comme le soleil ou l'éclairage. Il y a donc détection de la réflexion sur une surface quelconque.

**Note:** Étant donné qu'on mesure la position d'un point lumineux sur la caméra et non l'intensité lumineuse, le capteur n'est que peu impacté par la réflectance (i.e. la couleur de la surface)

Un tel capteur a un coût peu élevé: 15 $.

- Si retour signal IR $=>$ Obstacle présent.
- Absence de retour IR -> Absence d'obstacle? *Pas nécessairement (couleur noire, miroir, angle prononcé*)

De plus, un capteur de proximité infrarouge est de courte portée. La distance maximale varie selon le capteur de 50 cm à 2 m.

### Capteurs tactiles

Détection contact mécanique avec obstacle (interrupteur électrique binaire)

Pour une "voiture", on a un pare-choc sensible à la pression/force.

Un capteur tactile est souvent la dernière ligne de défense.

#### Pression

Peau synthétique de caoutchouc résistif.
Pression signifie changement de résistance. On détecte le changement par matrice de contact électrique (balayage 2D de résistance électrique de la surface).

### Capteurs par temps de vol

#### Sonar

- Appelé aussi *capteur ultrasonique*
- Même principe que les chauve-souris
  - Il y a émission d'un son court, par exemple 1.2 ms, et qui contient une multitude de fréquences
- Premier problème: On doit pouvoir détecter l'écho (pas toujours évident)

Distance du temps de vol $d = \frac{vt}{2}$ où $v \approx 330$ m/s dans l'air.

La distance mnimum est donc $165t_{chirp}$ (21 cm pour 1.2ms).
> Note: La forme du faisceau impacte la résolution spatiale de capteur. La forme du faisceau "idéale" ressemble à celle du laser. Mais ordinairement on a un type de cône.

Il y a aucun écho s'il y a **réflexion spéculaire**, car le signal est perdu. Il y a aussi une erreur due au coin de cube:

- Rayon est réfléchi deux fois sur deux pans de mur en coin.
- Le calcul de la distance est faux.
- Un mur fantôme apparaît à 45 degrés du coin.

#### Télémètre (LiDAR)

Mesure du temps de vol d'une impulsion laser (1D). L'écho lumineux du laser est beaucoup plus diffus.

Deux méthodes de calcul:

- Par délai (horloge)
- Par différence de phase

Portée: dépend de la puissance (de $m$ à plusieurs $km$)
Précision: de l'ordre du millimètre.

Problèmes:

- Détection des objets noirs
- Verre
- Grilles d'aération

On fait un balayage 2D par miroir rotatif.

Un **faisceau étroit** a une longue portée et une bonne résolution spatiale mais il y a beaucoup d'angle morts.

Un **faisceau large** est plus sécuritaire (car pas d'angles morts) mais peut créer des artéfacts.

On peut avoir une caméra active qui mesure la réflectance de la surface, indépendamment de l'illumination ambiante.

#### Radar

- Fréquence radio de 1 à 12.5 GhZ
- Pulsé: temps de vol
- Effet Doppler: changement de fréquence (vitesse de la cible)
- Signal difficile à interpréter

