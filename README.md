# PARE
PARE: a computational pipeline to Predict Active Regulatory Element

Description
===========
    PARE is an implementation of novel approach to detect Peak-Valley-Peak (PVP) pattern defined based on H3K4me1 and H3K4me3 signal at enhancers and promoters, respectively.
    Genomic regions enriched for H3K4me1 PVP pattern are predicted as active enhancers.
    Genomic regions enriched for H3K4me3 PVP pattern are predicted as active promoters.

Version
=======
    0.02

Programs and datasets
=====================
    Generally, the user would be interested in following two scripts:
    1. pare: it is the main script to detect enhancers or promoters based on input BAM files (H3K4me1 - enhancers; H3K4me3 - promoters).
    2. bed2direction: this script is used to detect directionality of stable transcription at promoter regions, provided as input in BED format.

Installation
============

    1. To install PARESuite, download PARESuite.tar.gz and unpack it. A directory, PARESuite will be created

        tar -zxvf PARESuite.tar.gz

    2. Now compile and create executable blockbuster

        make or make all

    3. Export environment variable 'PAREPATH' containing path to PARESuite installation directory

        export PAREPATH=<path to PARESuite installation directory>

    4. Add 'PAREPATH' to your 'PATH' environment variable

        export PATH=$PATH:$PAREPATH/bin

    5. Add 'PAREPATH' to your 'PERL5LIB' environment variable

        export PERL5LIB=$PERL5LIB:$PAREPATH/share/perl/

    To permanently add or update the environment variable(s), add the last three export commands in your ~/.bashrc file

Dependency
==========

    We assume that the following programming platforms are installed and working: perl, R, and gcc. Besides, following packages should be installed.

    1. Install the needed perl modules

        sudo cpan Tie::IxHash Statistics::Basic

    2. R modules are installed by entering R (type R on the cmdline) and then enter the following three commands (follow the instructions on the screen):

        install.packages(c("ggplot2", "gridExtra", "optparse", "randomForest", "e1071"))
        source("http://bioconductor.org/biocLite.R")
        biocLite(c("DESeq"))

    3. download samtools from http://sourceforge.net/projects/samtools/files/samtools/1.2/samtools-1.2.tar.bz2/download, go to the download location and do

        tar xjf samtools-1.2.tar.bz2
        cd samtools-1.2
        make -j10 prefix=$HOME install

    4. download bedtools from https://github.com/arq5x/bedtools2/releases/download/v2.23.0/bedtools-2.23.0.tar.gz, go to the download location and do

        tar xzf BEDTools.v2.23
        cd bedtools-2.23.0/
        make -j 10
        cp bin/* $HOME/bin

    5. download featureCounts (subread) from http://sourceforge.net/projects/subread/files/subread-1.4.6-p4/, go to the download location and do

        tar xzf subread-1.4.6-p4-Linux-x86_64.tar.gz
        cd subread-1.4.6-p3-Linux-x86_64
        cp bin/featureCounts $HOME/bin

    6. download bedGraphToBigWig from http://hgdownload.soe.ucsc.edu/admin/exe/ for your operating system, go to the download location and do

        cp bedGraphToBigWig $HOME/bin
        chmod 755 $HOME/bin/bedGraphToBigWig

Usage
=====

    PARESuite is called with the following parameters

    pare -i <BAM file (rep1)> -j <BAM file (rep2)> [OPTIONS]

Example
=======

    An usage example of PARESuite is shown below. As input, the pipeline requires mapped reads in BAM format. Example dataset files are provided with the download

    pare -i data/test_data/h3k4me1_helas3_Rep1.bam -j data/test_data/h3k4me1_helas3_Rep2.bam -k data/test_data/optimal.h3k4me1_helas3_Rep0_Vs_control_helas3_Rep0.regionPeak.gz -o data/test_run_for_reference/ -m hg19 -p -v 3000 &> data/pare.log

Input
=====

    As input, the pipeline requires mapped reads in BAM format. The name of the input files should be formatted as

    Input file name (replicate 1): <unique id><Rep1>.bam (example: h3k4me1_Rep1.bam)
    Input file name (replicate 2): <unique id><Rep2>.bam (example: h3k4me1_Rep2.bam)

    The chromosome identifier in the input BAM files should start with chr, for example as chrY and not like Y.

Output
======

    The results from the PARESuite are compiled in two text files:
    a) RESULTS.TXT: main result file in BED format 

    For easy access, the html version of this files (RESULTS.HTML) is also available within the output directory

    b) RESULTS.UCSC: file to view the enhancer and promoter regions in UCSC browser

More info
=========

    for more and latest information, please refer to 

License
=======

    PARESuite: a computational pipeline to predict Active Regulatory Elements using histone marks
    Copyright (C) 2015  Sachin Pundhir (pundhir@binf.ku.dk)

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <http://www.gnu.org/licenses/>.

