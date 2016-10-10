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

#### 1.0 - Graphical Models
--

Graphical Models are a nice way of visualizing probabilistic models, and also to express the dependencies
that hold between the individual elements. There are several types of graphical models, but the
ones we are interested in (and the ones we mean when we use the term) are ***Bayes Nets*** and ***Hidden
Markov Models*** (HMMs). Graphical models consist of two elements, ***nodes*** and ***arcs***.

The nodes are ***random variables***. Random variables are events that have some probability, and come
in different flavors. If a random variable has exactly two values, like {`on`, `off`} or {`true`, `false`}, they
are ***binary*** (in the latter case ***boolean***). If they have a list of values (something like {`red`, `green`, `blue`}
or {`chocolate`, `vanilla`, `strawberry`, `pistacchio`}), they are ***discrete***. If they have numbers as values,
they are called ***continuous***. 
The ***probabilities*** associated with each of the values of a random variable have to
sum up to $1.0$, i.e., the variable `COLOR` with the values {`red`, `green`, `blue`} could have the respective probabilities {$0.2, 0.5, 0.3$} or
{$0.33, 0.33, 0.33$} associated with the values, but not {$0.8, 0.4, 0.7$}.

Arcs are the directed links between the random variables, and you can think of them as causal relations
(there are other kinds, but it is easiest this way). They denote what influence the parent has on the
child node. This influence is expressed by a conditional probability. 

<img src="pics/bn1.png" width="200px"/>
<div align="center">*Figure 1: A simple graphical model with three random variables*</div>

E.g., in a network like the one in Figure 1, we can say how likely it is that traffic ($T$) is bad, given that the weather ($W$) is rain. A node
$X$ can have several parents, which means that its value is influenced by several factors (traffic could
also be influenced by a Lakers game, $G$). If there are no links between two variables, then they are
***independent of one another***, i.e., whether the Lakers play or not luckily has no influence on the weather
$W$ (the examples in this section are largely influenced by [Russell/Norvig 2003](#refRN)).

#### 1.1 - Bayes Nets
--
<img src="pics/bn2.png" width="450px"/>
<div align="center">*Figure 2: A Bayes Net with three random variables and associated parameters*</div>

If we combine several nodes in a network, we call it a ***Bayes Net***. Let’s look at a very simple example
(Figure 2), inspired by [Russell/Norvig 2003](#refRN). Say we have three random variables, namely the weather
($W$), with values {`sunny`, `rainy`}, traffic ($T$), which can be {`normal`, `bad`, `terrible`} and whether we are
late for a meeting ($L$: {`true`, `false`}).

From pop culture we know that it never rains in southern California, and from our meterological data
(see [section 2.1.1](#secprob)) we know that *never* means 5%. So the probabilities for $W$ are $(0.95, 0.05)$. If we
talk about the probability of a specific outcome of the variables values, we write $P(W =$ `sunny` $) = 0.95$
or shorter $P($ `sunny` $) = 0.95$.

If it rains, traffic tends to get worse, and if traffic is bad, we are more likely to be late for our meeting.
If it is sunny, the traffic behaves different than when it is rainy, so we have to specify the probability of
each value of $T$ for each value of $W$. We do that in a table, where each column is a value for a variable,
$T$ and $W$. Notice that the rows with the same value forW have to sum up to $1.0$. You can imagine that
each value for weather is a state you are in, and the different values for $T$ are options you can choose
from. Some options are more likely than others, but all probability is distributed between them (thus
summing to $1.0$). You cannot choose something that is not there.

Whether I am late for a meeting ($L$) in turn depends on the state of the traffic ($T$), so we have to
specify another table with probabilities for each value of $L$ given each value of $T$. Again you can see
that with worse traffic, our chances of being late increase.
Using the Bayes Net, we can now compute how likely we are to be late if the weather is bad but
traffic is normal, and other interesting things.
