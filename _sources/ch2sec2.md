## Egalisation linéaire avec critère ZF

### Principe

Le but de cette technique est d'imposer l'IES nulle en absence de bruit.
Le principe est assez simple. Supposons la réponse impulsionnelle $h[n]$
connue, ou de manière équivalente sa transformée en $\mathcal{Z}$
définie comme $\overline{h}(z)=\mathcal{Z}\{h[n]\}=\sum_k h[k] z^{-k}$.
Alors en utilisant $\overline{w}(z)=1/\overline{h}(z)$, un calcul
immédiat dans le domaine transformé montre que 

$$\begin{aligned}
\hat{x}&=w[n]*y[n] \nonumber \\
&= s[n] +w[n]*b[n]
\end{aligned}$$ 

Dans ce cas le signal estimé est bien le signal $s[n]$
sans IES. On obtient donc un système sans interférence avec un bruit
additif. C'est ce bruit qui limitera beaucoup les performances du
système dans le cadre de canaux très sélectifs (existence de *"zéros"*
du canal $h[n]$).

### Egalisation ZF - structure sans contrainte

On considère dans un premier temps qu'il n'y a pas de contrainte sur la
structure de l'égaliseur (réponse impulsionnelle éventuellement
infinie). Le signal reçu est alors donné par

$$y[n]=h[n]*s[n]+b[n]=\sum_{k=0}^{L-1}{h[k] s[n-k]+b[n]}$$

Après filtrage par $w[n]$, on obtient

$$\hat{s}[n]=w[n]*h[n]*s[n]+w*b[n]$$ 

Dans le domaine transformé en $\mathcal{Z}$, on aura donc

$$\overline{\hat{s}}(z)=\overline{w}(z)\overline{h}(z)\overline{s}(z)+\overline{w}(z)\overline{b}(z)$$

La fonction de transfert associée au système complet est donnée par

$$T(z)=\mathcal{Z}\{w[n]*h[n]\}=\overline{w}(z)\overline{h}(z)$$ 

et correspond au transfert quand le signal est non bruité. Par définition,
un égaliseur sera dît *zero-forcing* si on a 

$$T(z) = z^{-d},$$ 

soit de manière équivalente dans le domaine fréquentiel

$$\overset{\circ}{T}(\nu)= T(z=e^{+i 2 \pi \nu})= e^{-i 2 \pi \nu d},$$

et dans le domaine dans le domaine temporel

$$w[n]*h[n]=\delta(n-d), \forall n \in \mathbb{Z}$$ 

On cherche donc $\overline{w}(z)$ tel que le transfert global soit un délai pur, ie. pas
de distorsion en gain ($|\overset{\circ}{T}(\nu)|=1$) et une distorsion
en phase linéaire. On remarque également que le bruit n'influe par sur
le critère qui ne dépend que de $T(z)$. Si $\overline{w}(z)$ vérifie la
relation précédente, on obtient alors 

$$\hat{s}[n]=s[n-d]+w[n]*b[n].$$

Le critère ZF nous impose 

$$\overline{w}(z) \overline{h}(z)=z^{-d}.$$ 

On en déduit donc 

$$\overline{w}(z)=\frac{z^{-d}}{\overline{h}(z)}.$$ 

Dans le domaine de Fourier, on obtient

$$\overset{\circ}{w}(\nu)=\frac{e^{-i 2 \pi \nu d}}{\overset{\circ}{h}(\nu)}.$$

En pratique, $\overline{h}(z)$ sera associé à un filtre de type FIR.
Dans ce cadre, son inverse est un filtre de type IIR. Il se pose alors
la question de la stabilité du filtre. En effet, les "zéros du canal"
(ie. $z$ tel $\overline{h}(z)$=0) deviennent les pôles de
$\overline{w}(z)$. Il faut donc faire attention à la mise en oeuvre du
filtre inverse. Si tous les zéros sont contenus dans le cercle unité,
alors $\overline{w}(z)$ est un filtre IIR stable causal. Si les pôles
sont à l'intérieur et à l'extérieur du cercles unités, on se retrouve
avec un filtre IIR non causal, ce qui pose des problèmes
d'implémentation pratique.

