# Intelligent database

Seeking sound samples in a massive database can be a very tedious and painstaking task. Even when meta-informations are available, querying results may remain far from the mental representation of timbre expected by the user. This problem has seen a flourishing literature regarding melodic and sound databases. However, to the best of our knowledge, the same kind of high-level control and querying possibilities has never been proposed for sound samples. This may come from the fact that sound samples does not offer the same kind of high-level information extraction as songs (for example melody, lyrics, ...).  We thus worked on the development of the first intelligent sound sample database. We first proposed a scheme where sound can be retrieved simply by drawing the temporal shape of spectral descriptors. Then we addressed two completely novel ways of intuitive querying. First, by optimizing simultaneously the temporal evolution of multiple spectral properties //MultiObjective Spectral Evolution Query// (MOSEQ). Second, simply by performing a vocal imitation of the sound sample with //Query by Vocal Imitation// (QVI).

===== Database organization =====
As we are interested in performing intelligent queries over very large collections of sound samples, we have to maintain an organized database. We thus start by processing sound samples in order to extract any kind of relevant spectral information from the low-level signal description. The following figure depicts how sounds are analyzed and managed.

;#;
{{:esling:databasedesc.jpg|}}
;#;

Sound features are preliminarily extracted from each sound of large audio databases. We use the whole range of available descriptors in IRCAMDescriptor [Peeters 2004] ((PEETERS, G. “A large set of audio features for sound description (similarity and classification) in the cuidado project,” IRCAM, Paris, Tech. Rep., 2004.)) to represent as precisely as possible every perceptual aspect of a given sound. Each spectral descriptor is then processed in order to extract its mean and standard deviation which are stored in the SQL database. We then normalize each temporal shape and use time series analysis techniques in order to store an efficient representation of these shapes. As we can see, each element in the database contains several time series which represent different characteristics of this item. We already see here that even if this set of time series comes from audio analysis, the same kind of database can be find in various research topics like medical analysis. Furthermore, symbolic informations can be added to the database. These can either be automatically extracted by using a custom textual analysis over soundfile names or they can be directly input by the user. These informations will allow us to add symbolic constraints on the problem in order to restrict the size of the search space.
===== Temporal shape matching =====

==== Time series analysis ====

A time series represents a collection of values obtained from sequential measurements over time. Time series analysis stems from the desire to reify our natural ability to visualize the //shape// of data. Humans relies on complex schemes in order to perform such tasks. Indeed, we avoid focusing on small fluctuations in order to abstract a notion of //shape// and we are able to spot similarities on various time scales almost instantly. The following figure shows the typical paradigm of time series analysis.

;#;
{{:esling:dtwvseuclid.jpg|}}
;#;

When trying to find the similarity between two time series (a) a mathematical distance function like the //Euclidean norm// will perform a //point-to-point// comparison which is not consistent with our intuition. Whereas (b) our perception is able to perform //non-linear matching// between different sections of the series resulting in a more subtle and higher-level notion of similarity.
Major time series related tasks include //query by content// [Agrawal et. al 1993] ((AGRAWAL, R., FALOUTSOS, C., AND SWAMI, A. 1993. Efficient Similarity Search In Sequence Databases. In //Proceedings of the 4th International Conference on Foundations of Data Organization and Algorithms//. Springer, 69–84.)), //anomaly detection// [Weiss 2004] ((WEISS, G. 2004. Mining with rarity: a unifying framework. //ACM SIGKDD Explorations Newsletter// 6, 1, 7–19.)), //motif discovery// [Patel et. al 2002] ((PATEL, P., KEOGH, E., LIN, J., AND LONARDI, S. 2002. Mining Motifs in Massive Time Series Databases. In //Proceedings of IEEE International Conference on Data Mining// (ICDM02). 370–377.)), //prediction// [Weigned and Gershenfeld 1994] ((WEIGEND, A. AND GERSHENFELD, N. 1994. //Time Series Prediction: forecasting the future and understanding the past//. Addison Wesley.)), //clustering// [Lin and Keogh 2005] ((LIN, J. AND KEOGH, E. 2005. Clustering of time-series subsequences is meaningless: implications for previous and future research. //Knowledge and information systems// 8, 2, 154–177.)), //classification// [Bakshi and Stephanopoulos 1994] ((BAKSHI, B. AND STEPHANOPOULOS, G. 1994. Representation of process trends–IV. Induction of real-time patterns from operating data for diagnosis and supervisory control. //Computers & Chemical Engineering// 18, 4, 303–332)) and //segmentation// [Keogh et. al 2003] ((KEOGH, E., CHU, S., HART, D., AND PAZZANI, M. 2003. Segmenting time series: A survey and novel approach. //Data mining in time series databases//, 1–21.)).

=== Query by content ===
Our system is aimed at finding the sounds that are most similar in terms of time-evolving spectral properties. It is therefore a kind of //query by content// system where most similar items of a database has to be retrieved fast and orderly. The following figure depicts a typical query by content task represented on a 2-dimensional feature space.

;#;
{{:esling:querycontent.jpg|A typical query by content}}
;#;

