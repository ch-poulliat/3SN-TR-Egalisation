## Egalisation par filtrage de Wiener

```{figure} ./images/egal_wiener.png
---
height: 12cm
name: wiener
---
Principe du filtrage de Wiener
```


Une autre approche pour l'égalisation linéaire des canaux sélectifs en fréquences consiste à considérer comme critère d'optimisation la
minimisation de l'erreur quadratique moyenne (EQMM), *mimimum mean square error (MMSE)*. Comparé au cas d'un critère ZF, le critère MMSE
prend en compte ici le bruit additif et la réduction de l'interférence entre symboles qui sont les deux principaux termes de perturbation du
signal reçu. Contrairement au cas de l'égaliseur ZF qui ne gère que l'interférence entre symboles, l'égaliseur MMSE cherche un compromis
entre réduction des interférences entre symboles et amplification du bruit.

Le principe est alors le suivant (voir schéma {numref}`wiener`):

```{prf:definition}

Trouver le filtre optimal $w_{opt}(z)$ qui minimise la fonction de coût

$$J_{\mathbf{w}}=\mathbb{E}\left(|e[n]|^2\right), \; e[n]=\hat{s}[n]-s[n-d], \; s[n]=w*y[n]$$

```

### Principe d'orthogonalité

Sans contrainte sur la structure de $w[n]$, le critère à optimiser peut s'écrire

$$\begin{aligned}
J_{\mathbf{w}}&=\mathbb{E}\left(|e[n]|^2\right)\\
&=\mathbb{E}\left(\left(\sum_{k=-\infty}^{+\infty}{w[k]y[n-k]}-s[n-d]\right)\left(\sum_{-\infty}^{+\infty}{w^*[k]y^*[n-k]-s^*[n-d]}\right)\right)
\end{aligned}$$

Le filtre optimum s'obtient en recherchant les points stationnaires de la fonction $J_{\mathbf{w}}$ vue comme une fonction de $\mathbb{C}$ dans
$\mathbb{R}$ et dont on peut montrer dans le cas à dimension finie que c'est une fonction quadratique de $\boldsymbol{w}$. En appliquant les règles
de différenciation dans le cas complexe, on obtient l'expression suivante 

$$\begin{aligned}
\frac{\partial J}{\partial w^*[p]}&=\mathbb{E}\left(\left(\sum_{k=-\infty}^{+\infty}{w[k]y[n-kk]}\right)y^*[n-p]\right)\\
&=\mathbb{E}\left(e[n] y^*[n-p]\right) =0,\; \forall p \in \mathbb{Z}.
\end{aligned}$$ 

On obtient ainsi la règle dîte du principe d'orthogonalité, l'erreur étant dans ce cas orthogonale aux observations
si on interprète la covariance comme un produit scalaire.

```{prf:definition} Principe d'orthogonalité

$$\mathrm{CNS} : \; \mathbb{E}(e_{opt}[n]y[n-k]^*) = 0, \; \forall k \in \mathbb{Z}$$

```

````{prf:property}

$\mathbb{E}(XY^{*})=<X,Y>$ définit un produit scalaire sur
$\mathcal{H}=L^2(\Omega)$ si les variables sont centrées (espace des
variables aléatoires de variance finie). L'erreur optimale est donc
obtenue si elle est orthogonale à l'espace des observations (meilleure
estimation obtenue). C'est donc une sorte d'équivalent du théorème de
Pythagore.

```{figure} ./images/principe_ortho.png
---
height: 12cm
name: orthogonality
---
```
````

Nous avons donc à résoudre 

$$\begin{aligned}
\mathbb{E}(e[n]y^*[n-p])&=0,\; \forall p
\end{aligned}$$

ce qui donne en considérant $\hat{s}[n]=\sum_k{w[k] y[n-k]}$ et $e[n]=\hat{s}[n]-s[n-d]$,

$$\begin{aligned}
\sum_k{w[k]\mathbb{E}(y[n-k]y^*[n-p])}&=\mathbb{E}(s[n-d]y^*[n-p])\,\; \forall p
\end{aligned}$$

On obtient alors un système linéaire, appelé *équations normales* donné par

$$\begin{aligned}
w[p]*\boldsymbol{\gamma}_{y}[p]&= \boldsymbol{\gamma}_{sy}[p-d], \; \forall p
\end{aligned}$$

