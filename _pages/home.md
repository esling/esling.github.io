---
layout: single
permalink: /
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

<div markdown = "1">

I am currently an associate professor and research in data mining and artificial intelligence at [IRCAM](http://www.ircam.fr) and computer science at [Paris 6 Unversity (UPMC)](http://www.upmc.fr)

* [Research](/research/)
* [Teaching](/teaching/)
* [Projets](/projects/)
* [Software](/software/)

## Contact information
> Philippe Esling  
> c/o IRCAM  
> 1, Place Igor Stravinsky  
> F-75004 Paris, France  

Associate professor - University Paris 6 - UPMC  
PhD - Acoustics, Signal Processing and Informatics  
IRCAM - CNRS UMR 9912  
*Music Representations* team  

</div>{: .notice--blank}
