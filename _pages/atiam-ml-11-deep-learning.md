---
layout: single
permalink: /atiam-ml-11-deep-learning/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

# Deep learning

The present tutorials covers .

# Reference slides

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.11.Deep.Learning.pdf)

The corresponding slides cover

  - Deep learning
  - Applications
  
# Tutorial 

In this exercise, we will use the self-taught learning paradigm with a *sparse autoencoder* and (optionnaly in the supplementary exercice) *softmax classifier* to build both a classifier for spectral windows, but also an unsupervised audition system.  

First, you will train your sparse autoencoder on an **unlabeled** training dataset of audio data (in this case, you can use all the datasets from the tutorials, and even add your own audio files), which will be represented as a set of concatenated spectral windows (to keep the temporal information. This should produce features that are similar to the current theory of *Spectro-Temporal Receptive Fields* (SRTF), which models neurons in the primary auditory cortex (A1).  

Then, we will extract these learned features from the **labeled** dataset of audio files. These features will then be used as inputs to a *softmax classifier*. Concretely, for each example in the the labeled training dataset, we forward propagate the example to obtain the activation of the hidden units. This transformed representation is used as the new feature representation with which to train the softmax classifier.  

### 8.1 - Sparse Auto-Encoders (SAE)
We will rely on the set of spectral transforms described in the first exercice.  

In the starting code, we provide the basic functions to perform 
  * ''???.m''       - ???
  * ''???.m''       - ???

In order to perform the various computations, we will use the minFunc package and develop the following function

{% highlight Matlab %}
function dataStruct = computeTransforms(dataStruct)
% dataStruct   : Dataset structure with filenames

% Returns the dataStruct structure with
dataStruct.???     % ???
dataStruct.???     % ???
dataStruct.???     % ???
{% endhighlight %}  

We will use the unlabeled data (any audio files) to train a sparse autoencoder. However, we first need to prepare an input set, so that the given data is formatted to a common size (slices of audio input). In the following problem, you will implement the sparse autoencoder algorithm, and show how it discovers an optimal representation for spectral windows. 

Specifically, in this exercise you will implement a sparse autoencoder, trained with 4 consecutive spectral distributions (FFT, Mel, Bark or Cepstrum) using the L-BFGS optimization algorithm (this algorithm is provided in the `minFunc` subdirectory, which is a 3rd party CCA software implementing L-BFGS).

#### Inputs

The first step is to generate a training set. To get a single training example $$x$$, we need to compute the spectral transform from a sound and then subsample a set of a given number of consecutive spectral frames. This will allow the network to learn from the complete spectro-temporal information. However, the sampled parts will need to be converted into vectors.

  
**Exercise**  
<div markdown="1">  

  1. Update the code to generate examples
  2. Run your ''svmTrain'' function on the ''example3.mat'' dataset, you should obtain the result displayed below.
  3. Once again, display the decision boundary at each iteration of the algorithm.

</div>

#### Objective

As seen in course, the learning of an autoencoder is based on a cost function that tries to reconstruct the input from a combination of hidden units. The sparsity aspects allow to force the network to make this reconstruction from fewer data. To do so, we need to both define the cost function $$J_{sparse}(W,b)$$ and the corresponding derivatives of $$J_{sparse}$$ with respect to the different parameters. We will use the sigmoid function for the activation function
$$
\begin{equation}
f(z) = \frac{1}{{1+e^{-z}}} 
\end{equation}
$$

The sparse autoencoder is parameterized by matrices  $$W^{(1)} \in \Re^{s_1\times s_2}, W^{(2)} \in \Re^{s_2\times s_3}$$ vectors  $$b^{(1)} \in \Re^{s_2},  b^{(2)} \in \Re^{s_3}$$. However, for subsequent notational convenience, we will "unroll" all of these parameters into a very long parameter vector $$\theta$$ with $$s_1s_2 + s_2s_3 + s_2 + s_3$$ elements. The code for converting between the $$(W(1),W(2),b(1),b(2))$$ and the $$\theta$$ parameterization is already provided in the starter code.  

Implementational tip: The objective $$J_{sparse}(W,b)$$ contains 3 terms, corresponding to the squared error term, the weight decay term, and the sparsity penalty. You're welcome to implement this however you want, but for ease of debugging, you might implement the cost function and derivative computation (backpropagation) only for the squared error term first and then add both the *weight decay* and the *sparsity term* to the objective and derivative function  

In order to test the validity of your implementation, you can use the method of gradient checking, which allows you to verify that your numerically evaluated gradient is very close to the true (analytically computed) gradient.  

**Implementation tip**: If you are debugging your code, performing gradient checking on smaller models and smaller training sets (e.g., using only 10 training examples and 1-2 hidden units) may speed things up.

  
**Exercise**  
<div markdown="1">  

  1. Update your ''svmTrain'' code to perform a cross-validation .
  2. Run your ''svmTrain'' function on the ''example3.mat'' dataset, you should obtain the result displayed below.
  3. Once again, display the decision boundary at each iteration of the algorithm.
**Do not forget to vectorize your code for speed**

</div>{: .notice--info}  


### 8.2 - Training the SAE and visualizing 

Once you have coded and verified your objective and derivatives, you can train the parameters of the model and use it to extract features from the spectral windows. Equiped with the code that computes Jsparse and its derivatives, we're ready to minimize Jsparse with respect to its parameters, and thereby train our sparse autoencoder.  

We will use the L-BFGS algorithm. This is provided to you in a function called minFunc (code provided by Mark Schmidt) included in the starter code. (For the purpose of this assignment, you only need to call minFunc with the default parameters. You do not need to know how L-BFGS works). We have already provided code in train.m (Step 4) to call minFunc. The minFunc code assumes that the parameters to be optimized are a long parameter vector; so we will use the $$\theta$$ parameterization rather than the $$(W(1),W(2),b(1),b(2))$$ parameterization when passing our parameters to it.  

Train a sparse autoencoder with 4xN input units, 200 hidden units, and 4xN output units. In our starter code, we have provided a function for initializing the parameters. We initialize the biases $$b^{(l)}_i$$ to zero, and the weights $$W^{(l)}_{ij}$$ to random numbers drawn uniformly from the interval $$\left[-\sqrt{\frac{6}{n_{\rm in}+n_{\rm out}+1}},\sqrt{\frac{6}{n_{\rm in}+n_{\rm out}+1}}\,\right]$$, where $$n_{in}$$ is the fan-in (the number of inputs feeding into a node) and $$n_{out}$$ is the fan-out (the number of units that a node feeds into).  

** Visualization **
After training the autoencoder, use display_network.m to visualize the learned weights. (See train.m, Step 5.).

  
**Exercise**  
<div markdown="1">  

  1. Code
  
**Do not forget to vectorize your code for speed**

</div>{: .notice--info} 

### 8.3 - Logistic regression model

In softmaxCost.m, implement code to compute the softmax cost function $$J(\theta)$$. Remember to include the weight decay term in the cost as well. Your code should also compute the appropriate gradients, as well as the predictions for the input data (which will be used in the cross-validation step later).  

**Implementation Tip**: Computing the ground truth matrix - In your code, you may need to compute the ground truth matrix $$M$$, such that $$M(r, c)$$ is $$1$$ if $$y(c) = r$$ and $$0$$ otherwise. This can be done quickly, without a loop, using the MATLAB functions sparse and full. Specifically, the command `M = sparse(r, c, v)` creates a sparse matrix such that $$M(r(i), c(i)) = v(i)$$ for all i. That is, the vectors r and c give the position of the elements whose values we wish to set, and v the corresponding values of the elements. Running full on a sparse matrix gives a "full" representation of the matrix for use (meaning that Matlab will no longer try to represent it as a sparse matrix in memory). The code for using sparse and full to compute the ground truth matrix has already been included in softmaxCost.m.

**Implementation tip: Preventing overflows**  
In the softmax regression, we compute the unbounded hypothesis of the input belonging to each class, which can lead to overflow. However, given the definition of the logistic function, the overall (relative) probabilities remain equivalent if we substract the same quantity from each of the $$\theta_j^T x^{(i)}$$. Hence, to prevent overflow, we shall simply subtract some large constant value from each of the $$\theta_j^T x^{(i)}$$ terms before computing the exponential. 

**Implementation tip: Computing the predictions** 
You may also find `bsxfun` useful in computing your predictions. If you have a matrix $$M$$ containing the $$e^{\theta_j^T x^{(i)}}$$ terms, such that $$M(r, c)$$ contains the $$e^{\theta_r^T x^{(c)}}$$ term, you can use the following code to compute the hypothesis (by dividing all elements in each column by their column sum)

{% highlight Matlab %}
% M is the matrix as described in the text
M = bsxfun(@rdivide, M, sum(M))
{% endhighlight %}  

** Gradient checking **

Once you have written the softmax cost function, you should check your gradients numerically. In general, whenever implementing any learning algorithm, you should always check your gradients numerically before proceeding to train the model. 

** Learning parameters **

Now that you've verified that your gradients are correct, you can train your softmax model using the function softmaxTrain in softmaxTrain.m. softmaxTrain which uses the L-BFGS algorithm, in the function minFunc. \\

  
**Exercise**  
<div markdown="1">  

  - Update your ''svmTrain'' code to perform a cross-validation .
  - Run your ''svmTrain'' function on the ''example3.mat'' dataset, you should obtain the result displayed below.
  - Once again, display the decision boundary at each iteration of the algorithm.
**Do not forget to vectorize your code for speed**

</div>{: .notice--info}  

### 8.4 - Classifying the test set

Finally, complete the code to make predictions on the test set (testFeatures) and see how your learned features perform! If you've done all the steps correctly, you should get an accuracy of about 98% percent.
As a comparison, when raw pixels are used (instead of the learned features), we obtained a test accuracy of only around 96% (for the same train and test sets).
