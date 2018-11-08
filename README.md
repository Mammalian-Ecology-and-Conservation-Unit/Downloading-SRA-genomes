# Downloading-SRA-genomes
This repository contains the scripts for downloading fastq files from NCBI SRA

**1.)** First we need to ssh into port 2022
```
ssh -p 2022 name@cluster.edu
```
**2.)** We will be using Miniconda (specifically Bioconda) to get the parellel-fastq-dump

Download Miniconda here for 64-bit (bash installer): https://conda.io/miniconda.html

Then by right clicking the 64-bit (bash installer) link, I can get the path and use wget:

```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
```
- Then I can run this on port 2022: 
```
bash Miniconda3-latest-Linux-x86_64.sh
```
**3.)** Now can download Bioconda from the website http://bioconda.github.io/:  
```
conda config --add channels defaults
conda config --add channels bioconda
conda config --add channels conda-forge
```

- Double check it has parallel-fastq-dump: 
```
conda search parallel-fastq-dump 
```
**4.)** We need to create a new environment for the project and load parallel-fastq-dump: 
```
conda create -n AsiaWolfGenomics parallel-fastq-dump
```
### Using the screen platform to download
Using screen will prevent breaks in the download, such as being logged out of the 2022 port. 

We access screen by doing: 

```
screen
```

**5.)** Then we need to open up our project within screen: 

```
conda activate AsiaWolfGenomics

```

**5.) To download the fastq file, I did:** 

```
parallel-fastq-dump -I  --gzip --readids  --skip-technical -t 4 --aligned --origfmt --split-files -s SRR8049192
```

**TIPS WITH SCREEN** 

- This program makes a temporary directory, which I can ls in by:c 
```
ls -alh /tmp/pfd_tpmon9zh/*
```
- I can watch the files grow by: 
```
watch -- ls -alh /tmp/pfd_tpmon9zh/*
```
- To get out of screen and have it run in the background, I can do: 

```
Control A and D
```

- To get back into screen, I can do. 
```
screen -r 
```
