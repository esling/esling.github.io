---
layout: single
permalink: /react-project/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching"
---

<script language="JavaScript" type="text/javascript" src="https://code.jquery.com/jquery-latest.min.js"></script>
<script>
$(document).ready(function(){
    $(".abuttons").click(function () {
        var idname= $(this).data('divid');
        $("#"+idname).show("slow");
    });
    $("#div1").hide();
    $("#div2").hide();
    $("#div3").hide();
});
</script>

{% include toc %}

# Introduction

<div markdown = "1">

Cette page présente les projets tutorés 2019-2020 pour les leçons de [React Native](http://reactnative.dev/). Les deux sujets ciblent différentes notions vues en classe. Nous réintroduirons les mécanismes de base derrière chaque approche, ainsi que les concepts fondamentaux à comprendre, puis nous ciblerons une application spécifique de la programmation mobile.

## Instructions globales

Nous détaillons ici les instructions globales communes à tous les projets.
 - Groupes de **3 à 4 étudiants** par projet
 - **Répartition équilibrée** entre les deux sujets
 - Les projets sont **codés en React Native** (cf. section Style de codage ci-dessous)
 - Tous les projets doivent être accompagnés d'un petit rapport **en anglais**
 - Le rapport doit être de **8 pages maximum** suivant un format de _documentation développeur_
 - Les rapports doivent être rédigés en **LaTeX**
 - Les **contributions individuelles doivent être explicitées**

</div>{: .notice--blank}

## Evaluation

<div markdown = "1">

Tous les projets seront évalués de manière alternée avec une grille équivalente pour assurer l'équité entre les différents projets. Le projet doit être livré sous forme de 3 dossiers

`code /`: Devrait contenir votre code bien documenté (cf. section Style de codage) ainsi que des scripts simples qui démontrent l'utilisation des méthodologies développées. Nous vous recommandons d'organiser votre code en suivant les modules que vous devez définir dans l'architecture.

`report /`: Devrait contenir votre rapport au format PDF avec la source LaTeX. Celui-ci devra détailler la manière dont vous avez architecturé votre projet, les problèmes et solutions, ainsi que des screenshots d'utilisation.

`tests /`: devrait contenir un ensemble décrivant les tests, ainsi que la manière de les effectuer. Vous pouvez créer un autre document PDF décrivant l'ensemble de tests si vous en sentez le besoin, sinon détaillez-le dans votre rapport

Tous vos fichiers doivent être emballés dans un fichier zip se dépliant dans un dossier nommé
     \[React\]\[Projet2020\] (Nom de tous les élèves) .zip
La soumission peut également se faire sous forme d'un lien vers un repository sur GitHub.

**Date limite**: 25/12/2019 - 23h59
**Soumission**: esling [at] ircam (dot) fr
**Formatage**: courrier avec sujet: \[React\]\[Projet2020\] (Noms de tous les étudiants impliqués)

`Grille d'évaluation`: cette grille générique sera appliquée et les sous-grilles seront modulées pour chaque sujet.

**(6 pts) - Rapport** Noté à la fois sur le contenu et le style

**(6 pts) - Architecture, extensibilité** Qualité et exhaustivité de la modélisation, facilité à étendre l'application

**(8 pts) - Code** Exactitude, évaluation et style de codage


</div>{: .notice--blank}

## Code et style

<div markdown = "1">

Nous fournirons de petits codes de référence pour chaque projet si nécessaire. Ce code contiendra des fonctions d'assistance qui vous allégeront de la charge de l'importation de données et d'autres implémentations secondaires. Le code est en Python et s'appuie fortement sur le concept de «sections de code» qui vous permet d'évaluer seulement une partie du code (pour éviter d'exécuter plusieurs fois de longues tâches d'importation et de vous concentrer sur la question à résoudre).

Pour que le script de base fonctionne, vous devez avoir une distribution fonctionnelle de Python, ainsi que les bibliothèques suivantes [SciPy] (https://www.scipy.org/), [Music21] (http: // web .mit.edu / music21 /), [Librosa] (http://librosa.github.io/librosa/index.html), [Tensorflow] (https://www.tensorflow.org/), [Pytorch] ( http://pytorch.org/)
  
Nous vous recommandons fortement d'installer [Pip] (https://pypi.python.org/pypi/pip/) qui gérera l'installation automatique de ces bibliothèques Python (ainsi que leurs dépendances).

** Style de codage **
Nous imposons que votre code suive la recommandation de style de codage PEP8

[Style PEP8] (https://www.python.org/dev/peps/pep-0008/)

Chaque dossier représente un module, vous devez donc vous assurer de tout
liés à la définition du module.
 - Écrivez un fichier __init__.py
 - Vérifiez que la documentation à l'intérieur est valide
 - Documentez toujours toute nouvelle fonctionnalité
 - Implémenter des exemples dans un script basé sur root
    
** Documentation du code **
Tout le code doit être hautement documenté à tous les niveaux. Afin de faciliter une documentation commune, vous devez suivre la pratique du style de documentation Numpy, qui peut être trouvée ici

[Style de documentation Numpy] (http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_numpy.html)

** Tests unitaires **
Les tests unitaires sont facultatifs pour le projet mais fortement recommandés (et pour vos futurs projets en tout cas). Chaque fois que vous ajoutez une nouvelle fonctionnalité «indépendante» à la boîte à outils, vous devez développer un ensemble de tests unitaires afin de vous assurer que toutes les fonctions fonctionnent correctement et également que les modifications futures n'entraveront pas le développement précédent.
Si vous ne connaissez pas le principe du test unitaire, vous pouvez lire

</div>{: .notice--blank}

# Subjects 

<div markdown = "1">

Nous détaillons ici les différents sujets qui sont sous formes PDF, et dont le résumé est disponible par la suite. 

**[![](../images/pdf.png) Caillon / Bazin - Realtime instrument interpolation using Differentiable Digital Signal Processing](../documents/mlProj_2019_Caillon.pdf)**

**[![](../images/pdf.png) Carsault - Introduction of musical distances for multi-step inference of jazz chord progressions](../documents/mlProj_2019_Carsault.pdf)**

**[![](../images/pdf.png) Douwes / Chemla - Granular synthesis using variational learning](../documents/mlProj_chemla.pdf)**

**[![](../images/pdf.png) Prang - Multimodal embedding music for automatic piece recognition spaces](../documents/mlProj_2019_Douwes.pdf)**

## Caillon / Bazin

**Realtime instrument interpolation using Differentiable Digital Signal Processing**

**Abstract**
Most generative models of audio directly generate samples in one of two domains: time or frequency. While sufficient to express any signal, these representations are inefficient, as they do not utilize ex- isting knowledge of how sound is generated and perceived. A third approach (vocoders/synthesizers) successfully incorporates strong domain knowledge of signal processing and perception, but has been less actively researched due to limited expressivity and difficulty integrating with modern auto differen- tiation based machine learning methods. The use and potential of such approaches are to be evaluated during this Machine Learning project

**[![](../images/pdf.png) Full project](../documents/mlProj_2019_Caillon.pdf)**

## Carsault

**Introduction of musical distances for multi-step inference of jazz chord progressions**

**Abstract**
This project aims to predict chord progressions of jazz music, represented as coherent chord label sequences with the help of probabilistic models. In this study, we propose to use different neural network models to generate symbolic chord sequences. Besides, we study the impact of the introduction of different musical distances through the loss function during the training of our models. Thus, we want to improve existing methods by doing multi-step prediction and by injecting music theory knowledge through the learning method in order to be able to perform accurate prediction of chord sequence and jazz melody generation. Ultimately, this project could be used to perform automatic accompaniment and improvisation.

**[![](../images/pdf.png) Full project](../documents/mlProj_2019_Carsault.pdf)**

## Douwes / Chemla

**Granular synthesis using variational learning**

**Abstract**
Generative systems are machine-learning models whose training is based on two simultaneous optimization tasks. The first is to build a latent space, that provides a low-dimensional representation of the data, eventually subject to various regularizations and constraints. The second is the reconstruction of the original data through the sampling of this latent space. These systems are very promising because their space is a high-level, ”over-compressed” representation that can be used as an inter- mediate space for several tasks, such as visualization, measurements, or classification. The main goal of this project is to use variational models for raw audio in order to create a granular synthesizer based on latent sampling.

**[![](../images/pdf.png) Full project](../documents/mlProj_2019_Douwes.pdf)**

## Prang

**Multimodal embedding music for automatic piece recognition spaces**

**Abstract**
This project aims to develop new representations for symbolic and audio music. You will try to implement the work done by Dorfer et al. [2018] and published in ISMIR 2018. Your goal is to represent musical symbols and the corresponding short excerpts of audio in the same space called multimodal embedding space. This approach allows to address the problem of matching musical audio directly to musical symbols. Moreover, theses kind of spaces could be very powerful tools for the orchestration field. By disentangling the correlation between the orchestral score and the audio signal result, we can provide efficient systems for analyze and generate specific orchestral effects. You will use Convolutional Neural Networks in order to capture features of the both modalities and represent them with vectors of the same dimension. First, you will have to prepare your dataset by synthesizing and aligning corresponding audio from MIDI files. Then, you will implement the model proposed by Dorfer et al which is composed by two networks and train it on your synthesized dataset. Once your model will be efficient on the training data, you will test it on real data through two tasks: (1) piece/score identification from audio queries and (2) retrieving relevant performances given a score as a search query. Finally, you will propose (or even implement) improvements in the architecture or the training of the model.

**[![](../images/pdf.png) Full project](../documents/mlProj_Prang.pdf)**

</div>{: .notice--blank}
