---
layout: single
permalink: /atiam-ml-10-data-complexity/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

{% include toc %}

# Data complexity

The present tutorials covers .

# Reference slides

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.10.Data.Complexity.pdf)

The corresponding slides cover

  - Pitfalls of machine learning
  - Data complexity
  
# Tutorial 

## 10.0 - Curse and generalization

<div markdown = "1">

**Curse of dimensionality**

One of the biggest challenges of designing a good classifier for solving a ***Statistical Pattern Classification*** problem is to estimate the underlying parameters to fit the model - given that the forms of the underlying probability distributions are known. The larger the number of parameters becomes, the more difficult it naturally is to estimate those parameters accurately (***Curse of Dimensionality***) from a limited number of training samples.  

In order to avoid the ***Curse of Dimensionality***, pattern classification is often accompanied by ***Dimensionality Reduction***, which also has the nice side-effect of increasing the computational performance.
Common techniques are projection-based, such as ***Principal Component Analysis (PCA)*** (unsupervised) or ***Linear Discriminant (LDA)*** (supervised). It shall be noted though that regularization in classification models such as Logistic Regression, Support Vector Machines, or Neural Networks is to be preferred over using dimensionality reduction to avoid overfitting. However, dimensionality reduction is still a useful data compression technique to increase computational efficiency and data storage problems.

An alternative to a projection-based dimensionality reduction approach is the so-called ***Feature Selection***, and in this article, we will take a look at some of the established algorithms to tackle this combinatorial search problem. Note that those algorithms are considered as "subpoptimal" in contrast to an ***exhaustive search***, which is often computationally not feasible, though.

Therefore, the goal of the presented ***sequential selection algorithms*** is to reduce the feature space $D = {x_1, x_2, x_n}$ to a subset of features $D - n$ in order to improve or optimize the **computational performance** of the classifier and avoid the ***Curse of Dimensionality***.  
The goal is to select a "sufficiently reduced" subset from the feature space $D$ "without significantly reducing" the performance of the classifier. In the process of choosing an "optimal" feature subset of size $k$, a so-called ***Criterion Function***, which typically, simply, and intuitively assesses the ***recognition rate*** of the classifier.

F. Ferri, P. Pudil, M. Hatef, and J. Kittler investigated the performance of different ***Sequential Selection Algorithms*** for  ***Feature Selection*** on different scales and reported their results in a nice research article: *"[Comparative Study of Techniques for Large Scale Feature Selection](http://citeseerx.ist.psu.edu/viewdoc/download;jsessionid=02CB16CB1C28EA6CB57E212861CFB180?doi=10.1.1.24.4369&rep=rep1&type=pdf)," Pattern Recognition in Practice IV, E. Gelsema and L. Kanal, eds., pp. 403-413. Elsevier Science B.V., 1994.*  
Choosing an "appropriate" algorithm really depends on the problem - the size and desired recognition rate and computational performance. Thus, I want to encourage you to take (at least) a brief look at their paper and the results they obtained from experimenting with different problems feature space dimensions.

**Model generalization**

Fitting a model to our training data is one thing, but how do we know that it generalizes well to unseen data? How do we know that it doesn’t simply memorize the data we fed it and fails to make good predictions on future samples, samples that it hasn't seen before? And how do we select a good model in the first place?

Let us summarize the main points why we evaluate the predictive performance of a model:

1. We want to estimate the generalization accuracy, the predictive performance of our model on future (unseen) data.
2. We want to increase the predictive performance by tweaking the learning algorithm and selecting the best performing model from a given hypothesis space.
3. We want to identify the machine learning algorithm that is best-suited for the problem at hand; thus, we want to compare different algorithms, selecting the best-performing one as well as the best performing model from the algorithm's hypothesis space.

Of course, we want to estimate the future performance of a model as accurately as possible. However, if there’s one key take-away message from this article, it is that biased performance estimates are perfectly okay in model selection and algorithm selection if the bias affects all models equally. If we rank different models or algorithms against each other in order to select the best-performing one, we only need to know the "relative" performance. For example, if all our performance estimates are pessimistically biased, and we underestimate their performances by 10%, it wouldn’t affect the ranking order.

</div>{: .notice--blank}

## 10.1 - Dimensionality reduction

<div markdown = "1">

**Principal Component Analysis (PCA)**
A linear transformation technique that is commonly used to project a dataset (without utilizing class labels) onto a new feature space or feature subspace (for dimensionality reduction) where the new component axes are the directions that maximize the variance/spread of the data.

