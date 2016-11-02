---
layout: single
permalink: /atiam-ml-2-neural-networks/
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

# Neural networks

<div markdown = "1">

The present tutorials covers the implementation of neural networks, starting with a single neuron and then going up to a multilayer perceptron applied to audio classification.

</div>{: .notice--blank}

# Reference slides

<div markdown = "1">

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.2.Neural.networks.pdf)

  - The artificial neuron
  - Neural networks
  - Architecture zoo  
  
</div>{: .notice--blank}

# Tutorial 

<div markdown = "1">

In this tutorial, we will cover a more advanced classification algorithm through the use of *neural networks*. The tutorial starts by performing a simple **single neuron** discrimination of two random distributions. Then, we will study the typical **XOR problem** by using a more advanced 2-layer **perceptron**. Finally, we generalize the use of neural networks in order to perform classification on a given set of audio files.

To simplify your work, we provide the following set of functions that you should find in the `02_Neural_Networks` folder

  |**File**|*Explanation*|
  |-------:|:---------|
  |`plot3view.m`|Allows to plot a 3-dimensional view of data points|
  |`plotBoundary.m`|Plots the decision boundary of a single neuron with 2-dimensional inputs|
  |`plotBoundarySurface.m`|Plots the decision surface of a single neuron with 3-dimensional inputs|
  |`plotPatterns.m`|Plots input patterns (bi-dimensionnal)|
  |`plotPatterns3D.m`|Plots 3-dimensional input patterns|
  |`xorAns.dat`|Class values for the XOR problem|
  |`xorPats.dat`|Point values for the XOR problem|

</div>{: .notice--blank}

## 2.1 - Single neuron

<div markdown = "1">

For the first parts of the tutorial, we will perform the simplest classification model possible in a neural network setting, a single neuron. We briefly recall here that; given an input vector $$ \mathbf{x} \in \mathbb{R}^{n} $$, a single neuron computes the function  

$$
\begin{equation}
y=\sigma\left(\sum_{i = 1}^{n}w_{i}.x_{i} + b\right)
\label{eq1}
\end{equation}
$$

with $$ \mathbf{w} \in \mathbb{R}^{n} $$ a weight vector, $$ b $$ a bias and $$ \sigma\left(\right) $$ an *activation function*. Therefore, if we consider the *threshold* activation function ($$ \sigma_0\left(x\right)=1 $$ if $$ x \geq 0$$), a single neuron simply performs an *affine transform* and then a *linear* discrimination of the space. Geometrically, a single neuron computes an hyperplane that separates the space. In order to learn, we have to adjust the weights and know "how much wrong we are". To do so, we consider that we know the desired output $$ d $$ of a system for a given example $$ \mathbf{x} $$ (eg. a predicted value for a regression system, a class value for a classification system). Therefore, we define the loss function $$ \mathcal{L}_{\mathcal{D}} $$ over a whole dataset as

$$
\begin{equation}
\mathcal{L}=\sum_{j=1}^{k_{\mathcal{D}}}\left\Vert d_{j}-y_{j}\right\Vert ^{2}
\label{eq2}
\end{equation}
$$

In order to know how to change the weights based on the value of the errors, we need to now "how to change it to make it better". Therefore, we should compute the sets of derivatives of the error given each parameter

$$
\begin{equation}
\Delta\bar{\mathbf{w}}=\left(\frac{\delta\mathcal{L}_{\mathcal{D}}}{\delta w_{1}},\ldots,\frac{\delta\mathcal{L}_{\mathcal{D}}}{\delta w_{n}}\right)
\label{eq3}
\end{equation}
$$ 

<div markdown="1">
**Exercise**  

  1. Perform the derivatives of the output given a single neuron
  2. Perform the derivatives for the bias as well

</div>{: .notice--info}  

<div markdown = "1">

**Solution** [<a href="javascript:void(0)" class="abuttons" data-divid="divq1">Reveal</a>]

<div id="divq1">

Given that we have simply an $$ L_2 $$ (Euclidean) error criterion on a single neuron for the time being, the update of the weights for a single example $$ x $$, with desired output $$ d $$ can be simply computed by 

$$
\begin{equation}
w_{j}^{t+1}=w_{j}^{t}+\eta.\left(d-y\right).x_{j}
\label{eq4}
\end{equation}
$$

with $$ \eta $$ the *learning rate* parameter (which controls the size of the update steps). 

Similarly, for the bias, we simply have to compute  

$$
\begin{equation}
b^{t+1}=b^{t}+\eta.\left(d-y\right)
\label{eq4}
\end{equation}
$$

</div>

</div>{: .notice--success}

We will start by training a single neuron to learn how to perform this discrimination with a linear problem (so that a single neuron is enough to solve it). To produce such classes of problems, we provide a script that draw a set of random 2-dimensional points, then choose a random line in this space that will act as the linear frontier between 2 classes (hence defining a linear 2-class problem). The variables that will be used by your code are the following.  

{% highlight Matlab %}
patterns      % 2 x n matrix of random points
desired       % classes of the patterns 
inputs        % 3 x n final matrix of inputs (accounting for bias)
weights       % 3 x 1 vector of neuron weights
{% endhighlight %}  

