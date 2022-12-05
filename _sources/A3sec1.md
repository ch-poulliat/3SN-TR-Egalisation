## Caractérisation d'un processus aléatoire au premier et second ordre.


```{prf:definition} Moyenne d'un processus

$$m_X(n)= \mathbb{E}(X(n,\omega))$$ 

est la *moyenne* (stochastique), encore appelée espérance
mathématique. La moyenne étant prise sur les réalisations $\omega$, elle dépend à priori de l'instant d'observation $n$.
Un processus $X$ est dit centré si $m_X(n)= \mathbb{E}(X(n,\omega)) =0$ pour tout 
instant $n$.
```
```{prf:definition} Fonction de covariance/Autocorrélation

La *fonction de covariance* est définie par

$$
\begin{aligned}
\mathbf{\Gamma}_X(n_{1},n_{2}) &= \text{cov}(X_{n_{1}}, X_{n_{2}})  \\ 
&= \mathbb{E}(X(n_{1},\omega)X(n_{2},\omega)^{*}) - \mathbb{E}(X(n_{1},\omega)) \mathbb{E}(X(n_{2},\omega))^{*}\\ 
& = \mathbb{E}((X(n_{1},\omega)-m_X(n_{1}))(X(n_{2},\omega)- m_X(n_{2}))^{*}) \\
&  =  \mathbb{E}(X_c(n_{1},\omega)X_c(n_{2},\omega)^{*}) 
\end{aligned}
$$

la *fonction d'autocorrélation* est définie par

$$
\begin{aligned}
R_{X}(n_{1},n_{2}) &= \mathbb{E}(X(n_{1},\omega)X(n_{2},\omega)^{*})
\end{aligned}
$$  

```

$X_c(n,\omega)$ est déduit du processus $X(n,\omega)$ par centrage. 

La fonction de covariance mesure la ressemblance entre les valeurs du processus centré en 2 instants différents $n_{1}$ et $n_{2}$. Elle est donc maximale quand $n_{1}=n_{2}$, et tend à décroître quand $n_{1}- n_{2}$ devient grand. 

```{prf:definition} Intercovariance/intercorrélation

la *fonction d'intercovariance est donnée par

$$
\begin{aligned}
\mathbf{\Gamma}_{X,Y}{n_{1}}{n_{2}} &= \text{cov}(X_{n_{1}}, Y_{n_{2}})  \\ 
&=  \mathbb{E}(X(n_{1},\omega)Y(n_{2},\omega)^{*}) - \mathbb{E}(X(n_{1},\omega)) \mathbb{E}(Y(n_{2},\omega))^{*}\\
& = \mathbb{E}((X(n_{1},\omega)-m_X(n_{1}))(X(n_{2},\omega)- m_Y(n_{2}))^{*}) \\
&  =  \mathbb{E}(X_c(n_{1},\omega)Y_c(n_{2},\omega)^{*}) 
\end{aligned}
$$  


la *fonction d'intercorrélation est donnée par 

$$
\begin{aligned}

R_{X,Y}({n_{1}},{n_{2}})  &= \mathbb{E}(X(n_{1},\omega)Y(n_{2},\omega)^{*})
\end{aligned}
$$  

La fonction d'intercovariance mesure la ressemblance entre les 
valeurs des deux processus centrés en $2$ instants différents $n_{1}$ 
et $n_{2}$. 