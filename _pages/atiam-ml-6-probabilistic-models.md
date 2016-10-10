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
