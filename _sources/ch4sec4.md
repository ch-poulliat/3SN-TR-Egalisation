## Analyse de performances

Nous allons maintenant dériver une analyse du rapport signal à bruit en réception et le modèle échantillonné afin d'identifier le biais résultant. Comme le SC-FDE peut être vu comme un système SC-FDMA avec $M=N,$ on traitera le cas générale du SC-FDMA. De même la modélisation est indépendante du mapping fréquentiel obtenu, seul le gain sur les porteuses est important, on considérera donc le cas d'un utilisateur dont les porteuses d'intérêt sont $M$ premières porteuses.

Pour l'émetteur, on adoptera les conventions et notations selon la figure ci-après.

```{figure} ./images/emetteur.png
---
width: 16cm
name: emetteur_model
---
Modèle Emetteur SC-FDMA
```

Pour le récepteur, on adoptera les conventions et notations selon la figure ci-après.


```{figure} ./images/recepteur.png
---
width: 16cm
name: recpeteur_model
---
Modèle Récepteur SC-FDMA
```


### Modèle du signal en réception

En appliquant les différentes définitions dans les domaines temporel et fréquentiel, on peut donner les modèles suivant pour les signaux dans le domaine temporel et fréquentiel:

- **Domaine fréquentiel :**

$$
\begin{align}
Y[k]=&H[k]X[k]+B[k], \; \forall k=0:N-1 \notag \\
&\notag \\
Y_e[k]=& W[k]Y[K] \notag \\
=& W[k]H[k]X[k]+W[k]B[k], \; \forall k=0:M-1 \notag
\end{align}
$$

- **Domaine temporel :**

$$
\begin{align}
\hat{x}[n]=& TFD^{-1}(Y_e[k]), \; \forall n=1:M-1 \notag \\
=&\underbrace{\tilde{w}\circledast x[n]}_{\begin{smallmatrix} 
  \text{signal utile}\\ 
  \text{+} \\
  \text{interference} \\ \text{entre symbole}
\end{smallmatrix}} + \underbrace{w \circledast b[n]}_{bruit \; filtre} = \underbrace{x_u[n]+x_i[n]}_{\hat{x}_t[n]}+ \hat{b}[n] 
\end{align}
$$

avec $\tilde{w}=TFD^{-1}(\tilde{W}[k])=TFD^{-1}(W[k]H[k])$



### Variance du bruit en sortie de récepteur
 
En supposant, les échantillons de bruit indépendant en entrée de DFT, on peut calculer la variance de bruit après filtrage dans les domaines fréquentiel et temporel en utilisant que la DFT est une transformation orthogonale (mais non unitaire) et que par filtrage le bruit reste Gaussien et centré. On eput donc explicité le terme de bruit et la variance comme suit

- **Domaine temporel :**

$$
\begin{align}
\hat{b}[n]=& TFD^{-1}(W[k]B[k]), \; \forall n=0:M-1  \\
=& \frac{1}{M} \sum_{k=0}^{M-1} W[k] B[k] e^{-i \frac{2 \pi}{M} n k}
\end{align}
$$

- **Variance du bruit, cas générale :**

$$
\begin{align}
\sigma^2_{\hat{b}}\triangleq & \mathbb{E}(|\hat{b}[n]|^2) \notag \\
=&  \frac{\sigma_B^2}{M} \times \frac{1}{M}  \sum_{k=0}^{M-1}{\left|W[k]\right|^2} \notag \\
=&  \sigma_{\tilde{b}_M}^2 \sum_{n=0}^{M-1}{\vert w[n] \vert^2} \notag
\end{align}
$$

avec $\tilde{b}_M[n]=TFD^{-1}(B[k])$ et $w[n]=TFD^{-1}(W[k])$


On remarque dès lors que tout est fonction du filtre mis en oeuvre pour l'égalisation fréquentielle.

Dans le cas d'un filtre MMSE fréquentiel, on a

$$
\begin{align}
W_{mmse}[k]&= \frac{\gamma H[k]^{*}}{ \gamma \vert H[k]\vert^{2} + 1} \\
\gamma &=\frac{\sigma_X^2}{\sigma_B^2}\\
\gamma_k &=  \vert H[k]\vert^{2} \gamma
\end{align}
$$

et donc

$$
\begin{align}
\sigma^2_{\hat{b}} =& \frac{\sigma_B^2}{M^2} \sum_{k=0}^{M-1}{\frac{\gamma^2 \vert H[k] \vert^2}{ (\gamma \vert H[k]\vert^{2} + 1)^2}}
\end{align}
$$

