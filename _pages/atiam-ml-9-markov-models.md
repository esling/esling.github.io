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

<div markdown="1">

The present tutorials covers the use of Hidden Markov Models (HMM) in order to perform sequence likelihood, parsing and model inference. Most of the tutorial will be devoted to the implementation of the forward-backward algorithm for performing the EM learning of the HMM models. Then, we will apply this algorithm to a problem of audio segmentation.

</div>{: .notice--blank}

# Reference slides

<div markdown="1">

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.9.Hidden.Markov.Models.pdf)

The corresponding slides cover

  - Undirected graphical models
  - Hidden Markov models  
  
</div>{: .notice--blank}
  
# Tutorial 

## 9.0 - Introduction

<div markdown="1">

Hidden Markov Models (HMMs) are used to model the changes over time (or another dimension) in which different elements might be connected. To capture this, we can include conditional probabilities, expressing how a random variable changes over time. In this model, we assume that each state depends *solely* on the previous one, not all previous states, which is called the ***Markov property***

$$
\begin{equation}
P\left(x_{t} \mid x_{t - 1}, x_{t - 2}, \dots x_{2},x_{1}\right) = P\left(x_{t} \mid x_{t - 1}\right)
\end{equation}
$$

Hence, the model can be represented as a **Graphical Probabilistic Model** (GPM), in which the connections (arcs) between different states (nodes) are weighted by the probability of going from one state to another. This type of model is simply called a **Markov chain**. In order to make it an **Hidden** Markov Model, we assume that there is some observable variables but in fact, the real transitions come from a random variable that we are actually interested in but is not observable directly.

Based on this model, several tasks can be performed by a HMM

  1. **Parse** of a sequence
  2. **Decoding**
  3. **Model estimation**

In most applications, a single hidden layer is sufficient to model the behavior of a system. There are several algorithms to do the inference in a HMM, but we will be using the ***Forward-Backward*** (or Baum-Welch) algorithm for labeling.

What we want in the end is the ***model parameters*** of our graphical model (the conditional probability tables) that best explain the observed data. The configuration we want is the one which **maximizes the likelihood** of observing our data given one set of parameters for the model (the global maxima). Hence, we model a joint probability distribution  $$P(\mathbf{o}, \mathbf{h})$$, which represents the probability of an observation $$\mathbf{o}$$ and a hidden variable $$\mathbf{h}$$ sequence occurring together

$$
\begin{equation}
P(\mathbf{o},\mathbf{h}) = P(\mathbf{h}) \times P(\mathbf{o}\mid\mathbf{h}) = P(\mathbf{o}) \times P(\mathbf{h}\mid\mathbf{o})
\end{equation}
$$

This means that the probability of seeing an observation and hidden sequence together $$P(\mathbf{o}, \mathbf{o})$$ is equal to the probability of the hidden sequence $$P(\mathbf{h})$$ times the probability that we generate these observations given the hidden sequence
$$P(\mathbf{o}\mid\mathbf{h})$$. It is also equal to the probability of seeing those observations $$P(\mathbf{o})$$ times the probability of turning those observations into that hidden sequence $$P(\mathbf{h}\mid\mathbf{o})$$.

What we want to maximize is the last part, $$P(\mathbf{h}\mid\mathbf{o})$$ (i.e., what is the best hidden sequence for the observations we see), so we can rewrite the previous equation as

$$
\begin{equation}
\frac{P(\mathbf{h}) \times P(\mathbf{o}\mid\mathbf{h})}{P(\mathbf{o})} = P(\mathbf{h}\mid\mathbf{o})
\end{equation}
$$

Since we observe $$\mathbf{o}$$, we know that $$P(\mathbf{o}) = 1.0$$, so we can simply write

$$P(\mathbf{h}\mid\mathbf{o}) = P(\mathbf{h}) \times P(\mathbf{o}\mid\mathbf{h})$$

If we now consider $$P(\mathbf{h})$$, it is a sequence of hidden states, where each depends on the previous one. Because of the Markov property, the probability of seeing the whole sequence $$h_{1}, h_{2}, \cdots h_{n}$$ (i.e., $$P(\mathbf{h})$$) is just the product of seeing each of the states following another state. We can write that as

