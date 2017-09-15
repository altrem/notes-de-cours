# Cours 2

## Retour sur le premier cours

Pour la représentation machine d'une nombre

- 32 bits: généralement 6-7 C.S.
- 64 bits: généralement 15-16 C.S.

On a $\epsilon_{m}= max \Delta x / x \approx b^{1-N}$ où N est la longeur de la mantisse.

L'erreur absolue $\Delta x = fl(x) - x$

$\Delta x \approx |x|\epsilon_m$

Pour trouver le nombre de chiffres significatifs, il faut trouver m tel que:

$0.5 \times 10^{1-m} \leq \Delta x \leq 0.5 \times 10^m$

Ex:

$$
b = 2, n = 53, x = \frac{1}{9}
$$
$$
|f(x) - x| \approx |x|\epsilon_m = \frac{1}{9} * b^{-52} = 0.24 \times 10^{-52}
$$

où $f(x) - x$ est égal à $x^*$. On a donc 16 C.S.

## Erreurs dues aux opérations arithmétiques

Soit les réels $x$ et $y$.

On suppose que la somme de réels $x + y => fl(fl(x) + fl(y))$

On suppose que la différence de réels $x - y => fl(fl(x) - fl(y))$

Idem pour la multiplication et la division.

Ex:

$$N = 4, b = 10$$

$$x = 0.1000 \times 10^2 = fl(x), y = fl(y) = 0.1000 \times 10^{-2}$$

Alors:

$$
x + y = fl(0.1000 \times 10^2 + 0.1000 \times 10^{-2})
$$

$$
x + y = fl(0.1000 \times 10^2 + 0.0000 \times 10^2)
$$

Il y a perte de $y$! La réponse finale est donc:

$$
x + y = 0.1000 \times 10^2
$$

Ex:

$$N = 4, b = 10, \epsilon_m = 10^{-3}$$

$$
\Delta (x - y) \approx (0.1000 \times 10^3)\epsilon_m = 0.1 \leq 0.5 \times 10^0
$$

Donc,

$$
0.10\textbf{0}0 \times 10^3
$$
Notons qu'ici, le $^0$ indique que le dernier chiffre significatif à droite est à la position de l'unité. Le dernier chiffre significatif dans la représentation en virgule flottante est donc le troisième 0.

On aura 3 C.S ? On génère artificiellement des chiffres significatifs lors de la soustraction.

Ex:

$$x = 0.70, y = 0.33, z = 0.83$$

En tant qu'humain, $x + y + z = 1.86$

$$b = 10, N = 2$$

$$
x + y => fl(fl(x) + fl(y))
$$
$$
x + y => fl(1.03 \times 10^1) = 0.10 \times 10^1
$$

$$
x + y + z => fl(0.10 \times 10^1 + fl(z))
$$

$$
x + y + z = fl(0.10 \times 10^1 + 0.08 \times 10^1)
$$

$$
x + y + z = 0.18 \times 10^1
$$

On a perdu le 0.06!

Dans un autre ordre:

$$
y + z = fl(0.33 + 0.83)
$$

$$
y + z = fl(1.16)
$$

$$
y + z = fl(0.116 \times 10^1) = 0.12 \times 10^1
$$

$$
x + (y + z) = fl(0.70 + 0.12 \times 10^1)
$$

$$
x + (y + z ) = fl(0.07 \times 10^1 + 0.12 \times 10 ^1)
$$

$$
x + (y + z) = 0.19 x 10^1
$$

Ici, on a 1.90 et non 1.86!

**Conclusion**: L'ordre des opérations influence donc l'erreur associée! Mais il y a *toujours* une erreur.

>*Corollaire!* Moins il y a d'opérations dans l'algorithme, plus la précision de la réponse est élevée.

## Évaluation d'une fonction

Il faut transformer la fonction en un polynôme.
Écriture

$$
p_n(x) = a_0 + a_1x + a_2x^2 + ... + a_nx^n
$$

Ex:

$$
p_3(x) = 3 + 4x + 5x^2 + 6x^3
$$

Résolvons par la méthode *brutale*.

$p_3(2)$ ?

$$
3 + 4*2 = 2 opérations
$$
$$
+
5 * 2*2 = 3 opérations
$$
$$
+
6 * 2*2*2 = 4 opérations
$$

On a 9 opérations. Essayons maintenant en *factorisant*:

$p_3(2$) ?

$$
p_3(x) = 3 + x(4 + x(5 + 6x))
$$

Alors:

$5 + 6 * 2$ = 2 opérations

$4 + 2 * (5 + 6 * 2)$ = 2 opérations

$3 + 2 * (4 + 2 * (5 + 6 * 2))$ = 2 opérations

On a donc 6 opérations ici. On évalue seulement une addition et une multiplication à chaque "étape" ici!.

> Il s'agit de l'**algorithme de Horner**. Il demande $2n$ opérations, où $n$ est le degré du polynôme.

## Représentation des opérations trigonométriques

On peut approximer une opération trigonométrique par un développement de Taylor dont on prend un certain nombre de termes.

Soit $f$ une fonction dérable $n$ fois à la valeur $x_0$.

Le polynôme de Taylor de degré $n$ s'écrit de $f$ autour de $x_0$ est défini par:

$$
p_m(x) = f(x_0) + (x - x_0)f'(x_0) + \frac{(x - x_0)^2}{2!}f''(x_0) + ... + \frac{(x - x_0)^n}{n!}f^{(n)}(x_0)
$$

Ex: $f(x) = e^x$

Approximation de $f(x)$ par une constante:

$$
p_0(x) = f(x_0)
$$

Si $x_0 = 0$, l'approximation $f(x) = e^x$ pour une constante $x_0 = 0$ est

$$
p_0(x) = 1
$$

Approximation de $f(x)$ par une droite:

$$
p_1(x) = f(x_0) + (x - x_0)f'(x_0) = 1 + x
$$

On pourrait continuer indéfiniement.

$$
p_3(0) = 1 = f(0)
$$

Choisissons un point à côté:

$$
p_3(0.1) = 1 + 0.1 + \frac{(0.1)^2}{2} + \frac{(0.1)^3}{6}
$$

$$
p_3(0.1) = 1.10516667
$$

Mais on a aussi, f(0.1) = e^{0.1} = 1.105170918

On a les 4 premières décimales d'identiques uniquements! Il s'agit d'une approximation. Mais l'erreur est elle $\propto$ avec la distance?

$$
p_3(1) = 2.66666666667
$$

$$
f(1) = 2.71828182
$$

On n'a que le 2 en commun.

> **Conclusion**: Le polynôme de Taylor n'est que très précis au voisinage du point évalué (x_0) du polynôme.

Ex:

$$
f(x) = ln(1 + x) + cos(x)
$$

où $x > 0$ autour de $x_0 = 0$

$$
f(0) = 1
$$

Pour la dérivée première:

$$
f'(x) = \frac{1}{1+x} - sin(x)
$$
$$
f'(0) = 1
$$

Pour la dérivée deuxième:

$$
f''(x) = \frac{-1}{(1+x)^2}
$$
$$
f''(0) = -2
$$

Etc.
Pour les polynômes de Taylor:

$$p_0(x) = 1$$
$$p_1(x) = 1 + x$$
$$p_2(x) = 1 + x - x^2$$
$$p_3(x) = 1 + x - x^2 + \frac{x^3}{3}$$

> **Conclusion**: Plus on prend de termes, plus c'est précis. Plus on est proche du point d'évaluation $x_0$, plus c'est précis.

