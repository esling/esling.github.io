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

Choosing an "appropriate" machine learning algorithm depends on the problem, the size and desired recognition rate and computational performance. However, all algorithms fall prey to the same secular problems.

1. The curse of dimensionality
2. Poor generalization due to overfitting
3. Cross-validation and cherry picking

**Curse of dimensionality**

One of the biggest challenges for solving machine learning problem is to estimate the underlying parameters to fit the model. Obviously, the larger the number of parameters becomes, the more difficult it is to estimate those parameters accurately from a limited number of training samples, a problem known as the ***curse of dimensionality***. In order to avoid it, learning algorithms are often accompanied by ***dimensionality reduction*** techniques. Common approaches are projection-based, such as ***Principal Component Analysis (PCA)*** (unsupervised) or ***Linear Discriminant (LDA)*** (supervised). It shall be noted though that regularization in classification models such as Logistic Regression, Support Vector Machines, or Neural Networks is to be preferred over using dimensionality reduction to avoid overfitting. An alternative to these approaches is the ***feature selection***. In these, the goal is to reduce the feature space $$D = {x_1, x_2, x_n}$$ to a subset of features $$D - n$$ in order to improve both the *accuracy* and *computational performance* of the algorithms.  The goal is to select a "sufficiently reduced" subset from the feature space $$D$$ "without significantly reducing" the performance of the classifier. In the process of choosing an "optimal" feature subset of size $$k$$, a ***criterion Function*** allows to assess the ***recognition rate*** of the classifier.

**Model generalization and overfitting**

Usually, fitting a model to the training data can be iterated up to a perfect score, but interestingly this usually will lead to a model that performs very poorly on unseen data. In these case, the model is said to **generalize poorly** because of **overfitting**. A simple intuition for this effect is that the model becomes *too specialized* for the training data, and might simply memorize the data we fed it and fails to make good predictions on future samples that it hasn't seen before. However, the goal of machine learning is to provide models that are good at predicting unseen data. Hence, we have to evaluate the predictive performance of our model mainly for

1. Estimating the *generalization accuracy* (predictive performance of our model on unseen data).
2. Increasing the predictive performance by selecting the best performing model from a given hypothesis space.
3. Identifying the algorithm that is best-suited for the problem at hand

Of course, we want to estimate the future performance of a model as accurately as possible. However, biased performance estimates are perfectly okay in model selection and algorithm selection if the bias affects all models equally. If we rank different models or algorithms against each other in order to select the best-performing one, we only need to know the "relative" performance.

**Cross-validation and cherry picking**

Cross-validation is a statistical technique to estimate the prediction error rate by splitting the data into training, cross-validation, and test datasets. A prediction model is obtained using the training set, and model parameters

We will see in the following how to adress these problems and a few useful tricks to do so.

</div>{: .notice--blank}

## 10.1 - Dimensionality reduction

<div markdown = "1">

**Principal Component Analysis (PCA)**  

PCA is a linear transformation technique that is commonly used to project a dataset onto a new feature subspace (for dimensionality reduction) where the new axes are the directions that maximize the variance/spread of the data. The underlying idea is that by doing so, we can reduce the dimensions of the dataset with minimal loss of information.

Listed below are the 6 general steps for performing a principal component analysis, which we will investigate in the following sections.

1. Take a dataset consisting of $$d$$-dimensional samples $$\{x_{1}, x_{2}, \ldots, x_{m}\}$$, where $$x_{i} \in \mathbb{R}^{d}$$
2. Compute the $$d$$-dimensional mean vector (means for every dimension of the whole dataset)
3. Compute the scatter matrix (or covariance matrix) of the whole data set

$$
\begin{equation}
\Sigma = \frac{1}{m} \sum_{i=1}^{m} (x_{i})(x_{i})^{T}
\end{equation}
$$

4. Compute eigenvectors ($$\mathbf{e}_{1}, \mathbf{e}_{2}, \dots, \mathbf{e}_{d}$$) and corresponding eigenvalues ($$\mathbf{\lambda}_{1}, \mathbf{\lambda}_{2}, \dots, \mathbf{\lambda}_{d}$$)
5. Sort the eigenvectors by decreasing eigenvalues and choose $$k$$ eigenvectors with the largest eigenvalues to form a $$d \times k$$ dimensional matrix $$\mathbf{W}$$ (where every column represents an eigenvector)
6. Use this $$d \times k$$ eigenvector matrix to transform the samples onto the new subspace. This can be summarized by the mathematical equation: $$\mathbf{y}=\mathbf{W}^{T} \times \mathbf{x}$$ (where $$\mathbf{x}$$ is a $$d \times 1$$-dimensional vector representing one sample, and $$\mathbf{y}$$ is the transformed $$k \times 1$$-dimensional sample in the new subspace).

