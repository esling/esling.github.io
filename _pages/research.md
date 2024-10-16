---
layout: single
permalink: /research/
author_profile: false
sidebar:
  nav: "research"
---

<div markdown = "1">

# Research
I am currently an associate professor and research in data mining and artificial intelligence at [IRCAM](http://www.ircam.fr), where I am head of the [ACIDS research group](http://acids.ircam.fr) within the [Musical representations](http://repmus.ircam.fr/) and teaching computer science and mathematics at [Sorbonne Université (Formerly UPMC - Paris 6)](http://www.sorbonne-universite.fr/). I also participate in ecological monitoring and metagenomics research with [Geneva university (UNIGE)](http://genev.unige.ch/research/people/Philippe-Esling).

You can find detailed lists of  

1. [Projects](/projects/) and main research axes.
2. [Scientific publications](/publications/) and other papers.
3. [Supervision](/supervision/) of PhD and students.

## Selected projects

### Flow synthesizer

<img align="left" src="../images/research/flow_paper_workflow_full.svg">

Sound synthesizers are pervasive in music and they now even entirely define new music genres. However, their complexity and sets of parameters renders them difficult to master. We created an innovative generative probabilistic model that learns an invertible mapping between a continuous auditory latent space of a synthesizer audio capabilities and the space of its parameters. We approach this task using variational auto-encoders and normalizing flows Using this new learning model, we can learn the principal macro-controls of a synthesizer, allowing to travel across its organized manifold of sounds, performing parameter inference from audio to control the synthesizer with our voice, and  even address semantic dimension learning where we find how the controls fit to given semantic concepts, all within a single model. These ideas have been implemented in a real-time plugin as a Max4Live device

<img align="left" src="../images/research/flow_synth.jpeg">


You can download the device [here](https://github.com/acids-ircam/flow_synthesizer) along with the [source code](https://github.com/acids-ircam/flow_synthesizer) or find more information on the [dedicated webpage](https://acids-ircam.github.io/flow_synthesizer/), or read the [full research paper](https://arxiv.org/abs/1907.00971)

### Generative timbre spaces
##### Best presentation award at ISMIR 2019

<img align="left" width="400" height="400" src="../images/research/generative_timbre_0.png">

Timbre spaces have been used to study the relationships between different instrumental timbres,based on perceptual ratings. However, they provide limited interpretability, no generative capabilityand no generalization. Here, we show that variational auto-encoders (VAE) can alleviate these limitations, by regularizing their latent space during training in order to ensure that the latent space of audio follows the same topology as that of the perceptual timbre space. Hence, we bridge audio analysis, perception and synthesis into a single system.

You can download the [source code](https://github.com/acids-ircam/variational-timbre) or find more information on the [dedicated webpage](https://acids-ircam.github.io/variational-timbre/), or read the [full research paper](https://arxiv.org/abs/1805.08501)

### Automatic orchestration

#### Orchids
The orchids software is the first complete system for abstract and temporal computer-assisted orchestration and timbral mixture optimization. It provides a set of algorithms and features to reconstruct any time-evolving target sound with a combination of acoustic instruments, given a set of psychoacoustic criteria. It can help composers to achieve unthinkable timbral colors by providing efficient sets of solutions that best match a sound target. Find more information [on the dedicated webpage](http://forumnet.ircam.fr/product/orchids-en/)

#### Live Orchestral Piano
We recently developed the first live orchestral piano (LOP) system. The system provides a way to compose music with a full classical orchestra in real-time by simply playing on a MIDI keyboard. Our approach is to perform statistical inference on a [corpus of midi files](https://qsdfo.github.io/LOP/database.html). This corpus contains piano scores and their orchestration by famous composers.This objective might seem too ambitious : learning orchestration through the mere observation of scores ? We believe that by observing the correlation between piano scores and corresponding orchestrations made by famous composers, we might be able to infer the spectral kwnoledge of composers. The probabilistic models we investigate are neural networks with conditional and temporal structures. Find more information [on this webpage](https://qsdfo.github.io/LOP/)

## Selected publications  

**Esling P.**, Masuda, N. Bardet, A. Despres, R. Chemla--Romeu-Santos A. *Universal audio synthesizer control with normalizing flows*, 22nd International Digital Audio Effects (DAFx2019) Conference. 
[![](../images/pdf.png)](https://arxiv.org/abs/1907.00971) [![](../images/html.png)](https://acids-ircam.github.io/flow_synthesizer/) [![](../images/file.png)]() [[Blog]](https://acids-ircam.github.io/flow_synthesizer/) 

**Esling P.**, Chemla--Romeu-Santos A. & Bitton A. *Generative timbre spaces: regularizing variational auto-encoders with perceptual metrics*, 19th International Society for Music Information Retrieval (ISMIR2018) Conference. **Best presentation award**
[![](../images/pdf.png)](https://arxiv.org/pdf/1805.08501.pdf) [![](../images/html.png)](https://acids-ircam.github.io/variational-timbre/) [![](../images/file.png)]() [[Blog]](https://acids-ircam.github.io/variational-timbre/) 

**Esling P.**, Lejzerowicz F. & Pawlowski J. *High-throughput accuracy for multiplex amplicon sequencing*, Nucleic Acid Research, February 17, 2015 doi:10.1093/nar/gkv107. (2015). IF: 8.055  
[![](../images/pdf.png)](https://www.researchgate.net/profile/Philippe_Esling/publication/272513307_Accurate_multiplexing_and_filtering_for_high-throughput_amplicon-sequencing/links/54eb3c0c0cf25ba91c864edb.pdf) [![](../images/html.png)](http://nar.oxfordjournals.org/content/early/2015/02/16/nar.gkv107.full) [![](../images/file.png)]() [[Blog]](/blog/)  

**Esling P.** Agon C., *Multiobjective time series matching and classification* IEEE Transactions on Speech Audio and Language Processing, vol. 21, no. 10, pp. 2057–2072. (2013). IF: 1.675  
[![](../images/pdf.png)](https://www.researchgate.net/profile/Philippe_Esling/publication/260692536_Multiobjective_Time_Series_Matching_for_Audio_Classification_and_Retrieval/links/55192e1d0cf273292e70c5fa.pdf) [![](../images/html.png)](http://ieeexplore.ieee.org/document/6521366/) [![](../images/file.png)]() [[Blog]](/blog/)  

**Esling P.** Agon C., *Time series data mining* ACM Computing Surveys, vol. 45, no. 1., (2012). IF: 4.543  
[![](../images/pdf.png)](http://www.lcis.com.tw/paper_store./paper_store/%E6%95%B8%E6%93%9A%E6%8C%96%E6%8E%98_data_mining%20(145)-201563233943718.pdf) [![](../images/html.png)](http://dl.acm.org/citation.cfm?id=2379788) [![](../images/file.png)]() [[Blog]](/blog/)  

</div>{: .notice--blank}