</div>{: .notice--blank}
  
<div markdown="1">
**Exercise**  

  1. Update the neuron update loop so that it computes its error (forward propagate and compare to desired)
  2. Update the neuron update loop to perform learning of its weights (based on back-propagation)
  3. Run the complete learning procedure, which should produce a result similar to that displayed below.
  4. Perform multiple re-runs of the learning procedure (re-launching produces different datasets)
  5. What observations can you make on the learning process?
  6. (Optional) Change the input patterns, and confirm your observations.

</div>{: .notice--info}  

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div1">Reveal</a>]

<div id="div1">
<img src="../images/atiam-ml/02_2.1_single_1.svg" height="350" width="350"/> <img src="../images/atiam-ml/02_2.1_single_2.svg" height="350" width="350"/>
</div>

</div>{: .notice--blank}

## 2.2 - 2-layer XOR problem

<div markdown = "1">

In most cases, classification problems are far from being linear. Therefore, we need more advanced methods to be able to compute non-linear class boundaries. The advantage of neural networks is that the same principle can be applied in a *layer-wise* fashion. This allows to further discriminate the space in sub-regions (as seen in the course). We will try to implement the 2-layer *perceptron* that can provide a solution to the infamous XOR problem. The idea is now to have the output of the first neurons to be connected to a set of other neurons. Therefore, if we take back our previous formulation, we will have


$$
\begin{equation}
y_{2}=\sigma\left(\sum_{i = 1}^{n}w_{i}.y_{1}^{i} + b\right)
\label{eq5}
\end{equation}
$$  

Therefore, in order to *propagate* the derivatives, we can simply use the chain rule

$$
\begin{equation}
\frac{\delta\mathcal{P}}{\delta w_{1}}=\frac{\delta\mathcal{P}}{\delta y_{2}}.\frac{\delta y_{2}}{\delta w_{1}}
\label{eq6}
\end{equation}
$$  

Therefore, we can compute the derivative for the last layer as

$$
\begin{equation}
\delta_{i}^{L}=g'\left(h_{i}^{L}\right)\left[\delta_{i}^{u}-y_{i}^{L}\right]
\label{eq7}
\end{equation}
$$  

And for any previous layer, we rely on the development of the chain rule giving

$$
\begin{equation}
\delta_{i}^{l}=g'\left(h_{i}^{l}\right)\sum_{j}w_{ij}^{l+1}\delta_{j}^{l+1}\mbox{ }l\in\left[1\ldots L-1\right]
\label{eq8}
\end{equation}
$$  

We provide the prototypical set of XOR values in the `xorPat.mat` along with their class values in `xorAns.mat`. The variables that will be used by your code are the following.


{% highlight Matlab %}
patterns          % 2 x n matrix of random points
desired           % classes of the patterns 
inputs1           % 3 x n final matrix of inputs (accounting for bias)
nHiddens          % Number of hidden units
learnRate         % Learning rate parameter
momentum          % Momentum parameter
weights1          % 1st layer weights
weights2          % 2nd layer weights
TSS_Limit         % Sum-squared error limit
{% endhighlight %}   

</div>{: .notice--blank}

<div markdown="1">  
**Exercise**  

  1. Update the forward propagation and error computation (compared to desired).
  2. Update the back-propagation part to learn the weights of both layers.
  3. Run the complete learning procedure, which should produce a result similar to that displayed below.
  4. Perform multiple re-runs of the learning procedure (re-launching with different initializations)
  5. What observations can you make on the learning process?
  6. What happens if you initialize all weights to zeros?
  7. (Optional) Implement the *sparsity* constraint in your neural network.

</div>{: .notice--info}

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div2">Reveal</a>]

<div id="div2">
<img src="../images/atiam-ml/02_2.2_xor_1.svg" height="350" width="350"/> <img src="../images/atiam-ml/02_2.2_xor_2.svg" height="350" width="350"/>
</div>

</div>{: .notice--blank}

### 2.3 - 3-layer audio classification

<div markdown = "1">

We now return to our original classification problem and will try to perform neural network learning on a set of audio files. The data structure will be the same as the one used for parts 1 and 2. As discussed during the courses, even though a 2-layer neural network can provide non-linear boundaries, it can not perform "holes" inside those regions. In order to obtain an improved classification, we will now rely on a 3-layer neural network. The modification to the code of section 3.2 should be minimal, as the back-propagation will be similar for the new layer as one of the two others. We do not develop the math here as it is simply a re-application of the previous rules.

</div>{: .notice--blank}

<div markdown="1">  
**Exercise**

  1. Based on the previous neural network, upgrade the code to a 3-layer neural network
  2. Use the provided code to perform classification on a pre-defined set of features
  3. As previously, change the set of features to assess their different accuracies
  4. Evaluate the neural network accuracy for all features combinations
  5. (Optional) Implement the *sparsity* constraint in your neural network.

</div>{: .notice--info}

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div3">Reveal</a>]

<div id="div3">
<img src="../images/atiam-ml/00_0.2_bells.svg" height="350" width="350"/> <img src="../images/atiam-ml/00_0.2_speech.svg" height="350" width="350"/>
</div>

</div>{: .notice--blank}
