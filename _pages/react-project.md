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
     
`[React][Projet2020] (Nom de tous les élèves) .zip`
     
La soumission peut également se faire sous forme d'un lien vers un repository sur GitHub.

**Date limite**: 25/12/2019 - 23h59

**Soumission**: esling [at] ircam (dot) fr

**Formatage**: courrier avec sujet: \[React\]\[Projet2020\] (Noms de tous les étudiants impliqués)

### Grille d'évaluation
Cette grille générique sera appliquée et les sous-grilles seront modulées pour chaque sujet.

**(6 pts) - Rapport** Noté à la fois sur le contenu et le style

**(6 pts) - Architecture, extensibilité** Qualité et exhaustivité de la modélisation, facilité à étendre l'application

**(8 pts) - Code** Exactitude, évaluation et style de codage


</div>{: .notice--blank}

## Code et style

<div markdown = "1">

Le code est en React Native et s'appuie fortement sur le concept de ré-évaluation temps réelle qui vous permet de mettre à jour l'application de manière dynamique au fur et à mesure de l'implémentation (pour éviter d'exécuter plusieurs fois de longues tâches d'importation et de vous concentrer sur la question à résoudre). Il est donc **fortement conseillé** de bien réfléchir à la manière dont vous comptez vous répartir les tâches. Réfléchissez notamment au découpage du projet, ainsi que la manière dont vous partagerez l'état du code source à tout moment.
  
Nous vous recommandons fortement d'installer [Expo](https://expo.io/) et [Yarn](https://yarnpkg.com/) qui permettent de simplifier la gestion des bibliothèques React (ainsi que leurs dépendances).

** Style de codage **
Nous imposons que votre code suive un certain nombre de standards permettant de s'assurer que différents aspects de l'application soit sûrs et maintenable.

1. Utilisation de [prop-types](https://github.com/facebook/prop-types) (comme vu en cours), pour permettre de forcer des contraintes de types sur vos props
2. Ecrire des commentaires au format [Doxygen]() pour permettre par la suite d'utiliser [react-docgen](https://github.com/reactjs/react-docgen) pour générer automatiquement une documentation.
3. 

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

# Sujets 

<div markdown = "1">

Nous détaillons ici les différents sujets dont le résumé est disponible par la suite. Notez que les sujets sont **volontairement simplifiés**, car le but de ce projet est également d'évaluer votre _capacité à choisir intelligemment la structure et l'aarchitecture_ d'une application mobile complexe

</div>{: .notice--blank}

## Optimisateur de vie

<div markdown = "1">

</div>{: .notice--blank}

## Bot Twitter

<div markdown = "1">

</div>{: .notice--blank}
