---
layout: single
permalink: /atiam-ml-9-markov-models/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

{% include toc %}

# Hidden Markov Models

The present tutorials covers .

# Reference slides

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.9.Hidden.Markov.Models.pdf)

The corresponding slides cover

  - Undirected graphical models
  - Hidden Markov models  
  
# Tutorial 


<img src="pics/hmm-example.png" width="300px"/>
<div align="center">*Figure 3: A Hidden Markov Model, resulting from connecting several of the Bayes Net above in a sequence*</div>

Hidden Markov Models (HMMs) are used to model the changes over time (or another dimension), in which different elements might be connected. To capture this, we can include conditional probabilities, expressing how a random variable changes over time. In this model, we assume that each state depends only on the previous one, not all previous states, which is called the ***Markov property*** and can be written as
$$
\begin{equation}
P\left(x_{t} \mid x_{t - 1}, x_{t - 2}, \dots x_{2},x_{1}\right) = P\left(x_{t} \mid x_{t - 1}\right)
\end{equation}
$$

Hence, the model can be represented as a **Graphical Probabilistic Model** (GPM), in which the connections (arcs) between different states (nodes) are weighted by the probability of going to one state. This type of model is simply called a **Markov chain**. In order to make it a **Hidden** Markov Model, we assume that there is some observable variables but in fact, the real transitions come from a random variable that we are actually interested in but is not observable directly.

Based on this model, several tasks can be performed 

In most applications, a single hidden layer is sufficient to model the behavior of a system. There are several algorithms to do the inference in a HMM, but we will be using the ***Forward-Backward*** (or Baum-Welch) algorithm for labeling.

What we want in the end is the ***model parameters*** of our grpahical model (the conditional probability tables) that best explain the observed data. The configuration we want is the one which **maximizes the likelihood** of observing our data given one set of parameters for the model (the global maxima). Hence, we model a joint probability distribution  $$P(\mathbf{o}, \mathbf{h})$$., which represents the probability of an observation $$\mathbf{o}$$ and a hidden variable $$\mathbf{h}$$ sequence occurring together

$$
\begin{equation}
P(\mathbf{o},\mathbf{h}) = P(\mathbf{h}) \times P(\mathbf{o}|\mathbf{h}) = P(\mathbf{o}) \times P(\mathbf{h}|\mathbf{o})
\end{equation}
$$

This means that the probability of seeing an observation and hidden sequence together $$P(\mathbf{o}, \mathbf{o})$$ is equal to the probability of the hidden sequence $$P(\mathbf{h})$$ times the probability that we generate these observations given the hidden sequence
$$P(\mathbf{o}|\mathbf{h})$$. It is also equal to the probability of seeing those observations $$P(\mathbf{o})$$ times the probability of
turning those observations into that hidden sequence $$P(\mathbf{h}|\mathbf{o})$$.

What we want to maximize is the last part, $$P(\mathbf{h}|\mathbf{o})$$ (i.e., what is the best hidden sequence for the observations we see), so we can rewrite the previous equation as

$$
\begin{equation}
\frac{P(\mathbf{h}) \times P(\mathbf{o}|\mathbf{h})}{P(\mathbf{o})} = P(\mathbf{h}|\mathbf{o})
\end{equation}
$$

Since we observe $$\mathbf{o}$$, we know that $$P(\mathbf{o}) = 1.0$$, so we can simply write

$$P(\mathbf{h}|\mathbf{o}) = P(\mathbf{h}) \times P(\mathbf{o}|\mathbf{h})$$

If we now consider $$P(\mathbf{t})$$. It's a sequence of tags, where each depends on the previous one. The probability of seeing the whole tag sequence $t_1, t_2, \cdots t_n$ (i.e., P(\mathbf{t})) is therefore really
just the product of seeing each of the tags following another tag. We can write that as

$$P(\mathbf{t}) = P(t_1) \times P(t_2|t_1) \times P(t_3|t_2) \times \cdots \times P(t_n|t_{n-1})$$

or for short

$$P(\mathbf{t}) = P(t_1) \times \prod^n_2 P(t_i|t_{i-1})$$

We wanted to find the parameters for our model, and now we have them: $P(\mathbf{t})$ and $P(\mathbf{w}|{t})$. So we
put it all together, and what we want to optimize is finally the product of our two parameters.

$$ P(\mathbf{t}|\mathbf{w}) = P(t_1) \times P(w_1|t_1) \times \prod^n_2 P(t_i|t_{i-1}) \times P(w_i|t_i)$$

<a name="secimplementation"></a>5 Implementation Details
==

