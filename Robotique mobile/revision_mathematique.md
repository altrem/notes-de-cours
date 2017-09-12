# Révision mathématique

## Angles et cercles

### Radians

Angles en radians: Toujours conserver -pi <= theta <= pi.
Fonction s’apparentant à wrapToPi() sur Python?

### Géométrie d’un cercle

Besoin d’un compas à l’examen.

Tangente: Perpendiculaire au rayon

### Théorème de l’angle inscrit

 Arc $p1$ à $p2$, angle $\theta$ pour cet arc depuis le centre. Tout point $p3$ sur le reste du cercle (hors l’arc) a un angle constant $p1p3p2$ nommé $\omega$ où:

 $\omega$ = $\frac{\theta}{2}$

 Voir les notes de cours.

## Matrices

### Addition de matrices

Ajouter chaque case de la matrice $A$ avec la case à la même position de la matrice $B$.

### Multiplication de matrices

Pour une case $i,j$ de la matrice résultante, faire le produit scalaire de la rangée $i$ de la matrice A avec la colonne $j$ de la matrice $B$.

## Séries de Taylor

Représentation d'une fonction $f$ par une série infinie de dérivées de $f$ à un point $a$. On prend les $n$ premiers termes, et l'absence du reste nous donne une erreur sur le résultat de la fonction $f$.

$f(x) = f(a) + \frac{z'(x - a)}{1!} + \frac{z''(x - a)^2}{2!} + \frac{z'''(x - a)^3}{3!} + ...$

En résumé, la SdT nous permet d'approximer n'importe quelle fonction.

Choisis un point d'opération $a$.

Choisis le nombre de terme. Pour rendre linéaire, prendre seulement la première dérivée.

### Approximation de sin et cos pour des petits angles

$sin(\theta) = sin(0) + cos(0)\theta - 0.5sin(0)\theta^2 + ...$

Approximation linéaire pour $sin(\theta)$: $\theta$

$cos(\theta) = cos(0) - sin(0)\theta - 0.5cos(0)\theta^2 + ...$

Approximation linéaire pour $cos(\theta)$: 0

## Intégration

Se fera surtout de façon numérique.

## Robotique: combine matrice + intégration

Système linéaire (approximatif) représentant l'évolution de l'état d'un robot dans le temps.

Vecteur d'état $X = [x, v]$

Équations du système:

$x_{t+1} = x_t + v_t\delta t$

$v_{t+1} = v_t$

On peut faire un système d'équations $Ax = y$ avec cela. Il s'agit de notre estimation d'état.