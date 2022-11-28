## Signaux à temps discrets

### Séquences et Espace(s) des séquences

A partir des échantillons d'un signal analogique $x_a(t)$, on obtient un signal à temps discret représenté par des séquences de nombres qui sont notées $\left\{x[n]\right\},$ ou de manière vectorielle par ${\bf x}$, où $x[n]$ étant l'élément d'index temporelle $n$ ($n \in \mathbb{Z}$ entier relatif). Par souci de simplicité des notations, on omettra les parenthèses lorsque le contexte le permet. Généralement, on a à manipuler deux grandes catégories de séquences:

1. ***Les séquences discrètes à support temporel infini :*** 

    ce sont des séquences dont le support temporel $n$ est défini sur $\mathbb{Z}$ (dîtes infinies "à gauche" et "à droite", en référence à l'échantillon de référence pour $n=0$), sur $\mathbb{Z}_{+}$ (encore noté $\mathbb{N}$) (signal causal infini à droite), ou sur $\mathbb{Z}_{-}$ (signal infini à gauche). Ces séquences appartiennent appartiennent à l'espace vectoriel $\mathbb{C}^{\mathbb{Z}}$ et sont notées

$${\bf x}=\left[\begin{array}{lllll}{\cdots} & {x[-1]} & {x[0]} & {x[1]} & {\cdots}\end{array}\right]^{\top}.$$

2. ***Les séquences discrètes à support temporel fini :*** 

    Ces séquences sont à support fini et sont représentées de manière générale par un vecteur de taille fini ${\bf x} \in \mathbb{C}^N$ donné par
    
    $${\bf x}=\left[\begin{array}{lllll} x[-P] & \ldots & {x[0]} & {\ldots} & {x[M]}\end{array}\right]^{\top},$$

    avec $N=P+M-1$.

    Sans perte de généralité, si on doit travailler essentiellement avec des outils de l'algèbre linéaire classique, on préférera souvent se ramener  à une notations vectorielle classique de type 

    $${\bf x}=\left[\begin{array}{llll} x[0] & {x[1]} & {\ldots} & {x[N-1]}\end{array}\right]^{\top},$$

où ${\bf x}$ est assimilé à un vecteur de $\mathbb{C}^N$. L'indexation retenue ne correspond donc plus nécessairement à l'indexation temporelle des échantillons. 

#### Séquences à support infini

Pour les séquences à support infinies, les séquences de $\mathbb{C}^{\mathbb{Z}}$ définissent un espace vectoriel des séquences complexes infinies définies sur $\mathbb{Z}$ formellement décrit comme

$$\mathbb{C}^{\mathbb{Z}}=\left\{{\bf x}=\left[\begin{array}{lllll}{\cdots} & {x[-1]} & {x[0]} & {x[1]} & {\cdots}\end{array}\right]^{\top} | x[n] \in \mathbb{C}, n \in \mathbb{Z}\right\}$$

et pour lequel l'addition de vecteurs et la multiplication par un scalaire sont réalisés par composantes. C'est un espace de dimension infinie.

Parmi les sous-espaces d'intérêt, nous avons ***l'espace $\ell^{2}(\mathbb{Z})$ des séquences de carrés sommables***. Du point de vue vue du signal, cela s'identifie à ***l'espace des signaux discrets à énergie finie***. On construit ce sous-espace vectoriel normé en dotant $\mathbb{C}^{\mathbb{Z}}$ de la norme euclidienne $\ell^2$ définie par

$$\Vert x\Vert _2=\left(\sum_{n=0}^{N-1}\left|x_{n}\right|^{2}\right)^{1 / 2}$$

et induite par le produit scalaire usuel défini comme 

$$\langle x, y\rangle=\sum_{n \in \mathbb{Z}} x_{n} y_{n}^{*}.$$

Dans la notation précédente, on suppose que la dernière somme sur les indices à valeurs dans $\mathbb{Z}$ est par essence finie, ce qui est vérifié si on suppose $\Vert x\Vert _2$ et $\Vert y\Vert _2$ finies. Cet espace est un espace de Hilbert et donc hérite de toutes les propriétés géométriques associées connues à ce type d'espaces.

On peut également retenir *** l'espace vectoriel normé $\ell^{\infty}(\mathbb{Z})$ des séquences d'échantillons à amplitude bornée***, qui définit une contrainte plus faible sur les séquences de $\mathbb{C}^{\mathbb{Z}}$. Pour cet espace, les séquences sont telles que $|x[n]|< A,\; \forall n \in \mathbb{Z}$, et $A \in \mathbb{R}^+$ fini. La norme associée est alors la norme infinie donnée par

$$\Vert x\Vert _{\infty}=\sup _{n \in \mathbb{Z}}\left|x_{n}\right|$$

Enfin, *** l'espace vectoriel normé $\ell^{1}(\mathbb{Z})$ des séquences absolument sommables*** est l'espace des séquences dont la norme-$1$ $\ell^1$ est finie, définissant un ensemble plus contraint que $\ell^{2}(\mathbb{Z})$. 
La norme associé est donnée par

$$\Vert x\Vert _{1}=\sum_{n \in \mathbb{Z}}\left|x_{n}\right|$$

Les deux derniers sous-ensembles sont des cas particuliers des espaces vectoriels normés (complets) $\ell^{p}(\mathbb{Z})$, définit pour $p \in [1,+ \infty]$, et pour lequel  la norme-$p$ $\ell^p$ est finie. $\ell^p$ est définie par

$$\Vert x\Vert _{p}=\left(\sum_{n \in \mathbb{Z}}\left|x_{n}\right|^{p}\right)^{1 / p}$$

 On peut alors montrer que si $p<q$, alors $\ell^{p}(\mathbb{Z})\subset \ell^{p}(\mathbb{Z}$. Ceci implique que l'ensemble $\ell^{1}(\mathbb{Z}$ est l'ensemble de séquences le plus réduit/restreint. En particulier, pour ce qui nous concerne le plus, on s'intéresse surtout au fait que $\ell^{1}(\mathbb{Z})\subset \ell^{2}(\mathbb{Z})$. Cela induit en effet que que si une séquence à une norme $\ell^1$ finie alors elle aura une norme $\ell^2$ finie., les signaux absolument sommables sont donc de carrés sommables. L'inverse est faux.
 
 
#### Séquences à support temporel fini

Pour les séquences à support fini, les séquences de $\mathbb{C}^{\mathbb{Z}}$ définissent un sous-espace vectoriel de dimension finie des séquences complexes finies définies sur $\mathbb{Z}$ se décrivant formellement comme

$$\mathbb{C}^{N}=\left\{x=\left[\begin{array}{llll} x[0] & {x[1]} & {\ldots} & {x[N-1]}\end{array}\right]^{\top} | x[n] \in \mathbb{C}, n \in\{0,1, \ldots, N-1\}\right\}$$


Comme dans le cas in,fini, on peut alors associé le produit scalaire défini comme 

$$\langle x, y\rangle=\sum_{n = 0}^{N-1} x_{n} y_{n}^{*}={\bf y}^{\dagger}{\bf x},$$

où $^{\dagger}$, noté également $^{H}$, est l'opérateur conjoint de transposition et conjugaison. La norme-$2$ induite 

$$ \Vert x \Vert_2=\left(\sum_{n=0}^{N-1}\left|x_{n}\right|^{2}\right)^{1 / 2}$$
permet de dotée $\mathbb{C}^{N}$ de sa structure usuelle d'espace vectoriel normé, et comme nous sommes en dimension finie, ce dernier est un espace de Hilbert.

Comme dans le cas infini, onpeut également doté $\mathbb{C}^{N}$ d'autres normes, généralement des normes-$p$ définies pour $p\in[1, +\infty]$ par

$$\Vert x \Vert_p=\left(\sum_{n=0}^{N-1}\left|x_{n}\right|^{p}\right)^{1 / p}.$$

Pour $p=+\infty$, on obtient

$$\Vert x\Vert _{\infty}=\max \left(\left|x_{0}\right|,\left|x_{1}\right|, \ldots,\left|x_{N-1}\right|\right)$$
et pour $p=1$, 

$$\Vert x \Vert_1=\sum_{n=0}^{N-1}\left|x_{n}\right|.$$

### Séquences particulières

#### Impulsion Delta de Kronecker

La séquence dîte de Kronecker est donnée par définition par

```{prf:definition} Impulsion Delta de Kronecker

$$\delta[n]=\left\{\begin{array}{ll}{1,} & {\text { for } n=0 ;} \\ {0,} & {\text { otherwise }}\end{array} \quad n \in \mathbb{Z}\right.$$

En notation vectoriel, on  notera

$$\mathbf{\delta}=\left[\begin{array}{lllll}{\cdots} & 0 & {1} & {0} & {\cdots}\end{array}\right]^{\top}$$
```

L'ensemble $\left\{\delta[n-k]\right\}_{k \in \mathbb{Z}}$ qui correspond aux versions décalées de $k$ échantillons dans le temps de la séquence $\delta[n]$ forme la base orthonormale usuelle associée à $\ell^{2}(\mathbb{Z})$. On notera ${\bf \delta_k}$ la version vectorielle de $\delta[n-k]$.

En particulier, on aura les propriétés suivantes: 

```{prf:property}

-  ***Produit (terme à terme) d'une séquence par l'impulsion de Kronecker:***

$$x[n].\delta[n]=x[0]\delta[n]$$

- ***Produit scalaire d'une séquence par l'impulsion de Kronecker:***

$$\langle x, \delta_{n_0} \rangle =\sum_{k \in \mathbb{Z}}{x[k] \delta[k-n_0]}=x[n_0]$$

```

#### Séquence Impulsion Unité


La séquence d'impulsion Unité dîte Heaviside est donnée par définition par

```{prf:definition} Echelon Heaviside

$$U[n]=\left\{\begin{array}{ll}{1,} & {\text { for } n \in \mathbb{N} ;} \\ {0,} & {\text { otherwise }}\end{array} \quad n \in \mathbb{Z}\right.$$
```

On a la relation suivante par rapport à la séquence Delta

$$U[n]=\sum_{k=-\infty}^{n}{\delta[k]}.$$

On voit qu'il existe une relation d'intégration entre ces deux séquences.

Cette séquence a ses éléments bornés par 1 et donc appartient à $\ell^{\infty}(\mathbb{Z})$ et donc n'appartient ni à $\ell^{1}(\mathbb{Z})$, ni à $\ell^{2}(\mathbb{Z})$.

### Séquences sinusoïdales

Ce sont les séquences de type $x[n]=e^{i 2 \pi \mathbb{N}u n},$ ou $x[n]=sin(2nvn),$  et $x[n]=cos(2nvn),$ .

Par périodicité $x[n]=e^{i 2 \pi \mathbb{N}u n}$ et $x'[n]=e^{i 2 \pi (\mathbb{N}u+N) n}$  sont identiques pour $N$ est entier. Ceci peut être interprété  comme une conséquence du repliement de  spectre lors de  l'échantillonnage à la fréquence $F_e=1/T_e$. Ainsi, deux signaux continus définis par $x_a(t)=e^{i 2 \pi f t}$ et $x'_a(t)=e^{i 2 \pi (f+N F_e) t}$ sont indiscernables après échantillonnage à la fréquence $F_e$. En effet, le signal continu $x_a(t)=e^{i 2 \pi f t}$ échantillonné à la fréquence $F_e$ donne la séquence  $x[n] =e^{i 2 \pi \frac{f}{F_e} n}=e^{i 2 \pi \mathbb{N}u n}$ avec $\mathbb{N}u=\frac{f}{F_e}$. La fréquence du signal échantillonnée $\mathbb{N}u$ est donc égale à la fréquence $f$ du signal à temps continu, normalisée par rapport à la fréquence d'échantillonnage $F_e$. On parlera de fréquence normalisée. De plus, $x[n]=e^{i 2 \pi \mathbb{N}u n}$ étant $1$-périodique, on peut obtenir l'ensemble  des séquences associées à $x[n]$ en faisant varier le paramètre $\mathbb{N}u$ sur un intervalle de longueur $1$. On notera également que la périodicité n'est conservée que si $f/F_e$ est rationnel. 

