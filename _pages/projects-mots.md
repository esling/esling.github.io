---
layout: single
permalink: /projects-mots/
author_profile: false
sidebar:
  nav: "research-projects"
---

### Multiobjective time series matching
We present here an innovative problem that can be casted into a new approach merging multiobjective optimization and time series matching algorithms, called //MultiObjective Time Series// (MOTS) matching. We formally state this novel problem that could lead to a whole range of applications in several fields of research and report an efficient implementation. This approach allowed in the scope of sound samples querying to cope with the multidimensional nature of timbre perception and also to obtain a whole set of efficient propositions rather than a single best solution.

====== Multiobjective Time Series Matching ======

We present here an innovative problem that can be casted into a new approach merging multiobjective optimization and time series matching algorithms, called //MultiObjective Time Series// (MOTS) matching. We formally state this novel problem that could lead to a whole range of applications in several fields of research and report an efficient implementation. This approach allowed in the scope of sound samples querying to cope with the multidimensional nature of timbre perception and also to obtain a whole set of efficient propositions rather than a single best solution.

Esling Philippe, Agon Carlos "Intelligent sound samples databases with multiobjective time series matching" - IEEE Transactions on Speech, Audio and Language Processing, 2011 (PDF to come)

===== Problem definition =====

A multiobjective time series matching problem is defined as finding the efficient elements of a database that jointly minimize a set of time series similarity measures. The MultiObjective Time Series (MOTS) matching problem can therefore be stated formally as

;#;
{{:esling:fullequation.jpg|}}
;#;

with Q the query represented by a set of K time series, S an element of the database DB which also contains a set of time series corresponding to the same set of objectives as the query. Finally, DQk(S) is the time series similarity between the kth feature represented by time series Qk and Sk. Hence, finding the element S∗ that is the most similar to the query corresponds to minimizing jointly the similarities between two sets of time series. In multiobjective optimization S∗ is called the ideal point. It is a configuration that simultaneously optimizes all criteria. In most real-life scenarios, S∗ does not exist, and solving this problem then turns out to finding a set of tradeoff solutions that provide different compromises between conflicting objectives. A solution S is optimal if and only if there is no other solution in the search space that achieve better values than S on every criteria DQk (S). This last observation implies that we should know the distances in all objectives before deciding whether an element belongs to the Pareto front or not. The following figure illustrates these concepts. 

;#;
{{:esling:timeseriesparetoset_extended.jpg|}}
;#;

Hence the query is the origin of the criteria space as its distances with itself are obviously null in every objectives. There is no solution S∗ in the database that perfectly match those two properties. Solution A is the best match for objective O1, as we can see the first time series is closely similar to that of the query. Solution B is respectively the best match for objective O2. The element C would be the best solution for every weighted monobjective problem given any set of weights. We can see that it is not closely similar to any objective, which exhibits the relevancy of our approach. Indeed, it allows joint queries on several dimensions without favoring any of them at any point of the search procedure. Furthermore, the multiobjective approach is an appropriate paradigm when the relative weights of each desired objective cannot be known in advance as with timbre perception.

==== Problem difficulty ====
The computational complexity of this problem rise from objective functions which represents the similarity between time-evolving features. As explained in section III the concept of time series similarity is very subtle and can require a high level of complexity. Furthermore because of the multiobjective nature of this problem, it is impossible to gain straightforward efficiency from “classical” indexing methods. Indeed, these prune a large part of the search space by avoiding computation of elements. It is obvious that this is simply impossible in our problem, as we need to know distance values in every dimension before being able to discriminate potential solutions. Moreover, we are interested in finding the complete and exact Pareto front. It has been shown that the complexity of K-NN queries grow dramatically with the number of required solutions. We are almost in a configuration where we should process a S-NN query (with S the size of our database) for each objective. It is obvious that this resolution method would degenerate to brute force analysis which is computationally inefficient

==== Multivariate ====

