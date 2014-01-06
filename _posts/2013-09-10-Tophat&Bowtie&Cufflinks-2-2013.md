---
layout: post
title: Map the Short Reads to Reference Genome Using TopHat, Bowtie, Samtools and Cufflinks (Ubuntu) 
categories: [ubuntu, NGS, bioinformatics]
tags: [Tophat, Bowtie, Samtools, Cufflinks, workflow]
---

### The Workflow of Using Tophat, Bowtie, Samtools And Cufflinks:

- Step 1: Download the reference genome and **Tophat**, **Bowtie**, **Samtools** and **Cufflinks**.
- Step 2: Configure the working environment for **Tophat**, **Bowtie**, **Samtools**  and **Cufflinks**.
- Step 3: Build index for reference genome with **Bowtie**.
- Step 3: Align paired-end RNA-seq reads to reference genome via **Tophat**.
- Step 4: Use **Cufflinks** to calculate transcript abundances (**FPKM**) in RNA-seq samples
- Step 5: Use **R** to calculate the correlation of **FPKM** between the both replications.
- Step 6: Merge the replications and run **Tophat** and **Cufflinks** again.

#### Download the zebrafish reference genome
The next two weeks, all my works have been showed in the workflow above. In term of the paper ([Systematic identification of long noncoding RNAs expressed during zebrafish embryogenesis](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3290793/)) I was working, firstly I should figure out where the zebrafish reference genome the paper used is from. And it told me that:

![](http://i.imgur.com/0j2PDa5.png)

From this paragraph in the paper, it is supereasy to search out zebrafish reference genome from
following procedure:

```
The keyword typing into Google search bar: zebrafish reference genome -> Ensemble ->
Download DNA sequence(FASTA) -> ftp://ftp.ensembl.org/pub/release-71/fasta/danio_rerio/dna/
```
Note: The alternative link: ( ftp://ftp.sanger.ac.uk/pub/zfish/assembly/Zv9/ )
