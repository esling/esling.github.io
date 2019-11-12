---
layout: single
permalink: /exam-java/
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

# Examen Java, Androïd et Web réactif.

## Sujet

<div markdown = "1">

Vous trouverez le sujet de l'examen complet en [suivant ce lien](../documents/exam_12112019.pdf).

L'examen dure 2 heures, et tous les documents sont autorisés. Le rendu s'effectuera en envoyant une unique archive zip contenant
- Un fichier `exam.txt` à la racine (contenant les réponses textes et explications si nécessaires)
- Un dossier `exercice1`
- Un dossier `exercice2`
Les dossiers `exercice*` ne devront contenir que vos classes Java répondant aux questions

A la fin du temps imparti, envoyez votre archive par mail à l'adresse `esling (arobase) ircam (point) fr`, en indiquant comme sujet du mail
`[JAVA][L3][Examen] <Nom> <Prenom>`

Notez bien que les mails contiennent un timestamp qui indiquera tout retard sur le rendu.

</div>{: .notice--blank}
