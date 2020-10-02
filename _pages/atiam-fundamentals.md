---
layout: single
permalink: /atiam-fundamentals/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam"
---

<div markdown = "1">

## Slides
  * The lesson on data structures and algorithms [slides ![](../images/pdf.png)](../documents/Generic.5.Structures.pdf)

## Assignment

***Using multiple computer structures and solving symbolic alignments for classical music pieces in Python.***

In this exercise, we will use our knowledge on computer structures to solve a very well-known problem of symbolic alignement. Hence, the overall goal of your work is
1. Implement a *string alignment* algorithm
2. Try to apply this to a collection of classical music pieces names
3. Develop your own more adapted procedure to the specific problem of classical names matching
4. Proposing your own approach to the problem of *MIDI quality evaluation*
4. Extending your alignment algorithm to align MIDI scores
  
To simplify your work, the global layout of the exercise has been pre-coded inside the `atiam-fpa.py` script. You simply have to follow the questions written along the script, and insert your own code where the following tags appear

{% highlight Python %}
################
# YOUR CODE HERE
################
{% endhighlight %} 

The set of classical music pieces is provided in the `atiam-fpa.pkl` file, which is already loaded at this point of the script and contain two structures
{% highlight Python %}
composers         # Array of all composers in the database
composers_tracks  # Hashtable of tracks for a given composer
{% endhighlight %}  

### Dependencies

In order to get the baseline script to work, you need to have a working distribution of Python, along with the following libraries
  - [SciPy](https://www.scipy.org/)
  - [Music21](http://web.mit.edu/music21/)
  - [NwAlign](https://pypi.python.org/pypi/nwalign)
  
We highly recommend that you install [Pip](https://pypi.python.org/pypi/pip/) or [Anaconda](https://www.anaconda.com/download/) that will manage the automatic installation of those Python libraries (along with their dependencies). 

For those of you who have never coded in Python, here are a few interesting resources to get started.

  - [TutorialPoint](https://www.tutorialspoint.com/python/)
  - [Programiz](https://www.programiz.com/python-programming)

### Baseline

First download the [baseline code ![](../images/file.png)](../documents/atiam-fpa.zip)

After unzipping the file, you will find the following files

{% highlight Python %}
atiam-fpa/            # Folder of anonymized Beethoven MIDI files
atiam-fpa_alpha.dist  # Basic symbolic distance matrix
atiam-fpa_dna.dist    # Example of DNA-based distance matrix
atiam-fpa.pkl         # Serialized file with all track names and composers
atiam-fpa.py          # Basic script to start from
{% endhighlight %}

### Questions

All the questions are already detailed inside the code provided in the `atiam-fpa.py` script, but we recall them here and also provide an indicative grading value for each. Remember that if you have trouble implementing a given question, the different parts are almost completely independent, so you can jump to the next section. In open questions you can also at least provide a commented answer as to how you would approach the solution.

#### Part 1 - Exploring the collection / playing with MIDI


**(1 pts) - Q-1.1** Re-implement a sorting algorithm seen in class either bubble sort or quicksort (+1 pt)

**(1 pts) - Q-1.2** Sort the collection of composers by decreasing number of tracks

**(1 pts) - Q-1.3** Extend your sorting procedure, to sort all tracks from all composers alphabetically 

**(1 pts) - Q-1.4** Import some MIDI and produce prettier plots

**(1 pts) - Q-1.5** Compute the number of notes in a MIDI and sort the collection

#### Part 2 - Implementing the alignment algorithm


**(3 pts) - Q-2.1** Implement the basic (simple gap cost) Needleman-Wunsch (NW) algorithm

**(1 pts) - Q-2.2** Apply the NW algorithm between all tracks of each composer

**(2 pts) - Q-2.3** Extend your previous code so that it can compare more advanced properties

#### Part 3 - Extending the alignment algorithm and musical matching


**(2 pts) - Q-3.1** Extending your algorithm to perform to a true musical name matching

**(3 pts) - Q-3.2** Extend the NW algorithm to include affine gaps penalties ([Gotoh algorithm](http://helios.mi.parisdescartes.fr/~lomn/Cours/BI/Material2019/gap-penalty-gotoh.pdf))

#### Part 4 - Extending the alignment algorithm and musical matching


**(3 pts) - Q-4.1** Exploring MIDI properties

**(4 pts) - Q-4.2** Automatic evaluation of a MIDI file quality

**(4 pts) - Q-4.3** Extending your alignment algorithm to MIDI scores

### Instructions

The script defines the overall exercise which should be filled
 - Use the given file `atiam-fpa.py` as a baseline script
 - You are authorized to define other files if you prefer
 - If stuck with code, you can still write your overall approach as a set of comments to earn some point
 - All your files should be packed in a zip file named
     \[ATIAM\]\[FpA2020\]FirstName_LastName.zip

**Deadline**   : 06/11/2020 - 23h59  
**Submission** : esling [at] ircam (dot) fr  
**Formatting** : mail with subject : \[ATIAM\]\[FpA2020\] Name  

</div>{: .notice--blank}
