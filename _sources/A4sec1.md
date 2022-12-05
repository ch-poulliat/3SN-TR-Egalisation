## Filtre linéaire invariant par décalage

On considère un filtre numérique de réponse impulsionnelle $\{ h(k) \}_{k \in \mathbf{Z}}$. Soit $X(n,\omega)$ un processus aléatoire, supposé stationnaire au premier et second ordre. On nomme $Y(n,\omega)$ le processus résultant du filtrage de $X(n,\omega)$ par $\{ h(k) \}_{k \in \mathbf{Z}}$.
Le filtrage linéaire invariant par décalage résultant est alors défini par les relations~:

$$ X(n,\omega) \rightarrow \fbox{ $h$ } \rightarrow Y(n,\omega) $$

La relation entrée/sortie s'exprime alors comme l'équation de convolution suivante :

$$ Y(n,\omega) = \sum\limits_{k \in \mathbf{Z}} h(k) X(n-k,\omega)$$
