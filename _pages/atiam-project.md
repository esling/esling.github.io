===== ATIAM 2014 Project - Molecular clock synthesis =====

==== Subject ====

You can find the complete document for the ATIAM 2014 Project - Molecular clock synthesis here\\
{{:esling:description.pdf| PDF}}

=== Slides ===

Here are the slides to the project presentation\\
[[https://dl.dropboxusercontent.com/u/24122451/Cours_Projet.pdf| Slides]]
==== Source code ====

=== Multiple alignment softwares ===

In order to ease your pain, we downloaded and check the five best multiple alignment softwares currently used. For each of these, we include in the following a small description of the compilation procedure and also a list of useful parameters for the project. Note that a vast set of parameters is available for each software, which is why we also included the link to the complete documentation in this page. (We encourage you to perform full-scale evaluation of all parameters for all the softwares)\\
\\
All these softwares use the FASTA input file format, for which an example can be seen here\\
http://prodata.swmed.edu/promals/info/fasta_format_file_example.htm\\
\\
Most softwares rely on the BLAST matrix format for scoring matrix which can be seen here\\
ftp://ftp.ncbi.nih.gov/blast/matrices/\\
http://drive5.com/muscle/nucmx

**Clustal Omega 1.2.1**

{{:esling:clustal-omega-1.2.1.zip| Sources}}

  - Download the Clustal-Omega package (v1.2.1)
  - Install argtable2 (http://argtable.sourceforge.net/)
  - Configure and compile the code inside the package

<code>./configure
make
make install</code>

Complete help is available here: [[http://www.clustal.org/download/clustalw_help.txt|Documentation]]

//Interesting parameters//
<code>
-MATRIX=FILENAME Use a user-defined scoring matrix following BLAST format.
</code>

**MAFFT 7.213**

{{:esling:mafft-7.213.zip| Sources}}

  - Download the MAFFT package (v7.213)
  - Configure and compile the code inside the package

<code>cd core
make clean all
make install</code>

Complete help is available here: [[http://mafft.cbrc.jp/alignment/software/tips0.html|Tips]]

//Interesting parameters//
<code>
--anysymbol accepts any type of symbol in input
--matrix FILENAME Use a user-defined scoring matrix following BLAST format.
All infos: mafft --man
</code>
           
**MUSCLE 3.8.425**

{{:esling:muscle-3.8.425.zip| Sources}}

  - Download the MUSCLE package (v3.8.425)
  - Compile the code inside the package

<code>make clean all</code>

Complete help is available here: [[http://www.drive5.com/muscle/manual/|Manual]]

//Interesting parameters//
<code>
-seqtype option accepts any type of symbol in input
-matrix FILENAME Use a user-defined scoring matrix following BLAST format
</code>

**ProbCons 1.12**

{{:esling:probcons-1.12.zip| Sources}}

  - Download the ProbCons package (v1.12)
  - Compile the code inside the package

<code>make clean all</code>

Complete help is available here: [[http://genome.cshlp.org/content/suppl/2005/02/01/15.2.330.DC1/manual.pdf|Manual]]

//Interesting parameters//
<code>
-m, --matrixfile FILENAME
Read scoring matrix parameters from FILENAME
</code>
//Warning this matrix is not in BLAST format, its format is detailed in the manual//

**T-Coffee 6.18**

{{:esling:tcoffee-1.7.zip| Sources}}

  - Download the T-Coffee package (v6.18)
  - Compile the code inside the package

<code>make clean all</code>

Complete help is available here: [[http://www.tcoffee.org/Documentation/t_coffee/t_coffee_tutorial.htm|Tutorial]]

//Interesting parameters//
<code>
-matrix=FILENAME Use a user-defined scoring matrix following BLAST format.
</code>

=== MATLAB figures ===

Here are a few scripts offered to help you in producing high-quality figures.

  * {{:esling:polardendrogram.m.zip| Polar dendrogram plotting}}
  * {{:esling:setpaperquality.m.zip| Automatic paper quality script}}
  * {{:esling:graphic.zip| Set of plotting functions from the internet}}

