---
layout: single
permalink: /atiam-ml-11-deep-learning/
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
});
</script>

{% include toc %}

# Deep learning

<div markdown = "1">

The present tutorials covers the basic implementation towards *deep learning*. Most of this young research field is quite extensively based on the neural networks (that we implemented in a [previous tutorial](/atiam-ml-2-neural-networks/)). Therefore, a good knowledge of the previous implementations is required. We will first construct an **auto-encoder** to perform an *unsupervised learning* directly from any data. Then, we will see how we can *transfer* this knowledge to a more extensive *supervised classifier*. Finally, we will extend these implementations with the use and visualization of **convolutional filters**. This tutorial is an adaptation of the [UFLDL tutorials](http://ufldl.stanford.edu/wiki/index.php/UFLDL_Tutorial) for audio data.

</div>{: .notice--blank}

# Reference slides

<div markdown = "1">

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.11.Deep.Learning.pdf)

The corresponding slides cover

  - Deep learning
  - Applications

</div>{: .notice--blank}

# Tutorial  

<div markdown = "1">

In this tutorial, we will use the self-taught learning paradigm with a *sparse autoencoder* in order to build an unsupervised audition system. Then, we will see how to transfer this learning and also rely on the *softmax classifier* (implemented in the [neural networks tutorial](/atiam-ml-2-neural-networks/)) to build a classifier for spectral windows.

First, you will train your sparse autoencoder on an **unlabeled** training dataset of audio data (in this case, you can use all the datasets from the tutorials, and even add your own audio files), which will be represented as a set of concatenated spectral windows (to keep the temporal information).

Then, we will extract these learned features from the *weights* of the network trained in an unsupervised fashion, in order to apply this knowledge to a **labeled** dataset of audio files (by using these features as inputs to a *softmax classifier*). Finally, we will extend this classifier by using *convolutional filters*.

</div>{: .notice--blank}

## 8.1 - Sparse Auto-Encoders

<div markdown = "1">

The autoencoder aims at learning both an encoding function $$e\left(\mathbf{x}\right)$$ and a decoding function $$d\left(\mathbf{x}\right)$$ such that $${\textstyle d\left(e\left(\mathbf{x}\right)\right)=\tilde{\mathbf{x}}\approx\mathbf{x}}$$. Therefore, the AE is intended to learn a function approximating the identity function, by being able to reconstruct an approximation  $${\textstyle\tilde{\mathbf{x}}}$$ similar to the input $$\mathbf{x}$$ via a hidden representation. In the case of entirely random input data (for instance a set of IID Gaussian noise), this task would not only be hard but also quite meaningless. However, based on the assumption that there might exist an underlying hidden structure in the data (where part of the input features are consistently correlated), then this approach might be able to uncover and exploit these statistical regularities. The encoding function $$e:\mathbb{R}^{d_{x}}\rightarrow\mathbb{R}^{d_{h}}$$ maps an input $$\mathbf{x}\in\mathbb{R}^{d_{x}}$$ to an hidden representation $$\mathbf{h}_{\mathbf{x}}\in\mathbb{R}^{d_{h}}$$ by producing a deterministic mapping  

$$
\mathbf{h}_{\mathbf{x}}=e\left(\mathbf{x}\right)=s_{e}\left(\mathbf{W_{e}}\mathbf{x}+\mathbf{b}_{e}\right)
$$

where $$s_{e}$$ is a nonlinear activation function (usually the *sigmoid* function), $$\mathbf{W}_{e}$$ is a $$d_{h}\times d_{x}$$ weight matrix, and $$\mathbf{b}_{e}\in\mathbb{R}^{d_{h}}$$ is a bias vector.  

The decoding function $$d:\mathbb{R}^{d_{h}}\rightarrow\mathbb{R}^{d_{x}}$$ then maps back this encoded representation $$\mathbf{h_{x}}$$ into a reconstruction $$\mathbf{y}$$ of the same dimensionnality as $$\mathbf{x}$$  

$$
\mathbf{y}=d\left(\mathbf{h_{x}}\right)=s_{d}\left(\mathbf{W}_{d}\mathbf{h_{x}}+\mathbf{b}_{d}\right)
$$ 

where $$s_{d}$$ is the activation function of the decoder. Usually the weight matrix of the decoding layer $$\mathbf{W}_{d}$$ is tied to be the transpose of the encoder weight matrix $$\mathbf{W}_{d}=\mathbf{W}_{e}^{T}$$, in which case the AE is said to have tied weights.

Hence, training an auto-encoder can be summarized as finding the optimal set of parameters $$\theta=\left\{\mathbf{W}_{e},\mathbf{W}_{d},\mathbf{b}_{e},\mathbf{b}_{d}\right\}$$ (or $$\theta=\left\{ \mathbf{W},\mathbf{b}\right\}$$ in the case of tied weights) in order to minimize the reconstruction error on a dataset of training examples $$\mathcal{D}_{n}$$

