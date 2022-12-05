## Communications mono-porteuse par bloc :

### Principe

On considère le schéma donné par la Figure XXX. Pour ce schéma, on considère une transmission par bloc comme pour un système de type multi-porteuses. A l'émetteur, on considère la transmission d'une trame  de $N$ symboles notée $\textbf{x}=[x_p(0),\cdots,x(N-1)]$ où $x(n),\; n \in \{1 \cdots N\},$ représente le $n-$ième symbole modulé envoyé sur la trame courante émise tel que  $x(n) \in \mathcal{X}$, où $\mathcal{X} \subset \mathbb{C}$ est un ensemble de symboles d'une constellation $M$-aire.
Après ajout d'un préfixe cyclique, on obtient le vecteur, on retrouve le vecteur de symboles à émettre 

$${\bf \tilde{x}}=[\tilde{x}[0] \tilde{x}[1] \cdots \tilde{x}[N+N_{cp}-1]]=[x[N-N_{cp}] \cdots  x[N-1]|x[0] \cdots  x[N-1]].$$

Après transmission sur le canal sélectif en fréquence $h[n]$, on a

$$y[n]=h[n] * \tilde{x}[n]+ b[n]$$

Après retrait du CP, on a alors

$$y[n]=h[n] \circledast x[n]+ b[n].$$

### Modèles en réception - FDE
Au récepteur, après TFD, l'étape d'égalisation dans le domaine fréquentiel (FDE, \emph{frequency domain equalization}) consiste à appliquer un filtre $W[k], \; k=0 \cdots N-1$ sur chaque sous-bande. On obtient alors le modèle fréquentiel suivant

$$
\begin{align}
Y[k]=&H[k]X[k]+B[k], \; \forall k=0:N-1 \notag \\
&\notag \\
Y_e[k]=& W[k]Y[K] \notag \\
=& W[k]H[k]X[k]+W[k]B[k], \; \forall k=0:M-1 \notag
\end{align}
$$

Comme pour le cas temporel, différentes stratégies sont possibles pour le filtre $W[k], \; k=0 \cdots N-1$:

1. Cas MMSE

$$
\begin{align}
W[k]&= \frac{\gamma H[k]^{*}}{ \gamma \vert H[k]\vert^{2} + 1} \\
\gamma &=\frac{\sigma_X^2}{\sigma_B^2}\\
\end{align}
$$

2. Cas ZF

$$
\begin{align}
W[k]&= \frac{H[k]^{*}}{\vert H[k]\vert^{2}} 
\end{align}
$$



Ce modèle se transpose en temporel comme suit

$$
\begin{align}
\hat{x}[n]=& TFD^{-1}(Y_e[k]), \; \forall n=0:M-1 \notag \\
=&\underbrace{\tilde{w}\circledast x[n]}_{\begin{smallmatrix} 
  \text{signal utile}\\ 
  \text{+} \\
  \text{interference} \\ \text{entre symbole}
\end{smallmatrix}} + \underbrace{w \circledast b[n]}_{bruit \; filtre} = \underbrace{x_u[n]+x_i[n]}_{\hat{x}_t[n]}+ \hat{b}[n] 
\end{align}
$$

avec $\tilde{w}=TFD^{-1}(\tilde{W}[k])=TFD^{-1}(W[k]H[k]).$



Si on prend le modèle du signal après égalisation, on aura

$$
\begin{align}
\hat{x}[n]&= \alpha x[n] + x_i[n] + \hat{b}[n]\\
&= \alpha x[n] + b'[n]
\end{align}
$$

On pourra donc faire une détection en faisant une approximation Gaussienne sur $b'[n]$ et ainsi appliquer les mêmes détecteurs que le cas OFDM. Reste à déterminer le fameux facteur $\alpha$, qui est une facteur de biais comme dans le cas des filtres temporels.


### SC-FDMA: extension pour l'accès multiple

#### Principe
Ce schéma d'égalisation fréquentiel peut être étendu pour le cas de communications mono-utilisateurs. Le Principe générale est donné par les figure suivante.



Les données de l'utilisateur sont "précodées" par une DFT d'ordre $M$. Puis les $M$ données utiles fréquentielles de l'utilisateur sont réparties sur les $N$ entrées d'une IDFT d'ordre $N$ avec $M \leq N.$ Pour chaque utilisateur, le mapping fréquentielle doit assurer que chaque sortie de DFT de chaque utilisateur est mappé de manière unique une entrée de la $N$-IDFT et l'on doit également assuré qu'il n'y a aucune collision en tre les utilisateurs (une entrée de la IDFT n'est assignée qu'à un seul utilisateur), assurant par la même un accès fréquentiel orthogonale. Après ajout d'un préfixe cyclique, les données d'un bloc comprenant les données utiles plus les informations redondantes liées au CP sont transmisses sur le canal.  Au récepteur, on aura l'architecture suivante : les données reçues pour un bloc de taille $N$ qui comporte les données de différents utilisateurs sont d'abord translatées dans le domaine fréquentiel par une DFT d'ordre $N,$ puis on réalise une égalisation "par porteuse" en appliquant un filtre "égaliseur" par voie de sortie de DFT. Les sorties sont alors démultiplexer pour récupérer les données afférant à chaque utilisateur appliquant l'opération de démultiplexage inverse à l'opération de multiplexage réalisée à l'émission. Par chaque utilisateur, on peut alors récupérer les données estimées par application d'une IDFT d'ordre $M.$  On peut alors détecter les données en considérant le modèle de réception précédemment décrit et dont les paramètres analytique seront dérivés dans la section suivante.

Si on prend le modèle du signal après égalisation, on aura

$$
\begin{align}
\hat{x}[n]&= \alpha x[n] + x_i[n] + \hat{b}[n]\\
&= \alpha x[n] + b'[n]
\end{align}
$$

#### SC-FDMA vs OFDM

D'un point de vue structurel, la différence avec l'OFDM est donnée de la manière suivante :


Cette forme d'accès est souvent dénommée "DFT-spreaded OFDM" ou "Precoded OFDM, dans le sens où elle peut être vue comme une forme d'onde OFDM  dont les porteuses associée à un utilisateur d'intérêt sont précodées par une DFT. Ce précodage a pour effet de donner au signal montant SC-FDMA les caractéristiques d'une forme d'onde de type mono-porteuse, et donc d'hériter en particulier de ses propriétés de fluctuations d'enveloppes faibles, a contrario de l'OFDM.

#### Allocation de sous-porteuses

Plusieurs stratégies sont possibles pour allouer la puissance d'un utilisateur sur la bande allouée dans le domaine fréquentielle : on peut considérer soit un mode entrelacé (ou distribué) ou un mode localisé (allocation ar bloc de sous porteuses).
Les principales stratégies sont: IFDMA (Interleaved FDMA), DFDMA (Distributed FDMA) et enfin LFDMA (Localized FDMA). Seul le dernier mode a été retenu pour le système LTE (4G) pour des raisons de simplicité de signalisation et de sensibilité à la synchronisation fréquentielle en liaison montante.


Le schéma LFDMA dans le cas de deux utilisateurs peut être explicité comme suit,  où l'on remarque l'allocation par bloc des porteuses aux utilisateurs.

TO BE ADDED

Le récepteur associé peut être visualisé comme suit.

TO BE ADDED