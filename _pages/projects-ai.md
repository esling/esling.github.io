---
layout: single
permalink: /projects-ai/
author_profile: false
sidebar:
  nav: "research-projects"
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

# Artificial creative intelligence

I currently direct the [ACIDS](http://acids.ircam.fr) (Artificial Creative Intelligence and Data Science) group at [IRCAM](http://www.ircam.fr), where we seek to model musical creativity through variational learning approaches. Our major object of study lies in the properties and perception of both [musical orchestration](/projects-orchestration) and [musical co-improvisation](/projects-ai/). Orchestration is the subtle art of writing musical pieces for orchestra, by combining the spectral properties of each instrument to achieve a particular sonic goal. In this context, the multivariate analysis of temporal processes is required given the inherent multidimensional nature of instrumental mixtures. Furthermore, time series need to be scrutinized at variable time scales (termed here granularities) as a wealth of time scales co-exist in music (from the identity of single notes up to the structure of entire pieces). Furthermore, orchestration lies at the exact intersection between the symbol (musical writing) and signal (audio recording) representations.

We developped multiple state-of-art creative applications done in the past years, and focus on various applications of the variational learning framework to disentangle factors of audio variation. Several recent papers produced by our team, allow to regularize the topology of the latent space based on perceptual criteria, working with both audio waveforms and spectral transforms and performing timbre style transfer between instruments. The development of these approaches as creative tools allow to increase musical creativity in contemporary music and were used in recent pieces played at renowned venues.

## Understand

## Interact

## Generate

</div>{: .notice--blank}
