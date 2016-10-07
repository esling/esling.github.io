---
layout: single
permalink: /atiam-ml-3-support-vector-machines/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

{% include toc %}

# Support vector machines

The present tutorials covers the implementation of Support Vector Machines (SVM) and the notions of kernels.

# Reference slides

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.3.Support.Vector.Machines.pdf)

The corresponding slides cover

  - Support Vector Machines
  - Properties of kernels 

# Tutorial 

In this tutorial, we will cover a more advanced classification algorithm through the use of *Support Vector Machines* (SVMs). The goal is to gain an intuition of how SVMs works and how to use *Gaussian kernel* with SVMs to find out the decision boundary. The implementation proposed here follows the *Sequential Minimal Optimization* (SMO) algorithm for training support vector machines. You can find the full details on the mathematics involved in the following [paper link](http://cs229.stanford.edu/materials/smo.pdf).

Once again, to simplify your work, we provide the following set of functions that you should find in the *3_Support_Vector_Machines* folder

  * `example1.mat` - Example data for a quasi-linear problem
  * `example2.mat` - Example data for a non-linear but well-defined problem
  * `example3.mat` - Example data for a slightly non-linear problem with outliers
  * `plotData.m` - Allows to plot the set of data points
  * `visualizeBoundary.m` - Plots a non-linear decision boundary from a SVM model
  * `visualizeBoundaryLinear.m` - Plots a linear decision boundary

### 4.1 - Linear classification

For the first part of this tutorial, we will compute the main iterations of the algorithm (minimization of the objective function), while relying on a *linear* kernel. This implies that we will only be able to perform linear discrimination. However, remember that the SVM will provide an optimal and (gloriously) convex answer to this problem.

{% highlight Matlab %}
function pred = svmPredict(model, X)
% Returns a vector of predictions using a trained SVM model (svmTrain). 
% X       : m x n matrix where each example is a row. 
% model   : svm model returned from svmTrain.
% pred    : m x 1 column vector of class predictions ({0, 1} values).
{% endhighlight %}  

{% highlight Matlab %}
function [model] = svmTrain(X, Y, C, kernelFunction, tol, maxIter)
% Trains an SVM classifier using a simplified SMO algorithm. 
% X       : m x n matrix of m training examples (with n-dimensional features).
% Y       : column vector of class identifiers
% C       : standard SVM regularization parameter
% tol     : tolerance value used for determining equality of floating point numbers. 
% maxIter : number of iterations over the dataset before the algorithm stops.
{% endhighlight %}  

**Exercise**  
<div markdown="1">  

  1. Update the `svmTrain` code to perform the training of a SVM with linear kernel.
  2. Run your `svmTrain` function on the `example1.mat` (linear) dataset, you should obtain the result displayed below.
  3. Update the overall framework to display the decision boundary at each iteration of the algorithm.

</div>{: .notice--info}  

;#;
{{:esling:aml_p4_linear_data.jpg?nolink&400 |}}{{:esling:aml_p4_linear_bounds.jpg?nolink&400 |}}
;#;

### 4.2 - Gaussian kernel

**Exercise**  
<div markdown="1">  

  1. Update your `svmTrain` code to be able to rely on a Gaussian (RBF) kernel instead of a linear one.
  2. Run your `svmTrain` function on the `example2.mat` (non-linear) dataset, you should obtain the result displayed below.
  3. Once again, display the decision boundary at each iteration of the algorithm.

</div>{: .notice--info}  
\\

;#;
{{:esling:aml_p4_gaussian_data.jpg?nolink&400 |}}{{:esling:aml_p4_gaussian_bounds.jpg?nolink&400 |}}
;#;
