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

#### 5.0 - Bayesian framework

The Bayesian world-view interprets probability as measure of *believability in an event*, that is, how confident we are in an event occurring. To explicit this idea, we need to consider an alternative interpretation of probability: *Frequentist*, known as the more *classical* version of statistics, assumes that probability is the long-run frequency of events. For example, the *probability of plane accidents* under a frequentist philosophy is interpreted as the *long-term frequency of plane accidents*. This makes logical sense for many probabilities of events, but becomes more difficult to understand when events have no long-term frequency of occurrences. Consider: we often assign probabilities to outcomes of presidential elections, but the election itself only happens once! Frequentists get around this by invoking alternative realities and saying across all these realities, the frequency of occurrences defines the probability. 

Bayesians, on the other hand, have a more intuitive approach. Bayesians interpret a probability as measure of *belief*, or confidence, of an event occurring. Beliefs between 0 and 1 allow for weightings of other outcomes. This is also interesting, as this definition leaves room for conflicting beliefs between individuals. Different individuals have different beliefs of events occurring, because they possess different *information* about the world. Bayesian inference is mostly based on updating your beliefs after considering new evidence. Bayesian inference differs from more traditional statistical inference by preserving *uncertainty*. At first, this sounds like a bad statistical technique. Isn't statistics all about deriving *certainty* from randomness? To reconcile this, we need to start thinking like Bayesians.

To align with traditional probability notation, we denote our belief about event $$A$$ as $$P\left(A\right)$$. We call this quantity the *prior probability* of an event to occur. We denote our updated belief as $$ P\left( A \mid X \right) $$, interpreted as the probability of $A$ *given* the evidence $X$. We call the updated belief the *posterior probability* so as to contrast it with the prior probability. 

We do not completely discard the prior belief after seeing new evidence $X$, but we *re-weight the prior* to incorporate new evidence (i.e. we put more weight, or confidence, on some beliefs versus others). By introducing prior uncertainty about events, we admit that any guess we make is potentially very wrong. After observing data, evidence, or other information, we update our beliefs, and our guess becomes *less wrong*.

** Incorporating evidence **

As we acquire more and more instances of evidence, our prior belief is *washed out* by the new evidence. Denote $$N$$ as the number of instances of evidence we possess. As we gather an *infinite* amount of evidence, say as $$N \rightarrow \infty$$, our Bayesian results (often) align with frequentist results. Hence for small $N$, inference is *unstable*, where frequentist estimates have more variance and larger confidence intervals. This is where Bayesian analysis excels. By introducing a prior, and returning probabilities (instead of a scalar estimate), we *preserve the uncertainty* that reflects the instability of statistical inference of a small $N$ dataset. 

Frequentist methods are still largely useful in tools such as least squares linear regression, LASSO regression, and expectation-maximization algorithms. Bayesian methods complement these techniques by solving problems that these approaches cannot, or by illuminating the underlying system with more flexible modeling. 

** Developing Bayesian framework **

We are interested in beliefs, which can be interpreted as probabilities by thinking Bayesian. We have a *prior* belief in event $A$, beliefs formed by previous information. Secondly, we observe some evidence and we want to update our belief to incorporate this. We call this new belief the *posterior* probability. Updating our belief is done via the following equation, known as the Bayes' Theorem

$$
\begin{equation}
 P\left( A \mid X \right) \propto \frac{ P\left(X \mid A\right) P\left(A\right) } {P\left(X\right) }
\end{equation}
$$

Hence, we see that our posterior belief of event $$A$$ given the new evidence $$X$$ is proportional to ($$\propto$$) the *likelihood* of observing this particular evidence $$X$$ given the event $$A$$ multiplied by our prior belief in that event $$A$$.

** But what is $\lambda \;$? **

The parameter, $$\lambda$$ is usually the goal that motivates using statistical methods, as this parameter is usually hidden from us. We see only $$Z$$, and must go backwards to try and determine $$\lambda$$. The problem is difficult because there is no one-to-one mapping from $Z$ to $\lambda$. 

Bayesian inference is concerned with *beliefs* about $\lambda$ Rather than try to guess $\lambda$ exactly, we only talk about what $\lambda$ is likely to be by assigning a probability distribution to $\lambda$.

#### 7.1 - Maximum likelihood

