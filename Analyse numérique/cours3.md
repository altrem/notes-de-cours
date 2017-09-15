# Cours 3

## Reste du polynôme de Taylor

> Rappelons nous qu'on veut transformer toute fonction $f$ en un polynôme, donc le développement de Taylor est le choix le plus approprié.

Formule générale de l'erreur d'un polynôme:

$$
|f(x) - p_n(x)| = |\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1}|
$$
Où $\xi$ est dans l'intervalle [$x_0$, $x$].

On l'appelle le **reste** ou l'**erreur de troncature**.

On se rappelle que:

$$
p_n(x) = f(x_0) + (x - x_0)f'(x_0) + ... + \frac{(x - x_0)^n}{n!}f^{(n)}(x_0)
$$

Écriture en h. On pose $x = x_0 + h$ et $h = x - x_0$
Le polynôme de Taylor:

$$
p_n(h) = f(x_0) + hf'(x_0) + ... + \frac{h^n}{n!}f^{(n)}(x_0)
$$

Le reste est:

$$
|R_n(h)| = \frac{f^{(n+1)}(\xi)}{(n+1)!}h^{n+1}
$$

Problème? **Je ne sais pas qui est $\xi$.

*Remarques*

Généralement, les remarques suivantes s'appliquent sur le reste.

- Si $x$ s'approche de $x_0$ (si h tend vers zéro), l'erreur diminue;
- Si $x$ s'éloigne de $x_0$ (h augmente), l'erreur augmente.
- Si $x - x_0$ est petit (< 1), lorsque $n$ augmente l'erreur diminue. Si $n$ diminue, alors l'erreur augment.

## Choix de $x_0$

Comment choisir $x_0$ ?

- On veut facilement évaluer $f$ et ses dérivées. Par exemple, pour $e^x$, $x = 0$ est le plus simple
- On veut un point $x_0$ près des points d'intérêts. On cherche donc à diminuer $h$ ($x - x_0$)

Voir la page 38 du manuel, section 1.7: Comment évaluer avec précision en un point loin de $x_0$ ?

Ex:

$$
f(\theta) = sin(\theta)
$$
Notons qu'il faut toujours mettre $\theta$ en radians.

Essayons une approximation de degré 1 autour de $\theta_0 = 0$

$$
p_1(0) = f(\theta_0) + (\theta - \theta_0)f'(0)
$$

Alors

$$
p_1(0) = sin(0) + \theta cos(0)
$$

Pour de petits angles, on a $sin(\theta) = \theta$ avec une erreur se comportant comme $\theta^2$.

Ex:

$$
f(x) = \frac{1}{x}
$$

Approximation de degré 3 autour de $x_0 = 1$
Les dérivées:

$$
f(x) = \frac{1}{x}
$$
$$
f'(x) = -1x^{-2}
$$
$$
f''(x) = 2x^{-3}
$$
$$
f'''(x) = -6x^{-4}
$$ 

On a donc le polynôme de Taylor suivant:

$$
p_3(x) = 1 - (x - 1) + (x - 1)^2 - (x - 1)^3
$$

L'erreur se comporte comme $(x - 1)^4$, car **l'erreur se comporte toujours comme le $n+1$ ème terme.

Le reste maintenant. On veut trouver $\xi$, par exemple évaluons pour $x = \frac{1}{2}$

$$
|f(x) - p_3(x)| = |\frac{f^{(4)}(\xi)}{4!}(x - 1)^4|
$$

Pour $x = \frac{1}{2}$, $f(\frac{1}{2}) = 2$ et $p_3(\frac{1}{2}) = 1.875$ on a une erreur absolue de 0.125.

Or, on sait que $\xi$ est dans [$\frac{1}{2}$, 1] et que:

$$
0.125 = \xi^{-5}*(\frac{1}{2})^4
$$
$$
\xi = 0.87055
$$

En évaluant $\xi$, on se rend compte qu'il est absurde de vouloir calculer l'erreur exacte $\xi$, car on doit déjà connaître $\Delta x$ (voir le calcul suivant). Donc, autant ne pas prendre d'estimation.

Comment faire alors pour choisir $\xi$ ? **On peut choisir un chiffre qui rend certain que nous somme du côté sécuritaire de l'erreur**.

$$
|f(x) - p_n(x)| = |\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1}| \leq \frac{M_n}{(n+1)!}|(x - x_0)^{n+1}|
$$

Il faut pouvoir trouver ce $M_n$.

$$
M_n = max(a) => |f^{(n+1)}(a)|
$$

Il faut trouver le maximum, donc il faut annuler la dérivée première, etc.

Avec cet estimé du $\Delta x$, on peut maintenant tout faire, e.g:

- Estimer $f$
- Donner l'erreur approximative de $f$
- Etc.

Remarques:

- L'erreur est forcément $\leq$ au maximum d'erreur
- On peut trouver une autre borne un peu plus grande évitant de calculer $M_n$.

Ex:

$$
f(x) = \frac{1}{x}
$$

et

$$n = 3, x_0 = 1$$

Pour $x = 1/2$, on aura:

$$M_3 = max(1/2 \leq a \leq 1) \frac{24}{a^5} = (24)2^5 $$

$$|f(1/2) - p_3(1/2) \leq \frac{M_3}{24}(\frac{1}{2} - 1)^5 = 1$$

On sait, sans connaître $f$, que l'erreur est inférieure à1.