---
layout: post
title: Map the Short Reads to Reference Genome Using TopHat, Bowtie, Samtools and Cufflinks (Ubuntu) 
categories: [ubuntu, NGS, bioinformatics]
tags: [Tophat, Bowtie, Samtools, Cufflinks, workflow]
---

## The Workflow of Using Tophat, Bowtie, Samtools And Cufflinks:

- Step 1: Download the reference genome and **Tophat**, **Bowtie**, **Samtools** and **Cufflinks**.
- Step 2: Configure the working environment for **Tophat**, **Bowtie**, **Samtools**  and **Cufflinks**.
- Step 3: Build index for reference genome with **Bowtie**.
- Step 3: Align paired-end RNA-seq reads to reference genome via **Tophat**.
- Step 4: Use **Cufflinks** to calculate transcript abundances (**FPKM**) in RNA-seq samples
- Step 5: Use **R** to calculate the correlation of **FPKM** between the both replications.
- Step 6: Merge the replications and run **Tophat** and **Cufflinks** again.


### Download the zebrafish reference genome

The next two weeks, all my works have been showed in the workflow above. In term of the paper ([Systematic identification of long noncoding RNAs expressed during zebrafish embryogenesis](http://www.ncbi.nlm.nih.gov/pmc/articles/PMC3290793/)) I was working, firstly I should figure out where the zebrafish reference genome the paper used is from. And it told me that:

![](http://i.imgur.com/0j2PDa5.png)

From this paragraph in the paper, it is supereasy to search out zebrafish reference genome from
following procedure:

```
The keyword typing into Google search bar: zebrafish reference genome -> Ensemble ->
Download DNA sequence(FASTA) -> ftp://ftp.ensembl.org/pub/release-71/fasta/danio_rerio/dna/
```
Note: The alternative link: ([ftp://ftp.sanger.ac.uk/pub/zfish/assembly/Zv9/](ftp://ftp.sanger.ac.uk/pub/zfish/assembly/Zv9/))

### Configure the working environment for **Tophat**, **Bowtie**, **Samtools**  and **Cufflinks**  

You could reference the last journal of [Configuration of TopHat, Bowtie, Samtools and Cufflinks on Ubuntu](http://lushen.github.com/en/2013/09/Tophat%26Bowtie%26Cufflinks-1-2013/)  

### Build index for reference genome with **Bowite**  

#### Build the index with Bowtie   
You should unzip the zebrafish reference genome .gz file and use the command line is  
  
```   
$ gunzip -c Danio_rerio.Zv9.71.dna.toplevel.fa.gz > Danio_rerio   
```  
  
You could see an unzipped new FASTQ file and use the command of Bowtie to build the genome
index   

```   
$ /home/shenlu/temp/bowtie2-2.0.5/bowtie2-build /work/fish/shenlu/zebrafish_genome/Danio_rerio zebrafish_index zebrafish_index   
```   
#### Aligns paired-end RNA-seq reads to reference genome via Tophat   
Run the command line of tophat to generate FPKM:   

```    
$ tophat -p 4(or 3) /work/fish/shenlu/bowtie/zebrafish_index --library-type fr-unstranded /work/fish/shenlu/2-4_cell_1/SRR372787_1_trimmer.fastq /work/fish/shenlu/2-4_cell_1/SRR372787_2.fastq -G /work/fish/shenlu/zebrafish_genome/Danio_rerio_annotation -o zebrafish     
``` 
![]()

> Note: `/work/fish/shenlu/bowtie/zebrafish_index` is dumpped by the command: `bowtie2-build` (there
are six files, but we just use the name before the ".")   


### Use Cufflinks to calculate transcript abundances (FPKM) in RNA-seq samples

Using the outcomes of **Tophat**, I continued running **Cufflinks** to calculate out the **FPKM** of the gene and isoforms  

![]()

```   
$ /home/shenlu/temp/cufflinks-2.1.1.Linux_x86_64/cufflinks -G /work/fish/shenlu/zebrafish_genome/Danio_rerio_annotation /work/fish/shenlu/2-4_cell_1/tophat_out/accepted_hits.bam   
```   

> Note: `Danio_rerio_annotation` is the `.gtf` format file after unzipped out.

After runing this command, I generated two files with ```.fpkm_tracking``` at the end. As same as runing Tophat to estimate **FPKM** of ```SRR372787_1_trimmer.fastq``` and ```SRR372787_2.fastq```, I run **Tophat** to estimate **FPKM** of another replication: *2-4_cell_2* (```SRR372788_1.fastq``` and ```SRR372788_1.fastq```)

**Tophat** should set up various arguments, if you hesitated what arguments you should choose, we could find some clues about these arguments for the paper. For example, from the first paragraph in methods below, we could see the RNA-seq data is from ```strand-specific``` libraries.

![]()

And Tophat has provided three library types with us to choose a proper arguments. In terms of the paper, we should select ```fr-unstranded``` as the argument.   

![]()

### Using R to calculate the correlation between the replications   

Before runing the **Tophat**, first we should confirm if there is any strong correlation among two or more replications. In other words, whether the replications among RNA-seq samples are reliable to use.

Use the ```awk``` to tackle the both ```*fpkm_tracking``` files and extract the column with **FPKM** information

```   
$ awk < isoforms_2-4_cell_2.fpkm_tracking -F'[\t]' '{print $10 > "2-4_cell_isoform_example2.txt"}'   
```  
  
