# Introduction to PLINK

## Objectives
In this practical, you will learn how to use PLINK to manage genotyping data.

## Step 1: Understand the input data formats in PLINK
- First, create a working directory named `practical1` and change to the directory
```bash
mkdir practical1
cd practical1
```
- Download the genotype data in PLINK file format (`PED / MAP`) into the directory
```bash
wget 'http://github..../chr22.1000g.ped'
wget 'http://github..../chr22.1000g.map'
```
- Let's have a look at the files
```bash
```
# xxx.bim stores the SNP information
less -S xxx.bim   #type "q" to quit

# xxx.fam stores the pedigree information for each sample
less -S xxx.fam
```
