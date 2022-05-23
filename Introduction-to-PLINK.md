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
wget 'http://github..../chr22.1000g.ped'
wget 'http://github..../chr22.1000g.map'
```
- Let's have a look at the variant file (`MAP`)
```bash
head chr22.1000g.map
```
MAP file stores the variant information and is usually accompanied with a (`PED`) pedigree + genotype file.
A text file with no header line, and one line per variant with the following 3-4 fields:
> Chromosome code (either an integer, or 'X'/'Y'/'XY'/'MT'; '0' indicates unknown) or name
> Variant identifier
> Position in morgans or centimorgans (safe to use dummy value of '0')
> Base-pair coordinate (1-based; limited to 231-2)

  - How many SNPs are there?
```bash
wc -l chr22.1000g.map
```
```bash
less -S chr22.1000g.ped
```
# xxx.bim stores the SNP information
less -S xxx.bim   #type "q" to quit

# xxx.fam stores the pedigree information for each sample
less -S xxx.fam
```