$$  \mathcal{J}_{AE}\left(\theta\right)=\sum_{\mathbf{x}\in\mathcal{D}_{n}}\mathcal{L}\left(\mathbf{x},d\left(e\left(\mathbf{x}\right)\right)\right)
$$

Usual choices for the reconstruction error function $$\mathcal{L}$$ are either the squared error $$\mathcal{L}(x,y)=\left\Vert x-y\right\Vert ^{2}$$ (often used for linear reconstruction) or the cross-entropy loss of the reconstruction $$\mathcal{L}(x,y)=-\sum_{i=1}^{d_{x}}x_{i}log\left(y_{i}\right)+\left(1-x_{i}\right)log\left(1-y_{i}\right)$$ (if the input is interpreted as vectors of probabilities and a sigmoid activation function is used). 

As can be seen from the definition of the objective functions, by solely minimizing the reconstruction error, nothing prevents an auto-encoder with an input of $$n$$ dimensions and an encoding of the same (or higher) dimensionnality to simply learn the identity function. In this case, the AE would merely be mapping an input to a copy of itself. Surprisingly, it has been shown that non-linear autoencoders in this over-complete setting (with a hidden dimensionality strongly superior to that of the input) trained with stochastic gradient descent, could still provide useful representations, even without any additional constraints

We can see that the framework defined by AEs fit the overarching goal of unsupervised and self-taught learning, as it tries to exploit statistical correlations of the data structure to find a non-linear representation aimed at decomposing and then reconstructing the input. In the starting code, we provide the basic functions to perform this learning.

|**File**|*Explanation*|
|-------:|:---------|
|`base-toolboxes`|Toolboxes to perform learning|
|`display_network.m`|Network visualization function|
|`initializeParameters.m`|Random initialization of network weights|
|`params2stack.m`|Transform parameters as a stack|
|`pcaWhitening.m`|Perform PCA whitening on input data|
|`sampleSpectrums.m`|Sample from a set of spectrums|
|`sparseAutoencoderCost.m`|Cost and gradient function for an SAE|
|`stack2params.m`|Transform stack to a parameter|
|`stackedAECost.m`|Cost and gradient for multiple layers|
|`stackedAEPredict.m`|Prediction function for logistic regression|

In order to perform the various computations, we will use the `minFunc` package as an advanced optimizer and the unlabeled data (any audio files) to train a sparse autoencoder. However, we first need to prepare an input set, so that the given data is formatted to a common size (slices of audio input). In the following problem, you will implement the sparse autoencoder algorithm, and show how it discovers an optimal representation for spectral windows. 

Specifically, in this exercise you will implement a sparse autoencoder, trained with 4 consecutive spectral distributions (FFT, Mel, Bark or Cepstrum) using the L-BFGS optimization algorithm (this algorithm is provided in the `minFunc` subdirectory, which is a 3rd party CCA software).

**Inputs**

The first step is to generate a training set. To get a single training example $$x$$, we need to compute the spectral transform from a sound and then subsample a set of a given number of consecutive spectral frames. This will allow the network to learn from the complete spectro-temporal information. However, the sampled parts will need to be converted into vectors.

</div>{: .notice--blank}
  
**Exercise**  
<div markdown="1">  

  1. Update the `sampleSpectrums` function to generate examples
  2. Test your function on different transforms to observe the outputs
  3. Check the random intialization of parameters

</div> {: .notice--info}

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div1">Reveal</a>]

<div id="div1">
<img src="../images/atiam-ml/11_11.1_samples_constantq.svg" height="350" width="350"/> <img src="../images/atiam-ml/11_11.1_samples_chroma.svg" height="350" width="350"/>
</div>

</div>{: .notice--blank}

<div markdown = "1">

The learning of an autoencoder is based on a cost function that tries to reconstruct the input from a combination of hidden units. Hence, as underlined in the previous question, we will start by implementing the simplest reconstruction cost, given by  

$$  \mathcal{J}_{AE}\left(\theta\right)=\sum_{\mathbf{x}\in\mathcal{D}_{n}}\mathcal{L}\left(\mathbf{x},d\left(e\left(\mathbf{x}\right)\right)\right)=\sum_{\mathbf{x}\in\mathcal{D}_{n}}\left\Vert \mathbf{x}-\tilde{\mathbf{x}}\right\Vert ^{2}
$$

However, as discussed previously, solely minimizing the reconstruction error, nothing prevents an auto-encoder with an input of $$n$$ dimensions and an encoding of the same (or higher) dimensionnality to simply learn the identity function. One way to avoid this situation is to enforce a *sparsity constraint* on the learning. The idea is to force the network to make this reconstruction from fewer data. If we denote $$a^{h}_{j}\left(x\right)$$ as the activation of hidden unit $$j$$ in the hidden layer of the autoencoder when given a specific input $$x$$. Furthermore, let  

