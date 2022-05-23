# Introduction to PLINK

## Objectives
In this practical, you will learn how to use PLINK to manage genotyping data.

## Step 1: Understand the input data formats in PLINK
- First, create a working directory named `practical1` and change to the directory
```bash
mkdir practical1
cd practical1
```
- Download the genotype data in regular PLINK text file format (`PED / MAP`) into the directory
```bash
wget 'http://github..../practical1.ped'
wget 'http://github..../practical1.map'
```

#### PLINK text variant file (MAP)
- Let's have a look at the variant `MAP` file
```bash
head practical1.map
```
MAP file stores the variant information and must contain as many markers as are in the PED file.<br>
It contains no header line and each line describes a single marker and contain 4 columns:

> Chromosome code (1-22, 23/X, 24/Y, 25/XY, 26/MT; '0' indicates unknown)<br>
> Variant identifier<br>
> Position in morgans or centimorgans (safe to use dummy value of '0')<br>
> Base-pair coordinate (1-based)

**Q:** How many SNPs are there?
```bash
wc -l practical1.map
```

#### PLINK text pedigree and genotype file (PED)
- Let's have a look at the `PED` file
```bash
less -S chr22.1000g.ped
```
The PED file is a white-space (space or tab) delimited file: the first six columns are mandatory:
> Family ID<br>
> Individual ID<br>
> Paternal ID<br>
> Maternal ID<br>
> Sex (1=male; 2=female; other=unknown)<br>
> Phenotype (1=male; 2=female; other=unknown)<br>

**Q:** How many samples are there?
```bash
wc practical1.ped
```
# xxx.bim stores the SNP information
less -S xxx.bim   #type "q" to quit

# xxx.fam stores the pedigree information for each sample
less -S xxx.fam
```
