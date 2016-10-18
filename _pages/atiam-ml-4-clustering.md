---
layout: single
permalink: /atiam-ml-4-clustering/
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

# Clustering

<div markdown = "1">

The present tutorials covers the notions of clustering through the k-Means algorithm.

</div>{: .notice--blank}

# Reference slides

<div markdown = "1">
Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.4.Clustering.pdf)

  - Clustering motivations
  - K-Means and k-medoids
  - Hierarchical clustering  

# Tutorial 

<div markdown = "1">
In this part, we will use the principles of clustering to perform *spectral grouping*. The idea is to automatically discover the structure inside a spectrogram by using the simplest algorithm of clustering (k-Means algorithm). Hence, even though the results might be slightly drafty, it can give you a good sense of how to automatically uncover structure in an unsupervised way.  
</div>{: .notice--blank}

## 4.1 K-Means algorithms 

<div markdown = "1">
First to perform the implementation of the K-Means algorithm, the following exercises will rely on a first synthetic dataset (linearly separated Gaussian distributions generated similarly to the SVM exercises). Hence, we will create a data set from two Gaussian distributions in a two-dimensional space.  

Then, to evaluate the limitations of the K-Means algorithm, we will generate a dataset of two circle distributions. We briefly recall here that the most basic way to perform data clustering is to first start with a random guess of the cluster centroids and then alternate between assigning the data points to different clusters and then updating the centroids of corresponding clusters.  
</div>{: .notice--blank}
  
**Exercise**  
<div markdown="1">  

  1. Update the ''kmeanspp'' function to implement the clustering algorithm.
  2. Perform the plot using the spread function to display the results of clustering.
  3. Compare the results depending on the number of clusters (example are displayed below).
  4. What observations can you make on the quality of these clusters ?
  5. Compare your results with the Matlab kMeans function.
  
</div>{: .notice--info}  


;#;
{{:esling:aml_p5_cluster2.jpg?nolink&400 |}}{{:esling:aml_p5_cluster6.jpg?nolink&400 |}}
;#;

## 4.2 Descriptors and grouping

<div markdown = "1">
We will now try to rely on the clustering functions that we just devised to perform an unsupervised grouping of a dataset of audio files. We already provided the code to perform this task, however the tuning is still to be made.  
</div>{: .notice--blank}

**Exercise**  
<div markdown="1">  

  - Check that your ''kmeanspp'' function works on spectral features with 2 clusters.
  - Using the spread function, display the results of clustering for different numbers
  - How to devise a function to compute the overall quality of the clustering ?
  - Devise an algorithm to automatically adapt the number of clusters.
  - Compare results for different number of clusters

</div>{: .notice--info}  


## 4.3 - Spectral Grouping

<div markdown = "1">
In this section, we will rely on the previously implemented kMeans algorithm to perform a spectral clustering and observe the obtained clusterings.  By completing the code yourself, try to perform a binarization followed by a clustering of spectrograms in order to group spectral components together.  
</div>{: .notice--blank}
