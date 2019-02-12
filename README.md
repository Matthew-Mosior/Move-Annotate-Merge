# Move-Annotate-Merge: Tab-separated values file (.tsv) manipulation for manual review generated from sequencing data analysis


## Introduction

Preparing sequencing data for manual review can be tedious, time-consuming and a user error-prone process.  This script, implemented in [Haskell](https://www.haskell.org/), transforms user-defined .tsv files containing variant annotation output into a single merged, annotated file easily searched and ready for downstream filtration.

## Setting up the .tsv input file

A prerequisite for getting useful output from this Haskell script is to setup a input .tsv file that it expects.<br/>
Your input .tsv file should have the following structure:<br/><br/>
`[/Path/To/Tsv/File/example_variants.annotated.tsv]\t[Corresponding_sample_identifier]\t[/Path/To/Final/Directory]`<br/><br/>
There should be as many lines in this file as there are input .tsv files.



## Shell Implementation

### Setting up the Reference Genome Directory

A prerequisite to getting useful output from this shell script is to setup your reference genome directory correctly.<br/>
First, your reference genome directory should have the following structure:<br/><br/>
`[database directory] - [genome directory] - [fasta file]`<br/><br/>
To create this required reference genome directory, use the shell script **GCFrefgenomedirectory.sh**.  This shell script will 
correctly set-up your
reference genome directory, assuming you have downloaded GCF ([RefSeq assembly](https://www.ncbi.nlm.nih.gov/assembly/model/)) 
sequences.<br/><br/>
This shell script will change your initial reference genome directory setup of `[database directory] - [fasta file]` to the required
reference genome directory setup: `[database directory] - [genome directory] - [fasta file]`.<br/><br/>
Provide the path to the directory that contains the initial `[database directory]` as a command line argument as shown in the following 
example:<br/><br/>
`sh GCFrefgenomedirectory.sh /usr/home/ncbi/ncbi-genomes-2018-02-17`<br/><br/>



### Usage

This script is very easy to use, it takes **sigma_out.gvector.txt** as command line arguments.  Keep in mind, the Strains community
challenge has four datasets:<br/><br/>
`Simulated_Low_Complexity`<br/>
`Simulated_Medium_Complexity`<br/>
`Simulated_High_Complexity`<br/>
`RealData (Mouse fecal samples)`<br/><br/>
Each of these datasets contains four sets of paired-end sequencing reads, so in reality:<br/><br/>
`Simulated_Low_Complexity`<br/>
`sim_low_S1_PE1.fq`<br/>
`sim_low_S1_PE2.fq`<br/>
`sim_low_S2_PE1.fq`<br/>
`sim_low_S2_PE2.fq`<br/>
`sim_low_S3_PE1.fq`<br/>
`sim_low_S3_PE2.fq`<br/>
`sim_low_S4_PE1.fq`<br/>
`sim_low_S4_PE2.fq`<br/><br/>
`Simulated_Medium_Complexity`<br/>
`...`<br/><br/>
`Simulated_High_Complexity`<br/>
`...`<br/><br/>
`RealData (Mouse fecal samples)`<br/>
`...`<br/><br/>
Since each set of paired-end sequencing reads (i.e. sim_low_S1_PE1.fq and sim_low_S1_PE2.fq) are run together to output a 
**single** sigma_out.gvector.txt file, you should be running the script **for each dataset** as follows:<br/><br/>
`sh SigmatoMosaic.sh sigma1_out.gvector.txt sigma2_out.gvector.txt sigma3_out.gvector.txt sigma4_out.gvector.txt`<br/>
**&ast;Since all output files are named sigma_out.gvector.txt, you'll need to rename them so that they are all unique, as shown 
above.**<br/><br/>
If you have sigma_out.gvector.txt files with many identified organisms (lines that start with "**&ast;**"), it may be wise to do 
the following:<br/><br/>
`nohup sh SigmatoMosaic.sh sigma1_out.gvector.txt sigma2_out.gvector.txt sigma3_out.gvector.txt sigma4_out.gvector.txt &`<br/><br/>
This will run the script in the background after you logout (nohup) and puts the process into a subshell (&), which allows you
to continue to work in the current terminal session, and will keep it running once you logout.<br/><br/>
Running SigmatoMosaic.sh will output a single file, **mosaic.txt**.<br/><br/>
Please see example files **sigma_out.gvector.txt** and **mosaic.txt** (examples of input and output). 

### Update to Roadmap (05/31/2018) 

SigmatoMosaic.sh now has the following features:<br/>
-Incorrect file format detection.<br/>
-Placeholder zeros when organism wasn't identified (per file), so relative abundances will be mapped to specific 
sigma_out.gvector.txt input files.

## Haskell Implementation

### Setting up the Reference Genome Directory

A prerequisite to getting useful output from this haskell script is to setup your reference genome directory correctly.<br/>
First, your reference genome directory should have the following structure:<br/><br/>
`[database directory] - [genome directory] - [fasta file]`<br/><br/>
To create this required reference genome directory, use the shell script **GCFrefgenomedirectory.sh**.  This shell script will 
correctly set-up your
reference genome directory, assuming you have downloaded GCF ([RefSeq assembly](https://www.ncbi.nlm.nih.gov/assembly/model/)) 
sequences.<br/><br/>
This shell script will change your initial reference genome directory setup of `[database directory] - [fasta file]` to the required
reference genome directory setup: `[database directory] - [genome directory] - [fasta file]`.<br/><br/>
Provide the path to the directory that contains the initial `[database directory]` as a command line argument as shown in the following 
example:<br/><br/>
`sh GCFrefgenomedirectory.sh /usr/home/ncbi/ncbi-genomes-2018-02-17`<br/><br/>

### Usage

This script is very easy to use, it takes **sigma_out.gvector.txt** as command line arguments.  Keep in mind, the Strains community
challenge has four datasets:<br/><br/>
`Simulated_Low_Complexity`<br/>
`Simulated_Medium_Complexity`<br/>
`Simulated_High_Complexity`<br/>
`RealData (Mouse fecal samples)`<br/><br/>
Each of these datasets contains four sets of paired-end sequencing reads, so in reality:<br/><br/>
`Simulated_Low_Complexity`<br/>
`sim_low_S1_PE1.fq`<br/>
`sim_low_S1_PE2.fq`<br/>
`sim_low_S2_PE1.fq`<br/>
`sim_low_S2_PE2.fq`<br/>
`sim_low_S3_PE1.fq`<br/>
`sim_low_S3_PE2.fq`<br/>
`sim_low_S4_PE1.fq`<br/>
`sim_low_S4_PE2.fq`<br/><br/>
`Simulated_Medium_Complexity`<br/>
`...`<br/><br/>
`Simulated_High_Complexity`<br/>
`...`<br/><br/>
`RealData (Mouse fecal samples)`<br/>
`...`<br/><br/>
Since each set of paired-end sequencing reads (i.e. sim_low_S1_PE1.fq and sim_low_S1_PE2.fq) are run together to output a 
**single** sigma_out.gvector.txt file, you should be running the script **for each dataset** as follows:<br/><br/>
`runghc SigmatoMosaic.hs sigma1_out.gvector.txt sigma2_out.gvector.txt sigma3_out.gvector.txt sigma4_out.gvector.txt`<br/>
**&ast;Since all output files are named sigma_out.gvector.txt, you'll need to rename them so that they are all unique, as shown 
above.**<br/><br/>
If you have sigma_out.gvector.txt files with many identified organisms (lines that start with "**&ast;**"), it may be wise to do 
the following:<br/><br/>
`nohup runghc SigmatoMosaic.hs sigma1_out.gvector.txt sigma2_out.gvector.txt sigma3_out.gvector.txt sigma4_out.gvector.txt &`<br/><br/>
This will run the script in the background after you logout (nohup) and puts the process into a subshell (&), which allows you
to continue to work in the current terminal session, and will keep it running once you logout.<br/><br/>
Running SigmatoMosaic.hs will output a single file, **mosaic.txt**.<br/><br/>
Please see example files **sigma_out.gvector.txt** and **mosaic.txt** (examples of input and output).<br/><br/>
For maximum performance, please compile the source code.

## Credits

Shell implementation and documentation added April 2018.<br/><br/>
Haskell implementation and documentation added August 2018.<br/><br/>
Author : [Matthew Mosior](https://github.com/Matthew-Mosior)