It is important here to understand the fundamental differences between a multivariate matching algorithm (which has been extensively studied in the literature) and our multiobjective problem. First of all, a multivariate search is equivalent to a mono-objective problem spanning several dimensions. Indeed, the multivariate case can be seen as a reduction of the multiobjective search when weights for all objectives have the same value. This usually allows to circumvent the problem of pruning power raised by the notion of Pareto dominance. Moreover, multivariate usually implies that the time series are somehow statistically linked. Sometimes, inference is even possible between series of the set. Oppositely, multiobjective allows the optimization of objectives that can be conflictive with each other.
===== Pertinency =====

We show the pertinency of our approach thanks to a concrete real-life example taken from our [[esling/ipad.html|intelligent sound samples database]] application.

;#;
{{:esling:mots_vectorized.jpg|}}
;#;

We can see here the pertinency of our approach on a concrete real-life example. Solution A is the best match in the database for the first objective. We can see that the temporal evolution of its //energy envelope// is really very close to the time series sought by the user. Solution C on the other hand is the best match for the second objective. Once again, we can see that the //spectral centroid// is a very close match. Finally, if we look at solution B, we see that it performs a bit poorly on both objectives. This solution would have been the closest neighbor to the query in a mono-objective search.

==== Multidimensionality of timbre perception ====
The American Standards Association (ASA) defines timbre as “[...]// that attribute of sensation in terms of which a listener can judge that two sounds having the same loudness and pitch are dissimilar//”. Beyond this practical definition, several authors pointed out that timbre is a multidimensional phenomenon and that perception organizes these dimensions given a particular sound context. Most of the psychoacoustic studies that we find in the literature makes use of multidimensional spaces in order to classify various sounds. We therefore believe that this multidimensional nature of timbre perception shall be taken into account in any kind of audio matching process. The complexity of temporal structures perception in music must be used to infer the mental idea. A multiobjective approach appears to be mandatory. Now equipped with a set of features computed from the sounds, we cannot know which dimension was perceptually more relevant when the user performed the translation from his mental idea to a set of temporal features.

===== Algorithm =====

The underlying idea is that even if we cannot rule out large portions of the search space thanks to indexing, we could find a way to restrict the number of distance computations. Instead of computing distances between every sequence and the target for all objectives, we want to drop distance calculations as soon as it exceeds a limit where we are sure that the corresponding element will be dominated. This trick is known as //early abandon//. However, we have to make some fundamental modifications in order to take into account the multiobjective nature of the problem. Indeed, early abandon in a monoobjective context is based on keeping the best distance known so far to compare the current point against. However, in a multidimensional space where we seek a whole set of efficient solutions, this is meaningless. Our main idea is therefore to construct an approximate Pareto hyperplane to act as our theoretical limit. We can obtain this hyperplane by using the results of exact 1-NN queries for each objective. Indeed, we are sure that exact 1-NN queries on each dimension will give us elements of the final Pareto front.\\
The algorithm as it is presented here can be used with any representation, distance measure and indexing technique available for time series. We simply assume that there is a time series index constructed for each possible objective. In our implementation we used the iSAX indexing technique which is based on the SAX representation for time series. We also consider that the index provide an approximate lower bounding distance measure on indexing nodes in order to enhance the efficiency gain.

===== Results =====

We present here the results of our algorithm. As said earlier, this problem has never been addressed before to the best of our knowledge, there exists no actual strawman to test our algorithm against. We are therefore comparing its efficiency against a brute force analysis. Algorithms have been tested on several datasets with both synthetic and real data. The synthetic dataset is composed of random walk time series generated with a constant size of 256 time points. We also used a real sound collection which is a combination of instrumental databases Studio On Line (SOL), Real World Computing (RWC) and Vienna Symphonic Library (VSL). These databases when combined amounts to a total of 213.814 samples. The size of resulting time series is therefore highly variating as it depends on the length of the soundfile as well as length of the analysis window. However, in order to compare the efficiency of our algorithm between synthetic and real datasets, we resampled every time series to a constant size of 256 time points. Subsets of these collections were then randomly selected to test our problem on databases of increasing size.\\
The testing procedure is based on comparing the efficiency of both algorithms. Therefore, several subsets of the collections are randomly selected for a given database size. The set of objectives is also randomly selected based on the number of desired objectives. For each set of parameters, one hundred different queries are processed with the same collection and indexes in order to avoid statistical anomalies. Computations were performed on a Macbook 2.4 GHz Dual Core running under Mac OS X 10.6.6 with 2 GO of DDR3 RAM.\\