Dans le domaine en $\mathcal{Z}$, ceci à équivaut à

$$w(z)=\frac{\overline{\gamma}_{sy}(z) z^{-d}}{\overline{\gamma}_{y}(z)}$$

Dans le domaine de Fourier, on a également

$$\overset{\circ}{w}(\nu)=\frac{\overset{\circ}{\gamma}_{sy}(\nu) e^{-i2 \pi \nu d}}{\overset{\circ}{\gamma}_{y}(\nu)}$$

A partir des équations précédentes, on peut donner la propriété remarquable suivante qui illustre bien le principe d'orthogonalité vu
précédemment. Considérons l'autocorrélation du processus d'erreur $\{e[n]\}$ dont l'expression est donnée par 


$$\begin{aligned}
\boldsymbol{\gamma}_{e}[p]&=\mathbb{E}(e[n]e^*[n-p]) \\
&= \mathbb{E}(e[n](\hat{s}[n-p]-s[n-d-p])^*)\\
&=\boldsymbol{\gamma}_{e\hat{s}}[p]-\boldsymbol{\gamma}_{es}[p+d]
\end{aligned}$$

On a alors

$$\begin{aligned}
\mathbf{\gamma}_{e\hat{s}}[p]&=\sum_k{w^*[k]\underbrace{\mathbb{E}(e[n]y^*[n-p-k])}_{=0}} \\
&=0
\end{aligned}$$ 

Ceci signifie bien que l'erreur est orthogonale au signal estimé/prédit $\hat{s}$. On en déduit que

$$\boldsymbol{\gamma}_{e}[p]=-\boldsymbol{\gamma}_{es}[p+d]=\boldsymbol{\gamma}_{s}[p]-\boldsymbol{\gamma}_{\hat{s}s}[p+d],$$

en utilisant le fait que $e[n]=\hat{s}[n]-s[n-d]$ et dont on détaillera ci-après l'expression.

On peut cependant d'ores et déjà donner la variance de l'erreur comme

$$\begin{aligned}
\sigma_e^2 &=\boldsymbol{\gamma}_{e}[0] \\
&=\boldsymbol{\gamma}_{s}[0]-\boldsymbol{\gamma}_{\hat{s}s}[d] \\
&=\sigma_s^2-\boldsymbol{\gamma}_{\hat{s}s}[d]
\end{aligned}$$

```{prf:definition} Filtre de Wiener

1.  **Domaine temporel :**

    $$w[p]*\boldsymbol{\gamma}_{y}[p]=\boldsymbol{\gamma}_{sy}[p-d], \; \forall p$$

2.  **Domaine en $\mathcal{Z} $:**

    $$w(z)=\frac{\overline{\gamma}_{sy}(z) z^{-d}}{\overline{\gamma}_{y}(z)}$$

3.  **Domaine fréquentiel:**

    $$\overset{\circ}{w}(\nu)=\frac{\overset{\circ}{\gamma}_{sy}(\nu) }{\overset{\circ}{\gamma}_{y}(\nu)}e^{-i 2 \pi \nu d}$$

```

### Egaliseur MMSE sans contrainte

Dans le cadre de l'égaliseur sans contrainte, le filtre est un filtre IIR sans contrainte (infini \"à gauche\" et \"à droite \"). Il suffit
maintenant de calculer les termes intervenant dans les équations normales générales de la formulation du problème d'estimation de Wiener
en explicitant le modèle d'observation lié à la problématique d'égalisation. Dans notre cas, nous avons comme modèle d'observation

$$y[n]=\sum_k h[k] s[n-k]+b[n].$$

#### Expressions du filtre sans contrainte 

Par application directe des formules de filtrage d'un processus
aléatoire (centré) stationnaire au sens large (stationnaire à l'ordre
$1$ et $2$), les processus de bruit et du signal étant mutuellement
stationnaires et indépendants (décorrélés suffit), il vient

$$\boldsymbol{\gamma}_{y}[p]=h[p]*h^*[-p]*\boldsymbol{\gamma}_{s}[p]+\boldsymbol{\gamma}_{b}[p]=\gamma_{h}[p]*\boldsymbol{\gamma}_{s}[p]+\boldsymbol{\gamma}_{b}[p]$$

avec 

