# Sample-based and Variant-based Quality Control (QC)

## Objectives
After completing this practical, you will learn the data quality assessment and control steps that are typically carried out during genome wide association studies (GWAS).


## Dataset
- Genotyping data simulated from 1000 Genomes East Asian population
- SNP extracted from Illumina Asian Screening array

### Variant pruning
To avoid bias in xxxx, we first perform LD pruning to remove SNPs with moderate to strong LD.
**--indep-pairwise** takes the three parameters. The first parameter is the window size (in kb). The second parameter is the sliding window Its third parameter is a pairwise r2 threshold. at each step, pairs of variants in the current window with squared correlation greater than the threshold are noted, and variants are greedily pruned from the window until no such pairs remain. Since it does not need to keep the entire <window size> x <window size> correlation matrix in memory, it is usually capable of handling 6-digit window sizes well outside --indep's reach.)
<!--- SNP and sample QC/ Array QC
-->
