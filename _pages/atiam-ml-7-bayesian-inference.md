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

Two alternative interpretations of probability can be considered  

  * **Frequentist** (the more *classical* approach), assumes that probability is the long-run frequency of events. For example, the *probability of plane accidents* is interpreted as the *long-term frequency of plane accidents*. This becomes harder to interpret when events have no long-term frequency of occurrences. Interestingly, in that case (eg. probability in an election, which happens only once) frequentists consider alternative realities and that across all these realities, the frequency of occurrences defines the probability. 
  * **Bayesian** interprets probability as measure of *believability in an event*. Therefore, a probability is measure of *belief*, or confidence, of an event occurring. Interestingly, this definition leaves room for conflicting beliefs between individuals, based on the different *information* they have about the world. Hence, bayesian inference is mostly based on updating your beliefs after considering new evidence, which differs from more traditional statistical inference by preserving *uncertainty*.

To align with probability notation, we denote a belief about event $$A$$ as $$P\left(A\right)$$, called the *prior probability* of an event to occur. We denote the updated belief as $$ P\left( A \mid X \right) $$, interpreted as the probability of $$A$$ *given* the new evidence $$X$$, called the *posterior probability*. The prior beliefis not completely removed after seeing new evidence $$X$$, but we *re-weight the prior* to incorporate new evidence (i.e. we put more weight, or confidence, on some beliefs versus others). By introducing prior uncertainty about events, we admit that any guess we make can be wrong. However, with more and more instances of evidence, our prior belief is *washed out* by the new evidence. As we gather an *infinite* amount of evidence $$N \rightarrow \infty$$, the Bayesian results (often) align with frequentist results. Hence for small $$N$$, inference is *unstable*, where frequentist estimates have more variance and larger confidence intervals. However, by introducing a prior, and returning probabilities, we *preserve the uncertainty* that reflects the instability on a small $$N$$ dataset.  

Updating the *prior belief* to obtain our *posterior belief* is done via the the Bayes' Theorem

$$
\begin{equation}
 P\left( A \mid X \right) \propto \frac{ P\left(X \mid A\right) P\left(A\right) } {P\left(X\right) }
\end{equation}
$$

We see that our posterior belief of event $$A$$ given the new evidence $$X$$ is proportional to ($$\propto$$) the *likelihood* of observing this particular evidence $$X$$ given the event $$A$$ multiplied by our prior belief in that particular event $$A$$.

#### 7.1 - Bayesian inference

Suppose we have coin and want to estimate the probability of heads ($$p$$) for it. The coin is Bernoulli distributed:

$$ 
\begin{equation}
\phi(x)= p^x (1-p)^{(1-x)} 
\end{equation}
$$

where $$x$$ is the outcome, *1* for heads and *0* for tails. Based on $$n$$ *independent* flips, we have the likelihood:

$$ 
\begin{equation}
\mathcal{L}(p|\mathbf{x})= \prod_{i=1}^n p^{ x_i }(1-p)^{1-x_i} 
\end{equation}
$$

(the independent-trials assumption allows us to just substituted everything into $$ \phi(x)$$). 

The idea of *maximum likelihood* will be to maximize this as the function of $$p$$ after given all of the $$x_i$$ data. This means that our estimator, $$\hat{p}$$, is a function of the observed $$x_i$$ data, and as such, is a random variable with its own distribution.

**Defining the estimator**

The only way to know for sure that our estimator is correctly defined is to check if the estimator is unbiased, namely, if

$$ \mathbb{E}(\hat{p}) = p $$

**Exercise**
<div markdown = "1">

  1. Compute the *log-likelihood* $$J=\log(\mathcal{L}(p \mid \mathbf{x}))$$ of our given problem
  2. Based on this, compute its derivative $$ \frac{dJ}{dp} $$
  3. Solve it to find the estimator $$\hat{p}$$
  4. Verify that this estimator is unbiased $$ \mathbb{E}(\hat{p}) = p $$)
  5. Compute the variance of the estimator $$ \mathbb{E}\left(\hat{p}^2\right) $$

