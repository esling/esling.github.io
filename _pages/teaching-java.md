---
layout: single
permalink: /teaching-java/
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

# Programmation Java, Androïd et Web réactif.

## Descriptif de l'UE

<div markdown = "1">

Cette unité d’enseignement permet aux étudiants d’appréhender le langage Java qui est maintenant au coeur de l’informatique professionnelle. Devenu le language de référence pour le traitement multimédia, web client et serveur ainsi que des systèmes d’informations, celui-ci s’appuie sur une simplicité de syntaxe et une flexibilité issue de la programmation objet. L’unité permettra ainsi aux étudiants de partir des bases du langage Java puis à travers une formation rapide, leur permettre de développer leurs propres applications et interfaces jusqu’à l’intégration au développement d’applications plus ambitieuses dans le cadre d’un projet d’envergure. Après avoir appris les aspects essentiels de la programmation objets, l’unité se développera autour de mécanismes permettant d'accélérer les temps de développement de façon tangible et d'aborder des notions plus complexes : mécanismes d'exceptions, threads, réseau. Les étudiants iront par la suite jusqu’au développement d’une application sur des plateformes mobiles (telles que Androïd ou iPhone), de jeux vidéos (grâce à la librairie OpenGL pour Java) et pour le web réactif (à travers l’apprentissage des servlets). A noter que l’unité se termine par la réalisation d’un projet sur plusieurs mois qui appartiendra aux étudiants en fin d’année (leurs permettant ainsi de les rendre disponibles sur les stores d’applications des différentes plateformes).

</div>{: .notice--blank}

## Ressources générales 

<div markdown = "1">

