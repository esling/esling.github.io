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

#### Dependencies

In order to get the baseline script to work, you need to have a working distribution of Python, along with the following libraries
  - [SciPy](https://www.scipy.org/)
  - [Music21](http://web.mit.edu/music21/)
  - [NwAlign](https://pypi.python.org/pypi/nwalign)
  
We highly recommend that you install [Pip](https://pypi.python.org/pypi/pip/) or [Anaconda](https://www.anaconda.com/download/) that will manage any install of the Python libraries. 

#### Baseline

#### Questions

All the questions are already detailed inside the code provided in the `atiam-fpa.py` script, but we recall them here to help you out.

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