In order to compute the parameters, we have to develop a data structure that allows us to manipulate
them. We will use a Hidden Markov Model to represent the model and ***lattice-based dynamic
programming*** to compute and manipulate the probabilities. The following sections walk through the
individual parts and explain them in detail using pseudocode. You can find a Python implementation
(not optimized for performance) [further down](#secrunnable).

5.1 HMM as Lattice
--

The idea behind our HMM is something like this: what we can see (the words) was generated by something we
cannot see (the tag sequence). This is our ***generative story*** (see Figure 7). Sounds strange? Just wait... 
<img src="pics/hmm.png" width="200px"/>
<div align="center">*Figure 7: The Hidden Markov Model of the POS tagging task*</div>


Tags are connected by ***transition probabilities*** $P(t_i|t_{i-1})$, and emit words with ***emission probabilities*** $P(w_i|t_i)$. These look strangely familiar... 
We could also say “Assume the first word was generated by the first tag, how likely is it the next word was generated by the next tag, and how likely is it that that tag followed the first?" This translates to a sequence of conditional probabilities that we already know from earlier (aren’t you glad now we went through all those equations?):

$$ P(\mathbf{t}|\mathbf{w}) = P(t_1) \times P(w_1|t_1) \times \prod^n_2 P(t_i|t_{i-1}) \times P(w_i|t_i)$$

Again, this just means “the most likely tag sequence given a sentence is computed by concatenating
the most likely tags that can emit those words".

We can model HMMs as a matrix/***lattice*** (or automaton) of tags and words, as in Figure 8, by 
replacing each random variable in the HMM with all possible values and drawing all possible arcs
between them. This can be tricky, and translating from a graphical model to a lattice takes some
getting used to.
<img src="pics/lattice.png" width="600px"/>
<div align="center">*Figure 8: The lattice for the sentence "Mice like cheese" and two possible tags, N and V*</div>


In this case, we want to label “Mice like cheese", and have an alphabet of only two tags, `N` and
`V`. It is important to specify all the tags you want to use. We start from a designated start state and
from there choose one of the tags with the respective probability $P(t)$. From each of those possible tag
states, we can emit a word with the respective probability $P(w|t)$. Those are the horizontal lines in our
lattice. Then, we choose the next tag with some probability $P(t_i|t_{i-1})$. Those are the crossing lines in
the lattice.

To visualize this, we list all tags as rows. If we have a ***dictionary*** that tells us that some words 
can only have certain tags, we simply set all other $P(w|t)$ for this word to $0$ (here, we could set
($P($ `mice` | `verb` $) = 0$) and omit the arcs. If we don’t have a such a dictionary, we have to assume that all
words can be emitted by all tags and let EM figure it out.

Ultimately, we want to learn which tags follow one another, say `V` usually comes after `N`, and
which words have which tags, e.g., like is most of the times a verb, never a noun. Only expressed as
probabilities: what is $P($ `like`$|$ `V` $)$? So how do we assign those values? We reward good parameters, i.e.,
transitions that increase $P(sentence)$, and we decrease bad ones. As a first step, instead of just taking
whole counts of how often we see a transition, we "weigh" them by how likely the resulting sentence
was ($P(sentence)$). This is called ***fractional counts***.

We could try to just generate all possible taggings of a sentence (see Figure 9) and count how often
we see `N` following `V` and “cheese" was tagged as `N`, and then sum them all up to get $P(sentence)$. Here, we have two tags and three words, so we get $2^3=8$ possible paths through the lattice. But there is a problem...
<img src="pics/naive.png" width="600px"/>
<div align="center">*Figure 9: Brute-force enumeration of all possible tag sequences*</div>

Say each word has on avg. $2.5$ tags, and a sentence has $17$ words, like this one. That’s $2.5^{17}$, or
$5,820,766$ possible paths through that lattice. For just one sentence! Imagine a sentence with 50
words... Clearly, we cannot afford to do that. We will have to do something else. And that something
is dynamic programming, see [Section 5.2](#secdp).

An aside: since we multiply a lot of transitions to get through the lattice, the numbers can
quickly become very small. To deal with this, you can use the logarithm of the probabilities.
The smaller a number gets, the larger its negative log will be. Since the range of probabilities is
between 0 and 1:0, this corresponds an interval between negative infinity and 0 in log world.
If you do use logarithms, all multiplications shown here become additions (which is slightly faster),
and all additions have to be log-additions, a special computation that unfortunately is relatively slow,
and works like this (adapted from [Manning/Schütze 2000](#refMS)):

```
m = min(x,y)
big = 10^30
if y-x > log(big):
    return (y)
else if x- y > log(big):
    return (x)
else 
    return (m + log(exp(x-m)+exp(y-m)))
```

**NB:** In the remainder of the notebook, I use “normal” probabilities (not logs), to de-clutter the notation, but in the [implementation](#secrunnable), we will use logs, and the `scipy` function `logaddexp()`.

5.2 Dynamic Programming
--

Back to our question: we wanted to know what $P($ `like` | `V` $)$ is. This now turns into the question of how
likely it is that we end up at the node that has $P($ `like` | `V` $)$ as outgoing transition (in our example node
(2,3)). And once we took that transition, what is the probability from the node we reach (i.e., (2,4))
to the end?

Since we have modeled the HMM as a lattice, we can use dynamic programming techniques. This
allows us to compute how likely it is to arrive at each node (with the Forward algorithm), and to get to
the end from there (with the Backward algorithm).

So this is where we use the Forward-Backward algorithm! It consists of two parts.

We use Forward-Backward in order to efficiently compute for each sentence how often we see each
transition and what the probability of that sentence is. We need both for the fractional counts. Forward-
Backward is the E step in our EM implementation: we compute the expected counts given the current
model parameters.

When you model the lattice, it is a good idea to use a matrix or some such data structure in your
implementation, so you can access the nodes directly. In the following, we’ll use a matrix with two
columns for each word, to make everything easier to see. In practice, people use one column per word and later
tease out the fractional counts for each type of parameter.

**The Forward Algorithm **
<img src="pics/alphalattice.png" width="600px"/>
<div align="center">*Figure 10: Computing the alphas in the Forward pass*</div>

In the forward pass, we compute a new lattice with the same dimensions as the original one, which forward pass
contains for each node the sum of all possible paths that lead up to there (see Figure 10). These values
are also called alphas. $\alpha[i, j]$ denotes the probability of all paths up to node $(i, j)$ (i.e., assigning tag $i$ to word $j$). 

$\alpha[START]$ is always $1.0$. Each subsequent $\alpha$ is just the sum of all transitions arriving there, each multiplied by the $\alpha$ of the node where it (the transition) originated.

$\alpha[END]$ is the sum of all paths through the lattice, which is equal to $P(sentence)$. $P(data)$ is the
sum of all $P(sentence)$ in the data. In each iteration, just add up all the $\alpha[END]$ of the sentences.
Remember, $P(data)$ has to increase with each iteration, or there is something wrong! EM guarantees
that the likelihood of the data increases at each iteration over the data. Outputting $P(data)$ is thus a
good way of debugging your code: if it does not increase, something went wrong...

**The Backward Algorithm**
<img src="pics/betalattice.png" width="600px"/>
<div align="center">*Figure 11: Computing the betas in the Backward pass*</div>

The backward pass is almost the same as the forward pass, just backwards (note how the direction of backward
the arrows is reversed in Figure 11). Again, we compute a new lattice, which contains for each node pass
the sum of all possible paths that lead from that node to the end. These values are called ***betas***. $\beta[i, j]$
denotes the summed probability of all paths from node $(i, j)$ to the end. This time, however, we start at
the end. $\beta[END]$ is always $1.0$.

A useful property for debugging is the fact that $\beta[START] = \alpha[END]$.

**Collecting fractional counts**
<img src="pics/fraccount.png" width="300px"/>
<div align="center">*Figure 12: Collecting fractional counts for $P($ `like` | `V` $)$*</div>

Once we have the alphas and betas, it is easy to compute for each transition how much it contributes
to $P(sentence)$. So, once more, with conviction: how good is $P($ `like` | `V` $)$? Remember, we have to know
the likelihood of all possible paths arriving at node $(2,3)$, and the probability – once we have taken the
transition – from node $(2,4)$ to the end. See Figure 12.

We used the forward algorithm to get the probability of arriving at node $(2,3)$, and the backward
algorithm to compute how likely it is from node $(2,4)$ to the end. We divide that by the likelihood of
the sentence ($= \alpha[END]$), et voila!

**The M Step**

Computing alphas and betas and collecting the fractional counts for all free parameter transitions over
all examples is the ***E step***. This, as the name suggests, is one half of Forward-Backward EM, and in 
this case the bigger half. The ***M step*** is comparatively trivial: after having gone through all the data, we 
just normalize our fractional counts to get probabilities back (remember, probabilities are just normalized
counts).

<a name="secreading"></a>8 Useful Reading
==

If you want to read the original, go for [Dempster/Laird/Rubin (1977)](#refDempster).
[Rabiner/Juang (1986)](#refRabiner) is a general overview over ***parameter estimation***, but very math-heavy. [Manning/Schütze (2000)](#refMS) has a chapter on EM, based on clustering, but with an eye on other NLP applications.
One of the most famous implementations for NLP is the tagging paper by [Merialdo (1994)](refMerialdo),
which also gives you a good idea about the various parameters you can set.

If you want to know more about the ***Forward-Backward*** procedure of calculating alphas and betas,
check out Jason Eisner’s tutorial ([Eisner, 2002](#refEisner)), including a spreadsheet with the changing values.
The second edition of the AI handbook ([Russell/Norvig, 2003, 724 – 733](refRN)) has a comprehensive
section about EM.

Kevin Knight has written a very compelling ***introduction*** ([Knight, 2009a](#refKnightA)). It is mainly about
Bayesian Inference, but explains EM very nicely. You might also want to check out his tutorials
for Carmel ([Knight, 2009b](#refKnightB)), a software that helps you implement graphical models as automata and
train them with EM. Also, the workbook for MT ([Knight, 1999](#refKnightMT)) contains a useful section on EM.

[Vaswani/Pauls/Chiang 2010](#refVaswani) show how using ***L$_0$ normalization*** can lead to smaller models and a L0
sparser distribution, which improves language related tasks a lot, because it creates a more Zipfian normalization
distribution (see [Hovy et al. 2011](#refHovy) for another application).

<a name="secadvanced"></a>9 Advanced Topics
==

The goal of his section is mainly to give you an idea of some of the topics are out there to address
problems with EM. It would lead too far to go into detail for each, so we will give a very high-level
intuition and refer to related work for details.


9.1 Scaling
--

In the examples above, we have used logarithms to prevent underflow of the probabilities. That turned
all our multiplications into additions (which is good, because it’s fast), but it also turned every addition
into a function call to a log addition (which unfortunately is very slow). There is another way to prevent
underflow, called ***scaling***, but it requires some more bookkeeping. The idea is that we normalize each 
column in our lattice so that it sums to 1. That way, the probabilities won’t get too small, and we can
still use multiplication and normal addition.

Practically, we add a vector to our forward-backward procedure. It has the same length as out lattice,
and for each position of the lattice contains the sum of the forward probabilities at that position, the
***scaling factor***. Before we move on, we normalize the column by that factor, so that it sums to 1. The 
backward pass uses the same scaling parameters as the forward pass.
We can then use the scaled forward and backward matrices as well as the scaling factor vector to
compute the fractional counts. See [Shen (2008)](#refShen) for more details (abstract mathematical notation, but
very good explanations).


9.2 Variational Bayes
--

We have earlier seen the idea of adding pseudo-counts to the fractional counts, which helps with
smoothing. Variational Bayes inference works similarly, only that now we define a prior for our prior
parameters.

A ***prior*** is essentially a curve that looks similar to what we would like to achieve (see the example
above of how EM’s distribution differs from the real one: a prior would look like the real one). In
practice, the prior here is a ***Dirichlet distribution***, which takes two parameters: a probability distribution and a vector of shape parameters. Both have the same number of elements (or dimensions). If 
we have only two dimensions in each, the prior is called a Beta function. Typically, the probability
distribution are our transition parameters, and the shape parameters are something like pseudo-counts
for each element.

This sounds rather complicated, but is relatively easy to implement. The E-step stays the same
as before. In the M-step, the elements of the shape parameter vector are added as pseudo-counts
to the matching fractional counts, and the result is passed through a ***Digamma function*** and finally
exponentiated. To normalize, we add the sum of all elements in the shape vector to our denominator
and again run it though Digamma and exponentiation. This is like a softer version of smoothing with
pseudo-counts, where we have separate counts for each parameter.


9.3 Type and Token Constraints
--

So far, we have pretended that every word can be labeled with all tags. However, we know that that is
not true: for example, “I” can never be a preposition or an adverb. One way to encode that knowledge
is to add a ***dictionary***. For each word, it lists the allowed tags. Essentially, this sets all 
parameters for disallowed tags to 0. Using a dictionary encodes general type constraints for a word, type
i.e., the ***constraints*** hold whenever we see the word anywhere in our data. Dictionaries are either built 
by hand or derived from some annotated data. In our example, we could restrict the legal tags for the
word “I” to just nouns.

There is another type of constraints, namely ***token constraints***. A token is a specific word in a 
specific context, so these constraints only hold for certain words in certain contexts. In our example,
we just might happen to know that the first “can” is a verb. ***Type constraints*** can come from simple
rules (e.g., something like “any word after the is either an adjective or a noun”), manual annotations
(going through the data and tagging some sentences) or through transfer from another data set.

Both types of constraints basically do the same thing, though: they reduce the number of nodes for a word
in our lattice. Type constraints do that for all occurrences of the word, token constraints only for some.
When we have an actual annotation for a word, the number of nodes is reduced to one. This greatly
reduces the number of legal paths through a sentence, so not only does it make forward-backward
more efficient, it also guides the algorithm because you can now only collect fractional counts for
certain parameters. See [Täckström et al. (2013)](#refOscar) for examples of using type and token constraints in an
application.
