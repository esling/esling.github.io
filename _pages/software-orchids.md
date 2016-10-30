---
layout: single
permalink: /software-orchids/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
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

====== ATO-MS : Software release ======
==== Abstract Temporal Orchestration - Modular Structure ====

{{:esling:atoms-doc.pdf|Ato-ms documentation}}

===== Release =====



=== Installation Package ===



=== Applications ===

{{:esling:ato-me.zip|Ato-me client application}}

=== Documentation ===

{{:esling:atoms-doc.pdf|Ato-ms documentation}}

===== Sources =====

{{:esling:atoms-src.zip|Ato-ms server source code (Matlab)}}

{{:esling:atome-src.zip|Ato-me client source (Max/Msp + JS)}}

{{:esling:atoms-doc.pdf|Ato-ms documentation}}
