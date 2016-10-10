---
layout: single
permalink: /atiam-ml-7-bayesian-inference/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

{% include toc %}

# Bayesian inference

The present tutorials covers .

# Reference slides

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.7.Bayesian.Inference.pdf)

The corresponding slides cover

  - Bayesian learning
  - Undirected graphical models
  - Maximum likelihood  
  
# Tutorial 

### 5.1 - (Bayesian) probabilities 

The Bayesian world-view interprets probability as measure of *believability in an event*, that is, how confident we are in an event occurring. To explicit this idea, we need to consider an alternative interpretation of probability: *Frequentist*, known as the more *classical* version of statistics, assumes that probability is the long-run frequency of events. For example, the *probability of plane accidents* under a frequentist philosophy is interpreted as the *long-term frequency of plane accidents*. This makes logical sense for many probabilities of events, but becomes more difficult to understand when events have no long-term frequency of occurrences. Consider: we often assign probabilities to outcomes of presidential elections, but the election itself only happens once! Frequentists get around this by invoking alternative realities and saying across all these realities, the frequency of occurrences defines the probability. 

Bayesians, on the other hand, have a more intuitive approach. Bayesians interpret a probability as measure of *belief*, or confidence, of an event occurring. Beliefs between 0 and 1 allow for weightings of other outcomes. This is also interesting, as this definition leaves room for conflicting beliefs between individuals. Different individuals have different beliefs of events occurring, because they possess different *information* about the world. Bayesian inference is mostly based on updating your beliefs after considering new evidence. Bayesian inference differs from more traditional statistical inference by preserving *uncertainty*. At first, this sounds like a bad statistical technique. Isn't statistics all about deriving *certainty* from randomness? To reconcile this, we need to start thinking like Bayesians.

To align with traditional probability notation, we denote our belief about event $$A$$ as $$P\left(A\right)$$. We call this quantity the *prior probability* of an event to occur. We denote our updated belief as $$ P\left( A \mid X \right) $$, interpreted as the probability of $A$ *given* the evidence $X$. We call the updated belief the *posterior probability* so as to contrast it with the prior probability. 

We do not completely discard the prior belief after seeing new evidence $X$, but we *re-weight the prior* to incorporate new evidence (i.e. we put more weight, or confidence, on some beliefs versus others). By introducing prior uncertainty about events, we admit that any guess we make is potentially very wrong. After observing data, evidence, or other information, we update our beliefs, and our guess becomes *less wrong*.

### Bayesian Inference in Practice


#### Incorporating evidence

As we acquire more and more instances of evidence, our prior belief is *washed out* by the new evidence. Denote $$N$$ as the number of instances of evidence we possess. As we gather an *infinite* amount of evidence, say as $$N \rightarrow \infty$$, our Bayesian results (often) align with frequentist results. Hence for small $N$, inference is *unstable*, where frequentist estimates have more variance and larger confidence intervals. This is where Bayesian analysis excels. By introducing a prior, and returning probabilities (instead of a scalar estimate), we *preserve the uncertainty* that reflects the instability of statistical inference of a small $N$ dataset. 

Frequentist methods are still largely useful in tools such as least squares linear regression, LASSO regression, and expectation-maximization algorithms. Bayesian methods complement these techniques by solving problems that these approaches cannot, or by illuminating the underlying system with more flexible modeling. 

### The Bayesian framework

We are interested in beliefs, which can be interpreted as probabilities by thinking Bayesian. We have a *prior* belief in event $A$, beliefs formed by previous information. Secondly, we observe some evidence and we want to update our belief to incorporate this. We call this new belief the *posterior* probability. Updating our belief is done via the following equation, known as the Bayes' Theorem

$$
\begin{equation}
 P\left( A \mid X \right) \propto \frac{ P\left(X \mid A\right) P\left(A\right) } {P\left(X\right) }
\end{equation}
$$

Hence, we see that our posterior belief of event $$A$$ given the new evidence $$X$$ is proportional to ($$\propto$$) the *likelihood* of observing this particular evidence $$X$$ given the event $$A$$ multiplied by our prior belief in that event $$A$$.

#### Coin-flip example

Suppose that you are unsure about the probability of heads in a coin flip. You believe there is some true underlying ratio, call it $$p$$, but have no prior opinion on what $$p$$ might be. We begin to flip a coin, and record the observations: either $$H$$ or $$T$$. This is our observed data. An interesting question to ask is how our inference changes as we observe more and more data? More specifically, what do our posterior probabilities look like when we have little data, versus when we have lots of data. 

Below we plot a sequence of updating posterior probabilities as we observe increasing amounts of data (coin flips).


### But what is $\lambda \;$?

The parameter, $$\lambda$$ is usually the goal that motivates using statistical methods, as this parameter is usually hidden from us. We see only $$Z$$, and must go backwards to try and determine $$\lambda$$. The problem is difficult because there is no one-to-one mapping from $Z$ to $\lambda$. 

Bayesian inference is concerned with *beliefs* about $\lambda$ Rather than try to guess $\lambda$ exactly, we only talk about what $\lambda$ is likely to be by assigning a probability distribution to $\lambda$.