Dans le cas d'un filtre ZF, on

$$
\begin{align}
W_{ZF}[k]&= \frac{\gamma H[k]^{*}}{ \gamma \vert H[k]\vert^{2}}
\end{align}
$$

et donc

$$
\begin{align}
\sigma^2_{\hat{b}} =& \frac{\sigma_B^2}{M^2} \sum_{k=0}^{M-1}{\frac{1}{\gamma \vert H[k]\vert^{2}}}
\end{align}
$$

### Puissance du terme utile

Le signal en sortie de IDFT est donné par

$$
\begin{align}
\hat{x}_u[n]&= \tilde{w}[0]x[n]=x[n] \frac{1}{M} \sum_{k=0}^{M-1}{W[k]H[k]}
\end{align}
$$

On en déduit alors par calcul direct la variance

$$
\begin{align}
\sigma_{x_u}^2&= \sigma_x^2 \left\vert \frac{1}{M} \sum_{k=0}^{M-1}{W[k]H[k]} \right\vert^2
\end{align}
$$


### Puissance terme d'interférence entre symboles résiduelle


On peut monrer que la variance de $\hat{x}_i[n]$ est donnée par

$$
\begin{align}
\sigma_{x_i}^2&= \sigma_{x_t}^2 - \sigma_{x_u}^2
\end{align}
$$

avec

$$
\begin{align}
\sigma_{x_t}^2 &= \sigma_{x}^2 \sum_{m=0}^{M-1}{\vert \tilde{w}[<n-m>_M]\vert^2} \notag \\
&= \sigma_{x}^2 \frac{1}{M} \sum_{k=0}^{M-1}{\vert \tilde{W}[k]\vert^2} \notag \\
&= \sigma_{x}^2 \frac{1}{M} \sum_{k=0}^{M-1}{\vert {W}[k]H[k]\vert^2} \notag
\end{align}
$$

### Rapport signal à bruit en sortie de DFT

On peut alors en déduire le rapport  signal à bruit en sortie de DFT dont l'expression générale est donnée par

$$\begin{align}
SNR &= \frac{\sigma_{x_u}^2 }{\sigma_{x_t}^2 - \sigma_{x_u}^2+\sigma^2_{\hat{b}}}  \notag \\
&= \frac{\vert\alpha \vert^2}{\frac{1}{M} \sum_{k=0}^{M-1}{(\vert H[k] \vert^2 +\gamma^{-1}) \vert W[k] \vert^2 - \vert \alpha \vert^2}}
\end{align}$$

avec 

$$\alpha=\frac{1}{M} \sum_{k=0}^{M-1}{W[k]H[k]}$$

En fonction du filtre considéré on peut alors donner les expressions de SBR suivants 
:

- **Cas MMSE :**

$$
\begin{align}
 SNR &= \frac{\beta}{1 - \beta}
\end{align}
$$

avec 

$$\beta=\frac{1}{M} \sum_{k=0}^{M-1}{\frac{\gamma_k}{\gamma_k+1}}$$

- **Cas ZF :**

$$
\begin{align}
 SNR &= \frac{1}{\beta}
\end{align}
$$

avec 

$$\beta=\frac{1}{M} \sum_{k=0}^{M-1}{\frac{1}{\gamma_k}}$$

où pour rappel

$$
\begin{align}
\gamma &=\frac{\sigma_X^2}{\sigma_B^2}\\
\gamma_k &=  \vert H[k]\vert^{2} \gamma
\end{align}
$$
 
Si on prend le modèle du signal après égalisation, on aura bien une xepression du type

$$\begin{align}
\hat{x}[n]&= \alpha x[n] + x_i[n] + \hat{b}[n]\\
&= \alpha x[n] + b'[n]
\end{align}$$

où 

$$\alpha=\tilde{w}[0] = \frac{1}{M} \sum_{k-0}^{M-1} W[k] H[k]$$

$\alpha$ est donc un terme de biais tel que $\alpha=1$ pour le cas ZF. On retrouve donc que le récepteur ZF est non biaisé dans le cas fréquentiel et $0<\alpha<1$ dans le cas MMSE. C'est ce biais qu'il faudra prendre en compte dans la détection et on assimilera souvent $b'[n]$ à un bruit gaussien additif. Pour le cas SC-FDE, il suffira de considérer le cas $M=N.$ Ces résultats se généralisent au cas d'une forme d'onde filtrée avec un filtre défini dans le domaine fréquentiel (spectral shaping).


