## Caractérisation des signaux aléatoires filtrés

### Caractérisation au premier ordre

On suppose le processus d'entrée $X(n,\omega)$ stationnaire au premier ordre de moyenne et de moyenne $m_X=\mathbb{E}(X(n,\omega))$. On a alors

$$
\begin{align*}
m_Y(n) &= \mathbb{E}(Y(n,\omega)) = \sum\limits_{k \in \mathbb{Z}} h(k)
\mathbb{E}(X(n-k,\omega)) \\ &=
\sum\limits_{k \in \mathbb{Z}} h(k) m_X = m_X \overset{\circ}{h}(0)
\end{align*}
$$

avec  $\overset{\circ}{h}(\nu)=\sum\limits_{m \in \mathbb{Z}} h(n) e^{+i 2 \pi \nu n}$ la transformée de Fourier de la séquence $h(n)$.

```{prf:property} Caractérisation au premier ordre

Si $X(n,\omega)$ est stationnaire au premier ordre, $Y(n,\omega)$ est stationnaire au premier ordre et sa moyenne
vaut :

$$ m_Y = m_X \overset{\circ}{h}(0)$$
```

### Caractérisation au second ordre

On suppose $X(n,\omega)$ centré. Par application du résultat précédent, $Y$ est centré. Si $X$ est stationnaire au deuxième
ordre d'autocorrélation $\gamma_X[p]$, alors l'autocorrélation de $Y$ s'écrit :

$$
\begin{aligned}
R_Y(n, n-p) & =\mathbb{E}\left(\sum_{k \in \mathbf{Z}} h(k) X(n-k) \sum_{m \in \mathbf{Z}} h^*(m) X^*(n-p-m)\right) \\
& =\sum_{k \in \mathbf{Z}} \sum_{m \in \mathbf{Z}} h(k) h^*(m) \mathbb{E}\left(X(n-k) X^*(n-p-m)\right) \\
& =\sum_{k \in \mathbf{Z}} \sum_{m \in \mathbf{Z}} h(k) h^*(m) \gamma_X[p+m-k]
\end{aligned}
$$

L'expression précédente étant indépendante de $n$, $Y$ est stationnaire au second ordre. On obtient au final

$$
\begin{aligned}
R_Y(n, n-p) & =\sum_{k \in \mathbf{Z}} \sum_{l \in \mathbf{Z}} h(k) h^*(k-l) \gamma_X[p-l] \\
& =\sum_{l \in \mathbf{Z}} \gamma_X[p-l] \sum_{k \in \mathbf{Z}} h(k) h^*(k-l) \\
& =\gamma_Y[p]
\end{aligned}
$$

En utilisant l'autocorrélation déterministe de la réponse impulsionnelle $h(k)$, définie comme 

$$\gamma_h[l] = \sum\limits_{k \in \mathbf{Z}} h(k) h^*(k-l),$$ 

on obtient finalement :

$$ \gamma_Y[p] = \{\gamma_X * \gamma_h\}[p].$$

On peut aussi remarquer que $\gamma_h[l]=h(p)*\check{h}(p)$ où $\check{h}(p)=h^*(-p)$ est le filtre numérique adapté à $h(n)$.


En prenant la transformée de Fourier de la séquence $\gamma_Y[p]$, on obtient

$$ \overset{\circ}{\gamma}_Y(\nu)= |\overset{\circ}{h}(\nu)|^2 \overset{\circ}{\gamma}_X(\nu) $$

En appliquant maintenant la transformée en $Z$, on obtient

$$\overline{\gamma}_Y(z) = \overline{h}(z) \overline{h}^*(\dfrac{1}{z}) \overline{\gamma}_X(z)$$

où 

$$\overline{\gamma}_h(z)=\overline{h}(z) \overline{h}^*(\dfrac{1}{z})$$

avec $\overline{h}^*(z)=\sum\limits_{k \in \mathbb{Z}} h^*(k) z^{-k}$. 

```{prf:property} Caractérisation au second ordre

Si $X$ est stationnaire au second ordre, $Y$ est stationnaire au second ordre.

1. **Autocorrélation :**

$$\gamma_Y[p]=\left\{\gamma_X * \gamma_h\right\}[p]$$

2. **Densité spectrale de puissance :**

$$ \overset{\circ}{\gamma}_Y(\nu) = |\overset{\circ}{h}(\nu)|^2 \overset{\circ}{\gamma}_X(\nu) $$

3. **Densité en $\mathcal{Z}$ :**

$$\bar{\gamma}_Y(z)=\bar{h}(z) \bar{h}^*\left(\frac{1}{z}\right) \bar{\gamma}_X(z)$$

```