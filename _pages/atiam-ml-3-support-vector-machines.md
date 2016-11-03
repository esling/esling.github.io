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

In this tutorial, we will cover a more advanced classification algorithm through the use of *Support Vector Machines* (SVMs). The goal is to gain an intuition of how SVMs works and how to use *Gaussian kernel* with SVMs to find out the decision boundary. The implementation proposed here follows a simplified version of the *Sequential Minimal Optimization* (SMO) algorithm for training support vector machines, which is detailed in the following [paper](http://cs229.stanford.edu/materials/smo.pdf). The complete SMO algorithm can then be quite easily implemented following the [full paper](https://www.microsoft.com/en-us/research/wp-content/uploads/2016/02/tr-98-14.pdf).

Once again, to simplify your work, we provide the following set of functions that you should find in the `03_Support_Vector_Machines` folder


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

Therefore, solving the set of equations amounts to find the maximal margin between the support vectors (as they *support* classification). As seen in the slides, we know that this problem can also be expressed as  

$$
\begin{equation}
f\left(x\right)=\sum_{i=1}^{m}\alpha_{i}y_{i}\left\langle \phi\left(x_{i}\right),\phi\left(x\right)\right\rangle +b
\end{equation}
$$

Where we can introduce a kernel $$K\left(x_{i},x\right)=\phi\left(x_{i}\right)\cdot\phi\left(x\right)$$ in the equation in order to solve non-linear optimization problems. We can use this formulation to perform the *predictions* of the algorithm and in the first part of this tutorial, we will only conider the *linear* kernel $$K\left(x_{i},x\right)=x_{i}\cdot x$$. Computing the predictions should be performed in the `svmPredict` function

{% highlight Matlab %}
function pred = svmPredict(model, X)
% Returns a vector of predictions using a trained SVM model (svmTrain). 
% X       : m x n matrix where each example is a row. 
% model   : svm model returned from svmTrain.
% pred    : m x 1 column vector of class predictions ({0, 1} values).
{% endhighlight %}  

</div>{: .notice--blank}

**Exercise**  
<div markdown="1">  

  1. Update the `svmPredict` code to compute the SVM prediction (only with a linear kernel).
  2. Run the predictions on random initializations of the models

</div>{: .notice--info}  

**Learning phase**
<div markdown = "1">
In order to perform learning, we will try to maximize the *dual formulation* problem expressed as

$$
\begin{equation}
w\left(\alpha\right)=\sum_{i}\alpha_{i}-\frac{1}{2}\sum_{i}\sum_{j}y_{i}y_{j}\alpha_{i}\alpha_{j}\left\langle \phi\left(x_{i}\right),\phi\left(x_{j}\right)\right\rangle 
\end{equation}
$$

with $$0\leq \alpha_{i} \leq C$$ and $$\sum_{i=1}^{m}{\alpha_{i} y_{i}} = 0$$. $$C$$ is a chosen *regularization hyper-parameter*. To ease your work, we will implement only a simplified version of the SMO algorithm which is mainly focused on the optimization aspects. The SMO algorithm selects two $$\alpha$$ parameters, $$\alpha_{i}$$ and $$\alpha_{j}$$ and optimizes the objective value jointly for both these $$\alpha_{i,j}$$. Finally it adjusts the $$b$$ parameter based on the new $$\alpha_{i,j}$$. This process is repeated until the $$\alpha_{i,j}$$ converge.

**Selecting $$\alpha$$.** The full SMO algorithm use heuristics to choose which $$\alpha_{i}$$ and $$\alpha_{j}$$ to optimize (which greatly increase the convergence speed. However, for this simplified version, we will simply iterate on all $$\alpha_{i},i=1,\cdots ,m$$ and select a random $$\alpha_{j}$$, to perform the joint optimization of $$\alpha_{i}$$ and $$\alpha_{j}$$

**Optimizing $$\alpha_{i}$$ and $$\alpha_{j}$$.** To jointly optimize the value, we first find bounds $$L$$ and $$H$$ such that $$L\leq \alpha_{j} \leq H$$ holds to satisfy the constraint of the original problem $$0\leq \alpha_{i} \leq C$$

$$
\begin{array}{ccc}
if\mbox{ }y_{i}\neq y_{j}, & L=max\left(0,\alpha_{j}-\alpha_{i}\right), & H=min\left(C,C+\alpha_{j}-\alpha_{i}\right)\\
if\mbox{ }y_{i}=y_{j}, & L=max\left(0,\alpha_{i}+\alpha_{j}-C\right), & H=min\left(C,\alpha_{i}+\alpha_{j}\right)
\end{array}
$$

Now we want to find $$\alpha_{j}$$ so as to maximize the objective function. It can be shown (as in the original paper) that the optimal $$\alpha_{j}$$ is given by

$$
\alpha_{j}=\alpha_{j}-\frac{y_{j}\left(E_{i}-E_{j}\right)}{\eta}
$$

where

$$
\begin{array}{ccc}
E_{k} & = & f\left(x_{k}\right)-y_{k}\\
\eta & = & 2\left\langle x_{i},x_{j}\right\rangle -\left\langle x_{i},x_{i}\right\rangle -\left\langle x_{j},x_{j}\right\rangle 
\end{array}
$$

$$E_{k}$$ defines the error between the prediction of the SVM on the example $$k$$ and its desired label. When computing $$\eta$$, we can also replace the inner product by a kernel function $$K$$. Finally, we clip the value of $$\alpha_{j}$$ to lie within the selected bounds.

$$
\alpha_{j}=\begin{cases}
H & if\mbox{ }\alpha_{j}>H\\
\alpha_{j} & if\mbox{ }L\leq\alpha_{j}\leq H\\
L & if\mbox{ }\alpha_{j}<L
\end{cases}
$$

Now that we have solved $$\alpha_{j}$$, we can update the value for $$\alpha_{i}$$ through

$$
\alpha_{i}^{t}=\alpha_{i}^{t-1}+y_{i}y_{j}\left(\alpha_{j}^{(t-1)}-\alpha_{j}\right)
$$


**Computing threshold $$b$$.** Finally, we can compute the threshold $$b$$ to satisfy the original constraints by selecting

$$
b=\begin{cases}
b_{1} & if\mbox{ }0<\alpha_{i}<C\\
b_{2} & if\mbox{ }0<\alpha_{j}<C\\
\left(b_{1}+b_{2}\right)/2 & otherwise
\end{cases}
$$

where

$$
b_{1}=b-E_{i}-y_{i}\left(\alpha_{i}^{(t-1)}-\alpha_{i}\right)\left\langle x_{i},x_{i}\right\rangle -y_{j}\left(\alpha_{j}^{(t-1)}-\alpha_{j}\right)\left\langle x_{i},x_{j}\right\rangle   
$$
$$
b_{2}=b-E_{i}-y_{i}\left(\alpha_{i}^{(t-1)}-\alpha_{i}\right)\left\langle x_{i},x_{j}\right\rangle -y_{j}\left(\alpha_{j}^{(t-1)}-\alpha_{j}\right)\left\langle x_{j},x_{j}\right\rangle 
$$

For the first part of this tutorial, we will compute the main iterations of the algorithm (minimization of the objective function), while relying on a *linear* kernel. This implies that we will only be able to perform linear discrimination. However, remember that the formulation of the SVMs provide an *optimal* and (gloriously) *convex* answer to this problem.

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
  2. Run your `svmTrain` function on the `example1.mat` (linear) dataset to obtain the result displayed below.
  3. Update the framework to display the decision boundary at each iteration of the algorithm.

</div>{: .notice--info}  

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div1">Reveal</a>]

<div id="div1">
<img src="../images/atiam-ml/00_0.2_bells.svg" height="350" width="350"/> <img src="../images/atiam-ml/00_0.2_speech.svg" height="350" width="350"/>
</div>

</div>{: .notice--blank}

## 3.2 - Gaussian kernel

<div markdown = "1">

The Gaussian kernel (also called *Radial Basis Function (RBF)* kernel) allows to perform the optimization of non-linear classification problems. It is defined as  

$$
K\left(x,y\right)=exp\left(\frac{-\left\Vert x-y\right\Vert ^{2}}{\left(2\sigma^{2}\right)}\right)
$$

As seen in the slides, the underlying idea is that instead of trying to solve a non-linear separation problem in a given space, we might first transform the space into a target space in which the problem is linearly separable. Therefore, we transform the space through a kernel (which is directly expressed in the minimization problem) and solve the linear separation problem in the target space. Given the starter code and the previous exercise, you should be able to directly plug this kernel inside the `svmTrain` and `svmPredict` functions.

</div>{: .notice--blank}

**Exercise**  
<div markdown="1">  

  1. Update the `svmPredict` code to be able to rely on a Gaussian kernel.
  2. Update the `svmTrain` code to be able to rely on a Gaussian kernel.
  2. Run the `svmTrain` function on the `example2.mat` (non-linear) dataset to obtain the result displayed below.
  3. Once again, display the decision boundary at each iteration of the algorithm.

</div>{: .notice--info}  

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div2">Reveal</a>]

<div id="div2">
<img src="../images/atiam-ml/00_0.2_bells.svg" height="350" width="350"/> <img src="../images/atiam-ml/00_0.2_speech.svg" height="350" width="350"/>
</div>

</div>{: .notice--blank}

## 3.3 - Supplementary kernels

<div markdown = "1">

Now that you have mastered the concept of kernels and updated your code to include the Gaussian kernel, you can augment your classifier and optimizaton problem to include several different kernels as those proposed afterwards.

**Polynomial kernel.** Intuitively, the polynomial kernel looks not only at the given features of input samples to determine their similarity, but also combinations of these. 

$$
K\left(x,y\right)=\left(x^{T}y+1\right)^{d}
$$

**Sigmoid (tanh) kernel.** This kernel takes two parameters: $$a$$ and $$r$$. For $$a > 0$$, we can view $$a$$ as a scaling parameter of the input data, and $$r$$ as a shifting parameter that controls the threshold of mapping. For $$a < 0$$, the dot-product of the input data is not only scaled but reversed.

$$
K\left(x,y\right)=tanh\left(kx^{T}y+\Theta\right)
$$

</div>{: .notice--blank}

**Exercise**  
<div markdown="1">  

  1. Update the `svmPredict` code to include supplementary kernels.
  2. Update the `svmTrain` code to include supplementary kernels.

</div>{: .notice--info}  

## 3.4 - Audio application

<div markdown = "1">

As seen in the previous tutorial, we have considered only a *binary classification* problem (where elements can only belong to one of two classes). This simplifies the work as we simply need to separate the space between two types of points. However, in real-world problems, we usually want to solve *multi-class* problems with any given number of classes. For this tutorial, we will rely on a simple trick which is to consider that a $$n$$-class problem can simply be restated as $$n$$ different binary classification problems. The underlying idea is that each class defines a binary classifier which tells us if a given element is part of this class, or belongs to *any of the other* classes.

</div>{: .notice--blank}

**Exercise**  
<div markdown="1">  

  1. Change the training loop to define $$n$$ separate binary problems
  2. For each problem, train an SVM to perform classification.
  3. Evaluate the global classification accuracy of your system.

</div>{: .notice--info}  
