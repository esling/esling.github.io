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

Download the [slides ![](../images/pdf.png)](../documents/MML.Lesson.1.Introduction.pdf)

The corresponding slides cover

  * Introduction to artificial intelligence
  * Properties of machine learning
  * Nearest-neighbors

# Tutorial 
In this introduction, we will cover basic Music Information Retrieval (MIR) interactions, in which we process a dataset of sound files and try to observe the properties of their various temporal and spectral features. Hence, we will quickly review basic calculus required to perform further machine learning tasks.

### 1.0 - Reference code

Get the baseline code from this [zip file ![](../images/file.png)](../documents/atiam_ml_exercises.zip)

### 1.1 - Datasets
In order to do so, we will work with several datasets that should be downloaded on your local computer first from this [link ![](../images/file.png)](https://pchit.ircam.fr/public.php?service=files&t=a476001b408cfa9dacf8721149b9f151)

  * **Classification** - *MuscleFish* dataset
  * **Music-speech** - *MIREX Recognition* set
  * **Source separation** - *SMC Mirum* dataset
  * **Speech recognition** - *CMU Arctic* dataset

For the first parts of the tutorial, we will mostly use the classification dataset only. In order to facilitate the interactions, we provide the function `importDataset` that allows to import different audio datasets

{% highlight Matlab %}
function dataStruct = importDataset(classPath, type)
% classPath  : Path to the dataset (string)
% type       : Type of dataset (string: 'classify', 'plain', 'metadata')

% Returns the dataStruct structure with
dataStruct.filenames  % Cell containing the list of audio files
dataStruct.classes    % Vector of indexes assigning each file to a class
dataStruct.classNames % Cell of class names
{% endhighlight %}  

**Exercice**  
<div markdown="1">  

  1. Launch the import procedure  and check the corresponding structure
  2. Code a count function that prints the name and number of examples for each classes 

</div>{: .notice--info}  


### 1.2 - Preprocessing

We will rely on a set of spectral transforms that allow to obtain a more descriptive view over the audio information. As most of these is out of the scope of the machine learning course, we redirect you to a [signal processing course](https://ccrma.stanford.edu/~jos/sasp/) proposed by [Julius O. Smith](https://ccrma.stanford.edu/~jos/).  

The following functions to compute various types of transforms are given as part of the basic package, in the `0b_Preprocessing` folder  

  * `stft.m`       - [Short-term Fourier transform](https://en.wikipedia.org/wiki/Short-time_Fourier_transform)
  * `fft2barkmx.m` - [Bark scale](https://en.wikipedia.org/wiki/Bark_scale) transform
  * `fft2melmx.m`  - [Mel scale](https://en.wikipedia.org/wiki/Mel_scale) transform
  * `fft2chromamx` - [Chromas vector](https://en.wikipedia.org/wiki/Harmonic_pitch_class_profiles)
  * `spec2cep.m`   - [Cepstrum](https://en.wikipedia.org/wiki/Cepstrum) transform
  * `cqt.m`        - [Constant-Q](https://en.wikipedia.org/wiki/Constant_Q_transform) transform

In order to perform the various computations, we provide the following function, which performs the different transforms on a complete dataset.  


{% highlight Matlab %}
function dataStruct = computeTransforms(dataStruct)
% dataStruct   : Dataset structure with filenames

% Returns the dataStruct structure with
dataStruct.spectrumPower     % Power spectrum (STFT)
dataStruct.spectrumBark      % Spectrum in Bark scale
dataStruct.spectrumMel       % Spectrum in Mel scale
dataStruct.spectrumChroma    % Chroma vectors
dataStruct.spectrumCepstrum  % Cepstrum
dataStruct.spectrumConstantQ % Constant-Q transform
{% endhighlight %}   

**Exercice**  
<div markdown="1">  

  1. Launch the transform computation procedure and check the corresponding structure
  2. For each class, select a random element and plot its various transforms on a single plot. You should obtain plots similar to those shown afterwards.
  3. For each transform, try to spot major pros and cons of their representation.

</div>{: .notice--info}

;#;
{{:esling:aml_p1_altotrombone.jpg?nolink&400 |}}{{:esling:aml_p1_speech.jpg?nolink&400 |}}
;#;
\\

### 1.3 - Features
As you might have noted from the previous exercice, most spectral transforms have a very high dimensionality, and might not be suited to exhibit the relevant structure of different classes. To that end, we provide a set of functions for computing the following features in the `0c_Features` folder

  * `featureSpectralCentroid.m` - Spectral centroid
  * `featureSpectralCrest.m` - Spectral crest
  * `featureSpectralDecrease.m` - Spectral decrease
  * `featureSpectralFlatness.m` - Spectral flatness
  * `featureSpectralKurtosis.m` - Spectral kurtosis
  * `featureSpectralRolloff.m` - Spectral rolloff
  * `featureSpectralSkewness.m` - Spectral skewness
  * `featureSpectralSlope.m` - Spectral slope
  * `featureSpectralSpread.m` - Spectral spread
  * `featureMFCC.m` - Mel-Frequency Cepstral Coefficients (MFCC)

Once again, we provide a function to perform the computation of different features on a complete set. Note that for each feature, we compute the temporal evolution in a vector along with the mean and standard deviation of each feature. We only detail the resulting data structure for a single feature.  

{% highlight Matlab %}
function dataStruct = computeFeatures(dataStruct)
% dataStruct   : Dataset structure with filenames

% Returns the dataStruct structure with
dataStruct.SpectralCentroid     % Temporal value of a feature
dataStruct.SpectralCentroidMean % Mean value of that feature
dataStruct.SpectralCentroidStd  % Standard deviation
{% endhighlight %}  


**Exercice**

<div markdown="1">

  1. Launch the feature computation procedure and check the corresponding structure
  2. This time for each class, superimpose the plots of various features on a single plot, along with a boxplot of mean and standard deviations. You should obtain plots similar to those shown afterwards.
  3. What conclusions can you make on the discriminative power of each feature ?
  4. Perform scatter plots of the mean features for all the dataset, while coloring different classes.
  5. What conclusions can you make on the discriminative power of mean features ?

</div>{: .notice--info}

;#;
{{:esling:aml_p1b_bells.jpg?nolink&400 |}}{{:esling:aml_p1b_speech.jpg?nolink&400 |}}\\
{{:esling:aml_p1c_scatter1.jpg?nolink&400 |}}{{:esling:aml_p1c_scatter2.jpg?nolink&400 |}}
;#;
\\
  
