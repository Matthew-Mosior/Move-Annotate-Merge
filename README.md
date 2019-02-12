# Move-Annotate-Merge: Tab-separated values file (.tsv) manipulation for manual review generated from sequencing data analysis


## Introduction

Preparing sequencing data for manual review can be tedious, time-consuming and a user error-prone process.  This script, implemented in [Haskell](https://www.haskell.org/), transforms user-defined .tsv files containing variant annotation output into a single merged, annotated file easily searched and ready for downstream filtration.

## Prerequisites

**MoveAnnotateMerge.hs** assumes you have a the [GHC](https://www.haskell.org/ghc/) compiler and libraries installed that it imports.  The easiest way to do this is to download the [Haskell Platform](https://www.haskell.org/platform/).<br/><br/>
**Required libraries**
 - Data.List
 - Data.List.Split 
 - System.Process
 - System.Environment
 - System.IO
 - Text.PrettyPrint.Boxes
 - Text.Regex

## Setting up the .tsv input file

A prerequisite for getting useful output from this Haskell script is to setup a input .tsv file that it expects.<br/>
Your input .tsv file should have the following structure:<br/><br/>
`[/Path/To/Tsv/File/example_variants.annotated.tsv]\t[Corresponding_sample_identifier]\t[/Path/To/Final/Directory]`<br/><br/>
There should be as many lines in this file as there are input .tsv files.

## Usage

**MoveAnnotateMerge.hs** is easy to use.<br/><br/> 
You can call it using the **runghc** command provided by the GHC compiler as such:<br/>
`runghc MoveAnnotateMerge.hs inputfile.tsv`<br/><br/>
For maximum performance, please compile and run the source code as follows:<br/><br/>
`ghc -O2 -o MAM MoveAnnotateMerge.hs`<br/><br/>
`./MAM inputfile.tsv`<br/><br/>
A docker-based solution (Dockerfile) is availible in the corresponding [repository](https://github.com/Matthew-Mosior/Move-Annotate-Merge---Docker).

## Credits

Documentation was added February 2019.<br/>
Author : [Matthew Mosior](https://github.com/Matthew-Mosior)
