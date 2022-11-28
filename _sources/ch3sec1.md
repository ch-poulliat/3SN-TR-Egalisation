## Maximum de Vraisemblance

On va maintenant dériver le détecteur optimal au sens du maximum de vraisemblance.

### Modèle discret équivalent bande de base

```{figure} ./images/canalisieq.png
---
width: 10cm
name: isichannel
---
Modèle de filtrage
```

Le modèle équivalent bande de base que l'on considérera est le suivant:

$$
\begin{aligned}
y[n]&= \sum_{k \in \mathbb{N} }{s_k h_{n-k}} + b[n]  \\
&= \sum_{k =0 }^{L_h-1}{ h[k] s[n-k]} + b[n] \\
&= h_0 s[n]+ \underbrace{\sum_{k =1 }^{L_h-1}{ h[k] s[n-k]}}_{\mathsf{IES}} + b[n]
\end{aligned}
$$

### Modèle à états finis


```{figure} ./images/canalisi2.png
---
width: 15cm
name: isiregister
---
Modèle de filtrage
```


Le modèle discret équivalent est donné par  

$$
\begin{aligned}
y[n] &= \sum_{k \in \mathbb{N} }{s_k h_{n-k}} + b[n] \\
&= \sum_{k =0 }^{L_h-1}{ h[k] s[n-k]} + b[n] \\
&= h_0 s[n]+ \underbrace{\sum_{k =1 }^{L_h-1}{ h[k] s[n-k]}}_{\mathsf{IES}} + b[n]
\end{aligned}
$$  


On peut alors représenter le signal suivant le schéma donné figure {numref}`isiregister`. On voir alors que le canal est bien représenter par une ligne à retards (registre) et peut donc se voir comme un code convolutif défini sur $\mathbb{C}$ de mémoire $L-1$ de rendement $R_c=1$. C'est cette analogie qui sera exploitée pour bien comprendre le modèle à état sous-jacent. 

Le modèle à état peut se mettre en exergue en remarquant que l'on peut mettre l'équation précédente sous la forme suivante:


$$
\begin{aligned}
y[n] &= z[n] +b[n] \\
&=\mathbf{h}^T \left[\begin{array}{c}
s_n \\
\mathbf{\sigma}_{n-1}
\end{array}\right] +b[n]
\end{aligned}
$$    


$\sigma_n$ représente l'état "interne" (la mémoire du canal) de dimension $M^{(L-1)}$. On peut alors donner une représentation du canal par sa machine à états finis associée. Comme pour un code convolutif, de cette machine à état, on peut déduire une représentation en treillis en incluant la dimension temporelle. Pour décrire complètement le treillis associé au canal, on doit dériver la représentation fonctionnelle suivante:

- **Equation d'évolution :  passage d'un état à $\mathbf{\sigma}_{n-1}$ à $\mathbf{\sigma}_{n}$.**

 $$\mathbf{\sigma}_n = F_1(\mathbf{\sigma}_{n-1},s_n)$$
 
- **Equation d'observation :  génération des sorties observables $z_{n}=\sum_{k=0}^{L-1}{h_k s_{n-k}}$.**


  $$z_n = F_2(\mathbf{\sigma}_{n-1} ,s_n) = F_3(\mathbf{\sigma}_{n-1} ,\mathbf{\sigma}_{n})$$


Ainsi, pour une représentation en treillis chaque état(représenté par un noeud) du treillis est une réalisation possible de $\sigma_n \in \Sigma$. Les transitions (associées aux branches) entre ses états sont régies par l'équation d'évolution et les labels associés à ces branches (ie. les symboles émis et symboles reçus) sont donnés par l'équation d'observation. L'ensemble du treillis est périodique dont une période est complètement déterminée par les transitions occurant sur une section de treillis. On donne ci-après un exemple de treillis pour un canal de mémoire $2$ ($L=3$) et une modulation BPSK. Dans ce cadre $\sigma_n$ représente un vecteur de taille $2^2$.


```{figure} ./images/treillisisi.png
---
width: 15cm
name: treillis_isi
---
Exemple de treillis.
```

### Décodage d'une Séquence par Maximum de Vraisemblance (MLSE)

```{prf:definition} Décodage d'une Séquence par Maximum de Vraisemblance
La détection par maximum de vraisemblance consiste à recherche la séquence de symbole émis vérifiant:

$$
\hat{{\bf s}}= \mathrm{arg} \max_{{\bf s'}}{p({\bf y} | {\bf s'})}
$$

où
- ${\bf s}=[s_1 s_2 \ldots s_N]$,

- ${\bf y}=[y_1 y_2 \ldots y_N]$,

- $y[n] \sim \mathcal{N}(\sum_k{h_k s_{n-k}}, N_0)$ 

```
Dans le contexte d'une transmission sur un canal sélectif en fréquence avec un bruit additif Gaussien en réception, le critère se simplifie de la manière suivante:


$$
\begin{aligned}
\hat{\mathbf{s}}&= \mathrm{arg} \max_{\mathbf{s}'}{p(\mathbf{y} | \mathbf{s}')} \nonumber \\
&=  \mathrm{arg} \max_{\mathbf{s}'}{\prod_n{p(y_n | \mathbf{s}')}} \nonumber \\
&= \mathrm{arg} \min_{\left\{s_n \right\}}{\sum_n{|y_n-\sum_{k=0}^{L-1}{h_k s_{n-k}}|^2}}
\end{aligned}
$$  