$$\boldsymbol{\gamma}_{h}[p]=h[p]*\check{h}(p)$$

$$\check{h}(p)=h^*[-p].$$

Ici, $\check{h}(p)$ s'interprète comme le filtre numérique adapté à
$h[n]$ et $\boldsymbol{\gamma}_{h}[p]=\sum_k h[k]h^*[k-p]$ est ce que
l'on appelle l'autocorrelation déterministe associée à la séquence
$\{h[n\}]$ On en déduit facilement que dans le domaine en $\mathcal{Z}$,
on obtient

$$\gamma_{y}(z)=\overline{h}(z)\overline{h}^*(z^{-1})\gamma_s(z)+\gamma_b(z).$$

```{warning}
Par souci de notation simplifiée, on adopte la définition

$$\overline{h}^*(z)\triangleq \sum_k h^*[k] z^{-k}.$$

```

En remarquant que $\gamma_s(z)=\sigma_s^2$ et $\gamma_b(z)=\sigma_b^2$,
on obtient au final

$$\gamma_y(z)=\sigma_{s}^2 \overline{h}(z)\overline{h}^*(z^{-1})\gamma_s(z)+\sigma_b^2.$$

De même, en remarquant que par symétrie hermitienne
$\gamma_{sy}[k]=\gamma_{ys}^*[-k]$ et
$\gamma_{ys}[k]=h[k]*\gamma_s[k]=\sigma_s^2 h[k]$,

$$\gamma_{sy}(z)=\gamma^*_{ys}(z^{-1})=\sigma_s^2 \overline{h}^*(z^{-1})$$

Au final, nous obtenons

$$\begin{aligned}
\overline{w}_{\infty}(z)&=& \frac{\sigma_s^2 z^{-d} \overline{h}^*(z^{-1})}{\sigma_s^2 \overline{h}(z) \overline{h}^*(z^{-1})+\sigma_b^2}
\end{aligned}$$

A fort rapport signal sur bruit (ie $\frac{\sigma_s^2}{\sigma_b^2} \rightarrow +\infty$), on obtient alors

$$\overline{w}_{\infty}(z) \rightarrow \overline{w}_{\mathsf{ZF}}(z)=\frac{z^{-d} }{\overline{h}(z)}$$

A contrario, à faible rapport signal sur bruit,

$$\overline{w}_{\infty}(z) \rightarrow \overline{w}_{\mathsf{MF}}(z)=\frac{\sigma_s^2}{\sigma_b^2} z^{-d} \overline{h}^*(z^{-1})$$

On obtient facilement l'expression fréquentielle en posant $z=e^{j 2\pi \nu}$, les résultats pouvant alors se résumer comme suit :

```{prf:definition} Filtre de Wiener/MMSE sans contrainte

1.  **Domaine en $\mathcal{Z}$:**

    $$\overline{w}_{\infty}(z)= \frac{\sigma_s^2 z^{-d}\overline{h}^*(z^{-1})}{\sigma_s^2 \overline{h}(z) \overline{h}^*(z^{-1})+\sigma_b^2}$$
    
    avec $\overline{h}^*(z)=\sum_n{h^*(n) z^{-n}}$

2.  **Domaine fréquentiel :**

    $$\overset{\circ}{w}_{\infty}(\nu)= e^{-j 2 \pi \nu d} \frac{\sigma_s^2 \overset{\circ}{h}^*(\nu)}{\sigma_s^2 |\overset{\circ}{h}(\nu)|^{2}+\sigma_b^2}$$

3.  **Equivalence à fort SNR avec le filtre ZF:**

    $$\overline{w}_{\infty}(z) \approx w_{\mathsf{ZF}}(z)$$

4.  **Equivalence à faible SNR avec le filtre adapté:**

    $$\overline{w}_{\infty}(z) \approx \overline{w}_{\mathsf{MF}}(z)=\frac{\sigma_s^2}{\sigma_b^2} z^{-d} \overline{h}^*(z^{-1})$$
    
```

#### Analyse de performance

Nous allons nous intéresser par la suite à l'analyse des performances en
calculant le rapport signal sur bruit résultant. Sans perte de
généralité, on considérera dans le cas sans contrainte que le délai est
nul ($d=0$), ce dernier n'influant pas les performances du filtre
égaliseur sans contrainte, mais alourdissant les dérivations.

