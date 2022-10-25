## Fitrage adapté et blanchiment

Une stratégie optimale à la réception est d'appliquer un filtre adapté à l'ensemble des contributions convolutives de la chaîne de transmission.
Cette opération de filtrage s'accompagne de la nécessité d'une mise en oeuvre d'un filtre numérique de blanchiment après échantillonnage au rythme symbole. En effet, le bruit équivalent en sortie de filtre adapté est (hors cas pathologique) coloré. Le modèle d'observation de cette stratégie de réception est donné par


$$\begin{aligned}
y(t)&= h_r(t)*r(t) + h_r*b(t) \nonumber \\
&= \sum_{k \in \mathbb{Z} }{s_k (h_r*h_c*h_e)(t-k T)} +h_r(t)*b(t) \nonumber \\
&= \sum_{k \in \mathbb{Z} }{s_k h(t-k T)} + b_r(t)
\end{aligned}$$ 

avec $h(t)=h_r*h_c*h_e(t)$, enveloppe complexe du canal global *équivalent* en bande de base.

La stratégie de réception (optimal), dénommée *Whitened Matched Filter* \[Forney\] , est donnée par : 

1.  $h_r(t)$ est le filtre adapté à $g(t)=h_c(t)*h_e(t)$,

2.  échantillonnage au rythme symbole $T_s$, et application d'un filtre blanchissant,
        et nécessité d'un filtre blanchissant,

3.  Détection par bloc (interférence entre symbole toujours présente) au sens du maximum de vraisemblance ou critère de détection sous-optimaux.

Nous ne détaillerons pas ce schéma qui n'est pas toujours le plus simple à mettre en oeuvre dans un contexte de canal $h_c(t)$ variable rapidement en temps.