$$
\hat\rho_j = \frac{1}{m} \sum_{i=1}^m \left[ a^{h}_j(x_{i}) \right]
$$

be the average activation of hidden unit $$j$$ (averaged over the training set). We would like to (approximately) enforce the constraint  

$$
\hat\rho_j = \rho
$$

where $$\rho$$ is a given *sparsity parameter*, typically a small value close to zero. In other words, we would like the average activation of each hidden neuron $$j$$ to be small. To satisfy this constraint, the hidden unit's activations must mostly be near 0. To achieve this, we will add an extra penalty term to our optimization objective that penalizes $$\hat\rho_j$$ deviating significantly from $$\rho$$. Many choices of the penalty term will give reasonable results. We will choose the following  

$$
\sum_{j=1}^{n_{h}} \rho \log \frac{\rho}{\hat\rho_j} + (1-\rho) \log \frac{1-\rho}{1-\hat\rho_j}.
$$

Here, $$n_{h}$$ is the number of neurons in the hidden layer, and the index $$j$$ is summing over the hidden units in our network. If you are familiar with the concept of KL divergence, this penalty term is based on it, and can also be written

$$
\sum_{j=1}^{n_{h}} {\rm KL}(\rho || \hat\rho_j),
$$

where $$KL(\rho \mid \mid \hat\rho_j) = \rho \log \frac{\rho}{\hat\rho_j} + (1-\rho) \log \frac{1-\rho}{1-\hat\rho_j}$$ is the Kullback-Leibler (KL) divergence
 
Hence, we can simply define the cost function $$\mathcal{J}_{sparse}\left(\theta\right)$$ and the corresponding derivatives of $$\mathcal{J}_{sparse}$$ with respect to the different parameters as the original cost with the added constraint

$$
\mathcal{J}_{sparse}\left(\theta\right)=\mathcal{J}_{sparse}\left(\theta\right) + \beta \sum_{j=1}^{s_2} {\rm KL}(\rho \mid \mid \hat\rho_j)
$$ 

