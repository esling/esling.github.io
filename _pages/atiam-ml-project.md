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

This page introduces the 2017-18 projects for the ATIAM [machine learning](/atiam-ml) lessons. Each subject will target various notions seen in class. We will re-introduce the basic mecanisms behind each approach, along with the fundamental papers to understand and then, we will target specific applications to musical or audio data.

## Global instructions

We detail here the global instructions that are common to all projects.
 - Groups of **3 to 4 students** per project
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

**Deadline**   : 25/12/2017 - 23h59  
**Submission** : esling [at] ircam (dot) fr  
**Formatting** : mail with subject : \[ATIAM\]\[ML2017\] (Last names of all students involved)  

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

### [![](../images/pdf.png) Bitton - Disentangling variation factors in audio samples](../documents/mlProj_bitton.pdf)
### [![](../images/pdf.png) Carsault - Generation of lead sheets and inference in jazz](../documents/mlProj_carsault.pdf)
### [![](../images/pdf.png) Chemla - Regularization and representations in modular sound synthesis](../documents/mlProj_chemla.pdf)
### [![](../images/pdf.png) Crestel - Seq2seq generation of symbolic orchestral music](../documents/mlProj_crestel.pdf)
### [![](../images/pdf.png) Prang - Embedding music for automatic composition spaces](../documents/mlProj_prang.pdf)

## Bitton - Disentangling variation factors in audio samples

## Carsault - Generation of lead sheets and inference in jazz

## Chemla - Regularization and representations in modular sound synthesis

## Crestel - Seq2seq generation of symbolic orchestral music

## Prang - Embedding music for automatic composition spaces


</div>{: .notice--blank}
