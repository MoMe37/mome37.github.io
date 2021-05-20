---
layout: page
title: Techniques de survie
image: assets/images/pic01.jpg
nav-menu: true
usemathjax: true 
---

# Prise en main 

J'espère que le chapitre précédent, conceptuel et idéologique, t'a donné envie d'en savoir plus et de devenir le prochain Kaggle GrandMaster, parce qu'il est maintenant temps de se retrousser les manches et de mettre les mains directement dans le code. Tu trouveras sur cette page des ressources pour te mettre rapidement à niveau sur des techniques incontournables en ML/AI/DL et pouvoir comprendre les stratégies des projets AInimals et AlphSistant. 


### Python / Numpy 

Dans les NN, la majeure partie des calculs est relativement simple puisqu'il s'agit essentiellement d'additions et de multiplications. La particularité du domaine est que ces opérations sont appliquées à des matrices et qu'on parle donc d'algèbre linéaire. En pratique, d'un point de vue programmation on s'appuie **beaucoup** sur Numpy, une librairie python qui manipule des *arrays* (aka des tableaux). Vu que c'est un peu la base et l'inspiration de beaucoup de libraires de deep learning, il est crucial que tu comprennes le fonctionnement global de ces calculs. Si ce n'est pas déjà le cas, voilà un tutorial totalement inéluctable, qui aborde notamment Jupyter et Colab, des outils de scripting super pratique (Colab se passe directement dans le navigateur, pas besoin d'installer quoi que ce soit) :

* [Python Stanford](https://cs231n.github.io/python-numpy-tutorial/)

 
### Pandas

Tu as probablement déjà entendu dire que l'intelligence artificielle nécessitait des données pour fonctionner. C'est vrai, mais sur le terrain, elle a surtout besoin de pandas, une autre librairie python, qui permet de faire du kung-fu avec des CSV, d'extraire les secrets et les tendances des databases, de deviner les schémas de génération sous-jacents et de trouver les caractéristiques les plus importantes pour entrainer les modèles. Les liens suivant devraient te mettre à niveau rapidement (à faire dans l'ordre): 
* [Pandas niveau 0](https://www.kaggle.com/learn/pandas)
* [Niveau 1](https://www.kaggle.com/learn/intro-to-machine-learning)
* [Niveau 1.5](https://www.kaggle.com/learn/intermediate-machine-learning)


### Visualisation 

Un data-scientist qui ne sait pas visualiser ses données n'a de scientist que le nom (?). C'est effectivement incontournable, puisque ça permet notamment de: 

* Vérifier la cohérence des résultats 
* S'assurer de la forme des distributions des variables 
* Comparer des modèles
* Corrélation des variables

[Hop, un petit tuto pour devenir un master en seaborn et matplotlib](https://www.kaggle.com/learn/data-visualization)


### Conclusion

Après ces introductions, you're getting closer to the real sh!t that this website is all about. Next up: 
* Présentation des projets (pour digérer)
* Deep learning: Pytorch & Convolutional Neural Networks (CNN)
* Les stratégies spécifiques des projets 