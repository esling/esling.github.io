---
layout: single
permalink: /atiam-ml-5-boosting/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

{% include toc %}

# Meta-heuristics

The present tutorials covers .

# Reference slides

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.5.Boosting.pdf)

The corresponding slides cover

  - Genetic algorithms
  - Boosting  

## Tutorial 

### 4.0 - The Adaboost algorithm

We recall here quickly the principles of boosting. We consider a dataset, for which each datapoint $$ \mathbf{x} $$, we have assigned a target **label** $$ \mathbf{d} $$. We use the already labelled data as **training data** in order to perform learning. We will consider here **binary classifications**, meaning that the labels can only be one of two values.

Each input datapoint $$ \mathbf{x} \in \mathbb{R}^{n} $$ is actually a vector containing several dimensions. In the framework of *boosting*, we first notice that (as we are in a binary classification setup), we can generate a classifier for our dataset using only a single parameter (ie. one of the dimensions $$ x_{i}, i \in \left[1,n\right] $$ of the input vectors), by simply selecting a ** threshold ** value $$ t $$. Therefore, a classification decision could be made by simply computing

$$
\begin{equation}
y = \left( x_{i} \geq t\right)
\end{equation}
$$

We could have generated a different classifier by simply choosing a different threshold or a different input dimension. Therefore, a classifier can be uniquely defined by choosing a parameter, and a threshold for that parameter, ie. $$\mathcal(C)_{k} = {i, t}$$. We consider these classifiers as **weak classifiers**, which is just a classifier that is better than pure guessing. That is, it classifies more than half of the labelled data correctly. Even if it's success rate is just 51%, it still counts as a weak classifier. (Oppositely, a **strong classifier** is one that has a very good success rate, like 90%).

Now the main question is, can we quantitatively combine several weak classifier and weight them in order to obtain a strong classifier ? The main idea behind solving this is that we could rely not only on which weak classifier performs, but mostly *on which point* do they work? This is the **"boosting"** in Adaboost. It boosts the weightage of classifiers that are more relevant. 

We will be considering here, the Adaboost (**Adaptive Boosting**) algorithm, which is an iterative solution to our main question.

  1. In the first iteration, we pick the most accurate amongst all weak classifiers.
  2. This weak classifier must have obviously misclassified a lot of datapoints (a little less than half). The classifier that we pick in the next iteration should then be better at correctly classifying **this misclassified data**. To do so, **each data point is assigned a weight**. (in the first iteration, obviously all the datapoints had equal weightage). Then the weight of the misclassified datapoints is incremented, and that of correctly labelled data is decremented. So the error rate of the second classifier is calculated as a weighted sum: if it misclassifies an already misclassified datapoint, it gets a higher error rate. 
  3. In the second iteration, the classifier with the smallest error rate on the weighted data is chosen. Now we have chosen two weak classifiers. We again increment the weights of the datapoints that are collectively misclassified by the two weak classifiers, and decrement the weigths of the ones that they correctly classify.
  4. We repeat this process of reassigning weights and picking weak classifiers on the weighted data until we have made the error rate as small as we like.

So in a nutshell: Adaboost takes a lot of weak classifiers, assigns them appropriate weights, to make a strong classifier.

### 4.1 - Defining weak classifiers

We discussed how a classifier can be defined by selecting a parameter and a threshold for this parameter. 
The output of this classifier that we have defined would be +1 or -1 depending on whether the input's value for this parameter is greater than or smaller than the threshold, as we have discussed before.

But we had also talked about generating an error rate for weak classifiers in every iteration, on the weighted dataset. 
The following lines of code define a function weak_Classifier_error() that takes a weak classifier, a labelled and weighted dataset as input. 
*It's output is the error rate for this weak classifier on the dataset for the given weights.*
And the error rate, as mentioned before, just a weighted sum of the errors. 
The weigths are: 0 if it is correctly classified and 1 if incorrectly classified.
This simplfies to simply:
**Error rate= Sum of weigths of datapoints that were classified incorrectly**

But wait you say: The arguments for this function are threshold, dimension, sign, weight and label. Where is the weak classifier? Remember, how we said that a classifier is *uniquely* defined by it's parameter and threshold values? So we just input these.

Also, the use of 'sign' is simple: It basically flips the classifier on it's head. If sign is +1, then it will classify data as +1 if it is *greater* than threshold. If sign is -1, it will classify data as +1 if it is *smaller* than threshold.

We provide a set of datapoints  

** Exercise **  
<div markdown = "1">

  1. Implement the `weakClassifier_error` function that computes the error of a weak classifier based on its threshold, target dimension and the *weighted* dataset of examples.
  2. Implement different methods to generate different weak classifiers
      1. Grid search 
      2. Random generation
      3. Candidate pool
  3. Fill the main steps of the boosting loop 
  4. Plot the evolution the error rate across 
  5. Plot the different steps of classification in the input space

</div>{: .notice--info} 

{% highlight Matlab %}

{% endhighlight %}

### 4.2 - Main algorithm

### 4.3 - Audio application
