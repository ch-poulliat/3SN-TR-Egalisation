## OFDM, un exemple de forme d'onde circulaire

### Modélisation récepteur - domaine temporel

Soit un bloc de $N$ symboles modulés noté $X[k] \in \mathcal{X} \subset \mathbb{C}, \forall k=0 \cdots N-1$. Après passage par le bloc de TFD inverse, on obtient un bloc de symboles 

$$x[n]=TFD^{-1}(X[k]), \forall n=0 \cdots N-1.$$

Après ajout d'un préfixe cyclique, on obtient le vecteur 

$${\bf \tilde{x}}=[\tilde{x}[0] \tilde{x}[1] \cdots \tilde{x}[N+N_{cp}-1]]=[x[N-N_{cp}] \cdots  x[N-1]|x[0] \cdots  x[N-1]].$$

Après transmission sur le canal sélectif en fréquence de réponse impulsionnelle $h[n]$, on a

$$y[n]=h[n] * \tilde{x}[n]+ b[n].$$

Après retrait du CP, on retrouve bien la convolution circulaire des données avec le canal donnée par

$$y[n]=h[n] \circledast x[n]+ b[n].$$

On supposera $b[n]$ comme un processus Gaussien complexe ciculaire de variance $\sigma^2_b$

### Modélisation récepteur - domaine fréquentiel

La transformée de Fourier discrète transformant tout produit de convolution circulaire en produit terme à terme des TFD, on a $\forall k=0 \cdots N-1$

$$Y[k]=TFD(y[n])= H[k]X[k]+B[k]$$

où $H[k]=TFD(h[n])$ et $B[k]=TFD(b[n])$.Par propriétés de la transformée de Fourier, le bruit est toujours blanc Gaussien, mais $B[k]$ sont des échantillons de bruit complexes toujours centrés et variance $\sigma^2_B=N \sigma^2_b$ ($\sigma^2_B/2$ par dimension). On voit donc que l'on a "transformé" un canal sélectif en fréquence en canal sélectif en temps/à évanouissements temporels. On a donc translaté le problème de détection du domaine fréquentiel au domaine temporel. 

### Aspects récepteurs

Pour les systèmes OFDM, il est souvent présenté une "égalisation" des canaux avant décision. On "filtre" les données par un filtre "one-tap" (mono-coefficient) $W[k]$ chaque sous canaux (ie; $\forall k=1 \cdots N-1$). On obtient alors un symbole estimé donné par

$$\hat{X}[k]=W[k]Y[k]=W[k]H[k]X[k]+W[k]B[k]=\alpha_k X[k]+B[k]$$

Deux types de critère peuvent alors s'appliquer comme dans le cas temporelle, le critère ZF et MMSE. Les égaliseurs résultants sont alors données par

1.  **Critère Zero-forcing :**

$$W[k]=\frac{1}{H[k]}$$

2. **Critère MMSE :**

$$W[k]=\frac{\sigma_X^2H^*[k]}{\sigma_X^2|H[k]|^2+\sigma_B^2}$$

Cependant, si on réfléchit bien au modèle discret équivalent obtenu après DFT/FFT au récepteur, le modèle étant un modèle à évanouissements scalaires, cette étape n'est pas "nécessaire" si on considère un système OFDM codé. On peut appliquer les règles de détection classique pour un canal sans mémoire scalaire. La première stratégie de détection qui mène à une décision dure des symboles est donnée par le critère de détection par maximum de vraisemblance. En utilisant le modèle discret équivalent il vient directement 

$$\hat{X}[k]=\underset {X \in \mathcal{X}}{\operatorname {arg\,max} } \, P(Y[k]|X[k],H[k]),$$

où, dans le cas Gaussien, on a 

$$P(Y[k]|X[k],H[k]) \propto exp(-\frac{||Y[k]-H[k]X[k]||^2}{\sigma_B^2})$$

Si on souhaite avoir une une information souple au niveau du bit, nous verrons en 3A que l'on peut également appliquer une détection MAP bit pour un schéma codé à bits entrelacés. Si on note les vecteurs binaires $X_b[n]=[X_1[n] \cdots X_m[n]]$ les étiquettes qui servent à "mapper" les bits d'information sur les symboles $X[n] \in \mathcal{X}$, alors on peut définir une quantité appellée LLR (log-likelihood ratio), qui représente une information de type MAP associée au bit à la position $i$ de l'étiquette $X_b[n].$ Pour des symboles équidistribués, cette quantité est donnée par

$$
\begin{aligned}
 L(x_i[n])&=\log{\left(\frac{P(x_i[n]=0|Y[n])}{P(x_i[n]=1|Y[n])}\right)}\\
 & = \log{\left( \frac{\sum_{X[n] \in \mathcal{X}_0^i}{P(Y[n]|X[n],H[n])}}{\sum_{X[n] \in \mathcal{X}_1^i}{P(Y[n]|H[n],X[n])}} \right)}
\end{aligned}
$$ 

où $\mathcal{X}_0^i$ (resp. $\mathcal{X}_1^i$) représente le sous ensemble des symboles de $\mathcal{X}$ ayant une étiquette/un label avec $x_i=0$ (resp. $x_i=1$).