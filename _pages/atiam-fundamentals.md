---
layout: single
permalink: /atiam-fundamentals/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam"
---


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

All the questions are already detailed inside the code provided in the `atiam-fpa.py` script, but we recall them here and also provide an indicative grading value for each. Remember that if you have trouble implementing it, you can at least provide a commented answer as to how you would approach the solution.

**(3 pts) - Q-1.1** Implement the Needleman-Wunsch (NW) algorithm.

**(1 pts) - Q-2.1** Sort the collection of composers by decreasing number of tracks

**(1 pts) - Q-2.2** Apply the NW algorithm between all tracks of each composer

**(2 pts) - Q-2.3** Extend your previous code so that it can compare

**(5 pts) - Q-3.1** Extending to a true musical name matching

**(1 pts) - Q-4.1** Import and plot some MIDI files

**(3 pts) - Q-4.2** Exploring MIDI properties

**(5 pts) - Q-5.1** Automatic evaluation of a MIDI file quality

**(4 pts) - Q-6.1** Extending your alignment algorithm to MIDI scores

### Instructions

The script defines the overall exercise which should be filled
 - Use the given file `atiam-fpa.py` as a baseline script
 - You are authorized to define other files if you prefer
 - If stuck with code, you can still write your overall approach as a set of comments to earn some point
 - All your files should be packed in a zip file named
     \[ATIAM\]\[FpA2017\]FirstName_LastName.zip

**Deadline**   : 23/10/2017 - 23h59  
**Submission** : esling [at] ircam (dot) fr  
**Formatting** : mail with subject : \[ATIAM\]\[FpA2017\] Name  
