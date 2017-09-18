---
layout: single
permalink: /atiam-fundamentals/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam"
---

## ATIAM - Fundamentals

### Slides
  * The lesson on data structures and algorithms [slides ![](../images/pdf.png)](../documents/Generic.5.Structures.pdf)

### Assignment

Using multiple computer structures and solving symbolic alignments for classical music pieces

In this exercise, we will use our knowledge on computer structures to solve a very well-known problem of symbolic alignement. Hence, you this part is split 
  1 - Implement a string alignment algorithm
  2 - Try to apply this to a collection of classical music pieces names
  3 - Develop your own more adapted procedure to have a matching inside large set
  4 - Extending your approach to align MIDI scores
  5 - Proposing your own approach to MIDI quality evaluation
  
To simplify your 
The set of classical music pieces is provided in the `atiam-fpa.pkl` file, which is already loaded at this point of the script and contain two structures
    - composers         = Array of all composers in the database
    - composers_tracks  = Hashtable of tracks for a given composer

#### Baseline

#### Dependencies

#### Questions

All the questions are already detailed inside the code provided in the `atiam-fpa.py` script, but we recall them here to help you out.

1. Implement the dynamic programming algorithm presented in the following articles by using the language of your choice. (15 points)  

Y. Jeong, M. Jeong, and O. Omitaomu, *Weighted dynamic time warping for time series* Pattern Recognition, vol. 44, 2011.  
[![](../images/pdf.png)](http://lig-membres.imag.fr/bisson/cours/M2INFO-AIW-ML/papers/Jeong11.pdf)

2. Produce a musical application of this algorithm. (5 points)

##### Informations

The script defines the overall exercise which should be filled
 - Use this as a baseline script
 - You are authorized to define other files for functions
 - Write a (small) report document (PDF) explaining your approach if needed
 - All your files should be packed in a zip file named
     \[ATIAM\]\[FpA2017\]FirstName_LastName.zip

**Deadline**   : 23/10/2017 - 23h59  
**Submission** : esling [at] ircam (dot) fr  
**Formatting** : mail with subject : \[ATIAM\]\[FpA2017\] Name  
