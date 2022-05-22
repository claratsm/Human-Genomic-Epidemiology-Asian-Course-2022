# Sample-based and Variant-based Quality Control (QC)

## Objectives
In this practical, you will learn the stepd for data quality assessment and control that are typically carried out in genome wide association studies (GWAS).

## Why do we need the QC?
Study design, sample quality, and errors in genotype calling can introduce systematic biases into GWAS, leading to spurious associations. A thorough QC can help us identify samples and markers that should be removed prior to association analysis in order to minimize false-positive and false-negative associations.

Here we assume that the study design has been conducted appropriately and variants have been called from probe intensity data (e.g. using Illumina GenCall/zCall). 

## The QC protocol: from Sample QC to Variant QC 
The QC protocol of a GWAS is usually split into two broad categories, `Sample QC` and `Variant QC`. Sample QC is usually done prior to Variant QC in order to maximise the number of markers remained in the study.

### Sample QC
It consists of at least five steps:
```{r}
het<-read.table("test.het")
head(het)
```
## Dataset
- Genotyping data simulated from 1000 Genomes East Asian population
- SNP extracted from Illumina Asian Screening array

### Variant pruning
To avoid bias in xxxx, we first perform LD pruning to remove SNPs with moderate to strong LD.
**--indep-pairwise** takes the three parameters. The first parameter is the window size (in kb). The second parameter is the sliding window Its third parameter is a pairwise r2 threshold. at each step, pairs of variants in the current window with squared correlation greater than the threshold are noted, and variants are greedily pruned from the window until no such pairs remain. Since it does not need to keep the entire <window size> x <window size> correlation matrix in memory, it is usually capable of handling 6-digit window sizes well outside --indep's reach.)
<!--- SNP and sample QC/ Array QC
-->
