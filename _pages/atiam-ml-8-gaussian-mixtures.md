---
layout: single
permalink: /atiam-ml-8-gaussian-mixtures/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

<script language="JavaScript" type="text/javascript" src="https://code.jquery.com/jquery-latest.min.js"></script>
<script>
$(document).ready(function(){
    $(".abuttons").click(function () {
        var idname= $(this).data('divid');
        $("#"+idname).show("slow");
    });
    $("#div1").hide();
    $("#div2").hide();
    $("#div3").hide();
    $("#divq1").hide();
    $("#divq2").hide();
    $("#divq3").hide();
});
</script>

{% include toc %}

# Gaussian Mixture Models

The present tutorials covers .

# Reference slides

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.8.Gaussian.Mixture.Models.pdf)

The corresponding slides cover

  - Expectation Maximization
  - Mixture models  
  
## Tutorial 

<div markdown="1">
Expectation Maximization (EM) is a powerful technique for creating maximum likelihood estimators when the variables are difficult to separate. Here, we set up a Gaussian mixture experiment with two Gaussians and derive the corresponding estimators of their means using EM.
</div>{: .notice--blank}

#### 8.1 - Measuring from Unseen Groups 

<div markdown="1">
Suppose we have a population with two distinct groups of individuals with different heights. If we randomly pick an individual from the population, we don't know which group the individual belongs to. The goal is to estimate the mean heights of the two distinct groups when we have an unlabeled distribution sampled from both groups.

Both groups $$g_{1},g_{2}$$ are normally distributed, around two different means

$$ 
\begin{equation}
\mathcal{N}_{g_{i}}\left(x\right) =\mathcal{N}(x; \mu_{g_{i}},\sigma) 
\end{equation}
$$

Note that we fix the standard deviation $$\sigma$$ to be the same for both groups, but the means ($$\mu_{g_{1}},\mu_{g_{2}}$$) are different. The problem is to estimate the means given that you can't directly know which group you are picking from.

Then we can write the joint density for this experiment as

$$ 
\begin{equation}
f_{\mu_{g_{1}},\mu_{g_{2}}}(x,z)=  \frac{1}{2} \mathcal{N}_{g_{1}}(x) ^z \mathcal{N}_{g_{2}}(x) ^{1-z} 
\end{equation}
$$

where $$z=1$$ if we pick from group **$${g_{1}}$$** and $$z=0$$ for group **$${g_{2}}$$**. Note that the $$1/2$$ comes from the 50/50 chance of picking either group.  Unfortunately, since we do not measure the $$z$$ (latent) variable, we have to integrate it out of our density function to account for this handicap. Thus,

$$ 
\begin{equation}
f_{\mu_{g_{1}},\mu_{g_{2}}}(x)=  \frac{1}{2}  \mathcal{N}_{g_{1}}(x)+\frac{1}{2}  \mathcal{N}_{g_{2}}(x)
\end{equation}
$$

Now, since $$n$$ trials are independent, we can write out the likelihood:

$$ 
\begin{equation}
\mathcal{L}(\mu_{g_{1}},\mu_{g_{2}}|\mathbf{x})= \prod_{i=1}^n f_{\mu_{g_{1}},\mu_{g_{2}}}(x_{i})
\end{equation}
$$

We recall that the independent trials assumptions means that the joint probability is just the product of the individual probabilities. Usually, *maximum likelihood* allows to maximize this as the function of $$\mu_{g_{1}}$$ and $$\mu_{g_{2}}$$ based on all $$x_{i}$$. However, here we do not know which group we are measuring at each trial so we can not just estimate the parameters for each group separately.

</div>{: .notice--blank}

**Exercise**
<div markdown = "1">

  1. Simulate the experiment by sampling two populations
  2. Try different means and see how overlapping regions could be solved.

</div>{: .notice--info}

#### 8.2 - Expectation maximization

<div markdown="1">

The key idea of expectation maximization is that we will pretend to know the hidden $$z$$ value and use a maximum likelihood estimate (this is the *maximization* part), by computing an *expectation* (guess) over the missing variable (in this case, $$z$$). 

As usual, it is easier and more stable use the `log` of the likelihood function. It is useful to keep track of the *incomplete log-likelihood* ($$\log\mathcal{L}$$) since it can be proved that it is monotone increasing and provides a good way to identify coding errors.

</div>{: .notice--blank}

**Expectation step**  

<div markdown="1">

We denote $$\Theta=\left[\mu_{g_{1}},\mu_{g_{2}}\right]$$ as the set of parameters and $$x_{i}$$ the datapoints. The density function of $$z$$ and $$\Theta$$ can be written as the following

$$ 
\begin{equation}
\mathbb{P}(z,\Theta) = \frac{1}{2} \mathcal{N}_{g_{1}}(\Theta) ^ z \mathcal{N}_{g_{2}}(\Theta) ^ {(1-z)} 
\end{equation}
$$

For the expectation part we have to compute $$\mathbb{E}(z \mid \Theta)$$ 

