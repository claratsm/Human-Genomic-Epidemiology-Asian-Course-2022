# Introduction to PLINK

## Objectives
In this practical, you will learn how to use PLINK to manage genotyping data.

## Step 1: Understand the input data formats in PLINK
First, create a working directory named `practical1` and change to the directory
```bash
mkdir practical1
cd practical1
```
Download the genotype data in regular PLINK text file format (`PED / MAP`) into the directory
```bash
wget 'http://github..../practical1.ped'
wget 'http://github..../practical1.map'
```

#### PLINK text variant file (MAP)
Let's have a look at the variant `MAP` file
```bash
head practical1.map
```
MAP file stores the variant information and must contain as many markers as are in the PED file.<br>
It contains no header line and each line describes a single marker with 4 columns:

> 1. Chromosome code (1-22, 23/X, 24/Y, 25/XY, 26/MT; '0' indicates unknown)<br>
> 2. Variant identifier<br>
> 3. Position in morgans or centimorgans (safe to use dummy value of '0')<br>
> 4. Base-pair coordinate (1-based)

:green_book: **Q:** How many SNPs are there?
```bash
wc -l practical1.map
```

#### PLINK text pedigree and genotype file (PED)
Let's have a look at the `PED` file
```bash
less -S chr22.1000g.ped   # type 'q' to quit
```
The PED file is a white-space (space or tab) delimited file<br>
It has no header line, and one line per sample with 2V+6 fields where V is the number of variants. Tthe first six columns are mandatory and are the same as  in a `FAM` file. 

> 1. Family ID ('FID')<br>
> 2. Individual ID('IID')<br>
> 3. Within-family ID of father ('0' if father isn't in dataset)<br>
> 4. Within-family ID of mother ('0' if mother isn't in dataset)<br>
> 5. Sex (1=male; 2=female; 0=unknown)<br>
> 6. Phenotype (1=control, 2=case, -9 / 0=missing for case-control; numeric for quantitative trait)<br>

The 7th and 8th fields are the alleles for the first variant in the MAP file. The 9th and 10th are allele calls for the second variant and so on.

:green_book: **Q:** How many samples are there?
```bash
wc practical1.ped
```

## Step 2: Data conversion in PLINK
Read the `practical1` PLINK text fileset and convert to the PLINK binary fileset (`BED / BIM / FAM`)
<pre><code>plink <b>--file practical1</b> --make-bed --out practical1.1

## Equivalent to 
# plink <b>--file practical1</b> --out practical1.1
# plink <b>--ped practical1.ped --map practical1.map</b> --make-bed --out practical1.1`
</code></pre>
The command `--file **practical1**` reads in **practical1**.ped and **practical1**.map and outputs the PLINK binary files with prefix of **practical1.1**

> practical1.1.bed (binary file; not human readable)<br>
> practical1.1.bim <br>
> practical1.1.fam <br>

--> Paste and explain the log here <---

The FAM file stores the pedigree information of the PED file (i.e. the first 6 columns).<br>
The BIM file is the extended MAP file with first four columns same as the MAP file. The 5th and 6th columns record the A1 and A2 alleles:<br>

> 5. Allele 1 (**A1**; corresponding to the **minor allele** by default; 0 is monomorphic)<br>
> 6. Allele 2 (**A2**; corresponding to the **major allele** by default)<br>

📗 Q: What is the minor allele of the second SNP?
```bash
head practical1.1.bim
```

## Step 3: Data management in PLINK


```bash
plink --bfile practical1.1 --chr 22 --from-bp xxx --to-bp xxx --make-bed --out practical1.1.22p11
```

```bash
plink --bfile practical1.1.22p11 --freq --out practical1.1.22p11
```
