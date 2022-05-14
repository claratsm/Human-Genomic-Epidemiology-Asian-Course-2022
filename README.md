# Human Genomic Epidemiology Asian Course 2022

## Genotyping data for GWAS

1. PLINK binary data (Illumina ASA array)
2. 1000Genomes data (for PCA plot)
- Converted from vcf files from 1000 Genomes 

## Simulation
1. ~1000 samples simulated from haplotypes of 1000 Geomes CHB and CHS samples using [HAPGEN2](https://mathgen.stats.ox.ac.uk/genetics_software/hapgen/hapgen2.html)
2. 


## Software
- [PLINK](https://www.cog-genomics.org/plink2/) 1.9 beta

## Simulated samples with varying QC problems
1. Missingness
2. Sex mismatch (id2_300,id2_301,id2_500,id2_501)
3. Heterozygosity (CHSHet002, CHSHet01)
4. Non-East asian ancestry / admixture (BEB-BEB_1, CHS-BEB_1, CHS-CEU_1, CHS-ITU_1)
5. CNV (CHSTri21, CHSDel)
6. Relatedness (CHSQUAD)

## Testing commands
1. Missingness
```bash
~/Programs/plink --bfile chrAll.ASA --missing --out QC/chrAll.ASA

sort --key 6 -gr  QC/chrAll.ASA.imiss | head
    id1_382     id2_382          N    92781   481283   0.1928
    id1_944     id2_944          N    71370   481283   0.1483
    id1_671     id2_671          N    61587   482088   0.1278
    id1_563     id2_563          N    48433   481283   0.1006
    id1_875     id2_875          N    36187   482088  0.07506
    id1_220     id2_220          N    27181   481283  0.05648
    id1_500     id2_500          N     5957   482088  0.01236
    id1_300     id2_300          N     5836   482088  0.01211
    id1_826     id2_826          N     2782   481283  0.00578
  CHSHet002   CHSHet002          N     1861   482088  0.00386

```
