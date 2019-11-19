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

**[![](../images/pdf.png) Caillon / Bazin - Realtime instrument interpolation using Differentiable Digital Signal Processing](../documents/mlProj_2019_Caillon.pdf)**

**[![](../images/pdf.png) Carsault - Introduction of musical distances for multi-step inference of jazz chord progressions](../documents/mlProj_2019_Carsault.pdf)**

**[![](../images/pdf.png) Douwes / Chemla - Granular synthesis using variational learning](../documents/mlProj_chemla.pdf)**

**[![](../images/pdf.png) Prang - Multimodal embedding music for automatic piece recognition spaces](../documents/mlProj_2019_Douwes.pdf)**

## Caillon / Bazin

**Realtime instrument interpolation using Differentiable Digital Signal Processing**

**Abstract**
Most generative models of audio directly generate samples in one of two domains: time or frequency. While sufficient to express any signal, these representations are inefficient, as they do not utilize ex- isting knowledge of how sound is generated and perceived. A third approach (vocoders/synthesizers) successfully incorporates strong domain knowledge of signal processing and perception, but has been less actively researched due to limited expressivity and difficulty integrating with modern auto differen- tiation based machine learning methods. The use and potential of such approaches are to be evaluated during this Machine Learning project

**[![](../images/pdf.png) Full project](../documents/mlProj_2019_Caillon.pdf)**

## Carsault

**Introduction of musical distances for multi-step inference of jazz chord progressions**

**Abstract**
This project aims to predict chord progressions of jazz music, represented as coherent chord label sequences with the help of probabilistic models. In this study, we propose to use different neural network models to generate symbolic chord sequences. Besides, we study the impact of the introduction of different musical distances through the loss function during the training of our models. Thus, we want to improve existing methods by doing multi-step prediction and by injecting music theory knowledge through the learning method in order to be able to perform accurate prediction of chord sequence and jazz melody generation. Ultimately, this project could be used to perform automatic accompaniment and improvisation.

**[![](../images/pdf.png) Full project](../documents/mlProj_2019_Carsault.pdf)**

## Douwes / Chemla

**Granular synthesis using variational learning**

**Abstract**
Generative systems are machine-learning models whose training is based on two simultaneous optimization tasks. The first is to build a latent space, that provides a low-dimensional representation of the data, eventually subject to various regularizations and constraints. The second is the reconstruction of the original data through the sampling of this latent space. These systems are very promising because their space is a high-level, ”over-compressed” representation that can be used as an inter- mediate space for several tasks, such as visualization, measurements, or classification. The main goal of this project is to use variational models for raw audio in order to create a granular synthesizer based on latent sampling.

**[![](../images/pdf.png) Full project](../documents/mlProj_2019_Douwes.pdf)**

## Prang

**Multimodal embedding music for automatic piece recognition spaces**

**Abstract**
This project aims to develop new representations for symbolic and audio music. You will try to implement the work done by Dorfer et al. [2018] and published in ISMIR 2018. Your goal is to represent musical symbols and the corresponding short excerpts of audio in the same space called multimodal embedding space. This approach allows to address the problem of matching musical audio directly to musical symbols. Moreover, theses kind of spaces could be very powerful tools for the orchestration field. By disentangling the correlation between the orchestral score and the audio signal result, we can provide efficient systems for analyze and generate specific orchestral effects. You will use Convolutional Neural Networks in order to capture features of the both modalities and represent them with vectors of the same dimension. First, you will have to prepare your dataset by synthesizing and aligning corresponding audio from MIDI files. Then, you will implement the model proposed by Dorfer et al which is composed by two networks and train it on your synthesized dataset. Once your model will be efficient on the training data, you will test it on real data through two tasks: (1) piece/score identification from audio queries and (2) retrieving relevant performances given a score as a search query. Finally, you will propose (or even implement) improvements in the architecture or the training of the model.

**[![](../images/pdf.png) Full project](../documents/mlProj_Prang.pdf)**

</div>{: .notice--blank}
