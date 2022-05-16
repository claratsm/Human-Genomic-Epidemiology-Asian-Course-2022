# Human Genomic Epidemiology Asian Course 2022

## Genotyping data for GWAS

1. PLINK binary data (Illumina ASA array)
2. 1000Genomes data (for PCA plot) converted from vcf files from 1000 Genomes 

## Simulation
1. ~1000 samples simulated from haplotypes of 1000 Geomes CHB and CHS samples using [HAPGEN2](https://mathgen.stats.ox.ac.uk/genetics_software/hapgen/hapgen2.html)
2. Binary (497 cases + 501 controls, 6 missing) phenotype simulated using [GCTA](https://yanglab.westlake.edu.cn/software/gcta/#GWASSimulation) with hsq=0.8 and K=0.5

## Software
- [PLINK](https://www.cog-genomics.org/plink2/) 1.9 beta

## Download
- [Raw genotyping data](https://drive.google.com/file/d/1DBppyTtW5X924nHe-2SkDp359qcM_QKX/view?usp=sharing)
- [Data passed QC](https://drive.google.com/file/d/1E7eAqvOrA_uJJ9d-lrSlRNUG_-Ybgu1d/view?usp=sharing)

## Simulated samples with varying QC problems
1. Missingness
2. Sex mismatch (id2_300,id2_301,id2_500,id2_501)
3. Heterozygosity (CHSHet002, CHSHet01)
4. Non-East asian ancestry / admixture (BEB-BEB_1, CHS-BEB_1, CHS-CEU_1, CHS-ITU_1)
5. Relatedness (CHSQUAD)
6. CNV (CHSTri21, CHSDel)

## Testing commands
1. Missingness
```bash
~/Programs/plink --bfile chrAll.ASA --missing --out QC/chrAll.ASA

sort --key 6 -gr  QC/chrAll.ASA.imiss | head
#        FID         IID MISS_PHENO   N_MISS   N_GENO   F_MISS
#    id1_382     id2_382          N    92781   481283   0.1928
#    id1_944     id2_944          N    71370   481283   0.1483
#    id1_671     id2_671          N    61587   482088   0.1278
#    id1_563     id2_563          N    48433   481283   0.1006
#    id1_875     id2_875          N    36187   482088  0.07506
#    id1_220     id2_220          N    27181   481283  0.05648
#    id1_500     id2_500          N     5957   482088  0.01236
#    id1_300     id2_300          N     5836   482088  0.01211
#    id1_826     id2_826          N     2782   481283  0.00578
#  CHSHet002   CHSHet002          N     1861   482088  0.00386
  
sort --key 5 -gr  QC/chrAll.ASA.lmiss | head
# CHR                        SNP   N_MISS   N_GENO   F_MISS
#  19                19:41642811      484     1012   0.4783
#  16                16:73793954      451     1012   0.4457
#  10                kgp21558165      446     1012   0.4407
#  12                12:78152680      416     1012   0.4111
#   4                 rs77925406      393     1012   0.3883
#  17                  rs2367537      387     1012   0.3824
#   2                rs144130077      383     1012   0.3785
#  11                 rs76693355      344     1012   0.3399
#  11                  rs1580873      336     1012    0.332
#  15                 kgp8838271      333     1012   0.3291
```
2. Sex mismatch
```bash
~/Programs/plink --bfile chrAll.ASA --check-sex ycount 0.2 0.8 40 --out QC/chrAll.ASA

egrep PROBLEM QC/chrAll.ASA.sexcheck
#        FID         IID       PEDSEX       SNPSEX       STATUS            F   YCOUNT
#  CHSHet002   CHSHet002            1            0      PROBLEM       0.6763      804
#    id1_300     id2_300            1            2      PROBLEM      0.03288        2
#    id1_301     id2_301            2            1      PROBLEM            1      802
#    id1_500     id2_500            1            2      PROBLEM     0.008734        2
#    id1_501     id2_501            2            1      PROBLEM            1      805
```
3. Heterozygosity
```bash
~/Programs/plink --bfile chrAll.ASA --autosome --maf 0.05 --hwe 1e-5 --geno 0.02 --indep-pairwise 200 50 0.1 --out QC/chrAll.ASA
~/Programs/plink --bfile chrAll.ASA --extract QC/chrAll.ASA.prune.in --het --out QC/chrAll.ASA.pruned

sort --key 6 -gr  QC/chrAll.ASA.pruned.het | head
#        FID         IID       O(HOM)       E(HOM)        N(NM)            F
#     CHSDel      CHSDel        47030    4.592e+04        67195      0.05212
#  BEB-BEB_1   BEB-BEB_1        46796    4.592e+04        67195      0.04112
#    id1_430     id2_430        46315    4.591e+04        67183      0.01886
#    id1_510     id2_510        46268    4.591e+04        67179       0.0168
 
sort --key 6 -gr  QC/chrAll.ASA.pruned.het | tail
#        FID         IID       O(HOM)       E(HOM)        N(NM)            F
#   id1_583     id2_583        45486    4.591e+04        67183     -0.02004
#   CHSHet01    CHSHet01        44968    4.592e+04        67195     -0.04481
#  CHS-ITU_1   CHS-ITU_1        44825    4.592e+04        67195     -0.05153
#  CHS-BEB_1   CHS-BEB_1        44817    4.592e+04        67195     -0.05191
#  CHS-CEU_1   CHS-CEU_1        44550    4.592e+04        67195     -0.06446
#  CHSHet002   CHSHet002        41372    4.592e+04        67195      -0.2138
```
4. Relatedness
```bash
~/Programs/plink --bfile chrAll.ASA --extract QC/chrAll.ASA.prune.in --genome --out QC/chrAll.ASA.pruned

sort --key 12 -gr QC/chrAll.ASA.pruned.genome | head
#       FID1       IID1       FID2       IID2 RT    EZ      Z0      Z1      Z2  PI_HAT PHE       DST     PPC   RATIO
#    CHSQUAD         C1    CHSQUAD         C2 OT     0  0.2423  0.4298  0.3279  0.5428  -1  0.870124  1.0000 11.0616
#    CHSQUAD         C2    CHSQUAD         F1 OT     0  0.0000  0.9851  0.0149  0.5075  -1  0.843984  1.0000      NA
#    CHSQUAD         C1    CHSQUAD         F1 OT     0  0.0000  0.9875  0.0125  0.5062  -1  0.843597  1.0000      NA
#    CHSQUAD         C1    CHSQUAD         M1 OT     0  0.0000  0.9932  0.0068  0.5034  -1  0.842704  1.0000      NA
#    CHSQUAD         C2    CHSQUAD         M1 OT     0  0.0000  0.9946  0.0054  0.5027  -1  0.842481  1.0000      NA
#  BEB-BEB_1  BEB-BEB_1  CHS-BEB_1  CHS-BEB_1 UN    NA  0.0000  1.0000  0.0000  0.5000  -1  0.834296  1.0000      NA
#    id1_245    id2_245    id1_834    id2_834 UN    NA  0.9537  0.0341  0.0122  0.0293  -1  0.751325  0.9736  2.1466
![PCA plot with contaminated and non-Asian samples]()
 ```
5. Validation of ancestry
```bash
~/Programs/plink --bfile chrAll.ASA --update-name ASA.1000G.to-update-name.snp --make-bed --out chrAll.ASA.id-1000G
~/Programs/plink --bfile chrAll.ASA.id-1000G --bmerge chrAll.ASA.1000GP-All --geno 0.05 --make-bed --out merged.chrAll.ASA.1000G
~/Programs/plink --bfile merged.chrAll.ASA.1000G --maf 0.05 --hwe 1e-5 --geno 0.05 --indep-pairwise 200 50 0.1 --out merged.chrAll.ASA.1000G
~/Programs/plink --bfile merged.chrAll.ASA.1000G --extract merged.chrAll.ASA.1000G.prune.in --pca 3 --out merged.chrAll.ASA.1000G.pruned
```
6. Association
```bash
~/Programs/plink --bfile chrAll.ASA --remove QCneg.to-remove.indiv --maf 0.01 --geno 0.05 --hwe 1e-5 --assoc --adjust --out assoc/chrAll.ASA.QCpos.binary
```
