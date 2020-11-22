---
layout: single
permalink: /atiam-ml-project/
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

# Introduction

<div markdown = "1">

This page introduces the 2019-20 projects for the ATIAM [machine learning](/atiam-ml) lessons. Each subject will target various notions seen in class. We will re-introduce the basic mecanisms behind each approach, along with the fundamental papers to understand and then, we will target specific applications to musical or audio data.

## Global instructions

We detail here the global instructions that are common to all projects.
 - Groups of **4 to 5 students** per project
 - Projects are **coded in Python** (cf. Coding style section underneath)
 - All projects should be accompanied with a small report **in english**
 - The report should be of **8 pages maximum** following scientific papers
 - Reports must be written in **LaTeX** with a given **format style**
 - Each project has a **referent PhD** along with myself

</div>{: .notice--blank}

## Evaluation

<div markdown = "1">

All projects will be evaluated by the referent PhD, myself and another randomly picked PhD to ensure equity across different projects. The project should be delivered with an archive containing 3 folders

`code/` : Should contain your well-documented code (cf. Coding style section) along with simple scripts that demonstrate the use of the developped methodologies. We recommend that you organize your code following modules.

`report/` : Should contain your report in PDF format along with the LaTeX source and eventual figures.

`toy/` : Should contain a well-documented toy dataset, along with the procedural scripts to generate it. You can create another PDF document describing the set if you fill the need, otherwise detail it in your report

All your files should be packed in a zip file unfolding to a folder named
     \[ATIAM\]\[ML2017\] (LastName of all students).zip

**Deadline**   : 25/12/2019 - 23h59  
**Submission** : esling [at] ircam (dot) fr  
**Formatting** : mail with subject : \[ATIAM\]\[ML2019\] (Last names of all students involved)  

`Evaluation grid`: This generic grid will be applied and sub-grids will be modulated for each subject.

**(6 pts) - Report** Including content and style

**(6 pts) - Toy dataset** Quality and completeness of the dataset

**(8 pts) - Code** Accuracy, evaluation and coding style

</div>{: .notice--blank}

## Code and style

<div markdown = "1">

We will provide small reference codes for each project if needed. This code will contain helper functions that will alleviate you from the burden of data import and other sideline implementations. The code is in Python and relies heavily on the concept of `code sections` which allows you to evaluate only part of the code (to avoid running long import tasks multiple times and concentrate on the question at hand).

