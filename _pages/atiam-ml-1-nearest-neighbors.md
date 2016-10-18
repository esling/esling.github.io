---
layout: single
permalink: /atiam-ml-1-nearest-neighbors/
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

# Nearest neighbors

<div markdown = "1">
This tutorials corresponds to the same slides following the introductory developments performed in the [previous tutorial](/atiam-ml-0-intro/). Based on the features computed, we will implement a simple *querying* and *classification* system based on [Nearest Neighbors](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm).
</div>{: .notice--blank}

# Reference slides

<div markdown = "1">
Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.1.Introduction.pdf)

  * Introduction to artificial intelligence
  * Properties of machine learning
  * Nearest-neighbors
</div>{: .notice--blank}

# Tutorial 

<div markdown = "1">

In this tutorial, we will cover the simplest querying and classification algorithm, namely the *$$k$$-Nearest Neighbor* method. The idea is for a given (usually *unknown*) element, to find its closest neighbor(s), based on the distances between this element and the known dataset for a given set of features. Formally, given a set of elements $$e_{i}$$, $$i\in\left[1,N\right]$$ and their corresponding features $$\mathbf{f_{i,k}}\in\mathbb{R}^{n}$$ (which denotes the $$k^{th}$$ feature of the $$i^{th}$$ element, which can be $$n$$-dimensional), we will need to compute a distance measure $$\mathcal{D}\left(\mathbf{f_{i,k}},\mathbf{f_{j,k}}\right)$$ between the features of elements of the dataset. This distance will express the dissimilarity between two features. For the first two questions of the tutorial, we will simply consider that the dissimilarity between features is expressed by their Euclidean $$(l_{2})$$ distance.

$$
\begin{equation}
\mathcal{D}\left(\mathbf{f_{i,k}},\mathbf{f_{j,k}}\right)=\sqrt{\sum_{d=1}^{n}\left(f_{i,k}^{d}-f_{j,k}^{d}\right)^{2}}
\end{equation}
$$

Given distances for each feature, we need to *merge* these various dissimilarities and then select the nearest neighbor of a particular element by computing

$$
\begin{equation}
NN\left(e_{i}\right)=\underset{j\neq i}{argmin}\left(\frac{1}{K}\sum_{k=1}^{K}\left(\mathcal{D}\left(\mathbf{f_{i,k}},\mathbf{f_{j,k}}\right)\right)\right)
\end{equation}
$$

Of course, based on the types of features, different distance measures can be used, such as any of the $$l_{p}$$ distances (a generalization of the Euclidean distance)

$$
l_{p}\left(\mathbf{f_{i,k}},\mathbf{f_{j,k}}\right)=\sqrt[p]{\sum_{d=1}^{n}\left|f_{i,k}^{d}-f_{j,k}^{d}\right|^{p}}
$$

the *Cosine* distance

$$
cosine\left(\mathbf{f_{i,k}},\mathbf{f_{j,k}}\right)=1-\frac{\mathbf{f_{i,k}}\cdot\mathbf{f_{j,k}}}{\left\Vert \mathbf{f_{i,k}}\right\Vert \left\Vert \mathbf{f_{j,k}}\right\Vert }=1-\frac{\sum_{d=1}^{n}f_{i,k}^{d}f_{j,k}^{d}}{\sum_{d=1}^{n}\left(f_{i,k}^{d}\right)^{2}\sum_{d=1}^{n}\left(f_{j,k}^{d}\right)^{2}}
$$

or the *correlation* distance.

$$
correlation\left(\mathbf{f_{i,k}},\mathbf{f_{j,k}}\right)=1-\frac{\mathbf{\left(f_{i,k}-\mu_{\mathbf{f_{i,k}}}\right)}\cdot\left(\mathbf{f_{j,k}}-\mu_{\mathbf{f_{j,k}}}\right)}{\left\Vert \mathbf{f_{i,k}-\mu_{\mathbf{f_{i,k}}}}\right\Vert \left\Vert \mathbf{f_{j,k}}-\mu_{\mathbf{f_{j,k}}}\right\Vert }
$$

