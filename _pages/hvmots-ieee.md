---
layout: single
permalink: /hvmots-ieee/
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

======= IEEE : HV-MOTS Matching =======

This is the supporting webpage on MOTS matching :\\
  * Esling Philippe, Agon Carlos "Multiobjective time series matching for audio classification and retrieval", IEEE Transactions on Speech Audio and Language Processing 2012 (in review).

We provide in this page detailed informations about the results of MultiObjective Time Series (MOTS) matching. More informations about the MOTS paradigm can be found in the article and on a related page which presents the [[esling/mots.html|MultiObjective Time Series]] approach. Another page of this website also presents more information about the [[esling/ipad.html|sound sample database application]] along with a demonstration of an [[esling/ipad.html#ipad-interface|iPad interface]] which implements the approaches explained in the article. 

====== Introduction ======

  * [[esling/ieee-mots.html#audio-datasets|Audio datasets]] : Both datasets used in our study are available for download so that our experiments are fully reproducible. These datasets are available either as sound files and Matlab (.MAT) files. The MAT files contains an organized structure of the results from our spectral descriptors analysis.

  * [[esling/ieee-mots.html#statistical-significance|Statistical significance]] : This section provides extended results of statistical significance tests over both datasets. We separate the evaluation depending on the //best// and //mean// classification accuracies. The statistical tests are performed through a Tukey-Kramer HSD based on the results of Friedman's ANOVA.

  * [[esling/ieee-mots.html#classification-results|Classification results]] : This section provides extended classification results for our approach. [[esling/ieee-mots.html#general-results|General results]]  exhibit the various classification accuracies for different sets and [[esling/ieee-mots.html#features-combinations|features combinations]] provide an extended list of best features set for each level of analysis.

  * [[esling/ieee-mots.html#features-analysis|Features analysis]] provide an extended list of feature-by-feature discriminative power. We have only listed here the features which were selected after bi-objective combinations, ie. the feature which were used from three to more objectives classification (half of the complete feature set).

  * [[esling/ieee-mots.html#robustness-tests|Robustness tests]] provides more detailed results of each algorithm for various distortion classes. First the table for increasing objectives gives classification accuracies for each distortion. Then, complete figures gives an overview of the robustness for each method.


====== Audio datasets ======

This section contains the downloadable archives of both datasets used in the paper. For each dataset, two archives are available. The first contains the original sound files. The second contains the results of the spectral analysis module in Matlab (.MAT) format. The features file contains a structure named ''data'' which contains the ''name'', ''class'', ''sampleID'' and ''features'' structure. The ''features'' structure contains every descriptor listed in the paper in matrix format ''(nbDimensions x nbTimePoints)''. The corresponding descriptor are the raw values obtained from IRCAMDescriptor.

===== MuscleFish =====

  * [[http://repmus.ircam.fr/downloads/datasets/MuscleFish_Sounds.zip|Sound files]] **(5.5Mb)** - Contains the original dataset of 409 Sun/Next (.au) files divided in 16 classes.
  * [[http://repmus.ircam.fr/downloads/datasets/MuscleFish_Features.zip|Spectral features]] **(121Mb)** - Results of the spectral analysis of IRCAM descriptor for the entire dataset

This dataset was originally assembled for the following paper :
E. Wold, T. Blum, D. Keislar, and J. Wheaten, “Content-based classification, search, and retrieval of audio,” Multimedia, IEEE, vol. 3, no. 3, pp. 27–36, 1996.
All rights for thee sounds belong to the [[http://www.musclefish.com|MuscleFish]] company.

We would like to express our thanks to Erling Wold and Thom Blum for their kind help on retrieving these sounds and allowing us to upload the dataset on this supporting webpage.

===== Freesound =====

  * [[http://repmus.ircam.fr/downloads/datasets/Freesound_Sounds.zip|Sound files]] **(Warning : 1.3Gb)** - Contains the dataset of 2193 sound files divided in 54 classes collected specifically for our study.
  * [[http://repmus.ircam.fr/downloads/datasets/Freesound_Features.zip|Feature files]] **(Warning : 645.9Mb)** - Spectral analysis files of the Freesound dataset

Most of the sounds in this dataset were retrieved from the [[http://www.freesound.org/|Freesound project]] and, therefore, respective credits should be given to different users :
  * applause : [[http://www.freesound.org/people/recordinghopkins/packs/4859/| HQ Applause]] (by [[http://www.freesound.org/people/recordinghopkins/|Recordinghopkins]]), [[http://www.freesound.org/people/RHumphries/packs/111/| Applause]] (by [[http://www.freesound.org/people/RHumphries/|Rhumphries]]) and [[http://www.freesound.org/people/joedeshon/packs/7476/|Polite applause]] (by [[http://www.freesound.org/people/joedeshon/|Joedeshon]]).
  * birds : [[http://www.freesound.org/people/HardPCM/packs/2349/|Bird]] (by [[http://www.freesound.org/people/hardpcm/|Hardpcm]]) and [[http://www.freesound.org/people/tigersound/packs/517/|Bird sounds]] (by [[http://www.freesound.org/people/tigersound/|Tigersound]])
  * cat : [[http://www.freesound.org/people/NoiseCollector/packs/277/|Animals]] (by [[http://www.freesound.org/people/noisecollector/|Noisecollector]]), [[http://www.freesound.org/people/Department64/packs/4120/|BL_Cat]] (by [[http://www.freesound.org/people/department64/|Department64]]) and [[http://www.freesound.org/people/freemaster2/packs/4280/|Siamese cat]] (by [[http://www.freesound.org/people/freemaster2/|Freemaster2]])
  * crash : [[http://www.freesound.org/people/ltibbits/packs/889/|HQ-Cymbals]] (by [[http://www.freesound.org/people/ltibbits/|Ltibbits]]) and [[http://www.freesound.org/people/Robinhood76/packs/3940/|Sabian percussions]] (by [[http://www.freesound.org/people/robinhood76/|Robinhood76]])
  * dog : [[http://www.freesound.org/people/NoiseCollector/packs/3537/|Animals]] (by [[http://www.freesound.org/people/noisecollector/|Noisecollector]]) and [[http://www.freesound.org/people/Robinhood76/packs/4026/|Dogs]] (by [[http://www.freesound.org/people/robinhood76/|Robinhood76]])
  * drum-loops : [[http://www.freesound.org/people/VEXST/packs/1550/| Amen breaks]] (by [[http://www.freesound.org/people/vexst/|Vexst]]) and [[http://www.freesound.org/people/yewbic/packs/7087/|Music loops]] (by [[http://www.freesound.org/people/yewbic/|Yewbic]])
  * female : [[http://www.freesound.org/people/NoiseCollector/packs/207/|Phone]] (by [[http://www.freesound.org/people/noisecollector/|Noisecollector]]) and [[http://www.freesound.org/people/Corsica_S/packs/6131/|Woodio]] (by [[http://www.freesound.org/people/corsica_s/|Corsica-s]])
  * footsteps : [[http://www.freesound.org/people/soundmary/packs/7395/|Footsteps]] (by [[http://www.freesound.org/people/soundmary/|Soundmary]]), [[http://www.freesound.org/people/ragamuffin/packs/7471/|Footsteps]] (by [[http://www.freesound.org/people/ragamuffin/|Ragamuffin]]), [[http://www.freesound.org/people/Corsica_S/packs/2823/|Footsteps]] (by [[http://www.freesound.org/people/corsica_s/|Corsica-s]]), [[http://www.freesound.org/people/RutgerMuller/packs/3264/|Footsteps]] (by [[http://www.freesound.org/people/rutgermuller/|Rutgermuller]])
  * glockenspiel : [[http://www.freesound.org/people/angstrom/packs/583/|Glockenspiel]] (by [[http://www.freesound.org/people/angstrom/|Angstrom]])
  * guitar-distorted : [[http://www.freesound.org/people/SpeedY/packs/643/|Distorted]] (by [[http://www.freesound.org/people/speedy/|Speedy]]) and [[http://www.freesound.org/people/Koen/packs/51/|Distorted guitars]] (by [[http://www.freesound.org/people/koen/|Koen]])
  * gunshot : [[http://www.freesound.org/people/Cyberkineticfilms/packs/7026/|Gunshot]] (by [[http://www.freesound.org/people/cyberkineticfilms/|Cyberkineticfilms]]), [[http://www.freesound.org/people/Xenonn/packs/8014/|Layered gunshots]] (by [[http://www.freesound.org/people/xenonn/|Xenonn]]) and [[http://www.freesound.org/people/Robinhood76/packs/3932/|War and battles]] (by [[http://www.freesound.org/people/robinhood76/|Robinhood76]])
  * hi-hats : [[http://www.freesound.org/people/ltibbits/packs/889/|HQ-Cymbals]] (by [[http://www.freesound.org/people/ltibbits/|Ltibbits]]), [[http://www.freesound.org/people/Walter_Odington/packs/1583/|Hi-hats]] (by [[http://www.freesound.org/people/walter_odington/|Walter-odington]]), [[http://www.freesound.org/people/sandyrb/packs/2265/|Real hi-hats]] (by [[http://www.freesound.org/people/sandyrb/|Sandyrb]]) and [[http://www.freesound.org/people/Robinhood76/packs/3940/|Sabian percussion]] (by [[http://www.freesound.org/people/robinhood76/|Robinhood76]])
  * indian-santoor : [[http://www.freesound.org/people/batchku/packs/581/|Indian santoor]] (by [[http://www.freesound.org/people/batchku/|Batchku]])
  * indian-tabla : [[http://www.freesound.org/people/loofa/packs/1472/|Tabla & Baya]] (by [[http://www.freesound.org/people/loofa/|Loofa]])
  * indian-tambura : [[http://www.freesound.org/people/loofa/packs/1468/|Indian tambura]] (by [[http://www.freesound.org/people/loofa/|Loofa]])
  * indian-thumb-piano : [[http://www.freesound.org/people/madjad/packs/1332/|Indonesian thumb piano]] (by [[http://www.freesound.org/people/madjad/|Madjad]])
  * kick : [[http://www.freesound.org/people/Walter_Odington/packs/1579/|Kick drums]] (by [[http://www.freesound.org/people/walter_odington/|Walter-odington]]), [[http://www.freesound.org/people/sandyrb/packs/2295/|Hybrid kicks]] (by [[http://www.freesound.org/people/sandyrb/|Sandyrb]]) and [[http://www.freesound.org/people/robbiesurp/packs/191/|Derek murphy kicks]] (by [[http://www.freesound.org/people/robbiesurp/|Robbiesurp]])
  * laughter : [[http://www.freesound.org/people/hanstimm/packs/876/|Laughter]] (by [[http://www.freesound.org/people/hanstimm/|Hanstimm]]) and [[http://www.freesound.org/people/Robinhood76/packs/3864/|Funny voices]] (by [[http://www.freesound.org/people/robinhood76/|Robinhood76]])
  * male : [[http://www.freesound.org/people/Robinhood76/packs/5449/|Web design]] (by [[http://www.freesound.org/people/robinhood76/|Robinhood76]]) and [[http://www.freesound.org/people/alphahog/packs/3002/|Voices]] (by [[http://www.freesound.org/people/alphahog/|Alphahog]])
  * musicbox : [[http://www.freesound.org/people/tombola/packs/3141/|Toy record]] (by [[http://www.freesound.org/people/tombola/|Tombola]])
  * paper : [[http://www.freesound.org/people/Koops/packs/1237/|Paper book]] (by [[http://www.freesound.org/people/koops/|Koops]])
  * reese : [[http://www.freesound.org/people/Harha/packs/7265/|Access virus C]] (by [[http://www.freesound.org/people/harha/|Harha]]), [[http://www.freesound.org/people/hardwareshaba/packs/8664/|Tearing neurofunk]] (by [[http://www.freesound.org/people/hardwareshaba/|Hardwareshaba]]) and [[http://www.freesound.org/people/tenchu/packs/4789/|CyanVdist-Reese]] (by [[http://www.freesound.org/people/tenchu/|Tenchu]])
  * robotic : [[http://www.freesound.org/people/Puniho/packs/7103/|Strange talk]] (by [[http://www.freesound.org/people/puniho/|Puniho]])
  * scratching : [[http://www.freesound.org/people/junggle/packs/1822/|Turntablism]] (by [[http://www.freesound.org/people/junggle/|Junggle]])
  * screams : [[http://www.freesound.org/people/thanvannispen/packs/531/|Screams and pain]] (by [[http://www.freesound.org/people/thanvannispen/|Thanvannispen]]) and [[http://www.freesound.org/people/plagasul/packs/3/|Weird male screams]] (by [[http://www.freesound.org/people/plagasul/|Plagasul]])
  * singing-bowls : [[http://www.freesound.org/people/hanstimm/packs/1874/|Singing bowls]] (by [[http://www.freesound.org/people/hanstimm/|Hanstimm]])
  * siren : [[http://www.freesound.org/people/guitarguy1985/packs/3355/|Sirens and alarms]] (by [[http://www.freesound.org/people/guitarguy1985/|guitarguy1985]]) and [[http://www.freesound.org/people/radian/packs/4053/|Siren synth]] (by [[http://www.freesound.org/people/radian/|Radian]])
  * snare : [[http://www.freesound.org/people/crispydinner/packs/7652/|909 Snares]] (by [[http://www.freesound.org/people/crispydinner/|Crispydinner]])and [[http://www.freesound.org/people/robbiesurp/packs/189/|Derek Murphy Snares]] (by [[http://www.freesound.org/people/robbiesurp/|Robbiesurp]])
  * subway : [[http://www.freesound.org/people/WIM/packs/657/|London underground]] (by [[http://www.freesound.org/people/wim/|Wim]]) and [[http://www.freesound.org/people/RHumphries/packs/113/|Trains & Subways]] (by [[http://www.freesound.org/people/rhumphries/|Rhumphries]])
  * sword : [[http://www.freesound.org/people/lostchocolatelab/packs/94/|Sword]] (by [[http://www.freesound.org/people/lostchocolatelab/|Lostchocolatelab]])
  * tb303 : [[http://www.freesound.org/people/djgriffin/packs/1357/|Acid]] (by [[http://www.freesound.org/people/djgriffin/|Djgriffin]]),  [[http://www.freesound.org/people/sleep/packs/1748/|303 me]] (by [[http://www.freesound.org/people/sleep/|Sleep]]), [[http://www.freesound.org/people/laban/packs/3210/|x0xb0x]] (by [[http://www.freesound.org/people/laban/|Laban]]), [[http://www.freesound.org/people/Kara/packs/4468/|TB-303 loops]] (by [[http://www.freesound.org/people/kara/|Kara]]) and [[http://www.freesound.org/people/pitmusic/packs/474/|TB-303 Bass]] (by [[http://www.freesound.org/people/pitmusic/|Pitmusic]])
  * telephone : [[http://www.freesound.org/people/soundplusdesign/packs/4257/|Telephone]] (by [[http://www.freesound.org/people/soundplusdesign/|Soundplusdesign]])
  * thunder : [[http://www.freesound.org/people/SpeedY/packs/955/|Thunder storm]] (by [[http://www.freesound.org/people/speedy/|Speedy]]), [[http://www.freesound.org/people/Erdie/packs/1401/|Nature]] (by [[http://www.freesound.org/people/erdie/|Erdie]]) and [[http://www.freesound.org/people/nednednerb/packs/2430/|24-bit Thunder]] (by [[http://www.freesound.org/people/nednednerb/|Nednedberd]])
  * toms : [[http://www.freesound.org/people/sandyrb/packs/2633/|Processed toms]] (by [[http://www.freesound.org/people/sandyrb/|Sandyrb]])
  * tone-drum : [[http://www.freesound.org/people/patchen/packs/211/|Tone drum]] (by [[http://www.freesound.org/people/patchen/|Patchen]])
  * vocoder : [[http://www.freesound.org/people/harri/packs/619/|100 most common words]] (by [[http://www.freesound.org/people/harri/|Harri]]), [[http://www.freesound.org/people/hanstimm/packs/899/|Vocoder]] (by [[http://www.freesound.org/people/hanstimm/|Hanstimm]])
  * water : [[http://www.freesound.org/people/Robinhood76/packs/4100/|Water]] (by [[http://www.freesound.org/people/robinhood76/|Robinhood76]]), [[http://www.freesound.org/people/AGFX/packs/1253/|Water splash]] (by [[http://www.freesound.org/people/agfx/|Agfx]]) and [[http://www.freesound.org/people/Anton/packs/26/|Water]] (by [[http://www.freesound.org/people/anton/|Anton]])
  * whistle : [[http://www.freesound.org/people/Benboncan/packs/4290/|Sheepdog]] (by [[http://www.freesound.org/people/benboncan/|Benboncan]]) and [[http://www.freesound.org/people/joedeshon/packs/5194/|Slide whistle]] (by [[http://www.freesound.org/people/joedeshon/|Joedeshon]])
  * wobble : [[http://www.freesound.org/people/mikobuntu/packs/6749/|Dubstep]] (by [[http://www.freesound.org/people/mikobuntu/|Mikobuntu]]), [[http://www.freesound.org/people/DirtyJewbs/packs/7829/|Wobble basses]] (by [[http://www.freesound.org/people/dirtyjewbs/|Dirtyjewbs]]) and [[http://www.freesound.org/people/Ongitak/packs/8066/|B8 Wobbly Bass]] (by [[http://www.freesound.org/people/ongitak/|Ongitak]])
  * zipper : [[http://www.freesound.org/people/Anton/packs/316/|Zipper-anechoic]] (by [[http://www.freesound.org/people/anton/|Anton]])

All the instrumental sounds are part of IRCAM's Studio On Line (SOL) sound database.


====== Statistical significance ======

This section provides extended results of statistical significance tests over both datasets. We separate the evaluation depending on the //mean// classification accuracies. The statistical tests are performed through three different procedures for each level (number of features involved in the classification). First, a Tukey-Kramer HSD based on the results of Friedman's ANOVA allows to see the mean column rank of each method. The second provides the statistical mean accuracy for each method depending on the current number of dimensions involved. Finally, the //critical difference// graphs allows to discriminate the methods and group them into equivalent //clique// if their results are statistically equivalent.

==== 1 feature ====

{{:esling:hsd_1.jpg?nolink&300 |}} {{:esling:anova_1.jpg?nolink&300 |}} {{:esling:critical_1.jpg?nolink&300 |}}

==== 2 features ====

{{:esling:hsd_2.jpg?nolink&300 |}} {{:esling:anova_2.jpg?nolink&300 |}} {{:esling:critical_2.jpg?nolink&300 |}}

==== 3 features ====

{{:esling:hsd_3.jpg?nolink&300 |}} {{:esling:anova_3.jpg?nolink&300 |}} {{:esling:critical_3.jpg?nolink&300 |}}

==== 4 features ====

{{:esling:hsd_4.jpg?nolink&300 |}} {{:esling:anova_4.jpg?nolink&300 |}} {{:esling:critical_4.jpg?nolink&300 |}}

==== 5 features ====

{{:esling:hsd_5.jpg?nolink&300 |}} {{:esling:anova_5.jpg?nolink&300 |}} {{:esling:critical_5.jpg?nolink&300 |}}

==== 6 features ====

{{:esling:hsd_6.jpg?nolink&300 |}} {{:esling:anova_6.jpg?nolink&300 |}} {{:esling:critical_6.jpg?nolink&300 |}}

==== 7 features ====

{{:esling:hsd_7.jpg?nolink&300 |}} {{:esling:anova_7.jpg?nolink&300 |}} {{:esling:critical_7.jpg?nolink&300 |}}

==== 8 features ====

{{:esling:hsd_8.jpg?nolink&300 |}} {{:esling:anova_8.jpg?nolink&300 |}} {{:esling:critical_8.jpg?nolink&300 |}}
==== 2 features ====


====== Classification results ======

===== General results =====

==== Global results ====
