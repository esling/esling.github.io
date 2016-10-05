---
layout: single
permalink: /atiam-ml-2-neural-networks/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

# Neural networks

The present tutorials covers .

## [![](../images/pdf.png)](../documents/MML.Lesson.2.Neural.networks.pdf) Slides

The corresponding slides cover

  - The artificial neuron
  - Neural networks
  - Architecture zoo  

## Tutorial 

In this tutorial, we will cover a more advanced classification algorithm through the use of neural networks. The tutorial starts by performing a simple single neuron discrimination of two random distributions. Then, we will study the typical XOR problem by using a more advanced 2-layer perceptron. Finally, we generalize the use of neural networks in order to perform classification on our set of audio files.

To simplify your work, we provide the following set of functions that you should find in the //2_Neural_Networks// folder
  * ''plot3view.m'' - Allows to plot a 3-dimensional view of data points
  * ''plotBoundary.m'' - Plots the decision boundary of a single neuron with 2-dimensional inputs
  * ''plotBoundarySurface.m'' - Plots the decision surface of a single neuron with 3-dimensional inputs
  * ''plotBpBoundary.m'' - Plots multiple decision boundaries for a set of hidden units
  * ''plotBpPats.m'' - Plots input patterns for back-propagation
  * ''plotPats.m'' - Plots input patterns for single neuron problems
  * ''plotPats3D.m'' - Plots 3-dimensional input patterns for single neuron problems
  * ''xorAns.dat'' - Class values for the XOR problem
  * ''xorPats.dat'' - Point values for the XOR problem


== 3.1 - Single neuron discrimination ==

For the first parts of the tutorial, we will perform the simplest classification model possible in a neural network setting, a single neuron. We briefly recall here that 

\\
Therefore, a single neuron can only perform a //linear// discrimination of the space. We will start by training a single neuron to learn how to perform this discrimination with a linear problem (so that it can solve it). To produce such classes of problems, we provide a script that draw a set of random 2-dimensional points, then choose a random line in this space that will act as the linear frontier between 2 classes (hence defining a linear 2-class problem). The variables that will be used by your code are the following.

<code matlab>
patterns      % 2 x n matrix of random points
desired       % classes of the patterns 
inputs        % 3 x n final matrix of inputs (accounting for bias)
weights       % 3 x 1 vector of neuron weights
</code>
\\
<blockquote>
** Exercice to perform **
  - Update the neuron update loop so that it computes its error (forward propagate and compare to desired)
  - Update the neuron update loop to perform learning of its weights (based on back-propagation)
  - Run the complete learning procedure, which should produce a result similar to that displayed below.
  - Perform multiple re-runs of the learning procedure (re-launching produces different datasets)
  - What observations can you make on the learning process?
  - (Optional) Change the input patterns, and confirm your observations.
</blockquote>
\\

;#;
{{:esling:aml_p3_linear1.jpg?nolink&400 |}}{{:esling:aml_p3_linear2.jpg?nolink&400 |}}
;#;

== 3.2 - 2-layer classification on the XOR problem ==
In most cases, classification problems are far from being linear. Therefore, we need more advanced methods to be able to compute non-linear class boundaries. The advantage of neural networks is that the same principle can be applied in a //layer-wise// fashion. This allows to further discriminate the space in sub-regions (as seen in the course). We will try to implement the 2-layer //perceptron// that can provide a solution to the infamous XOR problem.
The idea is now to have the output of the first neurons to be connected to a set of other neurons. 

We provide the prototypical set of XOR values in the ''xorPat.mat'' along with their class values in ''xorAns.mat'' The variables that will be used by your code are the following.

<code matlab>
patterns          % 2 x n matrix of random points
desired           % classes of the patterns 
inputs1           % 3 x n final matrix of inputs (accounting for bias)
nHiddens          % Number of hidden units
learnRate         % Learning rate parameter
momentum          % Momentum parameter
weights1          % 1st layer weights
weights2          % 2nd layer weights
TSS_Limit         % Sum-squared error limit
</code>
\\
<blockquote>
** Exercice to perform **
  - Update the forward propagation and error computation (compared to desired).
  - Update the back-propagation part to learn the weights of both layers.
  - Run the complete learning procedure, which should produce a result similar to that displayed below.
  - Perform multiple re-runs of the learning procedure (re-launching with different initializations)
  - What observations can you make on the learning process?
  - What happens if you initialize all weights to zeros?
  - (Optional) Implement the //sparsity// constraint in your neural network.
</blockquote>
\\

;#;
{{:esling:aml_p3_xor1.jpg?nolink&400 |}}{{:esling:aml_p3_xor2.jpg?nolink&400 |}}
;#;

== 3.3 - 3-layer generalization to audio classification ==
We now return to our original classification problem and will try to perform neural network learning on a set of audio files. The data structure will be the same as the one used for parts 1 and 2. As discussed during the courses, even though a 2-layer neural network can provide non-linear boundaries, it can not perform "holes" inside those regions. In order to obtain an improved classification, we will now rely on a 3-layer neural network. The modification to the code of section 3.2 should be minimal, as the back-propagation will be similar for the new layer as one of the two others.

\\
<blockquote>
** Exercice to perform **
  - Based on the previous neural network, upgrade the code to a 3-layer neural network
  - Use the provided code to perform classification on a pre-defined set of features
  - As previously, change the set of features to assess their different accuracies
  - Evaluate the neural network accuracy for all features combinations
  - (Optional) Implement the //sparsity// constraint in your neural network.
</blockquote>
\\