En rappelant que $\boldsymbol{\gamma}_{e}[p]=\boldsymbol{\gamma}_{s}[p]-\boldsymbol{\gamma}_{\hat{s}s}[p+d]$,
il vient facilement que pour $d=0$

$$\boldsymbol{\gamma}_{e}[p]=\sigma_s^2 \delta[p]-(w*h*\gamma_{s})[p]$$

Dans le domaine en $\mathcal{Z}$, on trouve 

$$\begin{aligned}
\overline{\gamma}_{e}(z)&=\sigma_s^2-\overline{w}(z)\overline{h}(z)\overline{\gamma}_{s}(z)\\
&=\sigma_s^2-\frac{[\sigma_s^2]^2 \overline{h}(z)\overline{h}^*(z^{-1})}{\sigma_s^2 \overline{h}(z) \overline{h}^*(z^{-1})+\sigma_b^2}\\
&=\frac{\sigma_s^2 N_0}{\sigma_s^2 \overline{h}(z) \overline{h}^*(z^{-1})+N_0}
\end{aligned}$$ 

ou de manière équivalent dans le domaine de Fourier

$$\begin{aligned}
\overset{\circ}{\boldsymbol{\gamma}}_{e}(\nu)&=\frac{\sigma_s^2 N_0}{\sigma_s^2 \vert\overset{\circ}{h}(\nu)\vert^2+N_0}
\end{aligned}$$

On obtient alors la variance d'erreur suivante 

$$\begin{aligned}
\sigma_e^2&=\int_{[1]} \! \overset{\circ}{\boldsymbol{\gamma}}_{e}(\nu)\mathrm{d}\nu\\
&=\int_{[1]} \! \frac{\sigma_s^2 N_0}{\sigma_s^2 \vert\overset{\circ}{h}(\nu)\vert^2+N_0}\mathrm{d}\nu 
\end{aligned}$$

On peut à partir de cette expression exprimer le rapport signal-à-bruit
**en sortie de filtre égaliseur**. Notons
$\overline{h}_T(z)=\overline{w}(z)\overline{h}(z)$, le transfert totale
associé à la concaténation des filtres numériques du canal discret
équivalent et du filtre égaliseur. Le signal en sortie d'égaliseur peut
être interprété comme

$$\begin{aligned}
\hat{s}[n]&=w[n]*h[n]*s[n-d]+w[n]*b[n] \\
&=h_T[n]*s[n]+w[n]*b[n]\\
&=h_T[0]s[n]+\underbrace{\sum_{k \neq 0} h_T[k] s[n-k]}_{\mathrm{terme \; d'IES \; r\acute{e}siduel}}+\underbrace{w[n]*b[n]}_{\mathrm{bruit \; corr\acute{e}l\acute{e} \; b'[n]}}
&=h_T[0]s[n]+e'[n]
\end{aligned}$$ 

où $e'[n]$ est un terme de bruit plus interférences
entre symboles résiduelles. Ce terme ne contient pas la contribution du
symbole d'intérêt $s[n]$ et il est indépendant de ce dernier. On voit
également que l'estimateur MMSE introduit un biais égale à $h_T[0]$. On
a donc avant décision un modèle du type

$$\hat{x}[n]=\alpha s[n]+ e'[n].$$

où $\alpha=\mathbb{E}(\hat{x}[n]|x[n])=h_T[0]$ est le biais du modèle.
On définit alors les deux types de quantités pour le rapport signal à
bruit. On définit le rapport signal sur bruit lié à une estimation
biaisée sur le modèle $\hat{s}[n]=s[n]+e[n]$ comme étant

$$\mathsf{SNR_{biased}}=\frac{\sigma_s^2}{\sigma_e^2}.$$

D'après l'expression de $\sigma_e^2$ calculée précédemment, on obtient

$$\mathsf{SNR_{biased}}=\mathcal{H}\{\mathsf{SNR}(\nu)+1\}.$$

Le rapport signal sur bruit après égalisation qui prend en compte le
biais est donné quant à lui par

$$\mathsf{SNR_{unbiased}}=\frac{\alpha^2\sigma_s^2}{\sigma_{e'}^2}=\frac{h_T[0]^2\sigma_s^2}{\sigma_{e'}^2}.$$