;#;
{{:esling:querytime.jpg|}}
;#;

This figure shows the result of our algorithm for increasing database size on synthetic (left) and real (right) datasets. As we can see on the results for synthetic datasets, our algorithm provides a speedup between two to three times faster than the brute force algorithm. Even if it is already a significant speedup, the analysis of results reveals to be even more interesting on real sound collections. As we can see here, our algorithm can provide a speedup up to four times faster than the brute force algorithm. We think that this could be explained by the distribution of time series data in real datasets which is unlikely to be uniform as it is for random walk datasets. However, the most interesting finding is on the efficiency of our algorithm regarding the number of objectives

;#;
{{:esling:querytime_obj.jpg|}}
;#;

This figure shows the results of our algorithm for an increasing number of objectives on synthetic datasets and collections of real sound samples. As we can see here, our algorithm seems to be providing better speedups as the number of objectives grow. This could be explained by the greater probability that a large portion of the search space is ruled out by the approximate hyperplane with a greater number of dimensions. Once again, our algorithm performs better on real datasets than on synthetic datasets. These results shows the efficiency and usability of our approach as a first attempt to solve the multiobjective time series matching problem.

===== Application fields ======

We strongly believe that the topic of multiobjective time series matching could potentially lead to powerful applications. However, this algorithmic problem being unseen in the current literature, we are expecting to develop its application range in the next years. We envisioned some possible application fields for future work that we list in this section. Therefore, we kindly invite any interested researcher or curious reader to contact us directly if this topic seems appropriate to be applied for any subject of research interest :
<esling@ircam.fr> <agonc@ircam.fr>

==== Sound computing ====
We already applied our MOTS system to the analysis of spectral properties coming from sound samples. In this sound case, the choice of multiobjective is pertinent because of the multidimensional nature of timbre perception. On the other hand, the temporal aspect of sound is a core notion in our perception of sound. This make our approach a perfect match for sound sample querying. We have also experienced some variations on the multiobjective notion. It allows to perform query that tries to jointly minimize the mean, standard deviation and temporal shape of a descriptor.

==== Medical diagnosis ====
Multiobjective optimization techniques have a long history of successful applications in medical diagnosis and biological signal surveillance. Time series analysis have also been widely applied to medical situations. We therefore strongly believe that our multiobjective time series matching technique could be applied to medical diagnosis and prognosis. The fact is that a lot of information for medical analysis is coming from sensors. These are therefore producing time series observations as electrocardiogram (ECG), electroencephalogram (EEG), blood pressure and so forth.

==== Genetic analysis ====
In bioinformatics, a lot of research has been devoted to the analysis and matching of DNA sequences, considered as time series.  Furthermore there also seems to be a flourishing literature in multiobjective optimization for bioinformatics and computational biology. The field of genetic analysis therefore also appears as a promising topic for our algorithmic problem. 

==== Expected topics ====
  * Finance / Economics
  * Chemical engineering
  * Process design
  * Scheduling
  * Bioinformatics
  * Computational biology
  * Climate analysis
  * Therapy planning

==== Available datasets ====
  * Sound computing
    * //Studio On Line// (SOL)
    * //Vienna Symphonic Library// (VSL)
    * //Real World Computing// (RWC)
  * Medical surveillance
    * MGH/MF ECG Database
    * MIMIC PhysioBank
    * Apnea-ECG
  * UCR Classification tasks

===== Relevance feedback =====
We introduce a further optimization that has not yet been implemented that could allow to refine the search results. Depending on the problem, regions of the Pareto front might be preferred to others, according to personal preferences between objectives. This could allow for a relevance feedback scheme. The next figure exhibits the //induced Chebyshev norms// that can be inferred from the solutions and later used as weights to refine query results. That way it would be possible to perform a weighted mono-objective search refinement based on //listening preferences//.

;#;
{{:esling:inducednorms.jpg|}}
;#;

We can see in this figure that each solution corresponds implicitly to a set of weights that represents different optimization directions. For example, selecting solution A suggest that the user is more interested in the first objective than in the second. Conversely, selecting solution C implies the opposite listening preferences
===== iPad interface =====