Ainsi la séquence optimale au sens du maximum de vraisemblance est celle qui minimise la distance euclidienne entre la séquence émise et la séquence reçus. Une approche "brute force" par énumération de toutes les séquences possibles nous donne une complexité de l'ordre de $M^N=2^{\log_2{(M)} N}$, ie exponentielle en l'ordre de la modulation et de la longueur de la séquence. L'utilisation de la structure markovienne du canal va nous permettre de réaliser un décodage MLSE avec une complexité raisonnable. Ainsi l'exploitation de la structure markovienne du canal permet d'avoir une énumération efficace des séquences candidates à la maximisation du critère MLSE. Elle se base en partie sur les propriétés suivantes :

```{prf:property}

- ***Chaque chemin sur le treillis représente une séquence de symboles émis possibles :*** 

$$\begin{array}{ccc}
 &  &  \text{chemin le plus problable, ie} \\
 \text{séquence MLSE} & \Leftrightarrow &  \text{de plus petite  distance euclidienne} \\
& &  \text{cumulée sur le treillis}
\end{array}$$  


- ***Correspondance espace des états et des séquences :***


$$
\begin{array}{ccc}
\left \{ s[n] | n=1 \cdots N \right\} & \Longleftrightarrow & \left\{ \sigma[n] | n=0 \cdots N \right\}\\
 & &\\
\text{Espace des séquences} & &  \text{Espaces des Etats} 
\end{array}
$$  

```

En utilisant l'équivalence précédente, on peut alors par un simple jeu de réécriture instancier le problème d'optimisation initial dans le domaine des *d'états*.


$$
\begin{aligned}
\hat{\mathbf{s}}&= \mathrm{arg} \min_{\left\{s_n \right\}}{\sum_n{|y_n-\sum_{k=0}^{L-1}{h_k s_{n-k}}|^2}}\\
& = \mathrm{arg} \min_{ \left\{\sigma_n \right\}}{\sum_n{|y_n-{z_n(\sigma_{n-1},\sigma_n)}}|^2}
\end{aligned}
$$  


On peut alors dériver l'algorithme de Viterbi qui réalise un calcul efficace de la séquence MLSE à l'aide du treillis. La dérivation se fait par récurrence en analysant une métrique cumulée représentant la distance euclidienne entre la séquence reçue et celle équivalente à la séquence $\left\{\sigma_0, \sigma_1, \cdots, \sigma_{n-1}, \sigma_n \right\}$. En effet, pour une séquence d'états se terminant à la section de treillis $n$ et dans l'état $\sigma_n(s)$, on peut écrire une métrique cumulée notée $\Lambda_n(\sigma_n)$ donnée par
  
  
$$
\begin{aligned}
\Lambda_n(\sigma_n) &= \underset{\left\{\sigma_0, \sigma_1, \cdots, \sigma_{n-1}, \sigma_n \right\}}{\operatorname{min}}{\sum_{k=0}^{n}{|y_k-{ z_k(\sigma_{k-1},\sigma_k)}}|^2} \\
& \\  
& = \underset{\left\{\sigma_{n-1} \rightarrow \sigma_n \right\}}{\operatorname{min}} \left\{ \underset{\left\{\sigma_0, \cdots, \sigma_{n-1}\right\}}{\operatorname{min}} \left\{\sum_{k=0}^{n-1}{|y_k- z_k|^2} \right\} + |y_n- z_n(\sigma_{n-1},\sigma_n)|^2 \right\}  \\
& \\  
& =\underset{\underbrace{\left\{\sigma_{n-1} \rightarrow \sigma_n \right\}}_{\mbox{transitions possibles}}}{\operatorname{min}} \left\{ \Lambda_{n-1}{(\sigma_{n-1})} + \lambda_n(\sigma_{n-1},\sigma_n) \right\}
\end{aligned}
$$  


De cette récursion, on peut alors dériver l'algorithme suivant :

```{prf:algorithm} Algorithme de Viterbi

Pour chaque section $n$ ($n=1 \cdots N$), pour chaque état $\sigma_n=s$ ($s=0 \cdots |\mathcal{S}|$) : 

1.  calculer $\Lambda_n$ tel que

$$\Lambda_n{(\sigma_{n})}=\underset{\left\{\sigma_{n-1} \rightarrow \sigma_n \right\}}{\operatorname{min}} \left\{ \Lambda_{n-1}{(\sigma_{n-1})} + \lambda_n(\sigma_{n-1},\sigma_n) \right\}$$  


2. stocker l'état précédent $\sigma_{n-1}$ : pour chaque état $\sigma_n$, on peut donc associer une séquence \emph{survivante} $\left\{\sigma_0, \cdots, \sigma_n \right\}$ de distance euclidienne cumulée associée $\Lambda_n{(\sigma_{n})}$)


A la fin du treillis, il ne reste plus que $|\mathcal{S}|$ chemins possibles, après avoir sélectionné le plus probable, par parcours arrière des états du treillis, on obtient

$$\hat{{\bf s}}= \left\{\sigma_0, \sigma_1, \cdots, \sigma_{N-1}, \sigma_N | \underset{\sigma_N}{\operatorname{argmin}}\left\{\Lambda_{N}(\sigma_N) \right\} \right\} $$
```