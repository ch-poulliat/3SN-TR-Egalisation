## Transformée de Fourier des signaux à temps discrets/des séquences.

### Fonctions propres d'un système

On considère à l'entrée d'un FLID de réponse impulsionnelle $h[n]$, la séquence $x[n] = e^{i2 \pi \nu n}$. La sortie est alors 

$$y[n] =\sum_{p=-\infty}^{+\infty} h[{p}] {e}^{{j} 2 \pi \nu({n}-{p})}={e}^{{j} 2 \pi \nu {n}} \sum_{{p}=-\infty}^{+\infty} {h}[{p}] {e}^{-{j} 2 \pi \nu {p}}.$$

La sortie $y[n]$ est donc égale à l'entrée $x[n]$ multipliée par un terme complexe qui est ce que l'on appelle la réponse en fréquence du système. On notera

$${y}[{n}]=\overset{\circ}{h}({\nu}) {x}[{n}]=\lambda_{\nu} {x}[{n}]$$ 

avec 

$$\overset{\circ}{h}({\nu})=\sum_{{p}=-\infty}^{+\infty} {h}[{p}] \cdot {e}^{-{j} 2 \pi {\nu p}}.$$

Les séquences $e^{i2 \pi \nu n}$ sont donc les fonctions propres des systèmes linéaires à temps discret. La réponse en fréquence s'identifie à celle trouvée de la transformée  de Fourier d'une séquence comme définie ci-après.

### Transformée de Fourier des signaux à temps discrets


```{prf:definition} Transformée  de Fourier d'une séquence

La transformée  de Fourier d'une séquence $x[n]$ est définie (sous réserve de convergence)  par :

$$\overset{\circ}{x}{(\nu)}=\sum_{{n}=-\infty}^{+\infty} {x}[{n}] . {e}^{-{i} 2 \pi {\nu n}}$$

C'est une fonction **continue** de $\nu$ et $1$-périodique.
```

```{prf:definition} Transformée de Fourier inverse 

La transformée inverse est donnée par

$${x}[{n}]=\int_{[1]}{ \overset{\circ}{x}({\nu})  {e}^{+{i} 2 \pi {\nu n}}} {d}\nu.$$

```

On note souvent le passage de l'un à l'autre des domaines par la paire 

$$x[n]  \leftrightharpoons \overset{\circ}{x}(\nu)$$