### Egalisation ZF - structure contrainte

#### ZF partiel par inversion directe

Pour pallier à ce problème, on peut considérer une approche
sous-optimale avec une structure imposée de type FIR. En s'inspirant des
propriétés du filtre inverse, on considérera un filtre RIF anti-causal
$\lbrace w[n], n  \in \left[-N, \cdots, +N\right]  \rbrace$, ce qui
impose en pratique un délai $d=N$ pour le traitement et la décision.
Ici, $N$ est considéré comme fixe, mais en pratique, c'est un paramètre
à optimiser également. Le critère ZF s'écrit

$$w[n]*h[n]= \sum_{k=-N}^{N}{w_k h_{n-k}}=\left\{\begin{array}{l}1, \; n=0 \\ 0, \; n=\pm 1, \ldots, \pm N \end{array}\right.$$

On remarque alors, que pour le cas de la taille finie, on s'efforce de
forcer à zéro qu'un nombre fini de termes du transfert global $T(z)$. On
peut noter que si les filtres $h[n]$ et $w[n]$ sont RIF, on ne peut
avoir le critère satisfait pour $N \rightarrow +\infty$ que si les deux
filtres sont des diracs purs (éventuellement décalés). Donc de manière
formelle, il n'existe pas de filtre ZF FIR à proprement parlé car on ne
peut avoir une élimination complète de l'IES : on cherche ici juste à en
éliminer une grande partie seulement (généralement, les termes les plus
contributifs en terme de puissance).

Si on écrit le système sous forme matricielle, on obtient
$\lbrace w[n] \rbrace$ de taille $2 \times N -1$ comme solution du
système suivant 


$$\begin{pmatrix}
h[0]& \ldots & \ldots & h[-N] & \ldots & \ldots & h[-2N] \\ 
\vdots & &  & \vdots &  & & \vdots  \\ 
h[N-1] &\ldots & & h[-1] &  &\ldots & h[-N-1] \\ 
h[N] & \ldots& & h[0] &  &\ldots & h[-N] \\ 
h[N+1] & \ldots& & h[1] &  &\ldots & h[-N+1] \\ 
\vdots & & & \vdots &  & & \vdots \\ 
h[2N] & \ldots & & h[N] & & \ldots & h[0]
\end{pmatrix}\begin{pmatrix}
w_{-N}\\ 
\vdots \\ 
w_{-1}\\ 
w_{0}\\ 
w_{1}\\ 
\vdots \\ 
w_{N}
\end{pmatrix}=\begin{pmatrix}
0\\ 
\vdots \\ 
0\\ 
1\\ 
0\\ 
\vdots \\ 
0
\end{pmatrix}$$ 

Si on note ${\bf w}=[w_{-N},\cdots,w_{+N}]$,
$\Delta=[0,\cdots,0, 1, 0,\cdots,0]^\top$, on obtient le système

$${\bf H} {\bf w}=\Delta.$$ 

Et donc on aura simplement

$${\bf w}={\bf H}^{-1}\Delta.$$

#### ZF partiel par méthode des moindres carrés

Si elle est simple à mettre en oeuvre, l'approche précédente est
cependant fortement sous optimale dans le sens où l'on ne contrôle pas
ce qui se passe en dehors du support $[-N, N]$. Pour une approche
formelle plus satisfaisante, on peut également considérer la formulation
suivante comme un problème d'estimation au sens des moindres carrés. En
effet, si on note $\{e[n]\}$ la séquence qui mesure la différence entre
un dirac \"parfait\" et le transfert global
$t[n]=\mathcal{Z}^{-1}\{T(z)\}$, et $d$ le retard à introduire, on alors

$$e[n]=w[n]*h[n]-\delta[n-d].$$ 

Si on adopte la notation vectorielle ${\bf w}=[w[0],\cdots,w[L_w]]^{\top}$, l'optimisation de $w[n]$ revient
à chercher le filtre $w[n]$ qui va minimiser la fonction de coût
$\mathsf{J}({\bf w})=\sum_n{\vert e[n]\vert^2}$. Le transfert global

$$T(z)=\overline{w}(z)\overline{h}(z)=\sum_{k=0}^{L} t[k]z^{-k}$$ 

a un ordre fini $L$ car c'est la résultante de la convolution de deux FIR.
Notons $L=L_w+L_h$ et ${\bf t}=[t[0], \cdots, t[L]]^{\top}$. On a alors la relation 

$${\bf t}={\bf H} {\bf w}$$

où ${\bf H}$ est une matrice triangulaire inférieure dont l'expression est donnée par

$${\bf H}=\begin{pmatrix} { h [ 0 ] } & { 0 } & { \dots } & { 0 } & { \ldots } & { 0 } \\ { h [ 1 ] } & { h [ 0 ] } & { } & { } & { } & { 0 } \\ { \vdots } & { } & { \ddots } & { } & { } & { \vdots } \\ { h \left[ L _ { h } \right] } & { } & { } & { h [ 0 ] } & { } & { } \\ { 0 } & { \ddots } & { } & { } & { \ddots } & { } \\ { \vdots } & { } & { h \left[ L _ { h } \right] } & { } & { \dots } & { h [ 0 ] } \\ { 0 } & { \dots } & { 0 } & { h \left[ L _ { h } \right] } & { } & { h [ 1 ] } \\ { \vdots } & { } & { \vdots } & { } & { \ddots } & { \vdots } \\ { 0 } & { \ldots } & { 0 } & { } & { } & { h \left[ L _ { h } \right] } \end{pmatrix}.$$

Comme $T(z)$ a un ordre fini de même $\mathsf{J}({\bf w})$ aura un nombre fini de termes. En notant le vecteur de taille $(L+1)\times 1$

$$\begin{align*}
   {\bf 1}_{d}= & (0 & \cdots & 0  & \underbrace{1}_{\text{Position } d} & 0 & \cdots& 0)^{\top}
  \end{align*}
,$$ 

on peut alors formuler le problème d'optimisation ZF avec FIR comme la minimisation de la fonction quadratique suivante :


$$\mathsf{J}({\bf w})=\sum_{n=0}^L{\vert e[n] \vert^2}=\| {\bf t}-{\bf 1}_{d} \|_{2}^2=\| {\bf H} {\bf w}-{\bf 1}_{d} \|_{2}^2$$

Le problème à résoudre est donc un problème de minimisation au sens des
moindres carrés. La matrice ${\bf H}$ étant de rang plein sur les
colonnes, en notant $\dagger$ l'opérateur conjoint de transposition et de
conjugaison, la solution unique de ce problème est alors donnée par

$${\bf w}_{\mathsf{ZF-LS}}=({\bf H}^{\dagger}{\bf H})^{-1}{\bf H}^{\dagger}{\bf 1}_{d}={\bf H}^{\sharp}{\bf 1}_{d}.$$

La matrice ${\bf H}^{\sharp}=({\bf H}^{\dagger}{\bf \dagger})^{-1}{\bf H}^{\dagger}$
est la matrice pseudo-inverse de Moore-Penrose, notée quelquefois
également ${\bf H}^{+}$. A l'optimal, la fonction de coût est donnée par
la fonction de $d$ suivante

$$\mathsf{J}_{{\bf w},\min}(d)=\| {\bf H}({\bf H}^{\dagger}{\bf H})^{-1}{\bf H}^{\dagger}{\bf 1}_{d}-{\bf 1}_{d} \|_{2}^2.$$

On notera alors

$${\bf P}={\bf H}({\bf H}^{\dagger}{\bf H})^{-1}{\bf H}^{\dagger}={\bf H}{\bf H}^{\sharp}$$
qui est en fait la matrice de projection associée ayant les propriétés
suivantes : 

(a) hermitianité: ${\bf P}^{\dagger}={\bf P}$ 

(b) Idempotence ${\bf P}^{\dagger}{\bf P}={\bf P}^2={\bf P}$ 

On peut alors simplifier l'expression de $\mathsf{J}_{{\bf w},\min}(d)$ comme suit

$$\mathsf{J}_{{\bf w},\min}(d)=1-p_{d,d},$$ 

où $p_{d,d}$ est le $d$-ième élément de la diagonal de ${\bf P}$. Pour une taille de filtre ${\bf w}$
donnée, on atteint donc le minimum pour un délai $d$ correspondant à l'élément de la diagonal de ${\bf P}$ le plus grand. On peut d'ailleurs
montrer que $0 \leq p_{d,d} \leq 1, \; \forall d$. On obtient ainsi un filtre optimisé en délai. Le filtre optimal ${\bf w}$ en donc obtenu en
sélectionnant la $d$-ième colonne de ${\bf H}^{\sharp}$.

#### Résumé Structure Egaliseur ZF

````{tabs} 

```{tab} ZF non contraint

$$\begin{array}{|ccc|}
\hline 
\textrm{En Temporel }& \vert & \textrm{Domaine transformé en } \mathcal{Z}\\
\hline 
\hat{s}[n]=w_{ZF}[n]*y[n]=s[n-d] & \Longleftrightarrow & \overline{\hat{s}}(z)=\overline{w}_{ZF}(z)\overline{h}(z)\overline{s}(z)=\overline{s}(z)z^{-d}\\
& &\\
w_{zf}[n]*h[n]=\delta[n-d] & \Longleftrightarrow & \large \overline{w}_{zf}(z)=\frac{z^{-d}}{\overline{h}(z)}\\
& & \\
\hline
\end{array}$$

```
```{tab} ZF FIR, inversion directe

Pour $\mathbf{w}_{z f}=\left\{w_k, k=-N \ldots+N\right\},$

$$
w_{z f}[n] * h[n]=\sum_{k=-N}^N w_k h_{n-k}=\left\{\begin{array}{l}
1, n=0 \\
0, n=\pm 1, \ldots, \pm N
\end{array}\right.
$$

$$
\left(\begin{array}{ccccccc}
h[0] & \ldots & \ldots & h[-N] & \ldots & \ldots & h[-2 N] \\
\vdots & & & \vdots & & & \vdots \\
h[N-1] & \ldots & & h[-1] & & \ldots & h[-N-1] \\
h[N] & \ldots & & h[0] & & \ldots & h[-N] \\
h[N+1] & \ldots & & h[1] & & \ldots & h[-N+1] \\
\vdots & & & \vdots & & & \vdots \\
h[2 N] & \ldots & & h[N] & & \ldots & h[0]
\end{array}\right)\left(\begin{array}{c}
w_{-N} \\
\vdots \\
w_{-1} \\
w_0 \\
w_1 \\
\vdots \\
w_N
\end{array}\right)=\left(\begin{array}{c}
0 \\
\vdots \\
0 \\
1 \\
0 \\
\vdots \\
0
\end{array}\right)
$$

```
```{tab} ZF FIR, Moindres Carrés

Pour calculer $\mathbf{w}_{\mathrm{ZF}-\mathrm{LS}}=\left[w[0], \cdots, w\left[L_w\right]\right]^{\top}$,

avec 

$$
\mathbf{H}=\left(\begin{array}{cccccc}
h[0] & 0 & \ldots & 0 & \ldots & 0 \\
h[1] & h[0] & & & & 0 \\
\vdots & & \ddots & & & \vdots \\
h\left[L_h\right] & & & h[0] & & \\
0 & \ddots & & & \ddots & \\
\vdots & & h\left[L_h\right] & & \ldots & h[0] \\
0 & \ldots & 0 & h\left[L_h\right] & & h[1] \\
\vdots & & \vdots & & \ddots & \vdots \\
0 & \cdots & 0 & & & h\left[L_h\right]
\end{array}\right)
$$

1. Calculer $\mathbf{H}^{\sharp}=\left(\mathbf{H}^{\dagger} \mathbf{H}\right)^{-1} \mathbf{H}^{\dagger}$;

2. Calculer $\mathbf{P}=\mathbf{H H}^{\sharp}$;

3. Sélectionner $d$ tel que $p_{d, d}$ est la plus grande valeur de la diagonale;

4. Sélectionner la $d$-ième colonne de $\mathbf{H}^*$, identique au calcul $\mathrm{W}_{\mathrm{ZF}-\mathrm{LS}}=\mathrm{H}^* 1_d$.

```
````

### Analyse en présence de bruit

#### Egaliseur ZF sans contrainte

Dans le cadre de l'égalisation sans contrainte, ie. $w[n]*h[n]=\delta[n-d]$, on obtient en présence de bruit le modèle
suivant après filtrage numérique en réception par le filtre égaliseur

\begin{align*}
\hat{x}[n]&=w[n]*y[n]=w[n]*h[n]*s[n]+w[n]*b[n] \nonumber \\
&=s[n-d]+b_w[n]
\end{align*}

On a donc un modèle équivalent avec un bruit filtré

$$b_w[n]=w[n]*b[n].$$ 

$b_w[n]$ est donc issu d'un processus aléatoire de bruit Gaussien *coloré* et de moyenne nulle. En utilisant les formules
de filtrage d'un processus stationnaire au sens large (ordre 1 et 2), la densité spectrale de puissance associée s'écrit

$$\overset{\circ}{\boldsymbol{\gamma}}_{b_w}(\nu)=|\overset{\circ}{w}(\nu)|^2 \overset{\circ}{\boldsymbol{\gamma}}_{b}(\nu).$$

$b[n]$ étant un processus blanc Gaussien, l'autocorrélation du bruit est donnée par $\gamma_b[p]=\mathbb{E}(b[n]b^*[n-p])=\sigma_b^2 \delta[p]$
et donc

$$\overset{\circ}{\boldsymbol{\gamma}}_{b}(\nu)=\mathcal{F}\{\gamma_b[p]\}=\sigma_b^2.$$

On obtient au final

$$\overset{\circ}{\boldsymbol{\gamma}}_{b_w}(\nu))=\sigma_b^2 |\overset{\circ}{w}(\nu)|^2=\frac{\sigma_b^2}{|\overset{\circ}{h}(\nu)|^2},$$

