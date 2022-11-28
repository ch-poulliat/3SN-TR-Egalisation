## Egaliseur à retour de décision

### Structure et principe


```{figure} ./images/dfev2.png
---
width: 15cm
name: DFE
---
Schéma de principe du DFE
```


Une famille d'égaliseurs très répandue est celle des égaliseurs non linéaires à retour de décisions (nommés en anglais égaliseur ***DFE pour Decision Feedback Equalizers***) dont le schéma de principe est donné figure {numref}`DFE`. Ces égaliseurs entrent dans la catégorie des égaliseurs de type *data aided*, puisque les décisions sur les symboles passés à la réception vont être mises à profit pour améliorer les performances de détection.  Pour cette structure, le problème de design se résume à déterminer les filtres $f[n]$ et $g[n]$. L'aspect non linéaire de ce type de récepteurs est dû à la présence de l'organe de décision dure dans la structure même de l'égaliseur.

### Optimisation de la structure DFE

Différentes structures ont été proposées dans la littérature pour les approches de type DFE. Nous présentons ici une approche assez classique afin d'illustrer les problématiques d'optimisation liées à ces structures. Pour cela, nous allons comme souvent (pour ne pas dire toujours) modéliser le signal à la réception en passant par une écriture matricielle des signaux. En suivant les notations de la figure {numref}`DFE`, on obtient le modèle suivant:  

 
$$r[n]=\mathbf{F}^{\top} \mathbf{Y}_n-\mathbf{G}^{\top} \hat{\mathbf{S}}_{n-d-1}=\mathbf{w}^{\top} \tilde{\mathbf{Y}}_n$$


où $\mathbf{F}=[f_0, \ldots, f_{N-1}]^{\top}$, $\mathbf{G}=[g_1, \ldots, g_{M-1}]^{\top}$, $\mathbf{Y}_n=[y[n], \ldots, y[n-N+1]]^{\top}$, $\hat{\mathbf{S}}_{n-d-1}=[\hat{s}[n-d-1], \ldots, \hat{s}[n-d-M+1]]^{\top}$ et enfin $\tilde{\mathbf{Y}}_n=[\mathbf{Y}_n^{\top}, - \hat{\mathbf{S}}_{n-d-1}^{\top}]^{\top}$.

Dans ce modèle $r[n]$ ne dépend évidemment que des symboles passés $\hat{s}(n-d-k)$. Le vecteur $\tilde{\mathbf{Y}}_n$ est quant à lui interprété comme un vecteur de symboles reçus augmenté des décisions qui viennent d'être prises sur une fenêtre de taille $M$.

On cherche maintenant à déterminer les filtres RIF $f_{opt}[n]$ et $g_{opt}[n]$ qui minimisent le critère MMSE. Cela revient donc à trouver les filtres optimaux $f_{opt}[n]$ et $g_{opt}[n]$  qui minimisent la fonction de coût 

$$J{(\mathbf{w})}=\mathbb{E}\left(|e[n]|^2\right), \; e[n]=s[n-d]-r[n].$$

Le problème d'optimisation initial revient donc au problème classique de Wiener consistant à optimiser le filtre $\mathbf{w}$ avec comme vecteur d'observations étendu $\tilde{Y}_n$. La solution est donc donnée par


$$\mathbf{R}_{\tilde{y}} \mathbf{w} = \Gamma_{s \tilde{y}}$$
  

avec   


$$\mathbf{R}_{\tilde{y}}=\mathbb{E}(\tilde{\mathbf{Y}}_n^{*}\tilde{\mathbf{Y}}_n^{\top}), \mathbf{\Gamma}_{s\tilde{y}}=\mathbb{E}(s[n-d]\tilde{\mathbf{Y}}_n^{*}).$$
  
Par rapport au cas linéaire, la difficulté vient du fait que $\tilde{\mathbf{Y}}_n$ dépend de $\hat{\mathbf{S}}_{n-d-1}$ dont on connaît difficilement les propriétés statistiques du fait de la non linéarité. Il est donc difficile d'avoir accès aux quantités $\mathbf{R}_{\tilde{y}}$ et $\mathbb{E}(s[n-d]\tilde{\mathbf{Y}}_n^{*}).$ Pour contourner cette difficulté, on fait alors comme hypothèse de travail que les symboles décidés sont \emph{toujours} corrects, ce qui est bien évidemment faux en pratique. Grâce à cette hypothèse, on a alors

$$\hat{\mathbf{S}}_{n-d-1}=\mathbf{S}_{n-d-1}$$

Dans ce cas, les quantités  $\mathbf{R}_{\tilde{y}}$ et $\mathbb{E}(s[n-d]\tilde{\mathbf{Y}}_n^{*})$ peuvent être calculer explicitement et on peut donc obtenir un système analytique matriciel à résoudre pour déterminer $f_{opt}[n]$ et $g_{opt}[n]$. Ces expressions sont données par

$$
\mathbf{f} _ { \mathrm { opt } } = \left( \left( \mathbf{H}^ {*} \mathbf{ H } ^ { \top }  - \mathbf{ \tilde{H} } \mathbf{ \tilde{H} } ^ { \dagger }\right) + \frac{\sigma _ {b } ^ { 2 }}{\sigma_s^2} \mathbf{I}_N  \right) ^ { - 1 } \mathbf{ H }^{*}\mathbf{1}_d
$$  

$$\mathbf{ b } _ { \mathrm { opt } } = \mathbf{ \tilde{H} } ^ { H } \mathbf{ f }_ { \mathrm { opt } }$$

où

$$\mathbf{ \tilde{H} }=\mathbf{{H} G}$$

et  $G$ est une matrice dont la première partie est nulle avec $d+1$ ligne et la dernière partie est une matrice identité de taille $M-1$ donnée par

$$G=\begin{pmatrix}
0 & \cdots & \cdots & 0 \\ 
\vdots&  &  & \vdots \\ 
0 & \cdots & \cdots & 0 \\ 
1 & 0& \cdots & 0 \\ 
0 & 1 &  & \vdots \\ 
\vdots &  & 1 & \vdots \\ 
0 & \cdots & 0 & 1
\end{pmatrix} $$

### Avantages et inconvénients 

- **Avantages :** Bon compromis complexité performances, bien meilleur que les égaliseurs linéaires, mais plus complexe;

- **Inconvénients :** phénomènes de propagation d'erreurs, erreurs arrivent donc en *burst*

