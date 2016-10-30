---
layout: single
permalink: /hvmots-datasets/
author_profile: false
share: true
comments: true
sidebar:
  nav: "research"
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

# Multivariate time series

This is the supporting webpage for the HV-MOTS classification paradigm study. We provide in this page detailed informations about the results of HyperVolume-MultiObjective Time Series (HV-MOTS) classification scheme. More informations about the MOTS paradigm can be found in the article and on a related page which presents the [MultiObjective Time Series](/projects-mots/) approach. 

# Introduction

  * [Complete datasets](/hvmots-datasets/#datasets) : All the datasets used in our study are available for download so that our experiments are fully reproducible. These datasets are available either as raw files or Matlab (.MAT) features files. The MAT files contains an organized structure of the results from our analysis workflow. Corresponding references and weblink are also provided for each dataset.

  * [[esling/hvmots-datasets.html#classification-results|Classification results]] : This section provides extended classification results with detailed dataset-specific analysis. [[esling/hvmots-datasets.html#general-results|General results]]  exhibit the various classification accuracies for each dataset and the [[esling/hvmots-datasets.html#features-combinations|features combinations]] provide an extended list of best features set for each level of analysis.

  * [[esling/hvmots-datasets.html#statistical-significance|Statistical significance]] : This section provides extended results of statistical significance tests over various datasets. We separate the evaluation depending on the //best// and //mean// classification accuracies. The statistical tests are performed through a Tukey-Kramer HSD based on the results of Friedman's ANOVA.

  * [[esling/hvmots-datasets.html#features-analysis|Features analysis]] provide an extended list of feature-by-feature discriminative power. We have only listed here the features which were selected after bi-objective combinations, ie. the feature which were used from three to more objectives classification (half of the complete feature set).

# Datasets

This section contains the downloadable archives of both datasets used in the paper. For each dataset, two archives are available. The first contains the original sound files. The second contains the results of the spectral analysis module in Matlab (.MAT) format. The features file contains a structure named `data` which contains the `name`, `class`, `sampleID` and `features` structure. The `features` structure contains every descriptor listed in the paper in matrix format `(nbDimensions x nbTimePoints)`. The corresponding descriptor are the raw values obtained from IRCAMDescriptor.

^Datasets		^Description		^Feats	^Class	^Samples	^
|Arabic digit		|Spoken arabic digits	|13	|10	|8800		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Artificial characters	|Character recognition	|2	|10	|6000		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Australian signs	|Hand sign recognition	|10	|95	|6650		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Australian signs (HQ)	|Hand signs (HQ)	|20	|95	|2565		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|BciIII-03a-Graz	|Brain-Computer		|60	|4	|840		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|BciIV-01-Berlin	|Brain-Computer		|64	|3	|1400		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|BciIV-03-Freiburg	|Brain-Computer		|10	|4	|480		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Biomag-2010		|EEG analysis		|274	|2	|780		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Challenge-2011		|Cardiology		|12	|2	|2000		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Character-trajectories	|Character recognition	|3	|20	|2858		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Dachstein		|High altitude medicine	|3	|2	|698		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Eeg-alcoholism		|Medical analysis	|64	|6	|650		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Forte-2		|Climatology		|2	|7	|121		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Forte-6		|Climatology		|6	|7	|121		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Gaitpdb		|Gait analysis		|18	|2	|306		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Handwritten		|Character recognition	|2	|183	|8235		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Ionosphere		|Radar analysis		|34	|2	|358		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Japanese-vowels	|Speech analysis	|12	|9	|640		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Libras			|Movement recognition	|2	|15	|360		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Pen-chars-35		|Character recognition	|2	|62	|1364		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Pen-chars-97		|Character recognition	|2	|97	|11640		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Person activity	|Movement analysis	|12	|11	|164860		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Physical action	|Movement analysis	|8	|20	|80		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Ptbdb-1		|Cardiology		|15	|9	|2750		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Ptbdb-2		|Cardiology		|15	|9	|2750		|
|  [[http://www.google.com|Original webpage]] 	|||||
|Ptbdb-5		|Cardiology		|15	|9	|2750		|
|  [[http://www.google.com|Original webpage]] 	|||||
|Robot failures-1	|Robotics		|6	|4	|88		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Robot failures-2	|Robotics		|6	|5	|47		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Robot failures-3	|Robotics		|6	|4	|47		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Robot failures-4	|Robotics		|6	|3	|117		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Robot failures-5	|Robotics		|6	|5	|164		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Slpdb			|Sleep apnea analysis	|7	|7	|4085		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Sonar			|Sonar analysis		|60	|2	|208		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Synemp			|Climatology		|2	|2	|20000		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Vfdb			|Cardiology		|2	|15	|600		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Vicon physical		|Physiological analysis	|26	|20	|2000		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Wall-robot-4		|Robotics		|28	|4	|5460		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||
|Wall-robot-24		|Robotics		|28	|24	|5460		|
|  [[http://www.google.com|Download features]] 	|||||
|  [[http://www.google.com|Original webpage]] 	|||||

## Dataset specifications

##### Arabic-digit

//Spoken digit recognition//
This dataset contains the recordings of 10 spoken arabic digit by 88 speakers. Each digit is repeated 10 times for each speaker The data comes from 44 males and 44 females native Arabic speakers. Sound files have been analyzed to obtain 13 Mel-Frequency Cepstrum Coefficients (MFCCs) time series.

Classes Spoken arabic digits ([0-9]
Samples 8800 samples (10 digits x 10 repetitions x 88 speakers)
Sampling Computation from sound files at 11025 Hz sampling rate, 16 bits with Hamming window. A pre-emphasis filter was applied to the original signal.
Source This dataset is part of the UCI repository [frankasuncion2010] and is extensively described in [hammami2009tree, hammami2010improved].

Results A Vector Quantization (VQ) with a Maximum Weight Spanning Tree (MWST) leads to a final mean classification accuracy of 93.12% over every classes with single classes results varying from 85.55% to 99.00%

##### Artificial characters

//Character recognition//
This dataset has been artificially generated by using first order theory to describe the structure of ten capital letters of English alphabet. Each instance is described by a set of segments which imitate the way an automatic program would segment an image.

Features Each segment is represented by X and Y values for the starting and ending points.

Classes 10-classes problem representing the capital letters A, C, D, E, F, G, H, L, P and R

Samples 6000 samples (600 for each class)

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in [botta1993learning]

Results A Genetic Algorithm coupled with an histogram local optimization leads to a recognition rate of 98.68%

##### Australian-signs

//Sign recognition//
This dataset consists of samples of Auslan (Australian Sign Language) signs that were recorded with multiple sensors on a powered glove. Examples of 95 signs were collected from five signers with a total of 6650 sign samples

Features The glove recorded 10 different time series feature for each sign as the x, y and z position of the hand, the roll, pitch and yaw of the hand orientation and the bending for thumb, forefinger, index, ring and little fingers.

Classes Each sign represents a different class which amounts to 95 different classes.

Samples 6650 samples (varies for each class)

Source This dataset is part of the UCI dataset repository [frankasuncion2010] and is extensively described in [kadous1995grasp].

Results For the low quality set (Nintendo Power-glove), best results are obtained by a Hidden Markov Model (HMM) classifier with 71.2% classification accuracy [kadous2002temporal]

##### Australian-signs-hq

//Sign recognition//
This dataset is a highest quality version of the Australian-signs dataset. However, recordings were made with a single signer. It contains 27 examples of each of the same 95 signs for a total of 2565 signs collected from a native signer using high quality position trackers on both hands.

Features The same feature set is used, however this time both hands were recorded simultaneously.

Samples 2565 samples (27 for each class)

Articles This dataset is part of the UCI dataset repository [frankasuncion2010] and is described in [kadous2002temporal].

Results For this dataset, best results are obtained by the Naive Segmentation based on TClass algorithm with a 94.5% accuracy [kadous2002temporal].

##### BciIII-03a-graz

//Brain-Computer Interface//
Summary This dataset is composed of EEG recordings of cued motor imagery with 4 classes (left hand, right hand, foot, tongue) from 3 subjects (ranging from quite good to fair performance). Performance is measured using the kappa-coefficient.

Features 60 EEG channels (1-50Hz)

Classes 4-class problem between left hand, right hand, foot and tongue

Samples 840 samples (70 trials per subject for each class)

Sampling 250Hz sampling rate

Source This dataset is part of the 2003 BCI Competition 2003 [blankertz2004bci].

Results A multi-class CSP based on Fisher ratios obtained a kappa coefficient of 0.7926.

##### BciIV-01-berlin

//Brain-Computer Interface//
Motor imagery for an uncued EEG classifier application (for hand and foot); evaluation data is a continuous EEG which also contains periods of idle state 

Features 64 EEG channels (0.05-200Hz) 

Classes 3 classes (hand, foot and idle state)

Samples 1400 samples (200 trials per subject)

Sampling 1000Hz sampling rate 

Source This dataset is part of the BCI Competition IV [blankertz2007non]. The performance measure is the mean squared error with respect to the target vector

Results The output of the competition shows that a clustering procedure applied on a Principal Components Analysis (PCA) allows to obtain a MSE of 0.382.

##### BciIV-03-Freiburg

//Brain-Computer Interface//
Hand movement directions in MEG. The data set contains directionally modulated low-frequency MEG activity that was recorded while subjects performed wrist movements in four different directions. 

Features 10 MEG channels (filtered to 0.5-100Hz) located above the motor areas

Classes 4 classes (forward, backward, left and right wrist movements)

Samples 480 samples (120 for each classes with 60 trials per subject)

Technical The trials were cut to contain data from 0.4 s before to 0.6 s after movement onset and the signals were band pass filtered (0.5 to 100 Hz) and resampled at 400 Hz.

Source This dataset is part of the BCI Competition IV [blankertz2007non]. 

Results The final obtained accuracy is 46.9% over the 2 subjects with 59.5% for the first and 34.3% for the second. Feature extraction and reduction is then fed to a Genetic Algorithm (GA) which decide the features to use for classification with a combination of linear Support Vector Machine (SVM) and Linear Discriminant Analysis (LDA)

{{:esling:anova_bciIV-03-freiburg.jpg?nolink&300 |}} {{:esling:hsd_bciIV-03-freiburg.jpg?nolink&300 |}} 
{{:esling:critical_bciIV-03-freiburg.jpg?nolink&300 |}} 
{{:esling:time_bciIV-03-freiburg.jpg?nolink&300 |}} {{:esling:warp_bciIV-03-freiburg.pdf?nolink&300 |}}

##### Biomag-2010

//EEG analysis//
The goal of this dataset is to detect whether subjects are attending to the left or right visual field on each trial based on the MagnetoEncephaloGram (MEG) of the subjects. 

Features 274 MEG channels recorded independently

Classes 2-class problem (between left and right visual field).

Samples 780 samples

Source This dataset is described in [van2009attention]

Results The results reported in [van2009attention] shows that a Support Vector Machine (SVM) algorithm provide an accuracy of up to 69% correctly classified trials.

##### Challenge-2011

//Cardiology//
This dataset is composed of 12-lead ECG recordings, with the aim of providing useful feedback on the quality of the ECG signals by classifying them depending on their quality (from poor to excellent).

Features This dataset is composed of 12 leads (I, II, II, aVR, aVL, aVF, V1, V2 and V3)

Classes 2-class task between acceptable and unacceptable ECG recording depending on their qualities.

Samples 2000 samples (1000 for each class)

Technical The leads are recorded simultaneously for a minimum of 10 seconds; each lead is sampled at 500 Hz with a 16-bit resolution.

Source This dataset is part of the PhysioBank archive [goldberger2000physiobank] posted as the 2011 challenge.

Results The challenge was intended to see the selectivity and specificity of algorithms. The best system reports a 85.9% accuracy [xia2012computer] using the spectrum radius of a matrix of regularity.

{{:esling:anova_challenge-2011.jpg?nolink&300 |}} {{:esling:hsd_challenge-2011.jpg?nolink&300 |}} 
{{:esling:critical_challenge-2011.jpg?nolink&300 |}} 
{{:esling:time_challenge-2011.jpg?nolink&300 |}} {{:esling:warp_challenge-2011.pdf?nolink&300 |}}

##### Character-trajectories 

//Character recognition//
This dataset is composed of labelled samples of pen tip trajectories recorded for individual characters writing. All samples are from the same writer, for the purposes of primitive extraction. Only characters with a single pen-down segment were considered

Features The dataset is made of three time series for each instance, which represents the x and y position of the pen and the pen tip force.

Classes 20-class problem over different characters

Samples 2858 samples (varies for each class)

Technical Recordings have been made at 200 Hz sampling rate. Data has been numerically differentiated and Gaussian smoothed, with a sigma value of 2.

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in [williams2006extracting, williams2008modelling].

Results Reported classification accuracy of 87% in [zafar2006recognition] and 93.67% in [perina2009new] using a Gaussian Mixture Model (GMM) with a Hidden Markov Model (HMM).

##### Dachstein

//High altitude medicine//
Each instance represents EEG and ECG data for one cardiac cycle that were acquired at 900 m and at 2700m altitude. The subject performed a reaction time task. The data shows the influence of the loss of oxygen on event-related desynchronization (ERD) and event-related synchronization (ERS) and heart rate variability.

Features The recordings covers 2 channels of EEG (C3 and C4) and the ECG recordings.

Classes 2-class problem between 900m and 2700m recordings

Samples 698 samples (324 at 900m and 374 at 2700m)

Technical 256 Hz sampling rate with a 1 \mu V
  calibration

Source This dataset is described in [guger2005effects] where analysis is performed to show the influence of loss of oxygen

Results - No classification accuracy reported -

##### EEG-alcoholism

//Medical analysis//
This data comes from a large study to examine EEG correlates of genetic predisposition to alcoholism. It contains measurements from 64 electrodes placed on subject's scalps.

Features Each recording is composed of 64 EEG electrodes time series

Classes 2-class problem between alcoholic and control subjects

Samples 650 samples

Technical Data was recorded at 256 Hz sampling rate

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in [zhang1995event].

Results The results provided in [zhong2002hmms] show that a Multivariate HMM allows a classification accuracy of 90.5%. However, this result is obtained with only 10 pre-selected measurements. The true classification accuracy is 78.5%

##### Forte

//Climatology// (lightning prediction)
This dataset is split into three different problems depending on the number of classes they contain. Each dataset is aimed at predicting the type of lightning observed through recordings of the power density.

Features Ground density of Electro-Magnetic Power (EMP) recording

Samples 121 instances in each dataset.

Source The dataset is extensively described in[forte-dataset-05].

Results Classification resultsof 77.5% accuracy are reported in [bernecker2011quality] using a Shared-Nearest-Neighbors (SNN) algorithm with the Longest Common SubSequence (LCSS) distance.

Forte-2

Classes 2-class problem where distinction should be made between cloud-to-ground and intra-cloud lightning.

Forte-6

Classes 6-class problem where distinction should be made between CG (Positive-Initial Return Stroke), SR (Subsequent Negative Return Stroke), IR (Negative Initial Return Stroke), I (Impulsive Event), I2 (Impulsive Event Pair) and KM (Gradual Intra-Cloud Stroke) lightning events

##### Gaitpdb

//Medical analysis//
Summary This database contains measures of gait from patients with idiopathic Parkinson Disease (PD) (mean age: 66.3 years; 63% men), and healthy control subject (mean age: 66.3 years; 55% men). A disturbed gait is a common, debilitating symptom of PD; patients with severe gait disturbances are prone to falls and may lose their functional independence. The database includes the vertical ground reaction force records of subjects as they walked at their usual, self-selected pace for approximately 2 minutes on level ground. 

Features This dataset was recorded using 8 sensors under each foot, which gives the vertical ground reaction force for each foot as well as the total force under each foot. This amounts to 18 time series features.

Classes 2-class problem between healthy and parkinson subjects based on gait disturbances.

Samples 306 samples (214 parkinson and 92 healthy subjects)

Technical Recordings were made at 100 Hz sampling rate

Source This dataset is part of the PhysioBank database [goldberger2000physiobank] and is described in [frenkel2005treadmill]

Results Results introduced in [lee2012parkinson] shows that Neural Network with weighted fuzzy membership functions on Wavelet Transform coefficients allow to obtain a 77.33% classification accuracy.

##### Handwritten

//Character recognition//
This dataset contains 8235 online handwritten assamese characters. The “online” process involves capturing the data in real-time while the characters are written on a digitizing tablet with an electronic pen. This dataset was collected from 45 writers, each of which contributed 183 recordings

Features The acquisition program records the handwriting as a stream of X and Y coordinate points using the appropriate pen position sensor along with the pen-up and pen-down switching. No pressure level was recorded. 

Classes This is a 183-classes problem. Each writer contributed 52 basic characters, 10 numerals and 121 assamese conjunct consonants.

Samples 8235 samples (45 for each class). 

Source This dataset is part of the UCI repository [frankasuncion2010]

Results A classification accuracy of 92% with HMM to 96% with SVM is reported but only for digits (so only a 10-classes problem)

##### Ionosphere

//Radar analysis//
This dataset was collected by a radar system in Goose Bay, Labrador. The targets were free electrons in the ionosphere. "Good" radar returns are those showing evidence of some type of structure in the ionosphere. "Bad" returns are those that do not; their signals pass through the ionosphere. 

Features There were 17 pulse numbers for the Goose Bay system. Instances in this database are described by 2 attributes per pulse number, corresponding to the complex values returned by the function resulting from the complex electromagnetic signal which amounts to 34 features.

Classes 2-class binary task between good and bad radar returns.

Samples 358 samples

Technical The recording system consists of a phased array of 16 high-frequency antennas with a total transmitted power of 6.4 kilowatts. Received signals are processed using an autocorrelation function whose arguments are the time of a pulse and its number.

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in [Sigillito1989]

Results The best results is a 94.2 % classification accuracy reported in [eggermont2004genetic] using a Genetic Programming (GP) approach.

##### Japanese-vowels

//Speaker identification//
This dataset covers the topic of speaker identification for nine male speakers which uttered two Japanese vowels successively.

Features Each instance is represented by 12 LPC cepstrum coefficients time series.

Classes 9-class problem representing each speaker

Samples 640 samples (varies for each class)

Technical 10 kHz sampling rate analyzed with a 25.6ms window size and a 6.4ms hop size.

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in[kudo1999multidimensional].

Results The proposed classifier exhibits a classification accuracy of 94.1%, while a 5-state continuous Hidden Markov Model attained up to 96.2%

##### Libras

//Movement recognition//
The dataset contains 15 classes of 24 instances each. Each class represents to a hand movement type in LIBRAS (oficial brazilian signal language). 

Features In each frame, the centroid pixels of the segmented objects (the hands) are found. These successive points compose the discrete version of the curve which is represented by the x and y position time series. All curves are normalized in the unitary space.

Classes 15-class problem for swings, arcs, circle, lines, zigzag, waves, curves and tremble movements

Samples 360 samples (24 for each class).

Technical In the video pre-processing, a time normalization is carried out selecting 45 frames from each video, by following an uniform distribution.

Source This dataset is part of the UCI repository [frankasuncion2010], described originaly in [dias2009hand] and later used in [schliebs2011reservoir] 

Results An evolving Spiking Neural Network (eSNN) allows to obtain a 88.59% classification accuracy.

##### Pen-chars-35

//Character recognition//
This dataset is composed of upper and lowercase characters, digits, and other spanich characters, for a total of 62 different characters collected from 11 different writers which performed 2 repetitions.

Features Each character is represented by a sequence of segments summarized by their X and Y coordinates for each point.

Classes 62-classes problem.

Samples 1364 samples (2 repetitions for 11 writers for each class)

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in [prat2009template]

Results Classification accuracy is shown to be up to 89.15% if using a DTW matching algorithm on segment-based representation with a NN-rule.

##### Pen-chars-97

//Character recognition//
This dataset is composed of ASCII and non-ASCII characters which amount to a total of 97 different characters collected from 60 different writers which performed 2 repetitions.

Features Each character is represented by a sequence of segments summarized by their X and Y coordinates for each point.

Classes 97-classes problem.

Samples 11640 samples (2 repetitions for 60 writers for each class)

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in [castro2009improving]

Results Classification accuracy is presented in [castro2009improving] of 91.8% classification accuracy if using a template matching algorithm with a NN-rule however this results is only for a restricted set of 62 characters.

##### Person-activity

//Movement analysis//
People used for recording of the data were wearing four tags (ankle left, ankle right, belt and chest). Each instance is a localization data for one of the tags. The goal of this dataset was to dect falls only but we also test the accuracy in classifying all movement classes.

Features The four tags worn by subjects sent the x, y and z position for left and right ankle, chest and belt which amounts to 12 distinct features.

Classes This dataset features instances of different postures and actions with walking, falling, lying, lying down, sitting, sitting down, standing up from lying, on all fours, sitting on the ground, standing up from sitting and standing up from sitting on the ground.

Samples 164860 samples (varies for each class)

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in [kaluza2010agent] 

Results Classification accuracy is shown to be 72% for machine learning agents, 88% for expert-knowledge agents and 91.3% for meta-prediction agents. However, this results are for detecting falls only.

##### Physical-action

//Movement analysis//

Summary Three male and one female subjects (age 25 to 30), who have experienced aggression in scenarios such as physical fighting, took part in the experiment. Throughout 20 individual experiments, each subject had to perform ten normal and ten aggressive activities.

Features The data acquisition process involved eight skin-surface electrodes placed on the upper arms (biceps and triceps), and upper legs (thighs and hamstrings), which corresponds to eight input time series for all muscle channels (ch1-8). Each time series contains around 10000 samples (15 actions per experimental session for each subject). The electrodes were placed on right bicep (C1), right tricep (C2), left bicep (C3), left tricep (C4), right thigh (C5), right hamstring (C6), left thigh (C7) and left hamstring (C8)

Classes 2-class problem between aggressive and normal actions

Samples 80 samples (4 for each class)

Technical The subjects’ performance has been recorded by the Delsys EMG apparatus, interfacing human activity with myoelectrical contractions.

Source This dataset is part of the UCI repository [frankasuncion2010]

Results A Genetic Programming (GP) algorithm allows to obtain 73.3% classification accuracy [theodoridis2007action]. However these results are for six of the actions only.

##### Ptbdb

//Cardiology//
The ECGs were collected from healthy volunteers and patients with different heart diseases 

Features Each record includes 15 simultaneously measured cardiac signals. The conventional 12 ECG-leads (i, ii, iii, avr, avl, avf, v1, v2, v3, v4, v5, v6) together with the 3 Frank lead ECGs (vx, vy, vz). 

Classes 9 separate class representing healthy patients and patients suffering different heart conditions. The classes are therefore healthy controls, myocardial infarction, cardiomyopathy, bundle branch block, dysrhythmia, myocardial hypertrophy, valvular heart disease, myocarditis and miscellaneous.

Samples 2750 instances from 549 records performed on 290 subjects (aged 17 to 87, mean 57.2; 209 men, mean age 55.5, and 81 women, mean age 61.6; ages were not recorded for 1 female and 14 male subjects). Each subject is represented by one to five records.

Technical Each signal is digitized at 1000 samples per second, with 16 bit resolution over a range of ± 16.384 mV. with 0.5 μV/LSB (2000 A/D units per mV).

Source This dataset is part of the PhysioBank database [goldberger2000physiobank] and is described in [bousseljot1995nutzung].

Results The results provided in [gudmundsson2012test] shows that a Random Forest (RF) classifier provide a 75.1% classification accuracy

Ptdb-1

Technical This dataset contains single heart beats for classification

Ptdb-2

Technical This dataset contains two heart beats in each instance

Ptdb-5

Technical This dataset contains five heart beats in each instance

##### Robot-failures

//Robotics//
This dataset contains force and torque measurements on a robot after failure detection. Each failure is characterized by 15 force/torque samples collected at regular time intervals

Features The robots measure a set of x, y and z force position as well as a x, y and z torque measured after failure, which amounts to a total of 6 individual time series features.

Classes This dataset is divided into five sub-sets, each of them defining a different learning problem

Technical Each failure instance is characterized in terms of 15 force/torque samples collected at regular time intervals starting immediately after failure detection. A total observation window of 315ms is used for each failure instance. 

Source This dataset is part of the UCI repository [frankasuncion2010] and described [camarinha1996integration].

Results A set of five feature transformation strategies (based on statistical summary features, discrete Fourier transform, etc.) allows to obtain a maximal classification accuracy of 80%.

Robot-failures-lp1

Classes Failures in approach to grasp position 24% normal - 19% collision - 18% front collision - 39% obstruction

Samples 88

Robot-failures-lp2

Classes Failures in transfer of a part43% normal - 13% front collision - 15% back collision - 11% collision to the right - 19% collision to the left

Samples 47

Robot-failures-lp3

Classes Position of part after a transfer failure 43% normal - 19% slightly moved - 32% moved - 6% lost 

Samples 47

Robot-failures-lp4

Classes Failures in approach to ungrasp position 21% normal - 62% collision - 18% obstruction

Samples 117

Robot-failures-lp5

Classes Failures in motion with part 27% normal - 16% bottom collision - 13% bottom obstruction - 29% collision in part - 16% collision in tool

Samples 164

##### Slpdb

//Sleep apnea analysis//
The MIT-BIH Polysomnographic Database is a collection of recordings of multiple physiologic signals during sleep. Subjects were monitored in Boston's Beth Israel Hospital Sleep Laboratory for evaluation of chronic obstructive sleep apnea syndrome, and to test the effects of constant positive airway pressure (CPAP), a standard therapeutic intervention that usually prevents or substantially reduces airway obstruction in these subjects.

Features All recordings include an ECG signal, an invasive blood pressure signal (measured using a catheter in the radial artery), an EEG signal, and a respiration signal (in most cases, from a nasal thermistor). Seven-channel recordings also include a respiratory effort signal derived by inductance plethysmography, an EOG signal and an EMG signal (from the chin). Therefore the dataset is divided depending on the number of available features.

Classes Several tags can be applied at the same time for a subject. The first kind depends on the different sleep stage, depending on if the subject is awake, in sleep stage 1, 2, 3, 4 or REM sleep. Then phases of apnea are recorded between different types, with hypopnea, obstructive apnea and central apnea that can be with or without arousal. Final different movements are recorded for legs and arousal.

Summary 2-class task between apnea and normal based on 4 features (ECG, BP, EEG and Respiration)

Samples 4085 samples

Source This dataset is part of the PhysioBank database [goldberger2000physiobank] and described in [ichimaru1999development].

Results Between 83.24% to 88.97% classification accuracy [bsoul2010real] using a Multi-Scale Support Vector Classifier (MS-SVM)

##### Sonar

//Sonar analysis//
This dataset contains the patterns of sonar signals bouncing off either a metal cylinder or rocks. In both case, the angles and conditions varies. The goal is to correctly identify the metal cylinder returns.

Features Set of energy in 60 frequency bands over a certain period of time

Classes 2-class problem between mine and rock sonar signals.

Samples 208 samples (111 mines and 97 rocks)

Source TThis dataset is part of the UCI repository [frankasuncion2010] and is described in [tan2005mml].

Results The results reports a 76% classification accuracy by using a Minimum Message Length (MML) Oblique Tree.

##### Synemp

//Climatology// (lightning prediction)
Summary The classification tasks are aimed at studying varying speed of leading edge for different classes of lightning

Features Synthetic density of Electro-Magnetic Power (EMP) recording

Classes 2-class problem between slow and fast leading edge

Samples 20000 samples (10000 for each class)

Source This dataset is described in [syn-lightning-emp-05].

Results - No classification results reported -

##### Vfdb 

//Cardiology//
This database includes 22 half-hour ECG recordings of subjects who experienced episodes of sustained ventricular tachycardia, ventricular flutter, and ventricular fibrillation.

Features Two ECG recordings based on separate electrodes.

Classes 15-class problem between different ventricular fibrillations comprising atrial fibrillation, asystole, ventricular bigeminy, first degree heart block, high grade ventricular ectopic activity, normal sinus rhythm, nodal ("AV junctional") rhythm, noise, pacemaker (paced rhythm), sinus bradycardia, supraventricular tachyarrhythmia, ventricular escape rhythm, ventricular fibrillation, ventricular flutter and ventricular tachycardia.

Samples 600 samples (40 per class)

Source This dataset is part of the PhysioBank database [goldberger2000physiobank] and is described in [greenwald1985estimating]

Results A band-pass digital filtration and ECG peak detection algorithm allows to obtain a 91.5% classification algorithm in [krasteva2005assessment].

##### Vicon-physical

//Physiological analysis//
This dataset includes 10 normal and 10 aggressive physical actions based on various human activities. The data have been collected by 10 subjects using the Vicon 3D tracker.

Features The x, y and z positions define the 3D position of each marker in space for left and right wrist, elbow, ankle and knee which amounts to a total of 26 time series features for each action.

Samples 2000 instances (10 for each action)

Technical The duration of each action was approximately 10 seconds per subject, which corresponds to a time series of 3000 samples, with sampling frequency of 300Hz.

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in [theodoridis2007action].

Results 95.4% classification accuracy is reported using a Dynamic Neural Network, however it is only applied on 9 actions out of the 20 classes.

Classes 2-class problem between aggressive and normal actions

##### Wall-robot

//Robotics//
This dataset contains ultrasound readings for a wall-following task for robotic navigations.

Features 24 ultrasounds readings and 4 minimum sensor readings.

Classes 4-class problem between forward, slight-right, sharp-right and slight-left movements

Samples 5460 samples (1365 for each class)

Technical Sensor readings are sampled at a rate of 9 samples per second.

Source This dataset is part of the UCI repository [frankasuncion2010] and is described in [freire2009short].

Results The results exhibit a classification accuracy of 95.58% if using a Polynomial kernel SVM.

## Classification results

===== Summary =====

^Datasets 		^1-NN	^5-NN	^NC	^SVM	^MOTS	^NP-M.	^HV-M.	^
|[[esling/hvmots-datasets.html#arabic-digit|Arabic digit]]		|99.54	|99.26	|83.37	|99.31	|99.61	|99.52	|99.88	|
|[[esling/hvmots-datasets.html#artificial-characters|Artificial characters]]	|99.98	|99.98	|96.40	|99.98	|100.0	|99.98	|100.0	|
|[[esling/hvmots-datasets.html#australian-signs|Australian signs]]	|71.52	|70.23	|65.85	|72.33	|72.35	|69.23	|84.36	|
|[[esling/hvmots-datasets.html#australian-signs-hq|Australian signs (HQ)]]	|84.64	|82.46	|70.25	|85.22	|64.44	|76.14	|91.31	|
|[[esling/hvmots-datasets.html#bciIII-03a-graz|BciIII-03a-Graz]]	|34.17	|33.21	|25.12	|33.81	|33.93	|32.62	|35.59	|
|[[esling/hvmots-datasets.html#bciIV-01-berlin|BciIV-01-Berlin]]	|57.29	|56.93	|52.14	|56.54	|56.92	|56.43	|57.50	|
|[[esling/hvmots-datasets.html#bciIV-03-freiburg|BciIV-03-Freiburg]]	|33.40	|33.19	|32.76	|33.40	|36.40	|34.04	|36.62	|
|[[esling/hvmots-datasets.html#biomag-2010|Biomag-2010]]		|67.12	|68.36	|71.12	|73.42	|72.24	|69.62	|73.42	|
|[[esling/hvmots-datasets.html#challenge-2011|Challenge-2011]]		|90.58	|92.19	|88.38	|92.69	|90.58	|90.08	|91.98	|
|[[esling/hvmots-datasets.html#character-trajectories|Character-trajectories]]	|99.23	|98.67	|89.68	|99.22	|98.11	|99.16	|99.23	|
|[[esling/hvmots-datasets.html#dachstein|Dachstein]]		|97.42	|97.13	|89.67	|98.28	|98.13	|98.13	|98.57	|
|[[esling/hvmots-datasets.html#eeg-alcoholism|Eeg-alcoholism]]		|79.55	|81.36	|80.00	|80.06	|82.27	|79.55	|83.18	|
|[[esling/hvmots-datasets.html#forte|Forte-2]]		|82.64	|80.17	|74.38	|82.45	|81.54	|82.64	|83.47	|
|[[esling/hvmots-datasets.html#forte|Forte-6]]		|71.90	|70.25	|62.81	|71.56	|71.90	|71.90	|73.55	|
|[[esling/hvmots-datasets.html#gaitpdb|Gaitpdb]]		|89.87	|83.01	|73.20	|87.24	|77.78	|76.14	|89.87	|
|[[esling/hvmots-datasets.html#handwritten|Handwritten]]		|90.67	|82.34	|78.12	|84.72	|81.23	|80.32	|92.17	|
|[[esling/hvmots-datasets.html#ionosphere|Ionosphere]]		|94.20	|92.31	|88.89	|93.12	|89.17	|90.88	|94.59	|
|[[esling/hvmots-datasets.html#japanese-vowels|Japanese-vowels]]	|94.21	|95.00	|88.91	|94.77	|90.78	|92.03	|97.19	|
|[[esling/hvmots-datasets.html#libras|Libras]]			|84.44	|77.78	|55.00	|83.79	|79.72	|75.56	|91.39	|
|[[esling/hvmots-datasets.html#pen-chars-35|Pen-chars-35]]		|54.32	|52.18	|27.94	|54.12	|51.44	|49.59	|54.91	|
|[[esling/hvmots-datasets.html#pen-chars-97|Pen-chars-97]]		|47.69	|45.95	|20.66	|46.80	|50.52	|47.69	|56.80	|
|[[esling/hvmots-datasets.html#person-activity|Person activity]]	|89.35	|88.72	|71.80	|89.31	|85.09	|80.95	|91.60	|
|[[esling/hvmots-datasets.html#physical-action|Physical action]]	|95.00	|92.50	|90.00	|94.50	|92.50	|92.50	|93.75	|
|[[esling/hvmots-datasets.html#psychophysics|Psychophysics]]		|75.32	|77.27	|70.13	|75.03	|72.08	|74.03	|80.52	|
|[[esling/hvmots-datasets.html#ptbdb|Ptbdb-1]]		|98.77	|96.73	|52.73	|98.66	|97.34	|96.84	|99.12	|
|[[esling/hvmots-datasets.html#ptbdb|Ptbdb-2]]		|96.19	|93.23	|46.50	|95.29	|92.73	|91.12	|97.58	|
|[[esling/hvmots-datasets.html#ptbdb|Ptbdb-5]]		|91.19	|87.54	|42.15	|90.00	|87.23	|83.31	|93.73	|
|[[esling/hvmots-datasets.html#robot-failures|Robot failures-1]]	|96.59	|96.59	|76.13	|96.16	|92.04	|89.77	|97.73	|
|[[esling/hvmots-datasets.html#robot-failures|Robot failures-2]]	|78.72	|76.59	|72.34	|76.49	|76.59	|82.97	|78.72	|
|[[esling/hvmots-datasets.html#robot-failures|Robot failures-3]]	|86.97	|86.17	|71.17	|86.36	|85.83	|83.99	|91.49	|
|[[esling/hvmots-datasets.html#robot-failures|Robot failures-4]]	|94.87	|95.72	|74.36	|95.26	|98.29	|88.03	|98.29	|
|[[esling/hvmots-datasets.html#robot-failures|Robot failures-5]]	|77.44	|76.89	|62.80	|76.93	|75.00	|71.95	|79.88	|
|[[esling/hvmots-datasets.html#slpdb|Slpdb]]			|77.86	|81.18	|72.78	|79.81	|79.09	|74.71	|79.56	|
|[[esling/hvmots-datasets.html#sonar|Sonar]]			|86.54	|85.10	|70.67	|86.35	|86.54	|87.02	|88.94	|
|[[esling/hvmots-datasets.html#synemp|Synemp]]			|91.15	|87.35	|80.82	|90.24	|85.28	|76.23	|92.28	|
|[[esling/hvmots-datasets.html#vfdb|Vfdb]]			|60.64	|63.18	|43.58	|63.05	|56.08	|48.47	|58.62	|
|[[esling/hvmots-datasets.html#vicon-physical|Vicon physical]]		|97.00	|95.50	|89.00	|96.50	|94.00	|94.00	|96.00	|
|[[esling/hvmots-datasets.html#wall-robot|Wall-robot-4]]		|96.55	|96.55	|50.02	|97.31	|97.31	|97.31	|97.36	|
|[[esling/hvmots-datasets.html#wall-robot|Wall-robot-24]]	|91.92	|90.76	|41.60	|91.23	|91.46	|91.42	|92.47	|

====== Statistical significance ======

====== Features analysis ======