où

$$\overset{\circ}{h}(\nu)=\mathcal{F}\{h[n]\}=\sum_k{h[k]e^{+i 2 \pi \nu k}}$$

Par définition,

$$\sigma^2_{b_w}= \gamma_{b_w}(0) =\int_{[1]} \! \overset{\circ}{\boldsymbol{\gamma}}_{b_w}(\nu)\mathrm{d}\nu,$$

on obtient alors 

\begin{align*}
\sigma_{b_w}^2&=&\int_{[1]} \! \sigma_b^2 \frac{1}{|\overset{\circ}{h}(\nu)|^2}\mathrm{d}\nu.
\end{align*}

En considérant que $\sigma_b^2=N_0$ et $\sigma_s^2=\mathbb{E}(\vert s[n] \vert^2)=1$, le rapport signal sur
bruit (signal-to-noise ratio, *SNR*) s'exprime alors

$$\mathsf{SNR_{IIR-ZF}}=\frac{1}{\sigma^2_{b_w}}=\frac{1}{ \int_{[1]} \! \frac{N_0}{|\overset{\circ}{h}(\nu)|^2}\mathrm{d}\nu}$$

Cette expression peut s'interpréter de la manière suivante. Soit

$$\mathsf{SNR}( \nu ) = \frac{\sigma_s^2 \vert \overset{\circ}{h}{(\nu)}\vert ^ { 2 }}{ N _ { 0 }}$$

