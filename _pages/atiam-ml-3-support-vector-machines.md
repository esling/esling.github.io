---
layout: single
permalink: /atiam-ml-3-support-vector-machines/
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

# Support vector machines

<div markdown = "1">

The present tutorials covers the implementation of Support Vector Machines (SVM) and the notions of kernels.

</div>{: .notice--blank}

# Reference slides

<div markdown = "1">

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.3.Support.Vector.Machines.pdf)

  - Support Vector Machines
  - Properties of kernels 

</div>{: .notice--blank}

# Tutorial 

<div markdown = "1">

In this tutorial, we will cover a more advanced classification algorithm through the use of *Support Vector Machines* (SVMs). The goal is to gain an intuition of how SVMs works and how to use *Gaussian kernel* with SVMs to find out the decision boundary. The implementation proposed here follows the *Sequential Minimal Optimization* (SMO) algorithm for training support vector machines. You can find the full details on the mathematics involved in the following [paper link](http://cs229.stanford.edu/materials/smo.pdf).

Once again, to simplify your work, we provide the following set of functions that you should find in the *3_Support_Vector_Machines* folder


  |**File**|*Explanation*|
  |-------:|:------------|
  |`example1.mat`|Example data for a quasi-linear problem|
  |`example2.mat`|Example data for a non-linear but well-defined problem|
  |`example3.mat`|Example data for a slightly non-linear problem with outliers|
  |`plotData.m`|Allows to plot the set of data points|
  |`visualizeBoundary.m`|Plots a non-linear decision boundary from a SVM model|
  |`visualizeBoundaryLinear.m`|Plots a linear decision boundary|

</div>{: .notice--blank}

## 3.1 - Linear classification

<div markdown = "1">

We briefly recall here that the goal of SVMs is that given a set of input vectors $$ \mathbf{x} $$ separated in two classes ($$ \mathbf{x}^{+} $$ and $$ \mathbf{x}^{-} $$, we would like to find the *optimal boundary* (separating line) between the two classes. To do so, we want to find the separation that gives the *maximal margin* between the two sets. Hence, let us first try to find a solution to the following problem

$$
\begin{equation}
\begin{cases}
\mathbf{w}\cdot\mathbf{x}^{+}+\mathbf{b}\geq1\\
\mathbf{w}\cdot\mathbf{x}^{-}+\mathbf{b}\leq-1
\end{cases}
\label{eq1}
\end{equation}
$$

By setting the variable $$ y_{i}={+}/{-}1 $$, we can rewrite this problem as 

$$
\begin{equation}
y_{i}\left(x_{i}\cdot\mathbf{w}+\mathbf{b}\right)-1\geq0
\label{eq2}
\end{equation}
$$

The idea is that for some of the input vectors (called *support vectors*), we will have an equality in equation (1), where $$ \mathbf{w}\cdot\mathbf{x}^{+}+\mathbf{b}=1 $$ and $$ \mathbf{w}\cdot\mathbf{x}^{-}+\mathbf{b}=-1 $$. By substracting those two equation, we see that we are trying to find a solution to 

$$
\begin{equation}
\frac{\mathbf{w}}{\left\Vert \mathbf{w}\right\Vert }\cdot\left(x^{+}-x^{-}\right)=\frac{2}{\left\Vert \mathbf{w}\right\Vert }=Width
\label{eq3}
\end{equation}
$$

Therefore, solving the set of equations amounts to find the maximal margin between the support vectors (as they *support* classification).
 
For the first part of this tutorial, we will compute the main iterations of the algorithm (minimization of the objective function), while relying on a *linear* kernel. This implies that we will only be able to perform linear discrimination. However, remember that the formulation of the SVMs provide an *optimal* and (gloriously) *convex* answer to this problem.

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

</div>{: .notice--blank}

**Exercise**  
<div markdown="1">  

  1. Update the `svmTrain` code to perform the training of a SVM with linear kernel.
  2. Run your `svmTrain` function on the `example1.mat` (linear) dataset, you should obtain the result displayed below.
  3. Update the overall framework to display the decision boundary at each iteration of the algorithm.

</div>{: .notice--info}  

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div1">Reveal</a>]

<div id="div1">
<img src="../images/atiam-ml/00_0.2_bells.svg" height="350" width="350"/> <img src="../images/atiam-ml/00_0.2_speech.svg" height="350" width="350"/>
</div>

</div>{: .notice--blank}

## 3.2 - Gaussian kernel

**Exercise**  
<div markdown="1">  

  1. Update your `svmTrain` code to be able to rely on a Gaussian (RBF) kernel instead of a linear one.
  2. Run your `svmTrain` function on the `example2.mat` (non-linear) dataset, you should obtain the result displayed below.
  3. Once again, display the decision boundary at each iteration of the algorithm.

</div>{: .notice--info}  

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div2">Reveal</a>]

<div id="div2">
<img src="../images/atiam-ml/00_0.2_bells.svg" height="350" width="350"/> <img src="../images/atiam-ml/00_0.2_speech.svg" height="350" width="350"/>
</div>

</div>{: .notice--blank}