In order to get the baseline script to work, you need to have a working distribution of Python, along with the following libraries [SciPy](https://www.scipy.org/), [Music21](http://web.mit.edu/music21/), [Librosa](http://librosa.github.io/librosa/index.html), [Tensorflow](https://www.tensorflow.org/), [Pytorch](http://pytorch.org/)
  
We highly recommend that you install [Pip](https://pypi.python.org/pypi/pip/) that will manage the automatic installation of those Python libraries (along with their dependencies). 

**Coding style**
We impose that your code follow the PEP8 coding style recommandation

[PEP8 style](https://www.python.org/dev/peps/pep-0008/)

Each folder represents a module, you should consequently ensure everything
related to module definition.
 - Write a __init__.py file
 - Check that the documentation inside is valid
 - Always document any new functionality
 - Implement examples in a root-based script
    
**Code documentation**
All code should be highly documented at all levels. In order to facilitate a common documentation, you are required to follow the Numpy documentation style practice, which can be found here

[Numpy documentation style](http://sphinxcontrib-napoleon.readthedocs.io/en/latest/example_numpy.html)

**Unit testing**
Unit testing is optional for the project but highly recommended (and for your future projects in any case). Every time you add a new `independent` functionnality to the toolbox, you should develop a set of unit tests in order to ensure that all the functions work correctly and also that future modifications will not impair previous development.
If you do not know the principle of unit testing, you can read

[Unit testing](https://docs.python.org/2/library/unittest.html)

</div>{: .notice--blank}

# Subjects 

<div markdown = "1">

We detail here the various subjects (organized alphabetically by the last name of the referent PhD). For each, you can find a detailed PDF version in the following list, and we summarize the abstracts underneath.

<!--- **[![](../images/pdf.png) Caillon / Bazin - Realtime instrument interpolation using Differentiable Digital Signal Processing](../documents/mlProj_2019_Caillon.pdf)** --->

<!--- **[![](../images/pdf.png) Carsault - Introduction of musical distances for multi-step inference of jazz chord progressions](../documents/mlProj_2019_Carsault.pdf)** --->

<!--- **[![](../images/pdf.png) Douwes / Chemla - Granular synthesis using variational learning](../documents/mlProj_chemla.pdf)** --->

<!--- **[![](../images/pdf.png) Prang - Multimodal embedding music for automatic piece recognition spaces](../documents/mlProj_2019_Douwes.pdf)** --->

## Caillon / Bitton

**Learning controls and interactions for DDSP**

**Abstract**
Most generative models of audio directly synthesize samples in one of two domains: waveform or time-frequency. While sufficient to express any signals, these representations are inefficient as they do not utilize prior knowledge of how sound is produced and perceived. The Differentiable Digital Signal Processing (DDSP) model generates audio based on an additive sinusoidal synthesizer summed with a subtractive noise synthesizer (SMS decomposition), which are jointly controlled by a neural network. Conditioning signals of f0 and loudness are extracted from an audio at a 100Hz frame rate, then processed and upsampled by the DDSP decoder which infers time-varying control parameters for the output synthesizers. It achieves high audio quality with an unprecedented efficiency and has been used for creative purposes such as timbre transfer. However, its use for sampling and composition is limited since it requires fine-grained and realistic input envelopes. In this project, we will study several approaches aiming at generating expressive conditioning signals based on a quantized input (event classes, MIDI score) or in an unconditional fashion. Given a pretrained DDSP generator, the experiments will focus on learning an upstream control model and proposing new user interactions

<!--- **[![](../images/pdf.png) Full project](../documents/mlProj_2019_Caillon.pdf)** --->

## Carsault

**Harmonic arpeggiator using variational learning**

**Abstract**
In this project, we will target the modeling of complex harmonic structures using variational auto-encoding, in order to generate novel chord sequences from progressions taken from a limited set of data. Hence, we will simultaneously obtain an unsupervised representation of chord sequences and a generative chord generation process, that can be sampled to produce new sequences. Hence, your aim is twofold here : first, developing & training a suitable VAE system for chord generation, and then develop sampling & arpeggiating heuristics to make your model a convincing operational system.

<!--- **[![](../images/pdf.png) Full project](../documents/mlProj_2019_Carsault.pdf)** --->

## Devis

**Automatic rhythmic generation with control over semantic rhythms attribute**

**Abstract**
Generative systems are machine-learning models whose training is based on two simultaneous optimization tasks. The first consists in building a latent space, which provides a low-dimensional representation of the data, eventually subject to various regularization and constraints. The second is the reconstruction of the original data through the sampling of this latent space. These systems are very promising as their space is a high-level, over-compressed representation that can be used as an intermediate space for several tasks, such as visualization, measurements, or classification. The steps of this project are first to develop variational models to find generative rhythms synthesis space, where each point of this space corresponds to a new data content that comes from the high-level understanding of the input data, followed by the implementation of an approach that would provide a certain control over high-level semantic musical attributes of rhythm. The main goal is to develop a new creative tool that strives to break the commonprocess of rhythms composition.

## Douwes / Bazin

**Discrete Latent Representations of Sound for Lightweight Interactive Audio Effects**

**Abstract**
Generative systems are machine-learning models whose training is based on two simultaneous optimization tasks. The first is to build a latent space, that provides a low-dimensional representation of the data, eventually subject to various regularizations and constraints. The second is the reconstruction of the original data through the sampling of this latent space. These systems are very promising because their space is a high-level, ”over-compressed” representation that can be used as an inter- mediate space for several tasks, such as visualization, measurements, or classification. The main goal of this project is to use variational models for raw audio in order to create a granular synthesizer based on latent sampling.

<!--- **[![](../images/pdf.png) Full project](../documents/mlProj_2019_Douwes.pdf)** --->

</div>{: .notice--blank}