le rapport signal à bruit par unité de fréquence. On définit alors l'opérateur de moyenne harmonique $\mathcal { H }\{.\}$ par

$$\mathcal { H } \left\{ \overset{\circ}{x}{(\nu)} \right\} = \frac { 1 } { \int _ {[1]} {\frac { 1 } { \overset{\circ}{x}{(\nu)} }} d \nu }.$$

On peut alors écrire

$$\mathsf{SNR_{IIR-ZF}}=\mathcal { H }\{\mathsf{SNR}( \nu )\}$$ 

On peut également étudier différents cas limites:

1.  Si $\overline{h}(z)$ est un filtre passe-tout, ie.
    $\vert\overset{\circ}{h}(\nu)\vert=\alpha, \forall \nu \in [0,1]$,
    alors 
    
    $$\mathsf{SNR_{IIR-ZF}}=\frac{\alpha^2}{N_0}.$$ 
    
    On a alors un canal de type Gaussian sans IES.

2.  Ainsi si il existe $\nu$ tel que $\overset{\circ}{h}(\nu)=0$, ou si
    $\overline{h}(z)$ a des zéros proches du cercle unité, on peut avoir
    une variance très fortement augmentée ($\sigma_{b_w}^2 \rightarrow 0$), d'où une dégradation du rapport
    signal sur bruit ($\mathsf{SNR_{IIR-ZF}} \rightarrow +\infty$). Dans
    ce dernier cas, il devient évident que l'égalisation de type ZF aura
    des performances très faibles, ce qui fait que ce critère est très
    peu considéré en pratique pour cette application.

