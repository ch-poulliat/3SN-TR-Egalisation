## Représentation bande base des signaux sur canal sélectif en fréquence

### Modélisation sur canal Gaussien  - Rappel

On considère une modulation de phase et d'amplitude d'ordre $M$. Le
signal émis en bande de base est alors donné par 

$$\begin{aligned}
s(t)&= \sum_{k \in \mathbb{Z}}{s_k h_e(t-k T_s)}, \nonumber 
\end{aligned}$$ 

où

-   $\left\{ s_k = i_k + j q_k \right\}_{k \in \mathbb{Z}},\; s_k \in \mathbb{C}$ est la
    séquence de symboles émis appartenant à une constellation notée
    $\mathcal{S}$. On note $|\mathcal{S}|=M=2^m$.

-   $T_s$ :est la période symbole,

-   $h_e(t)$ est le filtre de mise en forme à l'émission.


Le signal émis en bande transposée (ie. le *signal modulé*) est donné
par 

$$\begin{aligned}
\tilde{s}(t)&= \sqrt{2}\Re[s(t) e^{j 2 \pi f_0 t}] \nonumber \\
&= \Re[s(t)] \sqrt{2} \cos(2 \pi f_0 t)-\Im[s(t)] \sqrt{2} \sin(2 \pi f_0 t) \nonumber \\
&= I(t) \sqrt{2} \cos(2 \pi f_0 t)- Q(t) \sqrt{2} \sin(2 \pi f_0 t)
\label{eqn:rice decomposition}
\end{aligned}$$ 

où

-   $f_0$ est la fréquence porteuse,

-   $I(t)=\sum_k{i_k h_e(t-kT)}$ est le signal dît en phase (*voie I*),

-   $Q(t)=\sum_k{q_k h_e(t-kT)}$ est le signal dît en quadrature (*voie
    Q*),

$s(t)$ est généralement nommé *enveloppe complexe* du signal
$\tilde{s}(t)$. Le facteur $\sqrt{2}$ est là pour assurer que les deux
signaux ont la même énergie/puissance (cas déterministe/cas aléatoire).
De même, l'équation
[\[eqn:rice decomposition\]](#eqn:rice decomposition){reference-type="eqref"
reference="eqn:rice decomposition"} représente la décomposition dîte de
Rayleigh-Rice du signal passe bande $\tilde{s}(t)$.

Au récepteur, en l'absence de bruit, la récupération idéale d'une voie se réalise comme suit. Pour la
voie en phase, on aura en utilisant les formules trigonométriques classiques 

$$\begin{aligned}
\tilde{s}(t) \sqrt{2} \cos{(2 \pi f_0 t)} &= I(t) + I(t) \cos{(4 \pi f_0 t)} - Q(t) \sin{(4 \pi f_0 t)} \nonumber 
\end{aligned}$$ 

On aura une expression similaire sur la voie en quadrature si on considère
$- \tilde{s}(t) \sqrt{2} \sin{(2 \pi f_0 t)}$. 

En supposant que le signal est à bande étroite, après filtrage passe-bas idéal, en combinant le résultat le résultat des deux traitements précédents, on retrouve
bien le signal

$$x(t)=I(t)+j Q(t)$$

Au récepteur, le bruit $\tilde{b}(t)$ Gaussien bande étroite de densité bilatérale de bruit $N_0/2$ peut s'écrire comme suit

$$\begin{aligned}
\tilde{b}(t)&= \sqrt{2}\Re[b(t) e^{j 2 \pi f_0 t}] \nonumber \\
&= \Re[b(t)] \sqrt{2}\cos(2 \pi f_0 t)- \Im[b(t)] \sqrt{2}\sin(2 \pi f_0 t) \nonumber \\
&= b_i(t) \sqrt{2} cos(2 \pi f_0 t)- b_q(t) \sqrt{2}sin(2 \pi f_0 t)\nonumber 
\end{aligned}$$ 

Les composantes $b_i(t)$ et $b_q(t)$ ont pour densité spectrale de puissance $N_0/2$ pour tout $f$ sur $[-B/2, B/2]$ soit

$$\overset{\circ}{\boldsymbol{\gamma}}_{b_i}(f)=\overset{\circ}{\boldsymbol{\gamma}}_{b_q}(f)=\left\lbrace \begin{array}{cl}
\frac{N_0}{2}&,\; \forall |f| \leq \frac{B}{2} \\
0& \mathrm{sinon}
\end{array}\right.$$

Dans le cas Gaussien, on peut donc écrire le signal reçu en bande transposée comme étant 

$$\tilde{r}(t)=\tilde{s}(t)+ \tilde{b}(t)$$ 

avec

$$\tilde{r}(t)=\sqrt{2}\Re[r(t) e^{j 2 \pi f_0 t}]$$ 

et

$$r(t)=r_i(t)+j r_q(t).$$

En appliquant le récepteur précédent, on retrouve bien

$$\begin{aligned}
r(t)&=s(t) + b(t) \nonumber \\
&=\sum_k{s_k h_e(t-kT_s)} +b(t)
\end{aligned}$$

où $b(t)$ est un bruit blanc complexe d'autocorrélation $\boldsymbol{\gamma}_{b}(\tau)=\mathbb{E}(b(t)b^*(t-\tau))=N_0 \;\delta(\tau)$

### Modèle sur canal à bande limitée sélectif en fréquence

Dans le cadre d'un canal à bande limitée de réponse impulsionnelle $\tilde{h}_c(t)={2} \Re[h_c(t)e^{j 2 \pi f_0 t}]$, le signal obtenu
après filtrage par $\tilde{h}_c(t)$ s'écrit

$$\tilde{r}(t)=\tilde{h}_c(t)*\tilde{s}(t)+\tilde{b}(t)$$

Après calcul, on peut montrer que le signal équivalent bande de bande
après démodulation peut s'écrire

$$\begin{aligned}
r(t)&=h_c(t)*s(t) + b(t) \nonumber \\
&=\sum_k{s_k (h_c*h_e)(t-kT_s)} +b(t)
\end{aligned}$$