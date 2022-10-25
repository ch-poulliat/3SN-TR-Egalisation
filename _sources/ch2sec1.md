## Principes

Comme vu dans le chapitre précédent, la transmission sur canal sélectif en fréquence mène à l'introduction d'interférences entre symboles sur le
signal reçu. On a obtenu alors le signal suivant

$$y[n]=\sum_{k=0}^{L-1}{h[k] x[n-k]+b[n]}$$ 

où $h[n]$ est la réponse impulsionnelle du canal discret équivalent bande de base et $b(n)$ est
un bruit blanc additif au niveau du récepteur. Au récepteur, on souhaite
*"combattre"* cette IES en traitant numériquement les échantillons
reçus. On cherche ainsi une estimée $\hat{s}[n]$ de $s[n-d]$, une
version une version éventuellement retardée de $s[n]$ d'un délai $d$.
Notons que $d$ introduit un délai de traitement pour le système complet.

Le principe général de l'égalisation dite linéaire est donnée par la
figure suivante :

::: center
![Chaine pour égalisation
linéaire](canalegallin.pdf){width="\\textwidth"}
:::

Au niveau du récepteur, $w[n]$ est un filtre numérique dît *filtre égaliseur* que
l'on cherche à déterminer/optimiser. Comme filtre numérique, il peut
avoir différentes structures possibles, ie. à réponse impulsionnelle
finie ou infinie (finite impulse response/*FIR*, infinite impulse
response/*IIR*). Du fait que le récepteur est un filtre, on parle
d'égalisation linéaire. Une fois la structure imposée, il existe
différents critères d'optimisation pour déterminer le filtre $w[n]$. Les
deux principaux sont :  

<span style="color: blue">1.   ***Le critère Zero-forcing - ZF :*** </span>  
    
Dans ce cas, les interférences entre symboles sont *"forcées à zéro"* par filtrage.  
    

<span style="color: blue">2.   ***Le critère MMSE (minimum mean square error) :*** </span>  
    
Dans ce cas, on cherche à minimiser l'erreur quadratique moyenne après filtrage par $w[n]$ entre le signal estimé et le signal réel.