- [Tutorial Git](https://try.github.io/levels/1/challenges/1)
- [Cours programmation / Java débutant](https://openclassrooms.com/courses/apprenez-a-programmer-en-java) (partie 1 principalement)
- [Tutoriels Java](https://www.ukonline.be/programmation/java/tutoriel/principal.php)
- Livres sur le développement logiciel :
- Gang of Four, Design Patterns: Elements of Reusable Object-Oriented Software.
- Andrew Hunt and David Thomas, The Pragmatic Programmer: From Journeyman to Master.
- Frederick Brooks, The Mythical Man-Month: Essays on Software Engineering.
- Robert C. Martin, Agile Software Development, Principles, Patterns, and Practices.
- Sites / Blogs :
- Forum d'entraide informatique [developpez.com](http://www.developpez.com/)
- [Stack Overflow](http://stackoverflow.com/)
- [Emmanuel Deloget, Architecture Orientée Objet](http://blog.emmanueldeloget.com/index.php?category/Ood)
- [Raccourcis clavier Netbeans](https://netbeans.org/project_downloads/usersguide/shortcuts-80.pdf)
- [Raccourcis clavier Eclipse](http://www.n0sl33p.org/dev/eclipse_keys.html)
- Livres sur l'écosystème Java :
- Maven: The complete reference et Maven by Example
- Appel Frank, Testing with JUnit
- Langr Jeff and Hunt Andrew and Thomas David, Pragmatic unit testing in Java 8 with JUnit
- Livres sur le développement WEB/Servlet :
- B. Basham, K. Sierra, and B. Bates, Head First Servlets and JSP. Sebastopol, Calif.; Farnham: O’Reilly, 2003.

</div>{: .notice--blank}

## Cours et exercices

<div markdown = "1">

- Semaine 1 : [Slides ![](../images/pdf.png)](../documents/cours1.pdf) - Exercice 
- Semaine 2 : [Slides ![](../images/pdf.png)](../documents/cours2.pdf) - Exercice 
- Semaine 3 : [Slides ![](../images/pdf.png)](../documents/cours3.pdf) - Exercice 
- Semaine 4 : [Slides ![](../images/pdf.png)](../documents/cours4.pdf) - Exercice
- [Sujet Pokedeck ![](../images/pdf.png)](../documents/Java_Pokedeck.pdf)
- Semaine 5 : Slides - Exercice 
- Semaine 6 : Slides - Exercice 
- Semaine 7 : Slides - Exercice
- Semaine 8 : Slides - Exercice 
- Semaine 9 : Slides - Exercice 
- Semaine 10 : Slides - Exercice 

</div>{: .notice--blank}


## Responsables pédagogiques

Philippe Esling (philippe.esling@ircam.fr)

## Modalités de contrôle des Connaissances

<div markdown = "1">

* Contrôle continu    : Pour chaque séance de cours (3h), les étudiants développeront une application pratique des connaissances proposées qui mènera ainsi à un ensemble de mini-projet. Chaque mini-projet devra être rendu avant le début de la séance suivante, permettant ainsi de développer ses capacités de programmation.
* Projet            : Dès le début du semestre, un projet devra être défini par groupes d’étudiants. Des sujets seront proposés par l’équipe pédagogique, mais l’étudiant reste entièrement libre de proposer son propre projet, les enseignants pouvant en modifier les modalités pour harmoniser la difficulté entre les différents groupes.

</div>{: .notice--blank}

## Programme par semaine

### 1er semestre

<div markdown = "1">

- __Présentation de l’UE et fondamentaux.__ 

De la programmation impérative à l’OO. Kernel impératif de Java : types primitifs, opérateurs arithmétiques/logiques, structures de contrôles. Kernel de base d’une couche objet : constructeurs, attributs, méthodes. Notion d’encapsulation, visibilité (public + private). Passage de paramètre par référence. 

** Mini-Projet : Bataille de carte (console) **

- __Énumération, héritage et polymorphisme.__ 

Retour sur la bataille de carte : Utilisation d’une énumération. Modèle mémoire (brève description du garbage collector – 1 ou 2 slides). Héritage avec les interfaces et classes abstraites, différences entre les deux. Visibilté protected. Overriding. Utilisation des interfaces/classes abstraites dans la librairie standard (exemple avec les ArrayList). 

** Mini-Projet : lecteur de fichiers complexe factorisé**

- __Règles des surcharges et surdéfinition.__ 

Overloading et overriding, les règles des surcharges. 

** Mini-Projet : types de données complexes et jeux (cartes pokémon)**

- __Gestion des erreurs et architecture d’un projet__ 

Gestion des erreurs (code de retour “à la C”, null, Optional<T>, exceptions), test unitaires (TDD). Retour sur le lecteur de fichier avec une gestion des erreurs réfléchie et tests. Diagramme de classe UML. Structure d’un projet (repertoires). 

** Mini-projet : Pokedeck **

- __Interfaces Homme/Machine__ 

Éléments de Communication Homme-Machine et création d’interfaces graphiques. 

** Mini-Projet : Pokedeck **

- __Design patterns I__ 

Introduction aux patterns avec le singleton. Retour sur les IHM avec observers. Mêler plusieurs design patterns : factory + observers. Quand utiliser un design pattern ? 

** Mini-Projet : Refactoring du projet sur les graphes en utilisant ces concepts. Implémentation d’un labyrinthe.**

- __Design patterns II__ 

Design patterns strategy, decorator, visitor. Architecture MVC. Aperçu des différents patterns et overengineering. 

**Séance projet 1**

- __Séance question/réponse et retour sur les projets__ 

Erreurs fréquemment commises sur les projets, ré-explication des notions mal comprises. Réponses aux questions des étudiants, notamment sur le design ou les patterns. 

** Mini-projet : module dans un application existante.**

</div>{: .notice--blank}

### 2ème semestre 

<div markdown = "1">

- __Modèles de programmation réseau et répartie.__

Threads, exécution parallèle. Modèle client/serveur.

** Mini-projet : Serveur de chat.**

- __Programmation web.__ 

Problématique du web (beaucoup de technologies/langages à maitriser). Solution partielle en Java à base de servlets, Awt, JSP, programmation réactive. 

** Mini-projet : servlet réactif.**

- __Programmation graphique__ 

Introduction à OpenGL 

** Mini-Projet : jeu vidéo colonization (part I)**

- __OpenGL et programmation jeux vidéos 3D__ 

Concepts avancés en OpenGL 

** Mini-Projet : jeu vidéo colonization (part II)**

- __Plateformes mobiles (Androïd, iPhone, ...)__ 

Contraintes des systèmes embarqués, introduction à la librairie LibGDX 

** Mini-Projet : jeu vidéo colonization (part III)**

- __Plateformes mobiles (Androïd, iPhone, …) - Concepts avancés__ 

Développement avancé sur plateformes mobiles, communication Bluetooth et Wifi 

** Mini-Projet : jeu vidéo colonization (part IV)**

- __Concept avancé et Java 8. Projet et extensions.__

Introduction aux concepts avancés et nouveautés de Java 8 tels que la reflection, introspection. Vers quoi tendent les langages ? Multi-paradigmes, notamment la programmation fonctionnelle. Gestion de l’avancement des projets et proposition d’extensions. 

** Projet final **

- __Projet Final et réponses aux questions.__ 

Gestion de l’avancement des projets. 

** Projet final **

</div>{: .notice--blank}

### Références bibliographiques

<div markdown = "1">

[1] Introduction à Java, par Patrick Niemeyer et Jonathan Knudsen. O'Reilly, 2002.

[2] Java in a Nutshell. D. Flanagan. O’Reilly, 2000.

[3] http ://java.sun.com


</div>{: .notice--blank}
