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

**Date limite**: 30/06/2020 - 23h59

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

Le code est en React Native, langage qui s'appuie fortement sur le concept de ré-évaluation temps réelle qui vous permet de mettre à jour l'application de manière dynamique au fur et à mesure de l'implémentation (pour éviter d'exécuter plusieurs fois de longues tâches d'importation et de vous concentrer sur la question à résoudre). Il est donc **fortement conseillé** de bien réfléchir à la manière dont vous comptez vous répartir les tâches. Réfléchissez notamment au découpage du projet, ainsi que la manière dont vous partagerez l'état du code source à tout moment.


Nous vous recommandons fortement d'installer [Expo](https://expo.io/) et [Yarn](https://yarnpkg.com/) qui permettent de simplifier la gestion des bibliothèques React (ainsi que leurs dépendances). Nous recommandons également de mettre en place dès le début une architecture de travail partagé (Git) et modulaire, permettant au groupe d'avancer de manière solide.

</div>{: .notice--blank}

### Style de codage

<div markdown = "1">

Nous imposons que votre code suive un certain nombre de standards permettant de s'assurer que différents aspects de l'application soient sûrs et maintenable.

1. Utilisation de [prop-types](https://github.com/facebook/prop-types) (comme vu en cours), pour permettre de forcer des contraintes de types sur vos props
2. Ecrire des commentaires au format [Doxygen](http://www.doxygen.nl/manual/starting.html) pour permettre par la suite d'utiliser [react-docgen](https://github.com/reactjs/react-docgen) pour générer automatiquement une documentation.
3. Définition d'une syntaxe commune (même simpliste) grâce à l'utilisation de [ESLint](https://eslint.org/)
4. Utilisation d'un schéma d'architecture objet (type UML) pensé à l'avance
5. Modules et dossiers séparés pour augmenter la lisibilité du code
6. Suivez une norme de code commune, par exemple la norme de [AirBnB](https://airbnb.io/javascript/react/) ou [Pagarme](https://github.com/pagarme/react-style-guide).


**Documentation du code**
Tout le code doit être hautement documenté à tous les niveaux. Afin de faciliter une documentation commune, vous devez suivre la pratique du style de documentation Doxygen, qui peut être trouvée [ici](http://www.doxygen.nl/manual/starting.html)

**Tests unitaires**
Les tests unitaires sont facultatifs pour le projet mais fortement recommandés (et pour vos futurs projets en tout cas). Chaque fois que vous ajoutez une nouvelle fonctionnalité «indépendante» à la boîte à outils, vous devez développer un ensemble de tests unitaires afin de vous assurer que toutes les fonctions marchent correctement et également que les modifications futures n'entraveront pas le développement précédent.
Si vous ne connaissez pas le principe du test unitaire, vous pouvez apprendre [Jest](https://jestjs.io/docs/en/tutorial-react-native)

</div>{: .notice--blank}

# Sujets 

<div markdown = "1">

Nous détaillons ici les différents sujets dont le résumé est disponible par la suite. Notez que les sujets sont **volontairement simplifiés**, car le but de ce projet est également d'évaluer votre _capacité à choisir intelligemment la structure et l'architecture_ d'une application mobile complexe. Les sujets définissent donc les grandes lignes du comportement et des fonctionnalités attendues, et vous laissons toute liberté sur les choix d'architecture et d'interface utilisateur.

</div>{: .notice--blank}

## Optimisateur de vie

<div markdown = "1">

Ces dernières années, de nombreuses applications permettant de gérer sa vie et d'améliorer sa productivité ont vues le jour. Cependant, peu d'applications permettent d'automatiser l'organisation des tâches régulières (lessive, lecture) de manière optimale. On se propose d'écrire une application qui trouvera pour nous un emploi du temps nous permettant de réaliser toutes les tâches qu'on se fixe pour chaque semaine.

***Partie 1 - Gestion de vie***

Nous allons dans un premier temps définir l'ensemble des tâches que nous devons gérer lors d'une semaine, ainsi le programme permettra de
1. Définir une liste de tâches "datées" (cours, rendez-vous)
2. Définir une liste de tâches "récurrentes" (lessive, lecture, etc...)
3. Modifier toutes les propriétés de chaque tâche
4. Personnaliser les tâches

Pour simplifier l'utilisation de l'application, nous voulons également qu'elle soit capable de
1. Récupérer des évènements dans d'autres calendriers (Google Calendar)
2. S'abonner à un flux d'évènements (RSS)
3. Importer des évènements iCal

***Partie 2 - Automatisation de calendrier***

Le coeur de l'application est de trouver la manière optimale d'organiser tous les évènements de notre semaine. Ici nous allons permettre de définir un algorithme simplissime d'organisation
1. L'utilisateur définit des propriétés (heure de réveil, heure de repas, ...)
2. L'algorithme place les évènements "datés" en premier
3. On calcule l'ensemble des "places restantes" (temps disponible entre tâches obligatoires)
4. L'algorithme range les jours aléatoirement
5. On place les tâches une à une en partant des plus longues vers les plus courtes

L'interface finale nous permettra de
1. Afficher le calendrier résultant
2. Modifier et sauver les résultats de l'algorithme

Pour permettre d'intégrer les résultats de notre application de manière plus forte avec les utilisateurs, nous voulons ajouter le lien avec les apps les plus utilisées (Google calendar, Calendrier MacOS). Pour cela l'application devra
1. Exporter des objets de type iCal
2. Interagir avec _Google Calendar_ (et autres au choix)
3. Editer les propriétés d'export

</div>{: .notice--blank}

## Bot Twitter

<div markdown = "1">

Le réseau social _Twitter_ propose une [API publique](https://developer.twitter.com/en), permettant de publier et analyser les tweets, ouvrant la possibilité de programmer un _bot_ (système de publication ou réponse automatique). 

Un _bot rudimentaire_ peut permettre de tweeter régulièrement de manière programmatique, ou inversement de répondre à des tweets. Un exemple de service permettant de mettre en place en bot sans aucune connaissance en programmation est [Cheap Bots Done Quick](http://cheapbotsdonequick.com/). Nous allons dans ce projet écrire une application permettant d'effectuer des analyses sur Twitter, et de mettre en place des bots très simples.

***Partie 1 - Utilisation de l'API Twitter***

Nous voulons avoir une première partie de l'application qui permet d'utiliser l'API Twitter d'un point de vue analytique. Il faudra donc utiliser l'API [Search](https://developer.twitter.com/en/docs/tweets/search/overview). Dans cette première partie, nous voulons pouvoir récupérer des méta-données et effectuer des analyses
1. Récupérer une liste d'utilisateurs
2. Récupérer les tweets d'un utilisateur particulier
3. Effectuer des recherches dans les tweets
4. Calculer des statistiques sur les tweets

***Partie 2 - Cheap bot***

Nous voulons une deuxième partie dans l'application permettant de mettre en place un bot simpliste. Celui-ci pourra être d'un des deux types (choisi par l'utilisateur) 
1. Répondeur automatique
2. Posteur automatique

Dans le cas du répondeur automatique, les comportements attendus sont
1. Définir une liste de messages automatiques
2. Choisir des propriétés de réponse
3. Répondre à des mentions faites au bot (type @xxxx)
4. Répondre aux messages d'un utilisateur

Dans le cas du posteur automatique, le bot permettra d'envoyer des messages définis par règles. On attend donc de pouvoir
1. Définir des règles sur les envois (message de base, combinaison des mots, ...)
2. Choisir les propriétés de l'envoi (heure, fréquence, etc ...)

</div>{: .notice--blank}
