## Transformée en $\mathcal{Z}$.

### Définition

```{prf:definition} Transformée en $\mathcal{Z}$

$$\overline{x}(z)=\mathcal{Z}\left\{x[n]\right\}=\sum_{n=-\infty}^\infty x[n] z^{-n} ,\;\; z\in \mathbb{C}$$

```

La transformée en $\mathcal{Z}$ joue, pour les séquences, un rôle analogue à celui de la transformation de Laplace pour les fonctions.

### relation avec la transformée de Fourier d'une séquence.

En posant, $z=e^{j 2 \pi \nu},$ il vient 

$$\overline{x}(z=e^{j 2 \pi \nu})=\sum_{n \in \mathbb{Z}}{x[n] e^{-j 2 \pi \nu n}}=\overset{\circ}{x}{(\nu)}.$$

Ainsi, dans le plan complexe, sur le cercle de rayon $1,$ la transformée en $\mathcal{Z}$ est égale à la transformée de Fourier.

### Région/Domaine de Convergence (region of convergence, ROC)

La transformation en $\mathcal{Z}$ ne converge pas partout dans le plan $\mathcal{Z}$ (sur le plan complexe).  Pour étudier le domaine de convergence de la série associée à la transformée, on cherche à caractériser sur quelle région la série $\sum_{n=-\infty}^\infty x[n] z^{-n}$ est absolument convergente. Cette série est à diviser en deux sous-partie telle que $\overline{x}(z)=\overline{x_a}(z)+\overline{x}_c(z)$ où 

$$\overline{x_a}(z)=\sum_{n=-\infty}^{-1}{x[n] z^{-n}},$$

est une série infinie à gauche et

$$\overline{x_c}(z)=\sum_{n=0}^{+ \infty}{x[n] z^{-n}},$$

est une série infinie à droite.


### Propriétés

La transformée en $\mathcal{Z}$ a des propriétés similaires à celle de la transformée de Fourier pour les signaux à temps discret. La seule différence est que l'on doit prendre garde au domaine de convergence quand on réalise certaines opérations sur les signaux. Comme précédemment évoqué, déterminer une transformée en $\mathcal{Z}$ d'un signal $x[n]$, c'est déterminer l'expression $\overline{x}(z)$ et définir sa ROC. Dans la suite, on considère les opérations sur des signaux $x[n]$ et $y[n]$ défini comme suit:

$$\mathcal{Z}\left\lbrace x[n] \right\rbrace=\overline{x}(z)\;\;\;\;ROC=R_x$$

et

$$\mathcal{Z}\left\lbrace y[n]\right\rbrace =\overline{y}(z)\;\;\;\;ROC=R_y$$

```{prf:property}

- **Linéarité**

    $$\mathcal{Z}\left\lbrace a x[n]+b y[n]\right\rbrace=a\overline{x}(z)+b\overline{y}(z), \;\;\;\;ROC \supseteq (R_x \cap R_y)$$

-  **Décalage en temps**

    $$\mathcal{Z}\left\lbrace x[n-n_0]\right\rbrace=z^{-n_0} \overline{x}(z),\;\;\;\;ROC=R_x$$

    La ROC est en générale la même que celle à l'initial sauf possible addition/suppression des points à l'origine ou à l'infini.


- **Convolution**

    $$ \mathcal{Z}\left\lbrace x[n]*y[n]\right\rbrace=\overline{x}(z) \overline{y}(z), \;\;\;\;ROC \supseteq (R_x \cap R_y)$$

    La ROC associée au produit de convolution peut être plus large que l'intersection de $R_x$ et $R_y$, ceci étant lié à la possible annulation de pôles ou zéros lors de la convolution.

- **Différence temporelle**

    $$ \mathcal{Z}\left\lbrace x[n]-x[n-1]\right\rbrace=(1-z^{-1}) \overline{x}(z), \;\;\;\;\;ROC=R_x$$


- **Accumulateur**

    $$ \mathcal{Z}\left\lbrace \sum_{k=-\infty}^nx[k]\right\rbrace=\frac{1}{1-z^{-1}} \overline{x}(z),
	\;\;\;\;ROC \supseteq [R_x \cap (|z|>1)]$$


- **Renversement temporel/folding**

    $$ \mathcal{Z}\left\lbrace x[-n]\right\rbrace=\overline{x}(1/z)$$


- **Changement d'échelle dans le domaine en $\mathcal{Z}$**

    $$ \mathcal{Z}\left\lbrace a^n x[n]\right\rbrace=\overline{x}\left(\frac{z}{a}\right),\;\;\;\;ROC=|a|R_x$$

- **Conjugaison**

    $$ \mathcal{Z}\left\lbrace x^*[n]\right\rbrace=\overline{x}^*(z^*), \;\;\;\;\;ROC=R_x$$


- **Différenciation**

    $$\mathcal{Z}\left\lbrace n x[n]\right\rbrace=-z\;\frac{d}{dz}\overline{x}(z), \;\;\;\; ROC=R_x$$

```