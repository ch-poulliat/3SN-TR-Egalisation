## Notations 
not_numbered: true

On adoptera dans la suite les notations suivantes:

- ***Transformée de Fourier Discrète, TFD :***

$$ X[k]=TFD(x[n])= \sum_{n=0}^{N-1}{x[n] e^{-i\frac{2 \pi}{N}k n}}, \; \forall k=1:N-1$$

- ***Transformée de Fourier Discrète Inverse, TFD inverse} :***

$$x[n]= TFD^{-1}(x[n])= \frac{1}{N} \sum_{k=0}^{N-1}{X[k] e^{+i\frac{2 \pi}{N}n k}}, \; \forall k=1:N-1$$

- ***Convolution circulaire :***

    - TD : Domaine temporel:

    $$\begin{align}    
    y[n] \triangleq & h[n] \circledast x[n]\notag \\
    =&\sum_{m=0}^{N-1}{x[m]h[<n-m>_{N}]} , \; \forall n=0:N-1 
    \end{align}$$
    
    - FD : Domaine fréquentiel :
    
    $$Y[k]=  H[k]X[k], \; \forall k=0:N-1$$
