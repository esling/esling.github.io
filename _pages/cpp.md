---
layout: single
permalink: /cpp/
author_profile: true
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

<div markdown = "1">

# CPP Application

This webpage contains all supplementary elements for the application of Philippe Esling to a Congé pour Projet Pédagogique (CPP) as Associate Professor in Section 27 (Computer science).

For any supplementary information, please contact me directly at

(+33) 6.32.58.91.08

esling \[at\] ircam (dot) fr 

## Application file

The main file contains all the principal information on teaching, research and administrative duties as well as supplementary files for the application.

Main CPP application - Philippe Esling

[PDF File]()

## PhD documents

### Multiobjective time series matching

Link to the full thesis manuscript

[Zipped PDF](http://repmus.ircam.fr/_media/esling/esling_thesis.pdf.zip)

### Reports

Official reports from the PhD reviewers

- [Habib Ammari](http://repmus.ircam.fr/_media/esling/rapport_ammari.pdf)
- [Malcolm Slaney](http://repmus.ircam.fr/_media/esling/rapport_slaney.pdf)

Final defence jury report

[Final report](http://repmus.ircam.fr/_media/esling/rapport_jury.pdf)

PhD diploma

[Diploma](http://repmus.ircam.fr/_media/esling/attestation_diplome.pdf)

### Jury

Pour chaque membre du jury, un lien est disponible vers sa page personnelle, contenant son CV et ses activités de recherche.\\

[Malcolm Slaney](http://slaney.org/malcolm/pubs.html)
Rapporteur - Professor - Stanford University
[Habib Ammari](http://www.cmap.polytechnique.fr/~ammari/)
Rapporteur - Directeur de recherche - ENS - CNRS
[Carlos Agon](http://repmus.ircam.fr/agon)
Directeur - Professeur des universités - UPMC
[Jean-Paul Allouche](http://www.math.jussieu.fr/~allouche/)
Examinateur - Directeur de recherche - CNRS - UPMC
[François Pachet](http://www.csl.sony.fr/~pachet/)
Examinateur - Senior Researcher - Sony CSL
[Patrice Perny](http://www-poleia.lip6.fr/~perny/fr/index.php)
Examinateur - Professeur des universités - LIP6
[Daniel Pressnitzer](http://lpp.psycho.univ-paris5.fr/person.php?name=DanielP)
Examinateur - Directeur de recherche - ENS - CNRS

<!---

Cette section contient les liens vers les versions complètes des articles publiés dans des journaux internationaux à comité de lecture.

Lecroq Béatrice, Lejzerowicz Franck, Esling Philippe, Baerlocher Loic, Farinelli Laurent, Pawlowski Jan "Ultra-deep sequencing of foraminiferal microbarcodes unveils hidden richness of early monothalamous lineages in deep-sea sediments", Publication of the National Academy of Science, vol.108, no.32, pp 13177-13182, August 2011.\\
\\
{{:esling:pnas-2011.pdf| - Article complet}}\\

Esling Philippe, Agon Carlos "Time series data mining and analysis", ACM Computing Surveys, vol. 46, no. 1, 2013.\\
\\
{{:esling:ts_review_short.pdf| - Article complet}}\\

Esling Philippe, Agon Carlos "Multiobjective time series matching for audio classification and retrieval", IEEE Transactions on Speech Audio and Language Processing 2013 (Accepted - Major changes).\\
\\
{{:esling:manuscript_double.pdf| - Article complet}}\\

==== Supports de cours ====

Notes de cours de l'UE LXTMI (Cycle IPCM) distribué aux élèves\\
{{:esling:coursJAVA.pdf| - Support de cours}}\\

Examen final de l'UE LXTMI (Cycle IPCM)\\
{{:esling:examFinal.pdf| - Examen final}}\\

Session d'exercice (TD 3)\\
{{:esling:ex_TD3.pdf| - Sujet}}\\
{{:esling:ex_TD3_Corrige.pdf| - Corrigé (distribué)}}\\

Session d'exercice (TD 6)\\
{{:esling:ex_TD6.pdf| - Sujet}}\\
{{:esling:ex_TD6_Corrige.pdf| - Corrigé (distribué)}}\\

==== Lettres de recommandation ====

** Enseignement **

{{:esling:lettre_manoury.pdf| - Lettre de recommandation de Pascal Manoury}}\\
Directeur de l'UFR Informatique et responsable de la section IPCM de l'UPMC

{{:esling:lettre_andreatta.pdf| - Lettre de recommandation de Moreno Andreatta}}\\
Directeur du Master 2 Recherche ATIAM à l'IRCAM

** Recherche **

{{:esling:lettre_agon.pdf| - Lettre de recommandation de Carlos Agon}}\\
Professeur des universités - Directeur de thèse

{{:esling:lettre_assayag.pdf| - Lettre de recommandation de Gérard Assayag}}\\
Directeur de l'unité CNRS - IRCAM (UMR 9912)

{{:esling:lettre_codognet.pdf| - Lettre de recommandation de Philippe Codognet}}\\
Directeur de l'unité UMI CNRS - JFLI à l'Université de Tokyo

{{:esling:lettre_mcadams.pdf| - Lettre de recommandation de Stephen McAdams}}\\
Directeur du laboratoire Cognition and Perception à l'Université de McGill à Montréal

-->

## Research information

I currently direct the [ACIDS](http://acids.ircam.fr) (Artificial Creative Intelligence and Data Science) group at [IRCAM](http://www.ircam.fr), where we seek to model musical creativity through variational learning approaches. Our major object of study lies in the properties and perception of both [musical orchestration](/projects-orchestration) and [musical co-improvisation](/projects-ai/). Orchestration is the subtle art of writing musical pieces for orchestra, by combining the spectral properties of each instrument to achieve a particular sonic goal. In this context, the multivariate analysis of temporal processes is required given the inherent multidimensional nature of instrumental mixtures. Furthermore, time series need to be scrutinized at variable time scales (termed here granularities) as a wealth of time scales co-exist in music (from the identity of single notes up to the structure of entire pieces). Furthermore, orchestration lies at the exact intersection between the symbol (musical writing) and signal (audio recording) representations.

</div>{: .notice--blank}