$$
\begin{equation}
P(\mathbf{h}) = P(h_{1}) \times P(h_{2} \mid h_{1}) \times P(h_{3} \mid h_{2}) \times \cdots \times P(h_{n} \mid h_{n-1})
\end{equation}
$$

or for short

$$
\begin{equation}
P(\mathbf{h}) = P(h_{1}) \times \prod^{n}_{2} P(h_{i} \mid h_{i-1})
\end{equation}
$$

Hence, the complete optimization of all parameters can be expressed as the product of our two parameters.

$$ 
\begin{equation}
P(\mathbf{h} \mid \mathbf{o}) = P(h_{1}) \times P(o_{1} \mid h_{1}) \times \prod^{n}_{2} P(t_{i} \mid t_{i-1}) \times P(w_{i} \mid t_{i})
\end{equation}
$$

In order to compute the parameters, we have to develop a data structure that allows us to manipulate
them. We will use a HMM to represent the model and ***lattice-based dynamic programming*** to compute and manipulate the probabilities. 

</div>{: .notice--blank}

## 9.1 - HMM as Lattice

<div markdown="1">

The idea behind HMM is that what we can see (obervations) was generated by something we cannot see (the hidden state), which is the ***generative interpretation***. Observations are connected by ***transition probabilities*** $$P(h_{i} \mid h_{i-1})$$, and emitted observations with ***emission probabilities*** $$P(o_{i} \mid h_{i})$$. We can translate this to a sequence of conditional probabilities

$$ 
\begin{equation}
P(\mathbf{h} \mid \mathbf{o}) = P(h_{1}) \times P(o_{1} \mid h_{1}) \times \prod^{n}_{2} P(h_{i} \mid h_{i-1}) \times P(o_{i} \mid h_{i})
\end{equation}
$$

We can model HMMs as a ***lattice*** of hidden states and observations, by replacing each random variable in the HMM with all possible values and drawing all possible arcs between them. It is important to specify all the hidden states you want to use. We start from a designated start state and from there choose one of the hidden state with the respective probability $$P(h)$$. From each of those possible hidden states, we can emit an observation with the respective probability $$P(o \mid h)$$. Then, we choose the next hidden state with some probability $$P(h_{i} \mid h_{i-1})$$.

Ultimately, we want to learn which hidden states follow one another, and which observations correspond to those sequences. Hence, as previously in this course, we need to reward good parameters (transitions that increase $$P(sequence)$$) and we decrease bad ones. As a first step, instead of just taking whole counts of how often we see a transition, we "weigh" them by how likely the resulting sequence was ($$P(sequence)$$). This is called ***fractional counts***.

</div>{: .notice--blank}

**Exercise**
<div markdown = "1">

  1. What would be the best representation for a lattice ?
  2. Implement a simple and complex data structure for HMMs
  3. What would be a good function to weight the transitions ?

</div>{: .notice--info}

<div markdown="1">
**Handling underflows**  
Since we will multiply probabilistic transitions, the numbers can quickly become very small and lead to an underflow (numbers too small to be handled numerically). As usual, to deal with this, we can use the logarithm of the probabilities. Furthermore, in this case, all multiplications become additions, and all additions have to be log-additions, a special computation that unfortunately is quite slow.
</div>{: .notice--warning}

## 9.2 - Dynamic Programming

<div markdown = "1">

If we decompose our original question of finding $$P(o \mid h)$$, we can see that this turns to ask how likely it is that we end up at the node that has $$P(o \mid h)$$ as outgoing transition. And once we took that transition, what is the probability from the node we reach to the end of the sequence. By using dynamic programming, we can compute how likely it is to arrive at each node (with the Forward algorithm), and to get to the end from there (with the Backward algorithm).

We use Forward-Backward in order to efficiently compute for each sequence how often we see each transition and what the probability of that sequence is. We need both for the fractional counts. Forward-Backward is the E step in an EM implementation: we compute the expected counts given the current model parameters.

**Forward algorithm**

In the forward pass, we compute a new lattice with the same dimensions as the original one, which forward pass contains for each node the sum of all possible paths that lead up to there. These values are also called ***alphas***, where $$\alpha_{i, j}$$ denotes the probability of all paths up to node $$(i, j)$$ (assigning hidden state $$i$$ to observation $$j$$). 