The same observation holds for the way we decided to "merge" the different distances. By looking at these given definitions, start by thinking about the following questions.  

</div>{: .notice--blank}

<div markdown="1"> 
**Questions**  

  1. What problems can arise from $$n$$-dimensional audio features?
  2. Based on the selection equation, what constraints are implicitly made on the distances?
  3. Does the Euclidean distance seems like a sound way to measure the similarity between temporal features?

</div>{: .notice--info}  

## 1.1 - Querying 

<div markdown = "1">

First, we can use the nearest-neighbor idea to devise a very simple *querying* system. This type of method is typically used in many systems such as *Query By Humming (QBH)* softwares (similar to [Shazam](http://www.shazam.com/)). As previously, we provide a baseline code in the main script. First, we create a $$ N x f $$ distance matrix `dataMatrix` corresponding to the features of the $$ N $$ elements of the datasets. We selected here only the *SpectralCentroidMean, SpectralFlatnessMean* and *SpectralSkewnessMean* features. Then, after your code is filled, the `dist` matrix should contain the mean distances (eventually, for various types of distances), which will then be sorted to the `nnIDs` vector allowing to select the nearest neighbors.

</div>{: .notice--blank}

<div markdown="1">
**Exercise**  

  1. Compute the set of distances between a random element and the rest of the dataset.
  2. Complete the plotting code in order to plot the element and its 10 nearest neighbors.
  3. Check that you obtain plots similar to those displayed below.
  4. Implement the $$l_{p}$$, *Cosine* and *correlation* distances
  5. Try the same piece of code by varying the distances and the `usedFeatures`.
  6. What can you tell about the discriminative power of features?
  7. What other steps should we perform on the features?
  8. (Optional) Extend your code to include temporal features
  9. (Optional) Extend your code to a fully functional *Query-By-Example* (QBE) system.

</div>{: .notice--info}  

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div1">Reveal</a>]

<div id="div1">
<img src="../images/atiam-ml/01_1.1_percussion.svg" height="350" width="350"/> <img src="../images/atiam-ml/01_1.1_violinbowed.svg" height="350" width="350"/>
</div>

</div>{: .notice--blank}

## 1.2 - Classification

<div markdown = "1">
For the second part of this tutorial, we will rely on the same technique (computing the distance of a selected point to the rest of the dataset) in a *classification* framework. The overarching idea behind $$k$$-NN classification is that elements from a same class should have similar properties in the *feature space*. Hence, the closest feature to those of an element should be from elements of its right class. These types of approaches are usually termed as *distance-based* classification methods. The skeleton for this algorithm is provided in the `01_Nearest_Neighbors/knnClassify.m` function.

{% highlight Matlab %}
function [probas, winnerClass] = knnClassify(dataStruct, testSample, k, normalize, useL1dist);
% This function is used for classifying an unknown sample using the kNN
% algorithm, in its multi-class form.
%
% Arguments :
% - dataStruct  : the data structure
% - testSample  : the input sample id to be classified
% - k           : the k (number of neighbors) parameter
% - distType    : type of distance ['Euclidean', 'Manhattan', 'Cosine'] (optional)
% - normalize   : use class priors to weight results (optional)
% Returns :
% - probas      : an array that contains the classification probabilities for each class
% - winnerClass : the label of the winner class
{% endhighlight %}  

The algorithm will globally look quite similar to the previous one. However, this time we will compute the $$k$$ Nearest Neighbors *for each of the classes separately*, which will allow to consider the resulting distance vectors as probabilities. Hence, we will compute for the set of classes $$\mathcal{C}_{t}$$ the vector of distances, and select the $$k$$ closest elements per class.

$$
\begin{equation}
NN_{\mathcal{C}_{t}}\left(e_{i}\right)=\underset{j\in\mathcal{C}_{t} \wedge j \neq i}{argmin}\left(\frac{1}{K}\sum_{k=1}^{K}\left(\mathcal{D}\left(\mathbf{f_{i,k}},\mathbf{f_{j,k}}\right)\right)\right)
\end{equation}
$$

Then, in order to consider the distances as probabilities, we compute for each class the mean distance of its $$k$$

$$
p_{\mathcal{C}_{t}}\left(e_{i}\right)=\frac{1}{k}\sum{j=1}^{k}NN_{\mathcal{C}_{t}}\left(e_{i}\right)
$$

In the `knnClassify` function, we store in `testFeatures` the vector of features from the element we are trying to classify, and construct a cell of features for each class in the `classFeats` cell.

</div>{: .notice--blank}
  
<div markdown="1">
**Exercise**  

  1. Update the `knnClassify` code to perform the basic k-NN classification function
  2. Run the algorithms for both 1-NN and 5-NN evaluation
  3. Plot the different confusion matrix to visually check the accuracies (you should obtain the values displayed in the following figure).
  4. Extend the code to take various distances into account (argument `distType`)
  5. What is the use of "class weighting" (argument `normalize`)?
  6. Implement the class weighting system and evaluate its effect
  4. Perform the same classification with various K and features to evaluate the properties and qualities of different parametrizations.
  5. (Optional) Automatize the evaluation of various configurations.

</div>{: .notice--info} 

<div markdown = "1">

**Expected output** [<a href="javascript:void(0)" class="abuttons" data-divid="div2">Reveal</a>]

<div id="div2">
<img src="../images/atiam-ml/01_1.2_confusion.svg" height="400" width="800"/>
</div>

</div>{: .notice--blank}

## 1.3 - Evaluation

<div markdown = "1">

When proposing machine learning algorithms, the fundamental aspects lies in correctly evaluating their performances. Depending on the application, methods, dataset and even the nature of corresponding data, a plethora of evaluation measures can be used. We highly recommend the following articles for those interested in machine learning, so that you develop your critical mind and do not limit yourself to narrow evaluations (by relying on statistical tests) and also that you avoid **cherry picking**  

  * Demšar, J. (2006).   *Statistical comparisons of classifiers over multiple data sets.*   The Journal of Machine Learning Research, 7, 1-30.   [PDF![](../images/pdf.png)](http://machinelearning.wustl.edu/mlpapers/paper_files/Demsar06.pdf)  
  * Sturm, B. L. (2013).   *Classification accuracy is not enough.*   Journal of Intelligent Information Systems, **41**(3), 371-406. [PDF![](../images/pdf.png)](http://vbn.aau.dk/files/70797941/Sturm20121030.pdf)  
  * Keogh, E., & Kasetty, S. (2003).   *On the need for time series data mining benchmarks: a survey and empirical demonstration.*   Data Mining and knowledge discovery, **7**(4), 349-371. [PDF![](../images/pdf.png)](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.13.2240&rep=rep1&type=pdf)  

However, for the scope of this tutorial, we will limit ourselves to typical measures minimally required to evaluate your classifier. Overall, the most important aspects of evaluation lies in different ways of comparing the *real labels* (ground truth) to the *assigned labels* (picked by the classifier).

  * The **confusion matrix** is computed simply by counting the occurences in which a particular instance of a real label (row) is classified to an assigned label (column). This code is already provided in the starter code, and all the following measures can be derived directly from it.
  * The **overall accuracy** is computed as the ratio of correctly classified examples divided by the complete number of examples.
  * The (per-class) **precision** defines the ratio of examples correctly assigned to a class divided by the number of instances assigned to that class by the classifier.
  * The (per-class) **recall** defines the ratio of examples correctly assigned to a class divided by the number of instances really belonging to that class.
  * The **F1 measure** is defined as the ratio between the geometric and harmonic means between the precision and recall measures.

You can implement these measures by simply completing the starter code. If you have doubts about the implementation of these measures, you can check the corresponding [Wikipedia article](https://en.wikipedia.org/wiki/Precision_and_recall)

</div>{: .notice--blank}

<div markdown="1">
**Exercise**  

  1. Implement the *accuracy*, *recall*, *precision* and *F1 measure*
  2. Evaluate the previous algorithms with your new measures.
  3. Perform an automatization of the previous evaluations.
  4. Run the automatic evaluation for different K, distances and features.
  5. Plot the corresponding results for comparison

</div>{: .notice--info} 