Each point in this space represents a series whose coordinates are associated with its features. (a) When a query is input to the system, it is first transformed into the same representation as other datapoints. Two types of query can then be computed. (b) A ε−range query will return the set of series which are within distance ε of the query. %%(c)%% A K−Nearest Neighbors query will return the K points closest to the query. We redirect the interested readers to our article on the topic of time series mining\\
\\
ESLING Philippe, AGON Carlos - "//Time series data mining and analysis//" in ACM Computing Surveys, 2011 (Accepted).

==== Sound samples application ====

In the context of sound sample database, our goal was to allow queries based on the temporal shapes of descriptors. Therefore we had to adapt to the overwhelming quantity of descriptors and sounds available to develop an efficient architecture. We used a representation based on Symbolic Aggregate approXimation (SAX)((LIN, J., KEOGH, E., LONARDI, S., AND CHIU, B. 2003. A symbolic representation of time series, with implications for streaming algorithms. In Proceedings of the 8th ACM SIGMOD workshop on Research issues in data mining and knowledge discovery. ACM New York, NY, USA, 2–11.)), which allows to transform a time series into a reduced set of symbols in order to minimize the computational complexity. The SAX transformation is depicted in the following figure

;#;
{{:esling:saxrepresentation.jpg|}}
;#;

In order to compare the time series, we use a Dynamic Time Warping (DTW) distance measure that allows to obtain a more subtle notion of similarity between time series. It is based on the LB_Keogh measure ((http://www.cs.ucr.edu/~eamonn/LB_Keogh.htm)) that allows to compute DTW in linear time thanks to the notion of upper and lower envelope. We further introduced a novel time series indexing scheme which allows to index up to millions of time series. Based on the iSAX representation system, we augmented a multi-resolution tree structure with a nearest neighbor graph-like structure in order to get faster exact matches. Indeed, whereas usual indexing structure use a priority queue or backward tracking in order to transform an approximate query into an exact one, our index only has to perform a single graph traversal in order to obtain the exact match.

;#;
{{:esling:indexstruct.jpg|}}
;#;

We therefore obtain efficient results even for massive time series databases.

;#;
{{:esling:indexresults.jpg|}}
;#;


===== Innovative interaction schemes =====

Our system already provides a higher-level possibility of sound querying by matching temporal shapes of spectral descriptors. It is therefore possible to find sounds by simply drawing the desired evolution of timbre characteristics. However, the system is still unable to cope with the multidimensional nature of timbre perception. Indeed, several authors pointed out that timbre is a multidimensional phenomenon and that perception organizes these dimensions given a particular sound context. Most of the psychoacoustic studies that we find in the literature makes use of multidimensional spaces in order to classify various sounds. We therefore believe that this multidimensional nature of timbre perception shall be taken into account in any kind of audio matching process.

==== General framework ====

We addressed the issue of how to specify a query over sound samples by matching the temporal evolution of multiple timbre properties. This problem can be casted into a new approach merging multiobjective optimization and time series matching systems. Our generic method, namely [[esling/mots.html|MultiObjective Time Series (MOTS) matching]] has never been addressed to our best knowledge. This approach could potentially lead to a whole set of applications in various research topics. The time series matching is motivated here by the greater relevance of temporal evolution in audio perception. On the other side, multiobjective approaches allows to cope with the multidimensionality of timbre perception. The following figure introduce the algorithmic framework for our novel interaction methods.\\

;#;
{{:esling:qsiframework.jpg|}}
;#;

We redirect the interested readers to our article and webpage on the topic of [[esling/mots.html|Multiobjective Time Series (MOTS)]] matching :\\
* ESLING Philippe, AGON Carlos "Intelligent sound samples database with multiobjective time series matching", IEEE Transactions on Speech Audio and Language Processing, 2011 (in review).\\

==== MultiObjective Spectral Evolution Query (MOSEQ) ====

The idea behind this interaction paradigm is that when a user seek a sound sample inside a database, he will create a mental representation of the associated sound. Usually, this representation is based on the temporal evolution of spectral properties. Therefore, the MOSEQ system allows users to draw the shapes of temporal evolution in order to project this mental representation into an efficient query. The user has to select a set of descriptors that are relevant to his query. Then for each, he has to draw the corresponding desired time series.

==== Query by Vocal Imitation ====
Based on the MOSEQ paradigm, we can go even further in terms of easiness of interaction. In order to project a mental representation of spectral properties, the most straightforward way is usually to perform a vocal imitation of the sound. We therefore believe that a natural way of querying a sound sample database would be to directly give a vocal imitation to the query system. The same analysis module used for filling the database allow us to obtain the complete set of spectral shapes within which the user can select its subset of desired criteria. The QVI problem then reduce to a MOSEQ problem.

===== iPad interface =====

All the aforementioned technical characteristics have been implemented as a multitouch interface using the iPad. This interface embed all interaction schemes and capabilities in an OpenGL / Objective-C framework. It has been developed as a client to a local computer server (which allows an extensive storage size) using OSC communication but can also be self-contained (even if the database size is inherently limited).

;#;
{{youtube>BT5zg8QIKz4?medium}}
;#;
==== Main screen ====

The following figure introduce the main screen for the interface which allows to access all of its capabilities.

;#;
{{:esling:maininterface.jpg|}}
;#;

The first idea was to allow an intuitive way of managing queries. Various constraints can therefore be placed in a constraint flow (as will be detailed in the next section). These are managed thanks to the upper section of the interface which provides :
  * //Add new constraint// : a new empty constraint appears at the end of the workflow.
  * //Remove constraint// : the current constraint is removed from the workflow.
  * //Perform query// : a temporal query with uniform weights is performed (cf. results view)
Higher-level interactions are provided in the lower section of the interface :
  * //Constraint flow view// : the current and main view for the system (cf. next section)
  * //Query by vocal imitation// : embeds the QVI system with an audio recorder
  * //Multiobjective// : perform a MOSEQ query given several temporal shapes
  * //Database configuration// : defines how the database is handled (local, distant, ...)
  * //System preferences// : various interface configuration options


==== Query flow view ====

The goal of the system being to perform fast and intuitive querying over large sound samples collections, it also provide an intuitive way to formulate the query. Each parameter of the query is seen as a constraint window. These constraints are organized as a //cover flow// which can be slided with the finger. The number of constraints is potentially infinite. The following figure introduce the query flow view. 

;#;
{{:esling:constraintsview.jpg|}}
;#;

  * //Static spectral constraint// : A constraint placed over a scalar descriptor which force resulting sounds to be between the given values.
  * //Symbolic constraint// : A textual constraint which use regular expression language.
  * //Temporal shape constraint// : A time series that a particular descriptor has to match

  * //Number of potential match// : This feature allows to directly see on the screen how many sounds could potentially match strict static and symbolic constraints. It is based on a incremental querying tree structure. At each time the query context is saved in a new branch. If the query is only a refinement of the previous one, it is performed only on the previous subset. It is also possible to backtrack to older queries.

==== Time series edition ====

In order to place temporal constraints over spectral descriptor, the user can simply tap on a temporal constraint to access the //time series edition// view :

;#;
{{:esling:serieseditor.jpg|}}
;#;

  * //Minimize window// : Returns to the //query flow// view
  * //Reverse time axis// : Reverse the sequential order of the time series
  * //Reverse amplitude axis// : Polarize the time series
  * //Smooth time series// : Use Bezier approximation on the series
  * //Reinitialize series// : Reset all the time points to zero

==== Query results view ====

Once the query has been launched by the user, the system answers with a list of best matching sounds. These results and a complete list of their properties are showed in the //query results// view

;#;
{{:esling:queryresultsview.jpg|}}
;#;

  * //Spectral static informations// : Every mean and standard deviation values of the spectral descriptors
  * //Symbolic informations// : Every textual information (meta-data) available for the sound

  * //Soundfile with playing controls// : A small sound player which shows the waveform and embeds playing capabilities

  * //Next result// : Show the next (less accurate) result
  * //Previous result// : Show the previous (more accurate) result
  * //Close results view// : Goes back to the //query flow// view

  * //Temporal shapes// : A selected subset of three temporal shapes for each sound
  * //Minimum// and //maximum// values : Automatically computed and showed at their respective time points

==== Multiobjective query ====

One of the core properties of our system is its ability to perform [[esling/mots.html|Multiobjective time series matching]] queries. When the user inputs several time series to be matched, results of the multiobjective query are shown in a bi-dimensional space. (If the number of objectives are greater than two, dimensions are projected on the two first descriptors).

;#;
{{:esling:mots_results.jpg|}}
;#;

We can already see here the pertinency of our approach on a concrete real-life example. Solution A is the best match in the database for the first objective. We can see that the temporal evolution of its //energy envelope// is really very close to the time series sought by the user. Solution C on the other hand is the best match for the second objective. Once again, we can see that the //spectral centroid// is a very close match. Finally, if we look at solution B, we see that it performs a bit poorly on both objectives. This solution would have been the closest neighbor to the query in a mono-objective search.

  * //Pareto front// (efficient solutions) : In multiobjective optimization, these represents the //optimal// sounds of the database. It means that no sound in the database is better in //every// objective at the same time.
  * //Dominated solutions// : On the opposite, these are less efficient solutions that have been dominated during the search.


  * //Objective name// : Name of the descriptor selected by the user for querying
  * //Best distance// : Best DTW distance value found in the database for this descriptor
  * //Solutions count// : Number of solutions found in the search (efficient and dominated)
  * //First// and //second// objectives : Show the time series drawn by the user for the query

  * //Show Pareto solutions// : Show the efficient solutions in a //query results// view, in order to access all of their properties.
  * //Add vocal imitation// : This allows to refine the search by placing additional constraints from a vocal imitation
  * //Close window// : Returns to the //query flow// view

===== Multiple clients implementation =====

==== OpenMusic ====

;#;
{{:esling:omclient.jpg|}}
;#;

==== Max / Msp ====

;#;
{{:esling:maquettesmax.jpg|}}
;#;
