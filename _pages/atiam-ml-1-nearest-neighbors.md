---
layout: single
permalink: /atiam-ml-1-nearest-neighbors/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

# Nearest neighbors

The present tutorials covers .

## [![](../images/pdf.png)](../documents/MML.Lesson.1.Introduction.pdf) Slides

The corresponding slides cover
  * Introduction to artificial intelligence
  * Properties of machine learning
  * Nearest-neighbors

## Tutorial 

In this tutorial, we will cover the simplest querying and classification algorithms derived from the k-Nearest Neighbor method. The idea is to find the closest neighbor to a point by assessing its multi-dimensional distance to the rest of the dataset.\\

INSERT MATH HERE

By looking at the previously given definitions, start by thinking about the following questions.

\\
<blockquote>
** Questions **
  - We considered that features were n-dimensional, but what problems can arise from audio features?
  - If we consider the equation of nearest neighbor, what constraints are implicitly made on the distances?
  - Does the Euclidean distance seems like a sound way to measure the similarity between temporal features?
</blockquote>
\\

== 2.2 - Querying ==

In a first step, we can use the nearest-neighbor method to devise a very simple //querying// system. This type of method is typically used in many systems such as //Query By Humming (QBH)// softwares (similar to [[http://www.shazam.com/|Shazam]]). As previously, we provide a baseline code in the main script. This allows to create a ''n x f'' distance matrix ''dataMatrix'' corresponding to the features of the ''n'' elements of the datasets. We selected here only the //SpectralCentroidMean, SpectralFlatnessMean// and //SpectralSkewnessMean// features.

\\
<blockquote>
** Exercice to perform **
  - Complete the code to compute the set of distances between a random element and the rest of the dataset.
  - Complete the plotting code in order to plot the element and its 10 nearest neighbors.
  - Check that you obtain plots similar to those displayed below.
  - Try the same piece of code by varying the ''usedFeatures'' list
  - What can you tell about the discriminative power of features?
  - (Optional) Extend your code to include temporal features
  - (Optional) Extend your code to a fully functional //Query-By-Example// (QBE) system.
</blockquote>
\\

;#;
{{:esling:aml_p2_query1.jpg?nolink&400 |}}{{:esling:aml_p2_query2.jpg?nolink&400 |}}
;#;
\\

== 2.2 - Classification ==

For the second part of this tutorial, we will rely on the same technique (computing the distance of a selected point to the rest of the dataset) in a classification framework. The overarching idea behind kNN classification is that elements from a same class should have similar properties in the //feature space//. Hence, the closest feature to those of an element should be from elements of its right class. These types of approaches are usually termed as //distance-based// classification methods.

<code matlab>
function [probas, winnerClass] = knnClassify(dataStruct, testSample, k, normalize, useL1dist);
% This function is used for classifying an unknown sample using the kNN
% algorithm, in its multi-class form.
%
% Arguments :
% - dataStruct  : the data structure
% - testSample  : the input sample id to be classified
% - k           : the k (number of neighbors) parameter
% - normalize   : use class priors to weight results
% - useL1dist   : use L1 instead of L2 distance
% Returns :
% - probas      : an array that contains the classification probabilities for each class
% - winnerClass : the label of the winner class
</code>
\\
<blockquote>
** Exercice to perform **
  - Update the ''knnClassify'' code to perform the k-NN classification function
  - Run the algorithms for both 1-NN and 5-NN evaluation
  - Plot the different confusion matrix to visually check the accuracies (you should obtain the values displayed in the following figure).
  - Perform the same classification with various K and features to evaluate the properties and qualities of different parametrizations.
  - (Optional) Automatize the evaluation of various configurations.
</blockquote>
\\

###
{{:esling:aml_p2_class.jpg?nolink&800 |}}
###
\\

== 2.3 - Evaluation ==
When proposing new algorithms for machine learning problems, the fundamental aspects of corresponding research lies in correctly evaluating their performances. Depending on the application, method proposed, dataset and even the nature of corresponding data, a plethora of evaluation measures can be used. We highly recommend the following articles for those interested in future work around machine learning, so that you develop your critical mind and do not limit yourself to narrow evaluations (by relying on statistical tests) and also that you avoid //cherry picking//\\
  * Demšar, J. (2006). //Statistical comparisons of classifiers over multiple data sets.// The Journal of Machine Learning Research, 7, 1-30. [ [[http://machinelearning.wustl.edu/mlpapers/paper_files/Demsar06.pdf|PDF Link]] ]
  * Sturm, B. L. (2013). //Classification accuracy is not enough.// Journal of Intelligent Information Systems, 41(3), 371-406. [ [[http://vbn.aau.dk/files/70797941/Sturm20121030.pdf|PDF Link]] ]
  * Keogh, E., & Kasetty, S. (2003). //On the need for time series data mining benchmarks: a survey and empirical demonstration.// Data Mining and knowledge discovery, 7(4), 349-371. [ [[http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.13.2240&rep=rep1&type=pdf|PDF Link]] ]\\

However, for the scope of this tutorial, we will stick to the typical measures that are minimally required to evaluate your classifier. Overall, the most important aspects of evaluation lies in different ways of comparing the //real labels// (ground truth) to the //assigned labels// (picked by the classifier).

  * The **confusion matrix** is computed simply by counting the occurences in which a particular instance of a real label (row) is classified to an assigned label (column). This code is already provided in the starter code, and all the following measures can be derived directly from it.
  * The **overall accuracy** is computed as the ratio of correctly classified examples divided by the complete number of examples.
  * The (per-class) **precision** defines the ratio of examples correctly assigned to a class divided by the number of instances assigned to that class by the classifier.
  * The (per-class) **recall** defines the ratio of examples correctly assigned to a class divided by the number of instances really belonging to that class.
  * The **F1 measure** is defined as the ratio between the geometric and harmonic means between the precision and recall measures.

You can implement these measures by simply completing the starter code. If you have doubts about the implementation of these measures, you can check the corresponding [[https://en.wikipedia.org/wiki/Precision_and_recall|Wikipedia article]]