In order to test the validity of your implementation, you can use the method of [*gradient checking*](http://ufldl.stanford.edu/wiki/index.php/Gradient_checking_and_advanced_optimization), which allows you to verify that your numerically evaluated gradient is very close to the true (analytically computed) gradient.

**Implementation tip**: If you are debugging your code, perform the learning on smaller models and smaller training sets (using few training examples and hidden units) to speed things up.

</div>{: .notice--blank}
  
**Exercise**  
<div markdown="1">
  
  
  1. Update the `sparseAutoencoderCost` to perform the simple Euclidean cost.  
  2. Test your algorithm and visualize the learned filters.  
  3. Update the `sparseAutoencoderCost` to include the *sparsity constraint*.  
  4. Test your algorithm and compare the results.  
  5. Also add the *weight decay* to further regularize learning.  

</div>{: .notice--info}  


## 8.2 - Training and visualizing 

<div markdown = "1">

Once you have coded and verified your objective and derivatives, you can train the parameters of the model and use it to extract features from the spectral windows. Equiped with the code that computes Jsparse and its derivatives, we're ready to minimize Jsparse with respect to its parameters, and thereby train our sparse autoencoder.  

We will use the L-BFGS algorithm. This is provided to you in a function called minFunc (code provided by Mark Schmidt) included in the starter code. (For the purpose of this assignment, you only need to call minFunc with the default parameters. You do not need to know how L-BFGS works). We have already provided code in train.m (Step 4) to call minFunc. The minFunc code assumes that the parameters to be optimized are a long parameter vector; so we will use the $$\theta$$ parameterization rather than the $$(W(1),W(2),b(1),b(2))$$ parameterization when passing our parameters to it.  

Train a sparse autoencoder with 4xN input units, 200 hidden units, and 4xN output units. In our starter code, we have provided a function for initializing the parameters. We initialize the biases $$b^{(l)}_i$$ to zero, and the weights $$W^{(l)}_{ij}$$ to random numbers drawn uniformly from the interval $$\left[-\sqrt{\frac{6}{n_{\rm in}+n_{\rm out}+1}},\sqrt{\frac{6}{n_{\rm in}+n_{\rm out}+1}}\,\right]$$, where $$n_{in}$$ is the fan-in (the number of inputs feeding into a node) and $$n_{out}$$ is the fan-out (the number of units that a node feeds into).  

** Visualization **
After training the autoencoder, you can use `display_network` to visualize the learned weights.

</div>{: .notice--blank}
  
**Exercise**  
<div markdown="1">  

  1. Run your full implementation on a reduced dataset.
  2. Perform the visualization in order to see the learned weights.
  3. Compare the results with using the full dataset.
  
</div>{: .notice--info} 

## 8.3 - Logistic regression

<div markdown = "1">

As we have seen in the [Neural Networks tutorial](/atiam-ml-2-neural-networks/), in order to perform multi-class predictions, we cannot rely on simply computing the distance between desired patterns and the obtained binary value. The idea here is to rely on the *softmax regression*, by considering classes as a vector of probabilities. If you have implemented the logistic regression in the [previous tutorial](/atiam-ml-2-neural-networks/), you can simply copy and paste your code here. Otherwise, we recall the mathematical bases behind these computations.  

The desired answers will be considered as a set of *probabilities*, where the desired class is $$1$$ and the others are $$0$$ (called *one-hot* representation). Then, the cost function will rely on the softmax formulation

$$
\begin{equation}
\mathcal{L_D}(\theta) = - \frac{1}{m} \left[ \sum_{i=1}^{m} \sum_{j=1}^{k} 1\left\{y^{(i)} = j\right\} \log \frac{e^{\theta_{j}^{T} x^{(i)}}}{\sum_{l=1}^{k} e^{ \theta_{l}^{T} x^{(i)} }}  \right]
\end{equation}
$$

Therefore, we compute the output of the softmax by taking 

$$
\begin{equation}
p(y^{(i)} = j | x^{(i)}; \theta) = \frac{e^{\theta_{j}^{T} x^{(i)}}}{\sum_{l=1}^{k} e^{ \theta_{l}^{T} x^{(i)}} }
\end{equation}
$$

By taking derivatives, we can show that the gradient of the softmax layer is

$$
\begin{equation}
\nabla_{\theta_{j}} \mathcal{L_D}(\theta) = - \frac{1}{m} \sum_{i=1}^{m}{ \left[ x^{(i)} \left( 1\{ y^{(i)} = j\}  - p(y^{(i)} = j \mid x^{(i)}, \theta) \right) \right]}
\end{equation}
$$

In `softmaxCost`, implement code to compute the softmax cost function $$J(\theta)$$. Remember to include the weight decay term in the cost as well. Your code should also compute the appropriate gradients, as well as the predictions for the input data (which will be used in the cross-validation step later).  

**Implementation Tip**: Computing the ground truth matrix - In your code, you may need to compute the ground truth matrix $$M$$, such that $$M(r, c)$$ is $$1$$ if $$y(c) = r$$ and $$0$$ otherwise. This can be done quickly, without a loop, using the MATLAB functions sparse and full. Specifically, the command `M = sparse(r, c, v)` creates a sparse matrix such that $$M(r(i), c(i)) = v(i)$$ for all i. This code for using sparse and full to compute the ground truth matrix is already provided in softmaxCost.m.

**Implementation tip: Preventing overflows**  
In the softmax regression, we compute the unbounded hypothesis of the input belonging to each class, which can lead to overflow. However, given the definition of the logistic function, the overall (relative) probabilities remain equivalent if we substract the same quantity from each of the $$\theta_j^T x^{(i)}$$. Hence, to prevent overflow, we shall simply subtract some large constant value from each of the $$\theta_j^T x^{(i)}$$ terms before computing the exponential. 

** Learning parameters **

Now that you've verified that your gradients are correct, you can train your softmax model using the function softmaxTrain in softmaxTrain.m. softmaxTrain which uses the L-BFGS algorithm, in the function minFunc. \\

</div>{: .notice--blank}
  
**Exercise**  
<div markdown="1">  

  - Update `softmaxCost` to compute the softmax cost
  - Train the softmax model by using `softmaxTrain` and the L-BFGS algorithm.
  - Evaluate the accuracy of training the softmax on different architectures.

</div>{: .notice--info}  

## 8.4 - Classification

<div markdown = "1">

Concretely, for each example in the the labeled training dataset, we forward propagate the example to obtain the activation of the hidden units. This transformed representation is used as the new feature representation with which to train the softmax classifier.

Finally, complete the code to make predictions on the test set (testFeatures) and see how your learned features perform! If you've done all the steps correctly, you should get an accuracy of about 98% percent.
As a comparison, when raw pixels are used (instead of the learned features), we obtained a test accuracy of only around 96% (for the same train and test sets).

</div>{: .notice--blank}

**Exercise**  
<div markdown="1">  

  1. Code
  
</div>{: .notice--info} 

## 8.4 - Convolutional layers

<div markdown = "1">

Finally.

</div>{: .notice--blank}


**Exercise**  
<div markdown="1">  

  1. Code
  
</div>{: .notice--info} 

## 8.5 - Visualizing filters

<div markdown = "1">

Finally.

</div>{: .notice--blank}


**Exercise**  
<div markdown="1">  

  1. Code
  
</div>{: .notice--info} 