</div>{: .notice--blank}

**Exercise**
<div markdown = "1">

1. Implement the PCA algorithm
2. Generate a 3-dimensional dataset following a multivariate Gaussian
3. Evaluate the application of PCA to rotate this data
4. Evaluate the dimensionality reduction by projection

</div>{: .notice--info}

<div markdown = "1">

**Linear Discriminant Analysis (LDA)**
LDA is a linear transformation technique (related to PCA) that is also commonly used to project a dataset onto a new feature subspace. However, this approach is supervised as the new component axes are selected to maximize the spread between multiple classes. More information can be found on the corresponding [Wikipedia page](https://en.wikipedia.org/wiki/Linear_discriminant_analysis)

</div>{: .notice--blank}

## 10.2 - Feature selection

<div markdown = "1">

**Feature Scaling and Standardization**
A data pre-processing step for re-scaling features from different measurements to match proportions of a standard normal distribution (unit variance centered at mean=0).

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

**Resubstitution Validation and the Holdout Method**

The holdout method is inarguably the simplest model evaluation technique. We take our labeled dataset and split it into two parts: A training set and a test set. Then, we fit a model to the training data and predict the labels of the test set. And the fraction of correct predictions constitutes our estimate of the prediction accuracy — we withhold the known test labels during prediction, of course. We really don’t want to train and evaluate our model on the same training dataset (this is called *resubstitution evaluation*), since it would introduce a very optimistic bias due to overfitting. In other words, we can’t tell whether the model simply memorized the training data or not, or whether it generalizes well to new, unseen data. (On a side note, we can estimate this so called *optimism bias* as the difference between the training accuracy and the test accuracy.)   

Typically, the splitting of a dataset into training and test sets is a simple process of *random subsampling*. We assume that all our data has been drawn from the same probability distribution (with respect to each class). And we randomly choose ~2/3 of these samples for our training set and ~1/3 of the samples for our test set. Notice the two problems here?

**Stratification**

We have to keep in mind that our dataset represents a random sample drawn from a probability distribution; and we typically assume that this sample is representative of the true population -- more or less. Now, further subsampling without replacement alters the statistic (mean, proportion, and variance) of the sample. The degree to which subsampling without replacement affects the statistic of a sample is inversely proportional to the size of the sample.

Assuming that the *Iris* dataset is representative of the true population (for instance, assuming that flowers are distributed uniformly in nature), we just created two imbalanced datasets with non-uniform class distributions. The class ratio that the learning algorithm uses to learn the model is “38.0% / 28.0% / 34.0%”. Then, we evaluate a model on a dataset with a class ratio that is imbalanced in the “opposite” direction: “24.0% / 44.0% / 32.0%”. Unless our learning algorithm is completely insensitive to these small perturbations, this is certainly not ideal. The problem becomes even worse if our dataset has a high class imbalance upfront. In the worst-case scenario, the test set may not contain any instance of a minority class at all. Thus, the common practice is to divide the dataset in a stratified fashion. ***Stratification*** simply means that we randomly split the dataset so that each class is correctly represented in the resulting subsets — the training and the test set.

Random subsampling in non-stratified fashion is usually not a big concern if we are working with relatively large and balanced datasets. However, in my opinion, stratified resampling is usually (only) beneficial in machine learning applications. Moreover, stratified sampling is incredibly easy to implement, and Ron Kohavi provides empirical evidence (Kohavi 1995) that stratification has a positive effect on the variance and bias of the estimate in k-fold cross-validation, a technique we will discuss later in this article.

**What's Next**

Since the whole article turned out to be quite lengthy, I decided to split it into multiple parts. In the following parts, we will talk about

- Repeated holdout validation and the bootstrap method for modeling uncertainty in [Part II](http://sebastianraschka.com/blog/2016/model-evaluation-selection-part2.html)
- *The holdout method for hyperparameter tuning* &mdash; splitting a dataset into three parts: a training, test, and validation set.  (Part III)
- *K-fold cross-validation*, a popular alternative to model selection.  (Part III).
- *Nested cross-validation*, probably the most common technique for model evaluation with hyperparameter tuning or algorithm selection. (Part IV).

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

Repeated Holdout Validation

One way to obtain a more robust performance estimate that is less variant to how we split the data into training and test sets is to repeat the holdout method *k* times with different random seeds and compute the average performance over these *k* repetitions

$$\text{ACC}_{avg} = \frac{1}{k} \sum^{k}_{j=1} {ACC_j},$$

where $$\text{ACC}_j$$ is the accuracy estimate of the *j*th test set of size *m*,

$$\text{ACC}_j = 1 - \frac{1}{m} \sum_{i=1}^{m} L\big(\hat{y}_i, y_i \big). $$

This repeated holdout procedure, sometimes also called *Monte Carlo Cross-Validation*, provides with a better estimate of how well our model may perform on a random test set, and it can also give us an idea about our model's stability &mdash; how the model produced by a learning algorithm changes with different training set splits. The following figure shall demonstrate how repeated holdout validation may look like for different training-test split using the [Iris](https://archive.ics.uci.edu/ml/datasets/Iris) dataset to fit to 3-nearest neighbors classifiers.

![figure of repeated holdout with a 50-50 split on iris data](images/model-evaluation-selection-part2/model-eval-iris.png)

To produce the subplot on the left, I performed 50 stratified training/test splits with 75 samples in the test and training set each; a K-nearest neighbors model was fit to the training set and evaluated on the test set in each repetition. The average accuracy of these 50 50/50 splits was 95%. I followed the same procedure to produce the left subplot. Here, I repeatedly performed 90/10 splits, though, so that the test set consisted of only 15 samples. This time, the average accuracy over these 50 splits was 96%. Back to the plot above: It really demonstrates two of the points that we previously discussed. First, we see that the variance of our estimate increases as the size of the test set decreases. Second, we see a small increase in the pessimistic bias when we decrease the size of the training set &mdash; we withhold more training data in the 50/50 split, which may be the reason why the average performance over the 50 splits is slightly lower compared to the 90/10 splits.

In the next section, we look at an alternative method for evaluating a model's performance; we will talk about different flavors of the bootstrap method that are commonly used to infer the uncertainty of a performance estimate.



## The Bootstrap Method and Empirical Confidence Intervals

The previous examples of Monte Carlo Cross-Validation may have convinced us that repeated holdout validation could provide us with a more robust estimate of a model's performance on random test sets compared to an evaluation based on a single train/test split. In addition, the repeated holdout may give us an idea about the stability of our model. In this section, we will explore an alternative approach to model evaluation and calculate its uncertainty using the bootstrap method.

Let's assume that we'd like to compute a confidence interval around our performance estimate to judge it's certainty &mdash; or uncertainty. How can we achieve this if our sample has been drawn from an unknown distribution? Maybe we could use the sample mean as a point estimate of the population mean, but how would we compute the variance or confidence intervals around the mean if its distribution is unknown? Sure, we could collect multiple, independent samples; this is a luxury we often don't have in real world applications, though. Now, the idea behind the bootstrap is to generate "new samples" by sampling from an empirical distribution. As a side note, the term "bootstrap" likely originated from the phrase "to pull oneself up by one's bootstraps:"

> Circa 1900, to pull (oneself) up by (one's) bootstraps was used figuratively of an impossible task (Among the "practical questions" at the end of chapter one of Steele's "Popular Physics" schoolbook (1888) is, "30. Why can not a man lift himself by pulling up on his boot-straps?"). By 1916 its meaning expanded to include "better oneself by rigorous, unaided effort." The meaning "fixed sequence of instructions to load the operating system of a computer" (1953) is from the notion of the first-loaded program pulling itself, and the rest, up by the bootstrap.

(Source: [Online Etymology Dictionary](http://www.etymonline.com/index.php?allowed_in_frame=0&search=bootstrap))

The bootstrap method is a resampling technique for estimating a sampling distribution, and in the context of this article, we are particularly interested in estimating the uncertainty of our performance estimate &mdash; the prediction accuracy or error. The bootstrap method was introduced by Bradley Efron in 1979 (Efron, 1979). About 15 years later, Bradley Efron and Robert Tibshirani even devoted a whole book to the bootstrap, "An Introduction to the Bootstrap" (Efron and Tibshirani, 1994), which I recommend you to read if you are interested in more details on this topic. In brief, the idea of the bootstrap method is to generate *new* data from a population by repeated sampling from the original dataset *with replacement* &mdash; in contrast, the repeated holdout method can be understood as sampling *without* replacement. Walking through it step by step, the bootstrap method works like this:

1. We are given a dataset of size *n*.
2. For *b* bootstrap rounds:
	1. We draw one single instance from this dataset and assign it to our *j*th bootstrap sample. We repeat this step until our bootstrap sample has size *n* &mdash; the size of the original dataset. Each time, we draw samples from the same original dataset so that certain samples may appear more than once in our bootstrap sample and some not at all.
3. We fit a model to each of the *b* bootstrap samples and compute the resubstitution accuracy.
4. We compute the model accuracy as the average over the *b* accuracy estimates

$$ \text{ACC}_{boot} = \frac{1}{b} \sum_{j=1}^b \frac{1}{n} \sum_{i=1}^{n} \bigg( 1 - L\big(\hat{y}_i, y_i \big) \bigg).$$

As we discussed previously, the resubstitution accuracy usually leads to an extremely optimistic bias, since a model can be overly sensible to noise in a dataset. Originally, the bootstrap method aims to determine the statistical properties of an estimator when the underlying distribution was unknown and additional samples are not available. So, in order to exploit this method for the evaluation of predictive models, such as hypotheses for classification and regression, we may prefer a slightly different approach to bootstrapping using the so-called *Leave-One-Out Bootstrap* (LOOB) technique. Here, we use *out-of-bag* samples as test sets for evaluation instead of evaluating the model on the training data. Out-of-bag samples are the unique sets of instances that are not used for model fitting as shown in the figure below.

![bootstrap concept figure](images/model-evaluation-selection-part2/bootrap_concept.png)

The figure above illustrates how three random bootstrap samples drawn from an exemplary ten-sample dataset ($$X_1, X_2, \dots X_{10}$$) and their out-of-bag sample for testing may look like. In practice, Bradley Efron and Robert Tibshirani recommend drawing 50 to 200 bootstrap samples as being sufficient for reliable estimates (Efron and Tibshirani, 1993).

To take a step back, assuming we have a sample that has been drawn from a normal distribution $$N(\mu, \sigma^2)$$ with unknown mean $$\mu$$ and variance $$\sigma^2$$. It's probably been a while since we took Statistics I, but if there's one thing we surely remember, it's that we could use the sample mean $$\bar{x}$$ as a point estimate of $$\mu$$,

$$\bar{x} = \frac{1}{n} \sum_{i=1}^{n} x_i,$$

and we could estimate the variance $$\sigma^2$$ as

$$\text{VAR} = \frac{1}{n-1} \sum_{i=1}^{n} (x_i - \bar{x})^2. $$

Hence, we compute the standard deviation as $$\text{SD} = \sqrt{\text{VAR}},$$
and we compute the standard error as

$$\text{SE} = \frac{\text{SD}}{\sqrt{n}}.$$

Using the standard error we can then compute a 95% confidence interval of the mean according to

$$\bar{x} \pm z \times \frac{\sigma}{\sqrt{n}}, $$

so that

$$\bar{x} \pm t \times \text{SE} $$

with z=1.96 for the 95% confidence interval. Since we estimate SD from the sample, we would have to consult a t-table to look up the actual value of *t*, which depends on the size of the sample &mdash; or the *degrees of freedom* to be precise. For instance, given a sample with n=100, we find that  $$t_{95} = 1.984 $$.

Similarly, we can compute the 95% confidence interval of the bootstrap estimate as

$$\text{ACC}_{boot} = \frac{1}{b} \sum_{i=1}^{b} \text{ACC}_i $$

and use it to compute the standard error

$$\text{SE}_{boot} = \sqrt{ \frac{1}{b-1} \sum_{i=1}^{b} (\text{ACC}_i - \text{ACC}_{boot})^2 }.$$

Finally, we can then compute the confidence interval around the mean estimate as

$$\text{ACC}_{boot} \pm t \times \text{SE}_{boot}.$$

Although the approach we outlined above seems intuitive, what can we do if our samples do *not* follow a normal distribution? A more robust, yet computationally straight-forward approach is the percentile method as described by B. Efron (Efron, 1981). Here, we pick our lower and upper confidence bounds as follows:

- $$\text{ACC}_{lower} = \alpha_{1}th$$ percentile of the $$\text{ACC}_\text{boot}$$ distribution
- $$\text{ACC}_{upper} = \alpha_{2}th$$ percentile of the $$\text{ACC}_{boot}$$ distribution,

where $$\alpha_1 = \alpha$$ and $$\alpha_2 = 1 - \alpha$$, and $$\alpha$$ is our degree of confidence to compute the $$100 \times (1 - 2 \times \alpha)$$ confidence interval. For instance, to compute a 95% confidence interval, we pick $$\alpha = 0.025$$ to obtain the 2.5th and 97.5th percentiles of the *b* bootstrap samples distribution as our upper and lower confidence bounds.

In practice, if our data is indeed (roughly) following a normal distribution, the "standard" confidence interval and percentile method typically agree as illustrated in the figure below.

![Bootstraps and Confidence Intervals](images/model-evaluation-selection-part2/bootstrap-histo.png)

In the left subplot, I applied the *Leave-One-Out Bootstrap* technique to evaluate 3-nearest neighbors models on Iris, and the right subplot shows the results of the same model evaluation approach on MNIST, using the same softmax algorithm that we discussed earlier.

In 1983, Bradley Efron described the *.632 Estimate*, a further improvement to address the pessimistic bias of the bootstrap cross-validation approach described above (Efron, 1983). The pessimistic bias in the "classic" bootstrap method can be attributed to the fact that the bootstrap samples only contain approximately 63.2% of the unique samples from the original dataset. For instance, we can compute the probability that a given sample from a dataset of size *n* is *not* drawn as a bootstrap sample as

$$P (\text{not chosen}) =  \bigg(1 - \frac{1}{n}\bigg)^n,$$

which is asymptotically equivalent to $$\frac{1}{e} \approx 0.368$$ as $$ n \rightarrow \infty. $$

Vice versa, we can then compute the probability that a sample *is* chosen as

$$P (\text{chosen}) = 1 - \bigg(1 - \frac{1}{n}\bigg)^n \approx 0.632$$

for reasonably large datasets, so that we'd select approximately $$0.632 \times n$$ uniques samples as bootstrap training sets and reserve $$ 0.368 \times n $$ out-of-bag samples for testing in each iteration.

![bootstrap concept figure](images/model-evaluation-selection-part2/bootstrap_prob.png){: .center-image  .image-80 }


Now, to address the bias that is due to this the sampling with replacement, Bradley Efron proposed the *.632 Estimate* that we mentioned earlier, which is computed via the following equation:

$$\text{ACC}_{boot} = \frac{1}{b} \sum_{i=1}^b \big(0.632 \cdot \text{ACC}_{h, i} + 0.368 \cdot \text{ACC}_{r, i}\big), $$

where $$\text{ACC}_{r, i}$$ is the resubstitution accuracy, and $$\text{ACC}_{h, i}$$ is the accuracy on the out-of-bag sample.

Now, while the *.632 Boostrap* attempts to address the pessimistic bias of the estimate, an optimistic bias may occur with models that tend to overfit so that Bradley Efron and Robert Tibshirani proposed the *The .632+ Bootstrap Method* (Efron and Tibshirani, 1997). Instead of using a fixed "weight" $$\omega = 0.632 $$ in

$$ACC_{\text{boot}} = \frac{1}{b} \sum_{i=1}^b \big(\omega \cdot \text{ACC}_{h, i} + (1-\omega) \cdot \text{ACC}_{r, i} \big), $$

$$\omega$$ is based on the "*no-information error rate*," which we compute by fitting a model to a dataset that contains all possible combinations between samples $$x_{i '}$$ and target class labels $$y_i$$ &mdash; we pretend that the observations and class labels are independent. For instance, we compute the *no-information error rate* $$\gamma $$ as follows:

$$\gamma = \frac{1}{n^2} \sum_{i=1}^{n} \sum_{i '=1}^{n} L(y_{i}, f(x_{i '})), $$

where $$f(\cdot)$$ is the hypothesis or classification rule and $$f(x_{i'})$$ to predict a class label $$\hat{y}_{i'}$$.

Then, we define $$\omega$$ as

$$ \omega = \frac{0.632}{1 - 0.368 \times R},$$

where *R* is the *relative overfitting rate*

$$R = \frac{(-1) \times (\text{ACC}_{h, i} - \text{ACC}_{r, i})}{\gamma - (1 -\text{ACC}_{h, i})}.$$

</div>{: .notice--blank}

## 10.6 - GPU Computing

<div markdown = "1">

</div>{: .notice--blank}

# References
