## Propriétés des fonctions d'autocorrélation.

Une fonction de corrélation d'un processus aléatoire \emph{centré} peut s'interpréter comme un
produit scalaire :

$$\gamma_X[p]= \mathbb{E}(X_{n}X_{n-p}^{*}) = <X_{n},X_{n-p}>$$

et il en résulte toutes les propriétés déjà vues pour les fonctions de corrélation de signaux
déterministes. $\gamma_X[p]$ est une fonction à symétrie hermitienne, 

$$\gamma_X[p]=\gamma_X[-p]^*$$ 

de type positif (on a $\sum\limits_{i,j }^{} a_{i}a_{j} \AC{X}{n_j , n_i} \; \geq  \; 0$). 

D'après la propriété de symétrie hermitienne, il  suffit d'obtenir les valeurs calculées de $\gamma_X[p]$ pour $p \geq 0$ pour connaître entièrement la fonction d'autocorrélation. 