#### Egalisation à structure contrainte

On peut reprendre le même type de calcul si on considère $w[n]$ de type RIF. Cependant, il devient aisé de redériver les calculs dans le domaine
temporel, plutôt que fréquentiel, où l'on peut avoir une autre interprétation. Ainsi, par définition, on a

$$\sigma^2_{b_w}= \gamma_{b_w}[0]=\sigma^2_b \gamma_w[0],$$ 

où l'on a a utiliser le fait que

$$\gamma_{b_w}[p]=w[p]*\gamma_{b}[p]=\sigma^2_b w[p]$$ 

Comme $w[n]$ est un filtre numérique de type RIF, on obtient facilement

$$\sigma^2_{b_w}=\sigma^2_b \sum_{k=-N}^{+N}{|w_k|^2}.$$ 

On a donc une variance augmentée d'un facteur $\sum_{k=-N}^{+N}{|w_k|^2}$ et donc une
diminution du rapport signal sur bruit du même facteur. Le rapport signal sur bruit est lui un peu plus compliqué a évaluer car, dans notre
cas, il reste de l'IES résiduelle dont l'expression dépend du filtre $w[n]$ obtenu après calcul. En effet après filtrage, le modèle du signal
estimé est donné par

$$\hat{x}[n]=w[n]*h[n]*s[n]+w[n]*b[n]=s[n]+\sum_{|k|>N}{(w*h)[k]s[n-k]}+w[n]*b[n].$$