</div>{: .notice--blank}  

**Exercise**
<div markdown="1">

  1. Compute the expression of the expectation $$\mathbb{E}(z \mid \Theta)$$ 
  2. Implement a function that computes it given a set of parameters

</div>{: .notice--info}  

**Solution** [<a href="javascript:void(0)" class="abuttons" data-divid="divq1">Reveal</a>]

<div id="divq1" markdown = "1">

Since $$z\in \lbrace 0,1 \rbrace$$, the expression of $$\mathbb{E}(z \mid \Theta)$$  simplifies easily

$$ 
\begin{equation}
\mathbb{E}(z \mid \Theta) = 1 \cdot \mathbb{P}(z=1 \mid \Theta) + 0 \cdot \mathbb{P}(z=0 \mid \Theta) =  \mathbb{P}(z=1 \mid \Theta)  
\end{equation}
$$

Now, the only thing left is to find $$  \mathbb{P}(z=1 \mid \Theta) $$ which we can do using Bayes rule:

$$  
\begin{equation}
\mathbb{P}(z=1 \mid \Theta)  = \frac{ \mathbb{P}(\Theta \mid z=1)\mathbb{P}(z=1)}{\mathbb{P}(\Theta)} 
\end{equation}
$$

The term in the denominator comes from summing (integrating) out the $$z$$ items in the full joint density $$ \mathbb{P}(z,\Theta) $$

$$ 
\begin{equation}
\mathbb{P}(\Theta) = (\mathcal{N}_{g_{1}}(\Theta) + \mathcal{N}_{g_{2}}(\Theta))\frac{1}{2} 
\end{equation}
$$

and since $$\mathbb{P}(z=1)=1/2$$, we finally obtain

$$  
\begin{equation}
\mathbb{E}(z \mid \Theta) =\mathbb{P}(z=1 \mid \Theta)  = \frac{\mathcal{N}_{g_{1}}(\Theta)}{\mathcal{N}_{g_{1}}(\Theta) + \mathcal{N}_{g_{2}}(\Theta)} 
\end{equation}
$$

</div>{: .notice--success}

**Maximization step**  

<div markdown="1">

Now, given we we have this estimate for $$z_{i}$$,  $$\hat{z}_{i}=\mathbb{E(z \mid \Theta_{i})}$$, we can go back and compute the log likelihood estimate of

$$ 
\begin{equation}
J= \log\prod_{i=1}^{n} \mathbb{P}(\hat{z}_{i},\Theta_{i}) \\ = \sum_{i=1}^{n} \hat{z}_{i}\log \mathcal{N}_{g_{1}}(\Theta_{i}) +(1-\hat{z}_{i})\log \mathcal{N}_{g_{2}}(\Theta_i) +\log(1/2)  
\end{equation}
$$

by maximizing it using basic calculus. 

</div>{: .notice--blank}  

**Exercise**
<div>

  1. Derive the maximization of the log-likelihood
  2. Implement a fonction that performs maximization on a set of data

</div>{: .notice--info}

**Solution** [<a href="javascript:void(0)" class="abuttons" data-divid="divq2">Reveal</a>]

<div id="divq2" markdown = "1">

The trick is to remember that $$\hat{z}_{i}$$ is *fixed*, so we only have to maximize the $$\log$$ parts. This leads to

$$ 
\begin{equation}
\hat{\mu_{g_{1}}} = \frac{\sum_{i=1}^{n} \hat{z}_{i} x_{i}}{\sum_{i=1}^{n}  \hat{z}_{i} }
\end{equation}
$$

and for $$\mu_{g_{2}}$$

$$ 
\begin{equation}
\hat{\mu_{g_{2}}} = \frac{\sum_{i=1}^{n} (1-\hat{z}_{i}) x_{i}}{\sum_{i=1}^{n}  1-\hat{z}_{i} } 
\end{equation}
$$

</div>{: .notice--success}


<div markdown = "1">
Now that we have both the *maximization* step and the *expectation* step ($$\hat{z}_{i}$$), we can simulate the algorithm and compute the estimates for both $$\mu_{a}$$ and $$\mu_{b}$$.

Expectation maximization is a powerful algorithm that is especially useful when it is difficult to de-couple the variables involved in a standard maximum likelihood estimation. Note that convergence to the "correct" maxima is not guaranteed, as we observed here. This is even more pronounced when there are more parameters to estimate (a much more detailed mathematical derivation is available [here](http://crow.ee.washington.edu/people/bulyko/papers/em.pdf)).

</div>{: .notice--blank}  

**Exercise**
<div markdown = "1">

  1. Fill the main loop of the EM algorithm
  2. Plot the evolution of the values for both $$\mu_{a}$$ and $$\mu_{b}$$
  3. Plot the corresponding incomplete likelihood function
  4. Analyze the speed of convergence for the EM algorithm
  5. Plot the error surface (in terms of parameters)
  6. Test your algorithm for different initial values.

</div>{: .notice--info}

