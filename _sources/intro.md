# Méthodes d'égalisation temporelles et fréquentielles

```{admonition} En bref

- **Nombre d'heures :** 7 Cours-TD, 2 TPs de 4 h.
- **Langue d'enseignement : Français**
- **Code :** N7EN02B
```


## Objectifs
L'objectif de ce cours est d'aborder les problématiques de détection et d'estimation dans le cadre de canaux sélectifs en fréquence. On s'intéressera en particulier aux méthodes dîtes d'égalisation linéaires et non-linéaires avec une instanciation dans le domaine temporel ou fréquentiel pour les communications mono-porteuses. Le lien sera fait avec le cours d'OFDM pour les communications multi-porteuses.

 

## Description
Cet enseignement présente les problématiques de détection et d'estimation pour des communications sur canaux sélectif en fréquence. Les points suivants seront abordés:

- ***Modélisation des canaux sélectifs en fréquence :*** modèles de canaux discrets équivalents;

- ***Egalisation linéaire temporelle :*** critère ZF et MMSE pour filtre RII non contraint et RIF; dimensionnement;

- ***Egalisation non linéaire temporelle :*** détection au sens du maximum de vraisemblance (notion de treillis, Algorithme de Viterbi); détection non linéaire à base de filtres ou par bloc (DFE);

- ***Egalisation linéaire dans le domaine fréquentiel :*** forme d'onde mono-porteuse circulaire par bloc; Egalisation fréquentielle (ZF,MMSE); mise en forme par filtrage "fréquentiel" (SC-OFDM/DFT precoded OFDM, EW-SC-OFDM); 

## Prérequis
````{grid} 2
```{grid-item-card} 
:link: https://ch-poulliat.github.io/Cours-TS-SN1A-N7
:text-align: center 
:shadow: md 
:class-header: bg-light center

**Traitement du Signal 1A SN**
^^^

Il est important de maîtriser les outils de Traitement du Signal.


```
```{grid-item-card} 
:link: https://moodle-n7.inp-toulouse.fr/course/view.php?id=2014
:text-align: center 
:shadow: md 
:class-header: bg-light center

**Télécommunications 1A SN**
^^^

Le présent cours est un complément au cours de Télécommunications de 1A-SN qui abordait les communications numériques monoporteuses sur canal gaussien.


```
````

## Ressources

#### Polycopiés

````{grid} 2
```{grid-item-card} 
:text-align: center 
:shadow: md 
:class-header: bg-light center

**Polycopié**
^^^

Une version en cours du polycopié.

+++

{download}`Polycopié (en cours de consolidation)<./downloads/PolyEgal.pdf>`

```
```{grid-item-card} 
:link: ch1intro
:link-type: doc
:text-align: center 
:shadow: md 
:class-header: bg-light

**Cours en ligne**
^^^

Le cours en ligne, version augmentée du polycopié avec les exercices et les notebooks associés.
```
````
#### Diapositives

````{card-carousel} 3
```{card} 
:text-align: center 
:shadow: md 
:class-header: bg-light center

**Modélisation du Canal à ISI**
^^^

Diapositives  sur la construction du canal discret équivalent

+++

{download}`Diapositives <./downloads/2SN_Egal_Channel.pdf>`

```
```{card} 
:text-align: center 
:shadow: md 
:class-header: bg-light center

**Egalisation linéaire temporelle**
^^^

Diapositives sur l'égalisation linéaire en temporel.

+++

{download}`Diapositives <./downloads/2SN_Egal_Lin.pdf>`

```

```{card} 
:text-align: center 
:shadow: md 
:class-header: bg-light center

**Egalisation non linéaire pra maximum de vraisemblance**
^^^

Diapositives sur l'égalisation par maximum de vraisemblance.

+++

{download}`Diapositives <./downloads/2SN_Egal_NL_ML.pdf>`
```

```{card} 
:text-align: center 
:shadow: md 
:class-header: bg-light center

**Egalisation non linéaire à base de filtres**
^^^

Diapositives sur l'égalisation de type DFE.

+++

{download}`Diapositives <./downloads/2SN_Egal_NL_DFE.pdf>`
```
```{card} 
:text-align: center 
:shadow: md 
:class-header: bg-light center

**Egalisation dans le domaine fréquentielle**
^^^

Diapositives sur l'égalisation appliquée dans le domaine fréquentiel.

+++

{download}`Diapositives <./downloads/2SN_Egal_Freq.pdf>`
```
````
## Travaux pratiques
Les séances de travaux pratiques sont dédiées à l'implémentation des algorithmes et modèles vus dans le cours.

````{grid} 2
```{grid-item-card} 
:text-align: center 
:shadow: md 
:class-header: bg-light center

**TP1 : Egalisation dans le domaine temporel**
^^^

Une première séance dédiée à l'implémenatation des égaliseurs dans le domaine temporel.

+++

{download}`Sujet et fichiers Séance 1<./downloads/Sujet et fichiers TP1.zip>`

```
```{grid-item-card} 
:text-align: center 
:shadow: md 
:class-header: bg-light

**TP2 : Egalisation dans le domaine fréquentiel**
^^^

Une deuxième séance dédiée à l'implémenatation des égaliseurs dans le domaine fréquentiel.
+++

{download}`Sujet et fichiers Séance 2<./downloads/Sujet et fichiers TP2.zip>`

```
````

## Compétences visées

- Comprendre les fondements des techniques de détections et estimations pour des transmissions sur canaux sélectifs en fréquence;

- Être capable de modéliser le modèle discret équivalent bande de base d'une chaîne de communication numérique pour un canal dispersif en fréquence;

- Connaître les principales méthodes pour la détection et l'égalisation;

- Savoir mettre en oeuvre une technique de détection et/ou d'égalisation pour chacun des contextes présenter;

- Savoir dimensionner les paramètres des différentes méthodes pour gérer le compromis performance/complexité. 

## Cours en ligne

Le cours est accompagné d'un cours en ligne qui revient en détails sur les notions et démonstrations des expressions vues en cours. 
Le plan suit la structure suivante :

````{admonition} Plan du cours en ligne

```{tableofcontents}
```

````