## Densité spectrale de puissance d'un processus

```{prf:definition} Densité spectrale de puissance 

La *densité spectrale de puissance (dsp) d'un processus stationnaire au second ordre est la transformée de Fourier de 
sa fonction d'autocorrélation :

$$
\overset{\circ}{\gamma}_X(\nu)=\mathcal{F}{\{\gamma_X[p]\}}=\sum\limits_{-\infty }^{+\infty} \gamma_X[p] e^{-j 2 \pi \nu p}
$$

```

```{prf:definition} Densité en $\mathcal{Z}$

La *densité  en  $\mathcal{Z}$* d'un processus stationnaire est la transformée en $\mathcal{Z}$ (lorsqu'elle est bien définie) de sa fonction d'autocorrélation,  soit~:

$$
         \overline{\gamma}_X(z)= \mathcal{Z}\{\gamma_X[p]\}=\sum\limits_{p=-\infty}^{+\infty } \gamma_X[p] z^{-p}
$$

```

La transformée de Fourier est la transformée en $\mathcal{Z}$ prise sur le cercle 
unité en $z = e^{j2\pi\nu}$. Pour assurer l'existence de la TF, il faut que le 
cercle unité appartienne au domaine de convergence de la TZ. Si $ | \gamma_X[p]| \leq 
r^{p}$ , avec $0 \leq r < 1$, alors $\overline{\gamma}_X(z)$ est bien définie pour $r \leq |z| \leq \dfrac{1}{r}$. 

```{prf:preoperty}

1. La densité spectrale est une fonction à valeurs réelles et positives ou nulles

2. Elle est $1$-périodique.

3. Si le signal est à valeurs réelles, la densité spectrale est symétrique.

```