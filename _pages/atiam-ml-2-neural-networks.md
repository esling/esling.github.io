---
layout: single
permalink: /atiam-ml-2-neural-networks/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

{% include toc %}

# Neural networks

The present tutorials covers the implementation of neural networks.

# Reference slides

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.2.Neural.networks.pdf)

The corresponding slides cover

  - The artificial neuron
  - Neural networks
  - Architecture zoo  

# Tutorial 

In this tutorial, we will cover a more advanced classification algorithm through the use of neural networks. The tutorial starts by performing a simple single neuron discrimination of two random distributions. Then, we will study the typical XOR problem by using a more advanced 2-layer perceptron. Finally, we generalize the use of neural networks in order to perform classification on our set of audio files.

To simplify your work, we provide the following set of functions that you should find in the *2_Neural_Networks* folder

  * `plot3view.m` - Allows to plot a 3-dimensional view of data points
  * `plotBoundary.m` - Plots the decision boundary of a single neuron with 2-dimensional inputs
  * `plotBoundarySurface.m` - Plots the decision surface of a single neuron with 3-dimensional inputs
  * `plotBpBoundary.m` - Plots multiple decision boundaries for a set of hidden units
  * `plotBpPats.m` - Plots input patterns for back-propagation
  * `plotPats.m` - Plots input patterns for single neuron problems
  * `plotPats3D.m` - Plots 3-dimensional input patterns for single neuron problems
  * `xorAns.dat` - Class values for the XOR problem
  * `xorPats.dat` - Point values for the XOR problem


### 3.1 - Single neuron

For the first parts of the tutorial, we will perform the simplest classification model possible in a neural network setting, a single neuron. We briefly recall here that; given an input vector $$ \mathbb{x} \in \mathbf{R}^{n} $$, a single neuron computes the function


$$
\begin{equation}
y=\sigma\left(\sum_{i\in in_{x}}w_{i}.x_{i}\geq T\right)
\label{eq1}
\end{equation}
$$

Therefore, if we consider the a single neuron can only perform a *linear* discrimination of the space. We will start by training a single neuron to learn how to perform this discrimination with a linear problem (so that it can solve it). To produce such classes of problems, we provide a script that draw a set of random 2-dimensional points, then choose a random line in this space that will act as the linear frontier between 2 classes (hence defining a linear 2-class problem). The variables that will be used by your code are the following.  

{% highlight Matlab %}
patterns      % 2 x n matrix of random points
desired       % classes of the patterns 
inputs        % 3 x n final matrix of inputs (accounting for bias)
weights       % 3 x 1 vector of neuron weights
{% endhighlight %}  
  
**Exercise**  
<div markdown="1">  

  1. Update the neuron update loop so that it computes its error (forward propagate and compare to desired)
  2. Update the neuron update loop to perform learning of its weights (based on back-propagation)
  3. Run the complete learning procedure, which should produce a result similar to that displayed below.
  4. Perform multiple re-runs of the learning procedure (re-launching produces different datasets)
  5. What observations can you make on the learning process?
  6. (Optional) Change the input patterns, and confirm your observations.

</div>{: .notice--info}  

;#;
{{:esling:aml_p3_linear1.jpg?nolink&400 |}}{{:esling:aml_p3_linear2.jpg?nolink&400 |}}
;#;

### 3.2 - 2-layer XOR problem
In most cases, classification problems are far from being linear. Therefore, we need more advanced methods to be able to compute non-linear class boundaries. The advantage of neural networks is that the same principle can be applied in a *layer-wise* fashion. This allows to further discriminate the space in sub-regions (as seen in the course). We will try to implement the 2-layer *perceptron* that can provide a solution to the infamous XOR problem.
The idea is now to have the output of the first neurons to be connected to a set of other neurons. 

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

**Exercise**  
<div markdown="1">  

  1. Update the forward propagation and error computation (compared to desired).
  2. Update the back-propagation part to learn the weights of both layers.
  3. Run the complete learning procedure, which should produce a result similar to that displayed below.
  4. Perform multiple re-runs of the learning procedure (re-launching with different initializations)
  5. What observations can you make on the learning process?
  6. What happens if you initialize all weights to zeros?
  7. (Optional) Implement the //sparsity// constraint in your neural network.

</div>{: .notice--info}

;#;
{{:esling:aml_p3_xor1.jpg?nolink&400 |}}{{:esling:aml_p3_xor2.jpg?nolink&400 |}}
;#;

### 3.3 - 3-layer audio classification
We now return to our original classification problem and will try to perform neural network learning on a set of audio files. The data structure will be the same as the one used for parts 1 and 2. As discussed during the courses, even though a 2-layer neural network can provide non-linear boundaries, it can not perform "holes" inside those regions. In order to obtain an improved classification, we will now rely on a 3-layer neural network. The modification to the code of section 3.2 should be minimal, as the back-propagation will be similar for the new layer as one of the two others.


**Exercise**  
<div markdown="1">  

  1. Based on the previous neural network, upgrade the code to a 3-layer neural network
  2. Use the provided code to perform classification on a pre-defined set of features
  3. As previously, change the set of features to assess their different accuracies
  4. Evaluate the neural network accuracy for all features combinations
  5. (Optional) Implement the *sparsity* constraint in your neural network.

</div>{: .notice--info}