On va maintenant déterminer ces termes et analyser leur comportement. En
remarquant que, par définition, $\hat{s}[n]=s[n]+e[n]$, on en déduit par
identification que

$$\hat{s}[n]=h_T[0]s[n]+\underbrace{e[n]+(1-h_T[0])s[n]}_{e'[n]}$$

Comme 

$$\begin{aligned}
\overline{h}_T(z)&=\frac{\sigma_s^2 \overline{h}(z)\overline{h}^*(z^{-1})}{\sigma_s^2 \overline{h}(z) \overline{h}^*(z^{-1})+\sigma_b^2}\\
&=1-\frac{\gamma_e(z)}{\sigma_s^2},
\end{aligned}$$ 

il vient 

$$\begin{aligned}
h_T[0]&=1-\frac{1}{\sigma_s^2}\int_{[1]} \! \frac{\sigma_s^2 N_0}{\sigma_s^2 \vert\overset{\circ}{h}(\nu)\vert^2+N_0}\mathrm{d}\nu \nonumber\\
&=\int_{[1]} \! \frac{\sigma_s^2 \vert\overset{\circ}{h}(\nu)\vert^2}{\sigma_s^2 \vert\overset{\circ}{h}(\nu)\vert^2+N_0}\mathrm{d}\nu >0 \nonumber\\
&=\int_{[1]} \! \frac{\mathsf{SNR(\nu)}}{\mathsf{SNR(\nu)}+1}\mathrm{d}\nu\\
&=1-\sigma_e^2/\sigma_s^2 < 1
\end{aligned}$$

On notera également que $h_T[0]$ est réel et $0<h_T[0]<1$. De plus, une
analyse à faible rapport signal à bruit, montre que
$h_T[0] \rightarrow 0$, alors que à fort rapport signal sur bruit
celui-ci tend vers $1$. On a donc toujours un biais $\alpha<1$. La
dernière expression nous montre que

$$\mathsf{SNR_{biased}}=\frac{1}{1-\alpha}.$$

Le calcul directe de $\sigma_{e'}^2$ nous donne 

$$\begin{aligned}
 \sigma_{e'}^2&=\mathbb{E}(\vert e'[n]\vert^2)\\
 &=(1-h_T[0])^2 \sigma_s^2+2*(1-h_T[0])\gamma_{ed}[0]+\sigma_{e}^2\\
 &=(1-h_T[0])^2 \sigma_s^2-2*(1-h_T[0])\sigma_{e}^2+\sigma_{e}^2.
\end{aligned}$$ 

On en déduit 

$$\begin{aligned}
\mathsf{SNR_{unbiased}}&=\frac{h_T[0]^2}{(1-h_T[0])^2-2 (1-h_T[0])^2+(1-h_T[0])}\\ 
 &= \frac{h_T[0]}{(1-h_T[0])}\\
 &= \frac{\alpha}{(1-\alpha)}
\end{aligned}$$

On en déduit le lien

$$\mathsf{SNR_{unbiased}}=\mathsf{SNR_{biased}}-1=\mathcal{H}\{\mathsf{SNR}(\nu)+1\}-1.$$

```{prf:property}

1.  **Biais sur l'estimateur MMSE :**

    $$\alpha=\int_{[1]} \! \frac{\mathsf{SNR(\nu)}}{\mathsf{SNR(\nu)}+1}\mathrm{d}\nu$$

    $$\mathsf{SNR}( \nu ) = \frac{\sigma_s^2 \vert \overset{\circ}{h}{(\nu)}\vert ^ { 2 }}{ N _ { 0 }}$$

2.  **Rapport signal sur bruit, estimateur biaisé :**

    $$\mathsf{SNR_{biased}}=\frac{1}{1-\alpha}.$$

3.  **Rapport signal sur bruit, estimateur biaisé :**

    $$\mathsf{SNR_{unbiased}}=\frac{\alpha}{1-\alpha}$$

4.  **Equivalence entre ces deux quantités:**

    $$\mathsf{SNR_{unbiased}}=\mathsf{SNR_{biased}}-1=\mathcal{H}\{\mathsf{SNR}(\nu)+1\}-1.$$

5.  **Relation d'ordre avec l'égaliseur ZF :**

    $$\mathsf{SNR_{unbiased}} > \mathsf{SNR_{ZF}}$$
    
```

### Egaliseur RIF de Wiener

Dans le cas où $w[n]$ est un filtre de taille $N$, le problème s'écrit alors

$$\hat{s[n]}=\sum_{k=0}^{N-1}{w_k y_{n-k}} \mbox{ et } \mathbb{E}(e_{opt}[n]y[n-p]^*) = 0, \; \forall p \in [0,N-1]$$

Par rapport à la section précédente, on a donc un nombre $N$ d'équations qui permettent de déterminer $w[n]$. En développant les expressions dans
le domaine temporel comme précédemment, on obtient alors le jeu d'équations normales

$$w*\boldsymbol{\gamma}_{y}[p]=\boldsymbol{\gamma}_{sy}[p-d], \; \forall p \in [0, \cdots N-1]$$

Ainsi, en prenant une écriture vectorielle, l'expression précédente peut alors s'écrire

$$[\boldsymbol{\gamma}_{y}[p] \boldsymbol{\gamma}_{y}[p-1] \cdots  \boldsymbol{\gamma}_{y}[p-N+1]] {\bf w}=\boldsymbol{\gamma}_{sy}[p-d], \;\forall p \in [0, \cdots N-1]$$

avec 

$${\bf w}=\begin{pmatrix}
w[0]\\
w[1]\\
\vdots\\
w[N-1]
\end{pmatrix}$$

En regroupant les $N$ équations pour $p \in [0, \cdots N-1]$, il vient
alors 

$$\begin{pmatrix}
\boldsymbol{\gamma}_{Y}[0] & \boldsymbol{\gamma}_{Y}[-1] & \cdots & \boldsymbol{\gamma}_{Y}[-N+1] \\
\boldsymbol{\gamma}_{Y}[1] & \boldsymbol{\gamma}_{Y}[0] & \cdots & \boldsymbol{\gamma}_{Y}[-N+2] \\
\vdots    & \vdots    & \ddots & \vdots    \\
\boldsymbol{\gamma}_{Y}[N-1] & \boldsymbol{\gamma}_{Y}[N-2] & \cdots & \boldsymbol{\gamma}_{Y}[0] \\
\end{pmatrix}\begin{pmatrix}
w[0]\\
w[1]\\
\vdots\\
w[N-1]
\end{pmatrix}=\begin{pmatrix}
\boldsymbol{\gamma}_{sy}[-d]\\
\boldsymbol{\gamma}_{sy}[1-d]\\
\vdots\\
\boldsymbol{\gamma}_{sy}[N-1-d]
\end{pmatrix}$$

En posant 

$$\boldsymbol{R}_y=\begin{pmatrix}
\boldsymbol{\gamma}_{Y}[0] & \boldsymbol{\gamma}_{Y}[-1] & \cdots & \boldsymbol{\gamma}_{Y}[-N+1] \\
\boldsymbol{\gamma}_{Y}[1] & \boldsymbol{\gamma}_{Y}[0] & \cdots & \boldsymbol{\gamma}_{Y}[-N+2] \\
\vdots    & \vdots    & \ddots & \vdots    \\
\boldsymbol{\gamma}_{Y}[N-1] & \boldsymbol{\gamma}_{Y}[N-2] & \cdots & \boldsymbol{\gamma}_{Y}[0] \\
\end{pmatrix},\; \Gamma_{sy}=\begin{pmatrix}
\boldsymbol{\gamma}_{sy}[-d]\\
\boldsymbol{\gamma}_{sy}[1-d]\\
\vdots\\
\boldsymbol{\gamma}_{sy}[N-1-d]
\end{pmatrix},$$

nous obtenons

$$\boldsymbol{R}_y \boldsymbol{w}=[(\gamma_{sy}(p-d))_{p=0 \cdots N-1}]= \Gamma_{sy}$$

L'expression détaillée en fonction des paramètres du modèle nous permet
alors de calculer *analytiquement* le filtre $\boldsymbol{w}$. En adoptant
les notations suivantes,

$$\boldsymbol{Y}_n=\left[ y[n]\; \ldots y[n-N+1]\right]^{\top},$$

$$\boldsymbol{B}_n=\left[ b[n]\; \ldots b[n-N+1]\right]^{\top},$$

$$\boldsymbol{H}=\left(\begin{array}{ccccccc}
h[0] & \ldots & h[L-1] & 0 & \ldots & \ldots& 0 \\ 
0 & h[0] & \ldots & h[L-1] & \ddots&  & \vdots \\ 
\vdots & \ddots &\ddots &  & \ddots & \ddots& \vdots \\ 
\vdots &  & \ddots & \ddots &  & \ddots& 0\\ 
0 & \ldots & \ldots & 0& h[0] & \ldots & h[L-1] 
\end{array} \right),$$

$$\boldsymbol{S}_n=\left[ s[n]\; \ldots s[n-N-L+2]\right]^{\top},$$

on obtient l'expression matricielle suivante pour le signal reçu :

$$\boldsymbol{Y}_n= \boldsymbol{H S}_n+\boldsymbol{B}_n.$$


En remarquant que $\boldsymbol{R}_y=\mathbb{E}(\boldsymbol{Y}_n^{*}\boldsymbol{Y}_n^{\top})$ et
$\mathbf{\Gamma}_{sy}=[(\gamma_{sy}(p-d))_{p=0 \cdots N-1}]=\mathbb{E}(s[n-d]\boldsymbol{Y}_n^{*})$,
il vient alors

$$\boldsymbol{R}_y=\sigma_s^2 \boldsymbol{H}^*\boldsymbol{H}^{\top}+\sigma_b^2 \boldsymbol{I}_N$$

et 

$$\mathbf{\Gamma}_{sy}=\sigma_s^2 \boldsymbol{H}^* \boldsymbol{1}_d$$

où

$$\boldsymbol{1}_d=[0 \cdots 0 \underbrace{ 1 }_{ \mbox{position d}} 0 \cdots 0]^{\top}.$$

On en déduit aisément l'expression analytique du filtre

$$\boldsymbol{w}=\sigma_s^2(\sigma_s^2 \boldsymbol{H}^*\boldsymbol{H}^{\top}+\sigma_b^2 \boldsymbol{I}_N)^{-1} \boldsymbol{H}^* \boldsymbol{1}_d.$$

A partir de

$$e[n]=\hat{s}[n]-s[n-d]=\boldsymbol{w}^{\top} \boldsymbol{Y} - s[n-d],$$ 

l'erreur quadratique moyenne se développe alors comme suit  

$$\begin{aligned}
J{(\boldsymbol{w})}&=\mathbb{E}(\vert e[n] \vert^2) \nonumber \\
&=\sigma_s^{2} + \boldsymbol{w}^{\dagger} \mathbf{R}_y \boldsymbol{w} - 2 \Re{(\mathbf{w}^{\dagger}{\Gamma}_{sy})}\nonumber 
\end{aligned}$$  

A l'optimal, on a 

$$\boldsymbol{R}_y \boldsymbol{w}=\left[(\gamma_{sy}(p-d))_{p=0 \cdots N-1}\right]= \Gamma_{sy}$$ 

et donc 

$$\begin{aligned}
\sigma_{e,\mathrm{opt}}^2 &=\sigma_s^{2}-\mathbf{\Gamma}_{sy}^{\dagger} \boldsymbol{w} \\
&= \sigma_s^{2}- \mathbf{w}^{\dagger}\mathbf{\Gamma}_{sy}\\
&=\sigma_s^{2}- \boldsymbol{w}^{\dagger} \mathbf{R}_y \boldsymbol{w}\\
&=\sigma_s^{2} (1 -\underbrace{\mathbf{w}^{\dagger} \mathbf{H}^{*} \mathbf{H}^{\dagger} \mathbf{w}}_{IES}- \underbrace{\mathrm{snr}^{-1} \Vert w \Vert ^2}_{bruit})
\end{aligned}$$

En utilisant les différentes expressions de $w$ et $\mathbf{\Gamma}_{sy}$, il vient 

$$
\sigma_{e,\mathrm{opt}}^2= \sigma _ { x }^2 - \sigma _ { x }^2\mathbf { 1 } _ { d } ^ { T } \mathbf { H }^{\top} \left[ \mathbf { H } ^ {*} \mathbf { H }^{\top} + \frac{\sigma_b^{2}}{\sigma_x^{2}}\mathbf{I}_N \right] ^ { - 1 } \mathbf {H} ^ { * }  \mathbf { 1 } _ { d }
$$

En notant

$$\mathbf{P}= \mathbf { H }^{\top} \left[ \mathbf { H } ^ {*} \mathbf { H }^{\top} + \frac{\sigma_b^{2}}{\sigma_x^{2}}\mathbf{I}_N \right] ^ { - 1 } \mathbf {H} ^ { * } ,$$

il vient

$$\begin{aligned}
\sigma_{e,\mathrm{opt}}^2&= \sigma _ { x }^2 ( 1 -  \mathbf { 1 } _ { d } ^ { T } \mathbf{P} \mathbf { 1 } _ { d } )\nonumber \\
&= \sigma _ { x }^2 ( 1 - \mathbf{p}_{d,d})
\end{aligned}$$

On peut alors montrer que 

$$\begin{aligned}
\hat { x }[ n ] &=w[n]*y[n] \\
&=\boldsymbol{w}^{\top}\boldsymbol{Y}_n \\
&= \boldsymbol{Y}_n^{\top} \boldsymbol{w} \\
&=\boldsymbol{S}_n^{\top}\mathbf { H }^{\top}(\boldsymbol{H}^*\boldsymbol{H}^{\top}+\frac{\sigma_b^2}{\sigma_s^2 } \boldsymbol{I}_N)^{-1} \boldsymbol{H}^*  \boldsymbol{1}_d+\boldsymbol{B}_n^{\top}\boldsymbol{w}\\
&= \alpha s \left[ n - { d } \right] + s_{\mathrm{IES}}[n] + b_f [ n ]
\end{aligned}$$

avec 

$$\alpha=\mathbf{p}_{d,d}$$ 

et

$$s_{\mathrm{IES}}[n]=\sum_{k=0^;k \neq d}^{N-1}{\mathbf{p}_{k,d} s[n-k]}$$

Comme dans le cas non contraint, on peut alors donner le rapport signal sur bruit biaisé comme étant

$$\mathsf{SNR_{FIR,biased}}=\frac{1}{1-\alpha}.$$

De même, on aura comme rapport signal sur bruit non biaisé

$$\mathsf{SNR_{FIR,unbiased}}=\frac{\alpha}{1-\alpha}=\mathsf{SNR_{FIR,biased}}-1.$$

On en déduit que les relations à taille finie sont identiques à celles
du cas non contraint.

```{prf:definition} Filtre Wiener RIF

1.  **Expression:**

    $$\boldsymbol{w}=\sigma_s^2(\sigma_s^2 \boldsymbol{H}^*\boldsymbol{ H}^{\top}+\sigma_b^2 \boldsymbol{I}_N)^{-1} \boldsymbol{H}^* \boldsymbol{1}_d$$
    
    où
    
    $$\boldsymbol{1}_d=[0 \cdots 0 \underbrace{ 1 }_{ \mbox{position d}} 0 \cdots 0]^{\top}$$

2.  **Rapport signal sur bruit, estimateur biaisé :** 

    En notant,
    
    $$\mathbf{P}= \mathbf { H }^{\top} \left[ \mathbf { H } ^ {*} \mathbf { H }^{\top} + \frac{\sigma_b^{2}}{\sigma_x^{2}}\mathbf{I}_N \right] ^ { - 1 } \mathbf {H} ^ { * } ,$$
    et 
    
    $$\alpha=\mathbf{p}_{d,d},$$ 
    
    il vient
    
    $$\mathsf{SNR_{FIR,biased}}=\frac{1}{1-\alpha}.$$

3.  **Rapport signal sur bruit, estimateur non biaisé :**
    
    $$\mathsf{SNR_{FIR,unbiased}}=\frac{\alpha}{1-\alpha}=\mathsf{SNR_{FIR,biased}}-1.$$

4.  **Equivalence à fort SNR avec le filtre ZF:** En utilisant associés
    au cas Wiener RIF, il vient
    
    $$\boldsymbol{w}_{\infty} \approx \boldsymbol{w}_{\mathsf{ZF-LS}}=(\boldsymbol{H}^*\boldsymbol{H}^{\top})^{-1} \boldsymbol{H}^*\boldsymbol{1}_{d}.$$

5.  **Equivalence à faible SNR avec le filtre adapté:**

    $$\overline{w}_{\infty}(z) \approx \overline{w}_{\mathsf{MF}}(z)=\frac{\sigma_s^2}{\sigma_b^2} z^{-d} \overline{h}^*(z^{-1})$$
    
```

