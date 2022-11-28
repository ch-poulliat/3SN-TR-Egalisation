## Systèmes à temps discret


### Filtres Linéaires Invariants par Décalage

#### Définitions

```{prf:definition} Filtre
Un filtre est un opérateur $\mathcal{H}[.]$ qui associe à une séquence $x[n] \in \mathcal{S}$ une séquence $y[n] = \mathcal{H}[x[n]] \in \mathcal{S'}$, où $\mathcal{S}$ et $\mathcal{S}'$ sont typiquement $\ell^2(\mathbb{Z})$ ou $\ell^{\infty}(\mathbb{Z})$. 
```
```{prf:definition} Filtre linéaire invariant par décalage 

Un filtre linéaire invariant par décalage (FLID) vérifie:

- ***la linéarité :*** 

$$\mathcal{H}[a x_1[n]  + b x_2[n]]   =a.\mathcal{H}[x_1[n]] + b.\mathcal{H}[x_2[n]]$$

-  ***l'invariance par décalage :***   

$$\mathrm{si }\; y[n] = \mathcal{H}[ x[n]] \;\mathrm{ alors }\; y[n-p] = \mathcal{H}[x[n-p]]$$
```

#### Réponse impulsionnelle et Produit de convolution discret

On note $h[n]  = \mathcal{H}[ \delta[n]]$  la réponse dîte *impulsionnelle* d'un système discret.  Si le système est linéaire et invariant par décalage, la connaissance  de $h[n]$ suffit pour caractériser totalement  le système, et permet de trouver la réponse à une entrée quelconque par une opération de convolution.

Considérons un signal d'entrée $x[n]$ quelconque. En utilisant la décomposition sur la base des impulsions Delta décalées, on peut écrire

$$x[n]=\sum_{k\in \mathbb{Z}}{x[k]\delta[n-k]}$$

On peut alors écrire en appliquant les propriétés de linéarité et d'invariance par décalage

$$y[n]=\mathcal{H}[x[n]]=\sum_{k \in \mathbb{Z}}{x[k]\mathcal{H}[\delta[n-k]]}=\sum_{k \in \mathbb{Z}}{x[k] h[n-k]}$$

On reconnaît ici le produit de convolution discret des séquences $x[n]$ et $h[n]$, qui s'écrit:

$$
y[n]= (h*x)[n]=\sum_{k=-\infty}^{+\infty}{x[k] h[n-k]}
$$

Le produit de convolution  discret est commutatif, ie. $y[n]= (h*x)[n]=(x*h)[n]$. On en déduit que l'ordre de mise en cascade de deux FLID est indifférent.

#### Critère(s) de stabilité

De manière générale, un système est stable si une entrée bornée provoque une sortie bornée (ce qui inclut les systèmes à la limite de stabilité), ce qui s'écrit

$$x \in \ell^{\infty}(\mathbb{Z}) \; \Rightarrow \; y=\mathcal{H}[x] \in \ell^{\infty}(\mathbb{Z})$$ 


Pour un système linéaire invariant par décalage, une condition nécessaire et suffisante de stabilité  est alors donnée par

$$\sum_{k \in \mathbb{Z}}{|h_k|} < +\infty$$




#### Causalité des FLID

Un système est causal si la sortie $y[n]$ est indépendante des échantillons  d'entrée $x[n']$ pour $n'  > n$. Pour un FLID, cette condition est équivalente à $$h[n] = 0\; \forall n < 0.$$


### Equations aux différences  :  systèmes RII et RIF

Les systèmes linéaires invariants par décalage sont définis par une équation aux différences  à coefficients constants. La forme générale est:

$$y[n]=\sum_{k=1}^{N} a_{k} \cdot y[n-k]+\sum_{r=P}^{M} b_{r} \cdot x[n-r].$$

On remarque ici que l'indice $k$ varie de $1$ à $N > 0$, i.e. que seules  interviennent les valeurs passées de la sortie, ce qui permet de calculer $y[n]$  de proche en proche. L'indice $r$ varie de $P$ à $M$ quelconques. Si $P < 0$, le filtre est non causal, mais reste cependant réalisable en temps différé.

Ces systèmes sont les correspondants  discrets des systèmes continus définis par une équation différentielle à coefficients constants. Ils sont classés en deux catégories :


- les  filtres à réponse impulsionnelle  finie,

- les filtres à réponse impulsionnelle  infinie.

#### Les filtres à réponse impulsionnelle finie

L'équation aux différences associée à des filtres à réponse impulsionnelle finie se réduit à 

$$y[n]=\sum_{r=P}^{M} b_{r} \cdot x[n-r].$$

Dans ce cas, la sortie $y[n]$ ne dépend pas des valeurs passées de la sortie. La réponse impulsionnelle  est triviale si on pose 
$x[n] = \delta[n]$, et vaut donc 

$$h[n]= b_n.$$ 

L'équation aux différences s'identifie de manière directe au produit de convolution $h[n]*x[n]$. La longueur de la réponse impulsionnelle correspond  aux nombres de termes de la somme sur l'indice $r$, ie. $M-P+1$, qui est obligatoirement  fini pour un filtre réalisable.

