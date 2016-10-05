---
layout: single
permalink: /atiam-ml-0-intro/
author_profile: false
share: true
comments: true
sidebar:
  nav: "teaching-atiam-ml"
---

{% include toc %}

# Introduction

The present tutorials covers coding exercices designed to implement the core notions seen in the machine learning lessons. Most techniques can be applied to any type of data from which sets of features can be computed. The exercices here target these techniques specifically applied to musical or audio data.

# Reference slides

Download the [![](../images/pdf.png) slides](../documents/MML.Lesson.1.Introduction.pdf)

The corresponding slides cover
  * Introduction to artificial intelligence
  * Properties of machine learning
  * Nearest-neighbors

# Tutorial 
In this introduction, we will cover basic Music Information Retrieval (MIR) interactions, in which we process a dataset of sound files and try to observe the properties of their various temporal and spectral features. Hence, we will quickly review basic calculus required to perform further machine learning tasks.

### 1.0 - Reference code

Get the baseline code from this {{:esling:atiam_ml_exercises.zip|link}}

### 1.1 - Datasets
In order to do so, we will work with several datasets that should be downloaded on your local computer first from this [[https://pchit.ircam.fr/public.php?service=files&t=a476001b408cfa9dacf8721149b9f151|link]]
  * Classification - MuscleFish dataset
  * Music-speech - MIREX Recognition set
  * Source separation - SMC Mirum dataset
  * Speech recognition - CMU Arctic dataset

For the first parts of the tutorial, we will mostly use the classification dataset only. In order to facilitate the interactions, we provide the function ''importDataset'' that allows to import different audio datasets

{% highlight Matlab %}
function dataStruct = importDataset(classPath, type)
% classPath  : Path to the dataset (string)
% type       : Type of dataset (string: 'classify', 'plain', 'metadata')

% Returns the dataStruct structure with
dataStruct.filenames  % Cell containing the list of audio files
dataStruct.classes    % Vector of indexes assigning each file to a class
dataStruct.classNames % Cell of class names
{% endhighlight %}  

<div>
** Exercice to perform **  

  1. Launch the import procedure  and check the corresponding structure
  2. Code a simple count function that prints the number of examples for each classes (along with its name)
</div>{: .notice--info}
  

### 1.2 - Preprocessing

We will rely on a set of spectral transforms that allow to obtain a more descriptive view over the audio information. As most of these is out of the scope of the machine learning course, we redirect you to a [[https://ccrma.stanford.edu/~jos/sasp/|signal processing course]] proposed by [[https://ccrma.stanford.edu/~jos/|Julius O. Smith]].\\

The following functions to compute various types of transforms are given as part of the basic package, in the //0b_Preprocessing// folder
  * ''stft.m''       - [[https://en.wikipedia.org/wiki/Short-time_Fourier_transform| Short-term Fourier transform]]
  * ''fft2barkmx.m'' - [[https://en.wikipedia.org/wiki/Bark_scale| Bark scale]] transform
  * ''fft2melmx.m''  - [[https://en.wikipedia.org/wiki/Mel_scale| Mel scale]] transform
  * ''fft2chromamx'' - [[https://en.wikipedia.org/wiki/Harmonic_pitch_class_profiles| Chromas vector]]
  * ''spec2cep.m''   - [[https://en.wikipedia.org/wiki/Cepstrum| Cepstrum]] transform
  * ''cqt.m''        - [[https://en.wikipedia.org/wiki/Constant_Q_transform| Constant-Q]] transform

In order to perform the various computations, we provide the following function, which performs the different transforms on a complete dataset.
<code matlab>
function dataStruct = computeTransforms(dataStruct)
% dataStruct   : Dataset structure with filenames

% Returns the dataStruct structure with
dataStruct.spectrumPower     % Power spectrum (STFT)
dataStruct.spectrumBark      % Spectrum in Bark scale
dataStruct.spectrumMel       % Spectrum in Mel scale
dataStruct.spectrumChroma    % Chroma vectors
dataStruct.spectrumCepstrum  % Cepstrum
dataStruct.spectrumConstantQ % Constant-Q transform
</code>


\\
<blockquote>
** Exercice to perform **
  - Launch the transform computation procedure and check the corresponding structure
  - For each class, select a random element and plot its various transforms on a single plot. You should obtain plots similar to those shown afterwards.
  - For each transform, try to spot major pros and cons of their representation.
</blockquote>
;#;
{{:esling:aml_p1_altotrombone.jpg?nolink&400 |}}{{:esling:aml_p1_speech.jpg?nolink&400 |}}
;#;
\\

### 1.3 - Features
As you might have noted from the previous exercice, most spectral transforms have a very high dimensionality, and might not be suited to exhibit the relevant structure of different classes. To that end, we provide a set of functions for computing the following features in the //0c_Features// folder
  * ''featureSpectralCentroid.m'' - Spectral centroid
  * ''featureSpectralCrest.m'' - Spectral crest
  * ''featureSpectralDecrease.m'' - Spectral decrease
  * ''featureSpectralFlatness.m'' - Spectral flatness
  * ''featureSpectralKurtosis.m'' - Spectral kurtosis
  * ''featureSpectralRolloff.m'' - Spectral rolloff
  * ''featureSpectralSkewness.m'' - Spectral skewness
  * ''featureSpectralSlope.m'' - Spectral slope
  * ''featureSpectralSpread.m'' - Spectral spread
  * ''featureMFCC.m'' - Mel-Frequency Cepstral Coefficients (MFCC)

Once again, we provide a function to perform the computation of different features on a complete set. Note that for each feature, we compute the temporal evolution in a vector along with the mean and standard deviation of each feature. We only detail the resulting data structure for a single feature.
<code matlab>
function dataStruct = computeFeatures(dataStruct)
% dataStruct   : Dataset structure with filenames

% Returns the dataStruct structure with
dataStruct.SpectralCentroid     % Temporal value of a feature
dataStruct.SpectralCentroidMean % Mean value of that feature
dataStruct.SpectralCentroidStd  % Standard deviation
</code>


\\
<blockquote>
** Exercice to perform **
  - Launch the feature computation procedure and check the corresponding structure
  - This time for each class, superimpose the plots of various features on a single plot, along with a boxplot of mean and standard deviations. You should obtain plots similar to those shown afterwards.
  - What conclusions can you make on the discriminative power of each feature ?
  - Perform scatter plots of the mean features for all the dataset, while coloring different classes.
  - What conclusions can you make on the discriminative power of mean features ?
</blockquote>
;#;
{{:esling:aml_p1b_bells.jpg?nolink&400 |}}{{:esling:aml_p1b_speech.jpg?nolink&400 |}}\\
{{:esling:aml_p1c_scatter1.jpg?nolink&400 |}}{{:esling:aml_p1c_scatter2.jpg?nolink&400 |}}
;#;
\\
  