</div>{: .notice--info}  

**Solution**
<div markdown = "1">

Because this problem is simple, we can solve for this in general noting that since $$x=0$$ or $$x=1$$, the terms in the product of $$\mathcal{L}$$ above are either $$p$$, if $$x_i=1$$ or $$1-p$$ if $$x_i=0$$. This means that we can write

$$ 
\begin{equation}
\mathcal{L}(p|\mathbf{x})= p^{\sum_{i=1}^n x_i}(1-p)^{n-\sum_{i=1}^n x_i} 
\end{equation}
$$

with the corresponding *log-likelihood* defined as

$$ 
\begin{equation}
J=\log(\mathcal{L}(p|\mathbf{x})) =  \log(p)  \sum_{i=1}^n x_i +   \log(1-p) \left(n-\sum_{i=1}^n x_i\right)
\end{equation}
$$ 

Taking the derivative of this gives:

$$  
\begin{equation}
\frac{dJ}{dp} = \frac{1}{p}\sum_{i=1}^n x_i + \frac{(n-\sum_{i=1}^n x_i)}{p-1} 
\end{equation}
$$

and solving this leads to

$$  
\begin{equation}
\hat{p} = \frac{1}{ n} \sum_{i=1}^n x_i 
\end{equation}
$$

This is our *estimator* for $p$. To check if this estimator is biased, we compute its expectation:

$$ 
\begin{equation}
\mathbb{E}\left(\hat{p}\right) =\frac{1}{n}\sum_i^n \mathbb{E}(x_i) = \frac{1}{n} n \mathbb{E}(x_i) 
\end{equation}
$$

by linearity of the expectation and where

$$
\begin{equation}
\mathbb{E}(x_i)  = p
\end{equation}
$$

Therefore,

$$ 
\begin{equation}
\mathbb{E}\left(\hat{p}\right) =p 
\end{equation}
$$

This means that the esimator is unbiased. This is good news. We almost always want our estimators to be unbiased. Similarly, 

$$ 
\begin{equation}
\mathbb{E}\left(\hat{p}^2\right) = \frac{1}{n^2} \mathbb{E}\left[\left(  \sum_{i=1}^n x_i \right)^2 \right]
\begin{equation}
$$

and where

$$
\begin{equation}
\mathbb{E}\left(x_i^2\right) =p
\end{equation}
$$

and by the independence assumption,

$$
\begin{equation}
\mathbb{E}\left(x_i x_j\right) =\mathbb{E}(x_i)\mathbb{E}( x_j) =p^2
\end{equation}
$$

Thus,

$$ 
\begin{equation}
\mathbb{E}\left(\hat{p}^2\right) =\left(\frac{1}{n^2}\right) n 
\left[
p+(n-1)p^2
\right]
\end{equation}
$$

So, the variance of the estimator, $\hat{p}$ is the following:

$$ 
\begin{equation}
\sigma_\hat{p}^2 = \mathbb{E}\left(\hat{p}^2\right)- \mathbb{E}\left(\hat{p}\right)^2  = \frac{p(1-p)}{n} 
\end{equation}
$$

Note that the $n$ in the denominator means that the variance asymptotically goes to zero as $n$ increases (i.e. we consider more and more samples). This is good news also because it means that more and more coin flips leads to a better estimate of the underlying $p$.

Unfortunately, this formula for the variance is practically useless because we have to know $p$ to compute it and $p$ is the parameter we are trying to estimate in the first place! But, looking at $ \sigma_\hat{p}^2 $, we can immediately notice that if $p=0$, then there is no estimator variance because the outcomes are guaranteed to be tails. Also, the maximum of this variance, for whatever $n$, happens at $p=1/2$. This is our worst case scenario and the only way to compensate is with more samples (i.e. larger $n$). 
</div>{: .notice--success}  

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
