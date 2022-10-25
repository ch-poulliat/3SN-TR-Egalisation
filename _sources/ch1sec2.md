## Exemple : Canaux à trajets multiples

Au niveau du récepteur, quand le signal émis est soumis à différentes réflexions sur l'environnement, on obtient le signal reçu suivant

$$\begin{aligned}
\tilde{r}(t)&= \alpha_0 \tilde{s}(t) + \sum_{l=1}^{L-1}{\alpha_l \tilde{s}(t-\tau_l)} +\tilde{b}(t)\nonumber \\
&= \alpha_0 \sqrt{2}\Re[s(t) e^{+i 2 \pi f_0 t}] + \sum_{l=1}^{L-1}{\alpha_l \sqrt{2}\Re[s(t-\tau_l) e^{+i 2 \pi f_0 (t-\tau_l)}]} +\tilde{b}(t)\nonumber \\
&= \sqrt{2} \Re[\sum_{k=0}^{L-1}{\alpha_k e^{-i 2 \pi f_0 \tau_l} s(t-\tau_k) e^{+i 2 \pi f_0 t}}]+\sqrt{2}\Re[b(t)e^{+i 2 \pi f_0 t}]\nonumber\\
&=  \sqrt{2}\Re[r(t) e^{+i 2 \pi f_0 t}] \nonumber \\
\end{aligned}$$

Après calcul, on en déduit l'enveloppe complexe associée

$$\begin{aligned}
r(t)&= h_c(t)*s(t)+b(t)\\
%&=& \sum_{k \in \mathbb{N} }{s_k \left[\sum_{l=0}^{L-1}{\alpha_l \exp{(-j 2 \pi f_0 \tau_l)} h_e(t-kT-\tau_l)}\right]} + b(t) \nonumber \\
&= \sum_{k \in \mathbb{Z} }{s_k (h_c*h_e)(t-kT)} +b(t) \nonumber
\end{aligned}$$

$h_c(t)$ agit donc comme un filtre et est alors défini comme la réponse impulsionnelle du canal de propagation *équivalent* en bande de base
donnée finalement par 

$$\begin{aligned}
h_c(t)&=\sum_{l=0}^{L-1}{\alpha_l e^{-j 2 \pi f_0 \tau_l} \delta(t-\tau_l)}
\end{aligned}$$

La réponse fréquentielle du "filtre de canal" est alors donnée par

$$\begin{aligned}
H_c(f) &= \mathcal{F}(h_c(t))=& \sum_{l=0}^{L-1}{\alpha_l e^{-j 2 \pi f_0 \tau_l} e^{-j 2 \pi \tau_l f}}
\end{aligned}$$