$$\alpha_{start}$$ is always $$1.0$$. Each subsequent $$\alpha$$ is just the sum of all transitions arriving there, each multiplied by the $$\alpha$$ of the node where the transition originated.

$$\alpha_{end}$$ is the sum of all paths through the lattice, which is equal to $$P(sentence)$$. $$P(data)$$ is the
sum of all $$P(sentence)$$ in the data. In each iteration, just add up all the $$\alpha_{end}$$ of the sentences. Remember, $$P(data)$$ has to increase with each iteration, or there is something wrong. The EM algorithm guarantees that the likelihood of the data increases at each iteration over the data.

</div>{: .notice--blank}

**Exercise**
<div markdown = "1">

  1. Implement the forward algorithm
  2. Compute the parse for the set of synthetic sequences
  3. Evaluate the different sequences 

</div>{: .notice--info}

<div markdown = "1">

**Backward algorithm**

The backward pass is almost the same as the forward pass, just backwards. Again, we compute a new lattice, which contains for each node pass the sum of all possible paths that lead from that node to the end. These values are called ***betas***, where $$\beta_{i, j}$$ denotes the summed probability of all paths from node $$(i, j)$$ to the end. This time, however, we start at
the end, so $$\beta_{end}$ is always $$1.0$$. A useful property for debugging is the fact that $$\beta_{start} = \alpha_{end}$$.

</div>{: .notice--blank}

**Exercise**
<div markdown = "1">

  1. Implement the forward algorithm
  2. Verify the likelihoods of the sequences
  3. Check that you obtain coherent probabilities

</div>{: .notice--info}

<div markdown = "1">
**Collecting fractional counts**

Once we have the alphas and betas, it is easy to compute for each transition how much it contributes
to $$P(sentence)$$. We have to know the likelihood of all possible paths arriving at a particular node $$(i,j)$$, and the probability – once we have taken the transition – from node $$(i,j+1)$$ to the end.  

We used the forward algorithm to get the probability of arriving at node $$(i,j)$$, and the backward algorithm to compute how likely it is from node $(i,j+1)$ to the end. We divide that by the likelihood of the sentence ($$= \alpha_{end}$$) in order to obtain the fractional counts.

</div>{: .notice--blank}

**Exercise**
<div markdown = "1">

  1. Implement the computation of the fractional counts

</div>{: .notice--info}

**The M Step**

Computing alphas and betas and collecting the fractional counts for all free parameter transitions over all examples is the ***E step***. This, as the name suggests, is one half of Forward-Backward EM. The ***M step*** is comparatively trivial: after having gone through all the data, we just normalize our fractional counts to get probabilities back (remember, probabilities are just normalized counts).

**Exercise**
<div markdown = "1">

  1. Implement the complete algorithm
  2. Run it on the set of sequences to obtain the model parameters

</div>

## 9.3 - Audio applications

## 9.4 - Advanced Topics

<div markdown = "1">

The goal of his section is mainly to give you a very high-level intuition and refer to related work for details.

**Scaling**

We used logarithms to prevent underflow of the probabilities. There is another way to prevent underflow, called ***scaling***. The idea is that we normalize each column in our lattice so that it sums to 1. That way, the probabilities won’t get too small, and we can still use multiplication and normal addition. Practically, we add a vector to our forward-backward procedure. It has the same length as out lattice, and for each position of the lattice contains the sum of the forward probabilities at that position, the ***scaling factor***.

**Variational Bayes**

We have earlier seen the idea of adding pseudo-counts to the fractional counts, which helps with smoothing. Variational Bayes inference works similarly, only that now we define a prior for our prior parameters. In practice, the prior here is a ***Dirichlet distribution***, which takes two parameters: a probability distribution and a vector of shape parameters. Both have the same number of elements (or dimensions). Typically, the probability distribution are our transition parameters, and the shape parameters are something like pseudo-counts for each element.

In the M-step, the elements of the shape parameter vector are added as pseudo-counts to the matching fractional counts, and the result is passed through a ***Digamma function*** and finally exponentiated. To normalize, we add the sum of all elements in the shape vector to our denominator and again run it though Digamma and exponentiation. This is like a softer version of smoothing with pseudo-counts, where we have separate counts for each parameter.

</div>{: .notice--blank}

## References

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
