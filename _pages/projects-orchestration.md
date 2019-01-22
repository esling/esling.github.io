---
layout: single
permalink: /projects-orchestration/
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

# Computational orchestration
Orchestration is the subtle art of mixing instrumental properties. Among all techniques of musical composition, it has always remained an empirical activity. Trying to approach orchestration from a scientific angle involve the use of unformalized knowledge and imply to solve a NP-Complete combinatorial problem.

Our approach is intended to search for sound combinations within instrument sample databases that best match a target timbre defined by the composer. However, former methods use either decomposition or matching pursuit algorithms, and therefore circumvent the combinatorial problem of orchestration. We propose an original approach for the discovery of relevant sound combinations, in which we explicitly address combinatorial issues and tackle the problem of temporal descriptors evolution.

## Research projects

ACTOR
MAKIMOno

## Research topics

As this problem lies at the crossroads of several research fields, we can ask ourselves to what extent this problem can be defined. The following figure depicts the various link between different parts of the orchestration problem.

We can see here that the orchestration problem have several ramifications in various research fields ranging from sound perception to combinatorial optimization. 

## Problem definition

The goal of computational orchestration is to find the mixtures of instruments that best match a given timbre. In our system the user speciﬁes the instruments he would like to use (constraints) and the characteristics of the sound to be produced (a sound target). This target is deﬁned as a set of features coming either from a sound analysis or from a compositional process. Then, an orchestration engine uses an instrumental knowledge database (features database) created by the analysis and structuring of large sound sample databases, to suggest instruments notes combinations (orchestration proposals) that sound closest the target. More precisely, the procedure searches for instrumental combinations whose features best match the target’s features.

Our problem is therefore to find a fast and efficient way to test instrumental mixtures in order to converge towards closely sounding elements.

### Complexity

The complexity of this problem arise from the exponential number of possible instrumental mixture. Indeed an orchestra can count up to hundred players and is usually composed of multiple instruments that are themselves able to produce a whole variety of playing mode. On the other hand, it is also hard to predict what are going to be the properties of a combination (as it is computationally too intense to recompute signal descriptors on each mixture). This problem unveils numerous facets of complexity
  * Circumvent the combinatorial explosion of possibilities.
  * Predicting the spectral properties of sound mixtures.
  * Coping with emergence phenomenon that arise from mixtures.
  * Multidimensional aspect of timbre perception.
  * Handling the temporal aspects of sound structures.
  * Linking symbolic (writing) and signal (timbre) aspects.


### Existing architecture

In order to solve the combinatorial problem, we have to use a fast exploration procedure. Moreover, we have to cope with the multidimensional aspect of timbre perception. Therefore, our system is based on a multi-objective genetic search algorithm. The following figure depicts the algorithmic workflow of our system.

### Temporal structures

All previous works on this subject have focused on vertical orchestration, analyzing only the sustained part of instruments and thus completely discarding the temporal evolution of sounds. However, the territory of timbre is not confined to a static structure of proportions. It rather comprises “variation laws” that regulate the interaction between frequency and amplitude functions in an evolving context over time. It is therefore essential to move to a higher level of modeling, by understanding the micro-temporal qualities of timbre in order to capture the sound as a spectro-temporal structure. Advantages of this approach are twofold. First, the generated orchestration may be considered more realistic as it accounts for the whole spectro-temporal structure. Second, it allows the use of evolving playing modes like crescendo, glissando, multiphonics and so on.

### Time series handling

In order to take temporal evolution into account, we first attempted to use a single temporal descriptor based on a Gaussian Mixture Model (GMM). However, this "holistic" descriptor seemed to make the algorithm stray too far from its original multiobjective spirit. Furthermore, model calculations were computationally too intense. We therefore decided to turn ourselves to time series analysis techniques in order to provide more efficient storage and fast querying and computations.

We redirect the interested readers to our webpage and article on time series mining which explains the time series technique and distance measure used in our system.

ESLING Philippe, AGON Carlos "Time series data mining and analysis", ACM Computing Surveys 2011 (Accepted with modifications).

### Addition functions

One of the biggest problem that we stumble upon is that descriptors used by our system are not linearly additive. Even if in the scalar case, the error is not too important, for the temporal case, the error function seems to be bursting a lot more. We analyzed over 10.000 instrumental mixtures for cardinalities going from 2 to 10 instruments. The following picture depicts the resulting prediction error for spectral centroid and total energy.

As we can see here, the addition functions are not robust, especially for the temporal case. But the linear drift is encouraging as maybe only part of the equation seems to be missing. In fact, a deeper analysis of these large-scale experiments show some wide error “anomalies” that seems to widely augment the prediction error.


### Comparison functions

Instead of using a simple Euclidean norm (as it is the case for scalar descriptors), we use a more subtle notion of similarity for comparing time series. The idea is to allow for non-linear warping on the time axis.

</div>{: .notice--blank}
