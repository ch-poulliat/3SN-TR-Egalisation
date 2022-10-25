## Filtrage adapté partiel

### Modèle d'observation

Le modèle précédent est parfois difficile à mettre en oeuvre car il
nécessite de mettre en oeuvre un filtrage adapté à la fois au canal et
au filtre d'émission (bande de base). On préfère pour des raisons de
complexité réaliser un filtrage adapté *partiel* où le récepteur est
seulement adapté au signal émis. On a alors le signal reçu suivant en
bande de base

$$\begin{aligned}
y(t)&= h_r(t)*r(t) + h_r*b(t) \nonumber \\
&= \sum_{k \in \mathbb{Z} }{s_k (h_r*h_c*h_e)(t-k T_s)} +h_r*b(t) \nonumber \\
&= \sum_{k \in \mathbb{Z} }{s_k h(t-k T_s)} + b_r(t)
\end{aligned}$$ 

On retrouve la mise en forme classique d'un signal à
l'aide d'une forme d'onde $h(t)=h_r(t)*h_c(t)*h_e(t)$ qui est l'enveloppe
complexe du canal global *équivalent* en bande de base.

###  Modèle discret équivalent bande de base au temps symbole

Après échantillonnage au temps symbole $T_s$ on obtient alors le mdoèle discret équivalent suivant :

$$\begin{aligned}
y[n]&\triangleq y(nT_s) \nonumber \\
&= \sum_{k \in \mathbb{Z} }{s_k h((n-k) T_s)} + b_r(nT_s) \nonumber \\
&= \sum_{k \in \mathbb{Z} }{s_k h_{n-k}} + b[n] \nonumber \\
\end{aligned}$$ 

$h[n]=h_r*h_c*h_e(nT)$ définit ce que l'on appelle la réponse impulsionnelle discrète du canal équivalent en bande de base.
$b_r(t)$ est un filtre Gaussien car filtré de $b(t)$. Dans le cadre de communications où l'on utilise un filtre de réception qui est un filtre de demi-Nyquist, on peut montrer que $b[n]$ est un processus dont les échantillons sont non corrélés et donc indépendants (échantillons de processus Gaussiens). 