- [Implementing a Principal Component Analysis (PCA) in Python step by step](http://sebastianraschka.com/Articles/2014_pca_step_by_step.html)

**Linear Discriminant Analysis (LDA)**
A linear transformation technique (related to Principal Component Analysis) that is commonly used to project a dataset onto a new feature space or feature subspace, where the new component axes maximize the spread between multiple classes, or for classification of data.

- [Linear Discriminant Analysis bit by bit](http://sebastianraschka.com/Articles/2014_python_lda.html)

</div>{: .notice--blank}

## 10.2 - Feature selection

<div markdown = "1">

**Feature Scaling and Standardization**
A data pre-processing step for re-scaling features from different measurements to match proportions of a standard normal distribution (unit variance centered at mean=0).

- [About Feature Scaling and Normalization](http://sebastianraschka.com/Articles/2014_about_feature_scaling.html)

The ***Sequential Fortward Selection (SFS)*** is one of the simplest and probably fastest *Feature Selection* algorithms.  
Let's summarize its mechanics in words:  
***SFS*** starts with an empty feature subset and sequentially adds features from the whole input feature space to this subset until the subset reaches a desired (user-specified) size. For every iteration (= inclusion of a new feature), the whole feature subset is evaluated (expect for the features that are already included in the new subset). The evaluation is done by the so-called ***criterion function*** which assesses the feature that leads to the maximum performance improvement of the feature subset if it is included.  
Note that included features are never removed, which is one of the biggest downsides of this algorithm.

</div>{: .notice--blank}

## 10.3 - Overfitting

<div markdown = "1">

***Bias***

When we use the term bias in this article, we refer to the *statistical* bias (in contrast to the bias in a machine learning system). In general terms, the bias of an estimator $$\hat{\beta}$$ is the difference between its expected value $$E[\hat{\beta}]$$ and the true value of a parameter $$\beta$$ being estimated.

$$Bias = E\big[\hat{\beta}\big] - \beta$$

So, if $$E\big[\hat{\beta}\big] - \beta = 0$$, then $$\hat{\beta}$$ is an unbiased estimator of $$\beta$$. More concretely, we compute the prediction bias as the difference between the expected prediction accuracy of our model and the true prediction accuracy. For example, if we compute the prediction accuracy on the training set, this would be an optimistically biased estimate of the absolute accuracy of our model since it would overestimate the true accuracy.

***Variance***

The variance is simply the statistical variance of the estimator $$\hat{\beta}$$ and its expected value $$E[\hat{\beta}]$$

$$\text{Variance} = E\bigg[\big(\hat{\beta} - E[\hat{\beta}]\big)^2\bigg]$$

The variance is a measure of the variability of our model’s predictions if we repeat the learning process multiple times with small fluctuations in the training set. The more sensitive the model-building process is towards these fluctuations, the higher the variance.

</div>{: .notice--blank}

## 10.4 - Model selection

<div markdown = "1">

- ***Hyperparameters:*** Hyperparameters are the *tuning parameters* of a machine learning algorithm — for example, the regularization strength of an L2 penalty in the mean squared error cost function of linear regression, or a value for setting the maximum depth of a decision tree. In contrast, model parameters are the parameters that a learning algorithm fits to the training data -- the parameters of the model itself. For example, the weight coefficients (or slope) of a linear regression line and its bias (or y-axis intercept) term are *model parameters*.

</div>{: .notice--blank}

## 10.5 - Cross-validation

<div markdown = "1">

Cross-validation is a statistical technique to estimate the prediction error rate by splitting the data into training, cross-validation, and test datasets. A prediction model is obtained using the training set, and model parameters are optimized by the cross-validation set, while the test set is held primarily for empirical error estimation.  

It is important to note that the test set should only be used once for evaluating the prediction error of a classifier after training it on the training dataset; repetitive evaluations of different models using the same test dataset would be prone to overfitting.  
A common approach to compare and evaluate different pre-processing techniques and models is cross-validation. Here, we will use a variant called "k-fold cross-validation" in order to compare different preprocessing steps and demonstrate the usefulness of a `Pipeline`.

In k-fold cross-validation, the original training dataset is split into *k* different subsets (the so-called "folds") where 1 fold is retained for testing the classifier and the other k-1 folds are used for training.

E.g., if we'd choose k=4 (4 folds) the classifier will be trained on the remaining using 3 different training set subsets and evaluated on the 4th fold (the test fold). This procedure is then repeated 4 times until every fold has been used as the test set once so that we can eventually calculate the average error rate of our model from the error rate of every iteration, which gives us an idea of how wel

</div>{: .notice--blank}

## 10.6 - GPU Computing

<div markdown = "1">

</div>{: .notice--blank}

# References
