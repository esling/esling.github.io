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
 - Groups if 3 to 4 students per project
 - Project should be coded in Python (cf. Coding style section underneath)
 - All projects should be accompanied with a small report **in english**
 -  

</div>{: .notice--blank}

## Evaluation

The following generic 
 - Use the given file `atiam-fpa.py` as a baseline script
 - You are authorized to define other files if you prefer
 - If stuck with code, you can still write your overall approach as a set of comments to earn some point
 - All your files should be packed in a zip file named
     \[ATIAM\]\[FpA2017\]FirstName_LastName.zip

**Deadline**   : 23/10/2017 - 23h59  
**Submission** : esling [at] ircam (dot) fr  
**Formatting** : mail with subject : \[ATIAM\]\[FpA2017\] Name  

`Evaluation grid`: 
**(4 pts) - Report** Including content and style
**(4 pts) - Toy dataset** Quality and completeness of the dataset
**(5 pts) - Strategy**
**(7 pts) - Code**

## Code and style

<div markdown = "1">

Along the tutorials, we provide a reference code for each section. This code contains helper functions that will alleviate you from the burden of data import and other sideline implementations. You will find designated spaces in each file to develop your solutions. The code is in MATLAB and relies heavily on the concept of [code sections](https://fr.mathworks.com/help/matlab/matlab_prog/run-sections-of-programs.html) which allows you to evaluate only part of the code (to avoid running long import tasks multiple times and concentrate on the question at hand.

In order to get the baseline script to work, you need to have a working distribution of Python, along with the following libraries
  - [SciPy](https://www.scipy.org/)
  - [Music21](http://web.mit.edu/music21/)
  - [Librosa](http://librosa.github.io/librosa/index.html)
  - [Yaafe](http://yaafe.sourceforge.net/)
  - [Keras](https://keras.io/)
  
We highly recommend that you install [Pip](https://pypi.python.org/pypi/pip/) or [Anaconda](https://www.anaconda.com/download/) that will manage the automatic installation of those Python libraries (along with their dependencies). 

# Subjects 

<div markdown = "1">

We detail here the various subjects. You can find a PDF version of the different topics here


</div>{: .notice--blank}