Suppose we have coin and want to estimate the probability of heads ($p$) for it. The coin is Bernoulli distributed:

$$ \phi(x)= p^x (1-p)^{(1-x)} $$

where $x$ is the outcome, *1* for heads and *0* for tails. The $n$ independent flips, we have the likelihood:

$$ \mathcal{L}(p|\mathbf{x})= \prod_{i=1}^n p^{ x_i }(1-p)^{1-x_i} $$

This is basically notation. We have just substituted everything into $ \phi(x)$ under the independent-trials assumption. 

The idea of *maximum likelihood* is to maximize this as the function of $p$ after plugging in all of the $x_i$ data. This means that our estimator, $\hat{p}$ , is a function of the observed $x_i$ data, and as such, is a random variable with its own distribution.

** Defining the estimator **

Note that the mean of the estimator ($\mu$) is pretty close to the true value, but looks can be deceiving. The only way to know for sure is to check if the estimator is unbiased, namely, if

$$ \mathbb{E}(\hat{p}) = p $$

Because this problem is simple, we can solve for this in general noting that since $x=0$ or $x=1$, the terms in the product of $\mathcal{L}$ above are either $p$, if $x_i=1$ or $1-p$ if $x_i=0$. This means that we can write

$$ \mathcal{L}(p|\mathbf{x})= p^{\sum_{i=1}^n x_i}(1-p)^{n-\sum_{i=1}^n x_i} $$

with corresponding log as

$$ J=\log(\mathcal{L}(p|\mathbf{x})) =  \log(p)  \sum_{i=1}^n x_i +   \log(1-p) \left(n-\sum_{i=1}^n x_i\right)$$ 

Taking the derivative of this gives:

$$  \frac{dJ}{dp} = \frac{1}{p}\sum_{i=1}^n x_i + \frac{(n-\sum_{i=1}^n x_i)}{p-1} $$

and solving this leads to

$$  \hat{p} = \frac{1}{ n} \sum_{i=1}^n x_i $$

This is our *estimator* for $p$. Up til now, we have been using `sympy` to solve for this based on the data $x_i$ but now we have it generally and don't have to solve for it again. To check if this estimator is biased, we compute its expectation:

$$ \mathbb{E}\left(\hat{p}\right) =\frac{1}{n}\sum_i^n \mathbb{E}(x_i) = \frac{1}{n} n \mathbb{E}(x_i) $$

by linearity of the expectation and where

$$\mathbb{E}(x_i)  = p$$

Therefore,

$$ \mathbb{E}\left(\hat{p}\right) =p $$

This means that the esimator is unbiased. This is good news. We almost always want our estimators to be unbiased. Similarly, 

$$ \mathbb{E}\left(\hat{p}^2\right) = \frac{1}{n^2} \mathbb{E}\left[\left(  \sum_{i=1}^n x_i \right)^2 \right]$$

and where

$$ \mathbb{E}\left(x_i^2\right) =p$$

and by the independence assumption,

$$ \mathbb{E}\left(x_i x_j\right) =\mathbb{E}(x_i)\mathbb{E}( x_j) =p^2$$

Thus,

$$ \mathbb{E}\left(\hat{p}^2\right) =\left(\frac{1}{n^2}\right) n 
\left[
p+(n-1)p^2
\right]
$$

So, the variance of the estimator, $\hat{p}$ is the following:

$$ \sigma_\hat{p}^2 = \mathbb{E}\left(\hat{p}^2\right)- \mathbb{E}\left(\hat{p}\right)^2  = \frac{p(1-p)}{n} $$

Note that the $n$ in the denominator means that the variance asymptotically goes to zero as $n$ increases (i.e. we consider more and more samples). This is good news also because it means that more and more coin flips leads to a better estimate of the underlying $p$.

Unfortunately, this formula for the variance is practically useless because we have to know $p$ to compute it and $p$ is the parameter we are trying to estimate in the first place! But, looking at $ \sigma_\hat{p}^2 $, we can immediately notice that if $p=0$, then there is no estimator variance because the outcomes are guaranteed to be tails. Also, the maximum of this variance, for whatever $n$, happens at $p=1/2$. This is our worst case scenario and the only way to compensate is with more samples (i.e. larger $n$). 

