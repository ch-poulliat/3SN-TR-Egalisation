## Stationnarité

La stationnarité d'un processus aléatoire $X(n,\omega)$ traduit une invariance dans le temps des propriétés statistiques du processus.

```{prf:definition} Stationnarité forte

$\forall k, \quad (X_{n_{1}},X_{n_{2}},\ldots,X_{n_{N}})$ a même loi de probabilité que
$(X_{n_{1}+k},X_{n_{2}+k},\ldots,X_{n_{N}+k})$.

```

```{prf:definition} Stationnarité du premier ordre

$$\mathbb{E}(X(n,\omega))=m_{X}(n)= m_{X}=\text{constante}$$

```

On dit que le processus $X(n,\omega)$ est *centré*  si sa moyenne est nulle pour tout $n$. Un processus centré est donc stationnaire au premier ordre. On notera $X_c$ le processus centré déduit du processus $X$ par :

$$X_c(n,\omega)=X(n,\omega)-m_X(n)$$

Le processus $X_c$ est stationnaire au premier ordre.

```{prf:definition} Stationnarité du Second ordre

$$ 
R_{X}({n_1},{n_2})=  R_{X}({n_1+k},{n_2+k}) \quad \forall \quad k \in \mathbb{z} \label{equ:st2} 
$$
```

L'expression donnée à l'équation~ précédente permet une interprétation aisée~: le processus est stationnaire à l'ordre 2 si sa fonction d'autocorrélation ne dépend pas des instants de calcul mais seulement du décalage  entre ces instants (pour le vérifier prendre $k=-n_1$). 
Pour cette raison, il est plus pratique de manipuler une expression de la covariance faisant  
apparaître ce décalage, noté $p$. On l'écrira :

$$R_{X}({n},{n-p})$$

$X$ sera stationnaire à l'ordre deux si $R_{X}({n},{n-p})$ dépend de $p$ uniquement (et pas de $n$). La même chose peut être appliquée à l'autocovariance.

```{prf:definition} Stationnarité au second ordre : fonction d'autocorélation

 Si $X$ est stationnaire au second ordre, alors $R_{X}({n},{n-p})$ ne dépend que de la seule variable $p$. 
 
 On note

$$\gamma_X[p]= R_{X}({n},{n-p})

 la *fonction d'autocorrélation du processus* $ X$. 
\end{definition}

On remarque que la stationnarité forte entraîne la stationnarité au premier et au deuxième
ordre, mais que la réciproque est généralement fausse (sauf dans le cas Gaussien)
```

```{prf:definition} Stationnarité mutuelle

 $X$ et $Y$ sont dits *mutuellement stationnaires* si leur intercorrélation 
$R_{X,Y}{n}{n-p} =\mathbb{E}(X(n,\omega)Y^*(n-p,\omega))$ ne dépend que de $p$. 

On note alors leur *fonction d'intercorrélation*

$$
\gamma_{X,Y}[p]= R_{X,Y}(n,n-p) 
$$ 

```

```{prf:property} Somme de processus
 Si $X$ et $Y$ sont stationnaires et mutuellement stationnaires, $X+Y$ l'est aussi et vérifie~:
 
$$\gamma_{X+Y}[p]= \gamma_{X}[p]+ \gamma_{X,Y}[p]+ \gamma_{Y,X}[p]+ \gamma_{Y}[p]$$

Alors, $\gamma_{X+Y}[p]= \gamma_{X}[p]+ \gamma_{Y}[p]$ si et seulement si $X$ et $Y$
sont orthogonaux.
```

La même chose peut être dérivée pour les fonctions de covariance avec la somme directe des autocoavriances si les processus sont décorrélés.