Le terme de bruit plus interférences à prendre en compte dans le rapport signal sur bruit plus interférence est alors donné par

$$b_i[n]=\sum_{|k|>N}{(w*h)[k]s[n-k]}+w[n]*b[n].$$ 

On définit alors la quantité 

$$\mathsf{SINR_{FIR-ZF}}=\frac{1}{\sigma_{b_i}^2}.$$ 

Une expression similaire peut être dérivée pour le cas d'un filtre obtenu par la méthode des moindres carrés.

#### Résumé Bruit ZF
````{tabs} 

```{tab} ZF non contraint

$$\begin{array}{|ccc|}
\hline 
\textrm{En Temporel }& \vert & \textrm{Domaine fréquentiel   } \\
\hline 
& & \stackrel{\circ}{\gamma}_{b_f}(\nu)=\sigma_b^2\left|\stackrel{\circ}{w}_{z f}(\nu)\right|^2 \;\;\;\\
\hat{s}[n]=s[n-d]+\underbrace{w_{Z F} * b[n]}_{b_f[n]}& & \Downarrow\\
& & \sigma_{b_f}^2=\sigma_b^2 \int_{[1]} \frac{1}{\mid \stackrel{\circ}{|h(\nu)|^2}} \mathrm{~d} \nu \;\;\;\\
\hline
\end{array}$$
```


```{tab} ZF FIR (sans délai)

$$
b_f[n]=\sum_{k=-N}^N w_k b_{n-k} \Rightarrow  \sigma_{b_f}^2=\sigma_b^2 \sum_{k=-N}^N\left|w_k\right|^2=\sigma_b^2 E_w
$$

```
````

Le terme égalisation se comprend très bien dans le domaine fréquentiel où le produit des deux réponses fréquentielles permet d'obtenir une réponse fréquentielle globale constante.


