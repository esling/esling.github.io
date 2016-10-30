---
layout: single
permalink: /teaching-mpil/
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

===== Projet LI332 - MPIL (2013/2014) =====

Cette page contient les informations et fichier relatifs au 2ème projet de LI332 (MPIL) pour l'année 2013-2014.

Le sujet du projet en PDF est disponible ici :\\
\\
{{:esling:sujet.pdf| Sujet}}

==== Sources ====

Comme expliqué dans le sujet, vous pouvez vous servir de votre propre implémentation des objets musicaux (cf. 1er projet) pour effectuer le reste du travail.

Pour ceux n'ayant pas réussi à implémenter l'intégralité des fonctions du premier projet, vous retrouverez les deux fichiers sources nécessaires ici :\\
\\
{{:esling:projet.zip| Sources librairie MIDI}}\\

Vous pouvez compiler et tester notre implémentation simplement en tapant\\
\\
''ocamlc Graphics.cma midi.ml projet.ml -o midiTransformer''\\

Nous avons implémenté la fonction ''load_midi'' (qui n'était pas demandée dans la première partie du projet). Celle-ci vous permettra d'importer un fichier MIDI quelconque dans notre type musical OCaml pour pouvoir appliquer nos transformations, et faire travailler nos algorithmes de plagiat. Celle-ci s'appelle de la manière suivante\\
\\
''load_midi "fichier.midi" nbTrack''\\
Le paramètre ''nbTrack'' permet ici de choisir quelle piste importer (en cas de fichier MIDI multi-pistes).

**Attention** : Cette fonction à été volontairement modifiée pour vous simplifier le travail et n'a pas un comportement "basique" de lecture MIDI. En effet, si vous effectuez "l'aller-retour" en passant par notre type OCaml :\\
\\
''save_midi (load_midi "Hendrix_Purple_Haze.mid" 1) "Hendrix_OCaml.mid"''\\
Vous remarquerez que le fichier résultat n'est pas identique, ceci est un **comportement volontaire** de la fonction qui a pour but de vous simplifier le travail pour le reste du projet. En effet, on considère ici que toute musique peut être importée sous forme d'une séquence (''Sequential'') d'accords (''Parallel''). Vous n'aurez donc pas à vous soucier des objets ''Parallel'' dans votre implémentation du plagieur, on considèrera juste que l'on travaille avec une succession d'objets musicaux quelconques. La fonction ''load_midi'' va donc automatiquement effectuer un découpage et une répétition des évènements parallèles de la manière suivante\\
\\
 ;#;
{{:esling:slicer.jpg?600|}}
;#;
==== Fichiers MIDI ====

Voici deux fichiers MIDI qui pourront vous servir pour tester votre projet. Ils ont été choisis d'après les excellents goûts musicaux de vos professeurs, mais n'hésitez pas à aller chercher vos propres fichiers MIDI sur le net.\\

{{:esling:hendrix_purple_haze.mid| Jimi Hendrix - Purple Haze}}\\
\\
{{:esling:bach_toccata-and-fugue-dm.mid| Johan Sebastian Bach - Toccata et Fugue en Ré mineur}}