Ces filtres sont toujours stables car la condition $\sum_k |h[k]|  < +\infty$ est toujours vérifiée. Ces filtres sont appelés filtres RIF (Réponse impulsionnelle  finie) et en anglais FIR (Finite Impulse Response filters). Ce sont des filtres non récursifs, encore dénommés filtres MA (Moving Average, ou Moyenne mobile) car l'opération de convolution ainsi réalisée peut-être assimilée à une opération de moyennage glissant si on normalise cette moyenne.

Par exemple, $y[[n] = x[n-l]+x[n]+x[n+l]$ est un filtre RIF non causal réalisant un lissage.

#### Les filtres à réponse impulsionnelle infinie

L'équation aux différences associée aux filtres dîts à réponse imulsionnelle infinie à la forme générale 

$$y[n]=\sum_{k=1}^{N} a_{k} \cdot y[n-k]+\sum_{r=P}^{M} b_{r} \cdot x[n-r].$$

La sortie $y[n]$ étant dépendante des valeurs passées $y[n-k]$, la réponse impulsionnelle sera infinie. 

Par exemple $y[n] = a.y[n-1] + x[n]$ est un filtre à réponse impulsionnelle  infinie du premier ordre. Le calcul de sa réponse impulsionnelle nécessite la connaissance d'un échantillon particulier (de même que la résolution d'une équation différentielle du premier ordre suppose la connaissance d'une condition initiale). Pour cet exemple ordre, $h[n]$ vaut $h[0].a^n$ pour $n > 0$ et vaut $(h[0]-1)a^n$ pour $n < 0$. L'équation aux différences a une infinité de solutions : toutes ces solutions différent de $K.a^n$, puisque  $K.a$ est solution de $y[n]- a.y[n-1]= 0$. Parmi toutes ces solutions, une seule correspond à un système causal (lorsque  $h[0] = 1$).

La réponse impulsionnelle  étant infinie, ces filtres peuvent être instables.
Ces filtres sont appelés filtres RII (Réponse impulsionnelle infinie), soit en anglais IIR (Infinite Impulse Response filters). Ce sont par nature des filtres récursifs.

Lorsque l'équation aux différences se limite à  

$$y[n]=\sum_{k=1}^{N} a_{k} \cdot y[n-k]+x[n],$$ 

ils sont appelés filtres AR (Auto-Regressive). Sous la forme la plus générale, ils sont également appelés filtres ARMA (Auto-Regressive Moving-Average).

### Filtres non invariants par décalage

Les formes les plus courantes des filtres non invariants par décalage sont :

- le compresseur,

- l'échantillonneur,

- le suréchantillonneur.

La condition d'invariance par décalage n'étant pas vérifiée, ces filtres ne sont pas régis par une équation de convolution,  et donc la connaissance  de leur réponse impulsionnelle ne permet pas de déduire leurs propriétés.

#### Le compresseur

Il est défini par 

$$y[n] = x[M.n].$$

Il est non invariant par décalage, car décaler l'entrée de $M$ échantillons décale la sortie de $1$ seulement, et décaler l'entrée de $P \neq k.M$ change complètement  les échantillons  en sortie. Il est évidemment  stable (car à une entrée bornée correspond une sortie bornée). Il est non causal (de manière évidente, on vérifie par exemple que $y[1]$ dépend de $x[M]$).
Sa réponse impulsionnelle  est $h[n] = \delta[n]$.

D'un point de vue pratique, cet opérateur correspond à une opération de sous-échantillonnage : si $x[n]$ est obtenu par échantillonnage  d'un signal $x_a(t)$ à la fréquence d'échantillonnage $F_e$, $y[n]$ correspond à l'échantillonnage  de $x_a(t)$ à la fréquence $F_e/M$.

#### L'échantillonneur

Il est défini par 

$$y[k.M] = x[k.M],$$

et $y[n] = 0$ si $n$ est non multiple de $M$.

Il est non invariant par décalage : décaler l'entrée de $M$ revient bien à décaler la sortie de M, mais décaler l'entrée de $P \neq k M$ change complètement  les échantillons en sortie. Il est évidemment  stable (une entrée bornée donne une sortie bornée) et causal. Sa réponse impulsionnelle  est $h[n] = \delta[n]$.

#### Le suréchantillonneur

Il est défini par  

$$y[k.M] = x[k],$$

et $y[n] = 0$ si $n$ est non multiple de $M$.

Il est non invariant par décalage : décaler l'entrée de $1$ échantillon, décale la sortie de $M$ échantillons. Il est évidemment stable (une entrée bornée donne une sortie bornée). Il est non causal (par exemple, $y[-M]$ dépend de $x[-1]$). Sa réponse impulsionnelle  est donnée par $h[n] = \delta[n]$.

Ce filtre permet d'élever la fréquence d'échantillonnage  d'un signal en intercalant $(M-1)$ échantillons nuls entre chaque échantillon.