All we have computed is the mean and variance of the estimator. In general, this is insufficient to characterize the underlying probability density of $\hat{p}$, except if we somehow knew that  $\hat{p}$ were normally distributed. This is where the powerful [*central limit theorem*](http://mathworld.wolfram.com/CentralLimitTheorem.html) comes in. The form of the estimator, which is just a mean estimator, implies that we can apply this theorem and conclude that  $\hat{p}$ is normally distributed. However, there's a wrinkle here: the theorem tells us that  $\hat{p}$ is asymptotically normal, it doesn't quantify how many samples $n$ we need to approach this asymptotic paradise. In our simulation this is no problem since we can generate as much data as we like, but in the real world, with a costly experiment, each sample may be precious. In the following, we won't apply this theorem and instead proceed analytically.

** Full density for the estimator **

To write out the full density for $\hat{p}$, we first have to ask what is the probability that the estimator will equal a specific value and the tally up all the ways that could happen with their corresponding probabilities. For example, what is the probability that

$$  \hat{p} = \frac{1}{n}\sum_{i=1}^n x_i  = 0 $$

This can only happen one way: when $x_i=0 \hspace{0.5em} \forall i$. The probability of this happening can be computed from the density

$$ f(\mathbf{x},p)= \prod_{i=1}^n \left(p^{x_i} (1-p)^{1-x_i}  \right) $$

$$ f\left(\sum_{i=1}^n x_i  = 0,p\right)= \left(1-p\right)^n  $$

Likewise, if $\lbrace x_i \rbrace$ has one $i^{th}$  value equal to one, then

$$ f\left(\sum_{i=1}^n x_i  = 1,p\right)= n p \prod_{i=1}^{n-1} \left(1-p\right)$$

where the $n$ comes from the $n$ ways to pick one value equal to one from the $n$ elements $x_i$. Continuing this way, we can construct the entire density as

$$ f\left(\sum_{i=1}^n x_i  = k,p\right)= \binom{n}{k} p^k  (1-p)^{n-k}  $$

where the term on the left is the binomial coefficient of $n$ things taken $k$ at a time. This is the binomial distribution and it's not the density for $\hat{p}$, but rather for $n\hat{p}$. We'll leave this as-is because it's easier to work with below. We just have to remember to keep track of the $n$ factor.

#### 7.2 - Classifying with MLE

Popular applications for Maximum Likelihood Estimates are the typical statistical pattern classification tasks, and in the past, I posted some [examples](https://github.com/rasbt/pattern_classification#param) using Bayes' classifiers for which the **probabilistic models and parameters were known**. In those cases, the design of the classifier was rather easy, however, in real applications, we are rarely given this information; this is where the Maximum Likelihood Estimate comes into play.

However, the Maximum Likelihood Estimate still **requires partial knowledge** about the problem: We have to assume that the **model of the class conditional densities is known** (e.g., that the data follows typical Gaussian distribution). In contrast, non-parametric approaches like the Parzen-window technqiue do not require prior information about the distribution of the data (I will discuss this technique in more detail in a future article, the IPython notebook is already in preparation).  

**To summarize the problem:** Using MLE, we want to estimate the values of the parameters of a given distribution for the class-conditional densities, for example, the *mean* and *variance* assuming that the class-conditional densities are *normal*  distributed (Gaussian) with $p(\pmb x \; | \; \omega_i) \sim N(\mu, \sigma^2)$.

#### 7.3 - Parameters known

Imagine that we want to classify data consisting of two-dimensional patterns, $\pmb{x} = [x_1, x_2]^t$ that could belong to 1 out of 3 classes $\omega_1,\omega_2,\omega_3$. 

Let's assume the following information about the model and the parameters are known:

####model: continuous univariate normal (Gaussian) model for the class-conditional densities


$ p(\pmb x | \omega_j) \sim N(\pmb \mu|\Sigma) $

$ p(\pmb x | \omega_j) \sim \frac{1}{(2\pi)^{d/2} \; |\Sigma|^{1/2}} exp \bigg[ -\frac{1}{2}(\pmb x - \pmb \mu)^t \Sigma^{-1}(\pmb x - \pmb \mu) \bigg]$

$p([x_1, x_2]^t |\omega_1) ∼ N([0,0]^t,3I), \\
p([x_1, x_2]^t |\omega_2) ∼ N([9,0]^t,3I), \\
p([x_1, x_2]^t |\omega_3) ∼ N([6,6]^t,4I),$

** Means of the sample distributions for 2-dimensional features **

$ \pmb{\mu}_{\,1} = \bigg[ 
\begin{array}{c}
0 \\
0 \\
\end{array} \bigg] $,
$ \; \pmb{\mu}_{\,2} = \bigg[ 
\begin{array}{c}
9 \\
0 \\
\end{array} \bigg] $,
$ \; \pmb{\mu}_{\,3} = \bigg[ 
\begin{array}{c}
6 \\
6 \\
\end{array} \bigg] $


** Covariance matrices for the statistically independend and identically distributed ('i.i.d') features **

$ \Sigma_i = \bigg[ 
\begin{array}{cc}
\sigma_{11}^2 & \sigma_{12}^2\\
\sigma_{21}^2 & \sigma_{22}^2 \\
\end{array} \bigg] \\  
\Sigma_1 = \bigg[ 
\begin{array}{cc}
3 & 0\\
0 & 3 \\
\end{array} \bigg] \\
\Sigma_2 = \bigg[ 
\begin{array}{cc}
3 & 0\\
0 & 3 \\
\end{array} \bigg] \\
\Sigma_3 = \bigg[ 
\begin{array}{cc}
4 & 0\\
0 & 4 \\
\end{array} \bigg] \\$

** Equal prior probabilities **
$P(\omega_1\; |\; \pmb x) \; = \;  P(\omega_2\; |\; \pmb x) \; = \; P(\omega_3\; |\; \pmb x) \; = \frac{1}{3}$

** Exercise **
<div markdown = "1">

  1. Generate some data (sample from the multivariate Gaussians)
  2. Plot the class-dependent data

</div>

Here, our **objective function** is to maximize the discriminant function $g_i(\pmb x)$, which we define as the posterior probability to perform a **minimum-error classification** (Bayes classifier). 

$ g_1(\pmb x) = P(\omega_1 | \; \pmb{x}), \quad  g_2(\pmb{x}) = P(\omega_2 | \; \pmb{x}), \quad  g_3(\pmb{x}) = P(\omega_2 | \; \pmb{x})$

So that our decision rule is to choose the class $\omega_i$ for which $g_i(\pmb x)$ is max., where  
 $ \quad g_i(\pmb{x}) = \pmb{x}^{\,t} \bigg( - \frac{1}{2} \Sigma_i^{-1} \bigg) \pmb{x} + \bigg( \Sigma_i^{-1} \pmb{\mu}_{\,i}\bigg)^t \pmb x + \bigg( -\frac{1}{2} \pmb{\mu}_{\,i}^{\,t}  \Sigma_{i}^{-1} \pmb{\mu}_{\,i} -\frac{1}{2} ln(|\Sigma_i|)\bigg) $
 
 
** Exercise **
<div markdown = "1">

  1. Implement the discriminant function
  2. Implement the decision rule (classifier)
  3. Classify the data generated in the previous exercise
  4. Plot the confusion matrix
  5. Calculate the empirical error

</div>

#### 7.3 - Unknown parameters case

** About the Maximum Likelihood Estimate (MLE) **

In contrast to the first section, let us assume that we only know the number of parameters for the class conditional densities $p (\; \pmb x \; | \; \omega_i)$, and we want to use a Maximum Likelihood Estimation (MLE) to estimate the quantities of these parameters from the training data (*here:* our random sample data).


Given the information about the form of the model - the data is normal distributed - the 2 parameters to be estimated are $\pmb \mu_i$ and $\pmb \Sigma_i$, which are summarized by the   
parameter vector $\pmb \theta_i = \bigg[ \begin{array}{c}
\ \theta_{i1} \\
\ \theta_{i2} \\
\end{array} \bigg]=
\bigg[ \begin{array}{c}
\pmb \mu_i \\
\pmb \Sigma_i \\
\end{array} \bigg]$ 

For the Maximum Likelihood Estimate (MLE), we assume that we have a set of samples $D = \left\{ \pmb x_1, \pmb x_2,..., \pmb x_n \right\} $ that are *i.i.d.* (independent and identically distributed, drawn with probability $p(\pmb x \; | \; \omega_i, \; \pmb \theta_i) $).  
Thus, we can **work with each class separately** and omit the class labels, so that we write the probability density as $p(\pmb x \; | \; \pmb \theta)$ 

** Likelihood of $ \pmb \theta $ **

Thus, the probability of observing $D = \left\{ \pmb x_1, \pmb x_2,..., \pmb x_n \right\} $ is: 
<br>
<br>
$p(D\; | \;  \pmb \theta\;) = p(\pmb x_1 \; | \; \pmb \theta\;)\; \cdot \; p(\pmb x_2 \; | \;\pmb \theta\;) \; \cdot \;...  \; p(\pmb x_n \; | \; \pmb \theta\;) = \prod_{k=1}^{n} \; p(\pmb x_k \pmb \; | \; \pmb \theta \;)$  
<br>
Where $p(D\; | \;  \pmb  \theta\;)$ is also called the ***likelihood of $\pmb\ \theta$***.

We are given the information that $p([x_1,x_2]^t) \;∼ \; N(\pmb \mu,\pmb \Sigma) $ (remember that we dropped the class labels, since we are working with every class separately).

And the mutlivariate normal density is given as:
$\quad \quad p(\pmb x) = \frac{1}{(2\pi)^{d/2} \; |\Sigma|^{1/2}} exp \bigg[ -\frac{1}{2}(\pmb x - \pmb \mu)^t \Sigma^{-1}(\pmb x - \pmb \mu) \bigg]$

So that  
$p(D\; | \;  \pmb \theta\;) = \prod_{k=1}^{n} \; p(\pmb x_k \pmb \; | \; \pmb \theta \;) =  \prod_{k=1}^{n} \; \frac{1}{(2\pi)^{d/2} \; |\Sigma|^{1/2}} exp \bigg[ -\frac{1}{2}(\pmb x - \pmb \mu)^t \Sigma^{-1}(\pmb x - \pmb \mu) \bigg]$

and the log of the multivariate density

$ l(\pmb\theta) =  \sum\limits_{k=1}^{n} - \frac{1}{2}(\pmb x - \pmb \mu)^t \pmb \Sigma^{-1} \; (\pmb x - \pmb \mu) - \frac{d}{2} \; ln \; 2\pi - \frac{1}{2} \;ln \; |\pmb\Sigma|$

** Maximum Likelihood Estimate (MLE) **

In order to obtain the MLE $\boldsymbol{\hat{\theta}}$, we maximize $l (\pmb  \theta)$, which can be done via differentiation:

with 
$\nabla_{\pmb \theta} \equiv \begin{bmatrix}  
\frac{\partial \; }{\partial \; \theta_1} \\ 
\frac{\partial \; }{\partial \; \theta_2}
\end{bmatrix} = \begin{bmatrix} 
\frac{\partial \; }{\partial \; \pmb \mu} \\ 
\frac{\partial \; }{\partial \; \pmb \sigma}
\end{bmatrix}$

$\nabla_{\pmb \theta} l = \sum\limits_{k=1}^n \nabla_{\pmb \theta} \;ln\; p(\pmb x| \pmb \theta) = 0 $

** MLE of the mean **

After doing the differentiation, we find that the MLE of the parameter $\pmb\mu$ is given by the equation:  
${\hat{\pmb\mu}} = \frac{1}{n} \sum\limits_{k=1}^{n} \pmb x_k$

As you can see, this is simply the mean of our dataset, so we can implement the code very easily and compare the estimate to the actual values for $\pmb \mu$.

** MLE of the covariance matrix $\pmb \Sigma$ **

Analog to $\pmb \mu$ we can find the equation for the $\pmb\Sigma$ via differentiation - okay the equations are a little bit more involved, but the approach is the same - so that we come to this equation:  

${\hat{\pmb\Sigma}} = \frac{1}{n} \sum\limits_{k=1}^{n} (\pmb x_k - \hat{\mu})(\pmb x_k - \hat{\mu})^t$

which we will also implement in Python code, and then compare to the acutal values of ${\pmb\Sigma}$.

** Classification using our estimated parameters **

Using the estimated parameters $\pmb \mu_i$ and $\pmb \Sigma_i$, which we obtained via MLE, we calculate the error on the sample dataset again. 
