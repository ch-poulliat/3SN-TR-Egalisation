# Exercices : testez-vous

Une transmission est réalisée autour d'une fréquence porteuse $f_0$ au rythme 
symbole $1/T_s$, à l'aide du filtre de mise en forme $h_e(t)$ et du filtre de 
réception $h_r(t)$ (adapté à $h_e(t)$). $g(t) = h_r(t) * h_e(t)$ vérifie le critère de Nyquist.
Le canal physique de transmission $h_c(t)$ ne varie pas dans la durée de transmission d'une trame. 
Au récepteur, on a un bruit blanc gaussien centré de variance $N_0$ indépendant des symboles émis. 
On utilise des symboles de type MAQ-4, notés $s_k$.

## Modèle du canal discret équivalent et interférences entre symboles induites


1. Rappeler l'expression de l'enveloppe complexe du signal émis en bande de base, $s(t)$.

2. On suppose la récupération de porteuse parfaitement effectuée. Quelle est alors l'expression de l'enveloppe complexe du signal reçu en bande de base à la sortie du filtre de réception, noté $y(t)$.  Montrer en particulier que cela revient à mettre en forme les symboles par une impulsion $h(t)$ dont l'expression sera donnée. 

3. Après échantillonnage au rythme symbole $T$, donner l'expression des échantillons $y_n$ en précisant la définition du canal discret équivalent. Qu'en déduisez-vous sur le taux d'erreur symbole associé au modèle de signal discret reçu en comparaison au cas sans trajet multiple?

4. ***Application :*** Considérer le canal discret équivalent suivant : $h(z)=1+ 0.7 z^{-1}$. En absence de bruit, combien observe-t-on de symboles ? faire un dessin. Que se passe-t-il en présence de bruit ?

## Représentation fréquentielle

Considérer le canal discret équivalent suivant : $h(z)=1+ a z^{-1}, \;\; |a|<1.$ 

1. Analyser le diagramme des pôles et des zéros. Interpréter en fonction de $a?$

2. Quelle est la densité spectrale de puissance (dsp) de la s\'equence des symboles émis (supposés i.i.d.) et quelle est celle des signaux reçus ? Illustrer par une figure.

