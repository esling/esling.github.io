---
layout: single
permalink: /projects/
author_profile: false
share: true
comments: true
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

<div markdown = "1">
# Research projects
## [Artificial Creative Intelligence](/projects-ai) (Creative AI)
The research project carried by the ACIDS team at IRCAM seeks to model musical creativity by extending variational learning approaches towards the use of multivariate and multimodal time series. Our major object of study lies in the properties and perception of musical orchestration. Orchestration is the subtle art of writing musical pieces for orchestra, by combining the spectral properties of each instrument to achieve a particular sonic goal. In this context, the multivariate analysis of temporal processes is required given the inherent multidimensional nature of instrumental mixtures. Furthermore, time series need to be scrutinized at variable time scales (termed here granularities) as a wealth of time scales co-exist in music (from the identity of single notes up to the structure of entire pieces). Furthermore, orchestration lies at the exact intersection between the symbol (musical writing) and signal (audio recording) representations.

After introducing the general framework and multiple state-of-art creative applications done in the past years, we will focus on various applications of the variational learning framework to disentangle factors of audio variation. Hence, we will detail several recent papers produced by our team, allowing to regularize the topology of the latent space based on perceptual criteria, working with both audio waveforms and spectral transforms and performing timbre style transfer between instruments. Finally, we discuss the development of these approaches as creative tools allowing to increase musical creativity in contemporary music and show case-study of recent pieces played at renowned venues.

## [Musical orchestration](/projects-orchestration/)
Orchestration is the subtle art of mixing instrumental properties. Among all techniques of musical composition, it has always remained an empirical activity. Our approach is intended to search for sound combinations within instrument sample databases that best match a target timbre defined by the composer. We propose an original approach for the discovery of relevant sound combinations, in which we explicitly address combinatorial issues and tackle the problem of temporal descriptors evolution.

## [Multiobjective time series matching](/projects-mots/)
We present here an innovative problem that can be casted into a new approach merging multiobjective optimization and time series matching algorithms, called *MultiObjective Time Series* (MOTS) matching. We formally state this novel problem that could lead to a whole range of applications in several fields of research and report an efficient implementation. This approach allowed in the scope of sound samples querying to cope with the multidimensional nature of timbre perception and also to obtain a whole set of efficient solutions.

Seeking sound samples in a massive database can be a very tedious and painstaking task. Even when meta-informations are available, querying results may remain far from the mental representation expected by the user. We worked on the development of the first intelligent sound sample database. We propose a scheme where sounds can be retrieved by  simply drawing the temporal shape of spectral descriptors. Then we addressed two completely novel ways of intuitive querying. First, by optimizing simultaneously multiple temporal shapes of descriptors with //MultiObjective Spectral Evolution Query// (MOSEQ). Second by performing a vocal imitation of the sound sample with //Query by Vocal Imitation// (QVI).

[//]: # $$ \Gamma $$  
[//]: # $ \sum{x}{y}x+y $  

[//]: # $$
[//]: # \begin{equation}
[//]: # \Gamma(z) := \int_{0}^{\infty}t^{z-1}e^{-t}dt.
[//]: # \label{eq1}
[//]: # \end{equation}
[//]: # $$



## [Ecological diversity analysis and metagenomics](/project-monitoring/)
The study of biological diversity through analysis of the DNA sequences found in the environment. We rely on billion-sized datasets of genetic sequences obtained from Next-Generation Sequencing (NGS) to monitor environmental impacts. This work is led with the Department of Genetics and Evolution at the University of Geneva, Switzerland.

</div>{: .notice--blank}
