---
layout: single
permalink: /atiam-ml-6-probabilistic-models/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

{% include toc %}

# Probabilistic models

The present tutorials covers .

# Reference slides

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.6.Probabilistic.Models.pdf)

The corresponding slides cover

  - Probabilities and distributions
  - Belief networks  

# Tutorial 

### 5.0 - Simple probabilities

We recall here the simple basics surrounding probabilities. The probability of an event $$a$$ is a real number $$P(a)$$, with $$0 \leq P(a) \leq 1$$, knowing that $$P(true)=1$$ and $$P(false)=0$$. The probability of two events occuring simultaneously is defined as $$P\left(a \wedge b \right)$$. Therefore, the probability of one event **or** the other occuring is defined as
$$
\begin{equation}
P\left(a \vee b \right) = P(a) + P(b) - P\left(a \wedge b \right)
\end{equation}
$$

The *conditional probability* of an event $$a$$ occuring *given* another event $$b$$ is denoted $$P \left(a \mid b \right)$$ and is defined as
$$
\begin{equation}
P \left(a \mid b \right) = \frac{P \left(a , b \right)}{P \left(b \right)}
\end{equation}
$$

This can be understood as the probability of event $$a$$ to occur if we restrict the world of possibilities to event $$b$$.  

The *chain rule* defines the probabilities of a set of events to co-occur simultaneously
$$
\begin{equation}
P \left(x_{1},...,x_{n} \right) = \prod_{i=n}^{1}{P \left(x_{i}\mid x_{i-1},..., x_{1} \right)}
\end{equation}
$$

Finally, we say that two events are independent if $$P(a\mid b) = P(a)$$.

## Probability Distributions


Let $$Z$$ be a random variable associated with a *probability distribution function* that assigns probabilities to the different outcomes $$Z$$ can take. We can divide random variables into three classifications:

-   **$$Z$$ is discrete**: Discrete random variables may only assume values on a specified list. 

-   **$$Z$$ is continuous**: Continuous random variable can take on arbitrarily exact values. 

- **$$Z$$ is mixed**: Mixed random variables assign probabilities to both discrete and continuous random variables, (i.e. a combination of the above two categories). 

#### Expected Value
The expected value $$E\left[X\right]$$ for a given probability distribution can be described as "the mean value for many repeated samples from that distribution." As the number of repeated observation goes to infinity, the difference between the average outcome and the expected value becomes arbitrarily small.

##### Discrete Case
If $$Z$$ is discrete, then its distribution is called a *probability mass function*, which measures the probability $$Z$$ takes on the value $$k$$, denoted $$P(Z=k)$$. Let's introduce one of the (many) useful probability mass functions. We say $$Z$$ is *Poisson*-distributed if:

$$
\begin{equation}
P\left(Z = k\right) =\frac{ \lambda^k e^{-\lambda} }{k!}, \; \; k \in \mathbb{N^{+}} 
\end{equation}
$$

$$\lambda \in \mathbb{R}$$ is a parameter of the distribution that controls its shape (usually termed the *intensity* of the Poisson distribution). By increasing $$\lambda$$, we add more probability to larger values. One can describe $\lambda$ as the *intensity* of the Poisson distribution. If a random variable $Z$ has a Poisson mass distribution, we denote it by

$$
\begin{equation}
Z \sim \text{Poi}(\lambda) 
\end{equation}
$$

One useful property of the Poisson distribution is that its expected value is equal to its parameter, i.e.:

$$E\large[ \;Z\; | \; \lambda \;\large] = \lambda $$

Below, we plot the probability mass distribution for different $\lambda$ values.

##### Continuous Case
A continuous random variable has a *probability density function*. An example of continuous random variable is a random variable with *exponential density*

$$
\begin{equation}
f_Z(z | \lambda) = \lambda e^{-\lambda z }, \;\; z\ge 0
\end{equation}
$$

When a random variable $Z$ has an exponential distribution with parameter $\lambda$, we say *$Z$ is exponential*

$$Z \sim \text{Exp}(\lambda)$$

Given a specific $\lambda$, the expected value of an exponential random variable is equal to the inverse of $\lambda$, that is:

$$E[\; Z \;|\; \lambda \;] = \frac{1}{\lambda}$$

** Exercise **

<div markdown="1">

1. Code the Poisson probability mass function
2. Code the exponential probability density functions 
3. Try these distributions with different $\lambda$ values. 
4. How to generate a random variable that follows one of these distributions ?

</div>
