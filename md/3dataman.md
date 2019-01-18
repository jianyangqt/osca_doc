
## Data Management {: .expand}

The DNA methylation (or gene expression) data are stored in a binary
format for storage efficiency. We store the data in
three separate files .oii (individual information, similar as a PLINK
.fam file), .opi (probe information) and .bod (a binary file to store
the DNA methylation or gene expression profiles).

To efficiently save the result of eQTL / vQTL analysis, OSCA also supports BESD format.

### BOD format

#### \# BOD format: an efficient format to store omics data

***myeed.oii***

```
F01 I01 0   0   NA
F02 I01 0   0   NA
F03 I02 0   0   NA
... 
```

Columns are family ID, individual ID, paternal ID, maternal ID and sex
(1=male; 2=female; 0=unknown). Missing data are represented by "<font color='red'>NA</font>".

***myeed.opi***

```
1   probe101    924243  Gene01  +
1   probe102    939564  Gene01  -
1   probe103    1130681 Gene01  -
... 
```

Columns are chromosome, probe ID (can be the ID of an exon or a
transcript for RNA-seq data), physical position, gene ID and gene
orientation.

***myeed.bod***

DNA methylation (or gene expression) data in binary format. <font color='red'>Please do
not try to open this file with a text editor</font>.

**Note:** The text below are for advanced users only. We use the first
12 bytes of the .bod file to store the descriptive information for the
data. The first 2 bytes are reserved for further extension of the
software. The type of data is indicated by the 3rd byte (0 for gene
expression data, 1 for DNA methylation data, and 2 for any other type of
data). The type of value is indicated by the 4th byte (0 for DNA
methylation beta value, 1 for DNA methylation m value and 2 for any
other type of value). The number of individuals and number of probes are
stored as integers (4 bytes each). For example, for a DNA methylation
data set (0x01) of m values (0x01) on 1,342 (0x53e) individuals and
228,694 (0x37d56) CpG sites, the first 12 bytes of the .bod file are:

```
0101 0000 3e05 0000 567d 0300
```

The bytes afterwards are for the DNA methylation or gene expression
data.

### Make a BOD file 
#### \# compile data in binary format from text format


```
 osca --efile myprofile.txt --methylation-beta --make-bod --out myprofile  
```

**\--efile** reads a DNA methylation (or gene expression) data file
in plain text format.

**\--methylation-beta** indicates methylation beta values in the
file.

**\--make-bod** saves DNA methylation (or gene expression) data in
binary format.

**\--out** saves data ( or results) in a file.

***myprofile.txt***
```
FID  IID cg00000658  cg26036652  cg00489772  ...
F01 I01 0.909   0.845   0.41    ...
F01 I02 0.832   0.732   0.503   ...
...
```
This is a file with a header line that contains family ID, individual ID
and names of probes. The column of family ID is optional. Please use the
flag "**\--no-fid**" for data without family ID.

```
osca --efile myprofile.txt  --methylation-beta --make-bod --no-fid --out myprofile 
```
**\--no-fid** indicates data without family ID.

```
osca --efile myprofile.txt  --methylation-m --make-bod --out myprofile 
```
 **\--methylation-m** indicates DNA methylation m values in the file.

If the profile is of gene expression value.

```
osca --efile myprofile.txt  --gene-expression --make-bod --out myprofile 
```
**\--gene-expression** indicates gene expression profiles in the
file.

For any other type of data:

```
osca --efile myprofile.txt --make-bod --out myprofile 
```

A binary file also can be made from a transposed file in text format.

```
osca --tefile mytprofile.txt --methylation-beta --make-bod --no-fid --out myprofile
```
***mytprofile.txt***

```
FID  F01 F01 ...
IID I01 I02 ...
cg00000658  0.909   0.832   ...
cg26036652  0.845   0.732   ...
cg00489772  0.41    0.503   ...
...
```

The row of family ID is optional. Please use the flag "**\--no-fid**" if
there is no family ID in your data.

```
osca --tefile mytprofile.txt --methylation-beta --make-bod --no-fid --out myprofile 
```
#### \# update probe annotation

Probe information are sometimes not available in the original DNA
methylation (or gene expression) data. These information can be updated
the command below.

```
osca --befile myprofile --update-opi annotated.opi 
```

**\--befile** reads a DNA methylation (or gene expression) data file
in binary format.

**\--update-opi** reads a fully annotated .opi file.

### Manage BOD file(s) 
#### \# make a subset

To extract a probe

```
osca --befile myprofile --probe cg00000658 --make-bod --out mysubprofile 
```

**\--probe** extracts a specified probe.

To exclude a probe

```
osca --befile myprofile --probe-rm cg00000658 --make-bod --out mysubprofile 
```

**\--probe-rm** excludes a specified probe.

To extract a subset of probes

```
osca --befile myprofile --extract-probe probe.list --make-bod --out mysubprofile 
```

**\--extract-probe** extracts a subset of probes.


***probe.list***

```
cg00000658
cg26036652
...                 
```

To exclude a subset of probes

```
osca --befile myprofile --exclude-probe probe.list --make-bod --out mysubprofile 
```

**\--exclude-probe** excludes a subset of probes.

To extract a subset of individuals

```
osca --befile myprofile --keep indi.list --make-bod --out mysubprofile 
```

**\--keep** extracts a subset of individuals.

***indi.list***

```
F01    I01
F01 I02
...                  
```

To exclude a subset of individuals

```
osca --befile myprofile --remove indi.list --make-bod --out mysubprofile 
```

**\--remove** excludes a subset of individuals.

To extract a subset of genes

```
osca --befile myprofile --genes gene.list --make-bod --out mysubprofile 
```

**\--genes** extracts a subset of genes.

***gene.list***

```
MAN1B1
EDEM2
...                    
```

To extract a gene

```
osca --befile myprofile --gene MAN1B1 --make-bod --out mysubprofile 
```

**\--gene** extracts a gene.


To extract a subset of probes based on the order

```
osca --befile myprofile --from-probe probe0 --to-probe probe1 --make-bod --out mysubprofile 
```

**\--from-probe** specifies the start probe.

**\--to-probe** specifies the end probe.

To extract a subset of probes in a genomic region centred at a specific
probe

```
osca --befile myprofile --probe cg00000658 --probe-wind 500 --make-bod --out mysubprofile 
```

**\--probe-wind** defines a window \<kb\> centred on a specified probe.

To extract a subset of probes on a chromosome

```
osca --befile myprofile --chr 1 --make-bod --out mysubprofile 
```

**\--chr** specifies a chromosome to select probes.

To extract a subset of probes based on physical positions

```
osca --befile myprofile --from-probe-kb 100 --to-probe-kb 200 --make-bod --out mysubprofile 
```

**\--from-probe-kb** specifies the start physical position of the probes.

**\--to-probe-kb** specifies the end physical position of the
probes.

#### \# merge BOD files

```
osca --befile-flist mybod.flist --make-bod --out myprofile 
```
**\--befile-flist** reads a file to get the full paths of the binary files.

***mybod.flist***

```
path1/my_bod1
path2/my_bod2
...                 
```
#### \# Quality control

To remvoe probes with low variance

```
osca --befile myprofile --sd-min 0.02 --make-bod --out newprofile 
```

**\--sd-min** removes the probes with the standard deviation smaller
than a specified threshold.

To remove probes with a missing rate threshold

```
osca --befile myprofile --missing-ratio-probe 0.01 --make-bod --out newprofile 
```

**\--missing-ratio-probe** specifies a missing proportion threshold
to remove probes.




#### \# Quality control of methyaltion data

To remove constitutively methylated/unmethylated probes

```
osca --befile myprofile --upper-beta 0.8 --lower-beta 0.2 --make-bod --out newprofile 
```
**\--upper-beta** removes the DNA methylation probes with the mean
beta value larger than a specified threshold.

**\--lower-beta** removes the DNA methylation probes with the mean
beta value smaller than a specified threshold.

To QC with detection p-values

```
osca --befile myprofile --detection-pval-file dpval.txt --dpval-mth 0  --dpval-thresh 0.05 --make-bod --out newprofile 
```
**\--detection-pval-file** reads a file that contains DNA
methylation detection p-values.

**\--dpval-mth** specifies a method to do quality control with the
detection p-values, 0 for removing the probes with one or more
detection p-values violating a threshold (default as 0.05), and 1
for dropping the samples violating a proportion threshold (default
as 1%) and simultaneously dropping the probes violating a proportion
threshold (default as 1%).

**\--dpval-thresh** specifies a threshold of detection p-value.

```
osca --befile myprofile --detection-pval-file dpval.txt --dpval-mth 1  --ratio-probe 0.01 --ratio-sample 0.01 --dpval-thresh 0.05 --make-bod --out newprofile 
```

**\--ratio-probe** specifies a proportion threshold to remove
probes.

**\--ratio-sample**specifies a proportion threshold to remove
individuals.

the file "dpval.txt" is in the same format with a transposed profile
file. Option "**\--no-fid**" is also valid here.

#### \# adjust the covariates for each probe
```
osca --befile myprofile --covar my.cov --qcovar my.qcov --adj-probe --make-bod --out newprofile 
```
**\--adj-probe** adjusts the covariates for each probe.

#### \# standardize each probe
```
osca --befile myprofile --std-probe --make-bod --out newprofile 
```
**\--std-probe** standardizes each probe.

```
osca --befile myprofile --rint-probe --make-bod --out newprofile 
```
**\--rint-probe** normalizes each probe by Rank-based Inverse Normal Transformation.


#### \# other options
Transform methylation beta value to methylation m value and vice versa

```
osca --befile myprofile --m2beta --make-bod --out newprofile 
```
**\--m2beta** calculates the methylation beta value from the
methylation m value.

```
osca --befile myprofile --beta2m --make-bod --out newprofile 
```

**\--beta2m** calculates the methylation m value from the
methylation beta value.



### Query a BOD file 

#### \# make a text format file

```
osca --befile myprofile --make-efile --out myprofile.txt 
```

**\--make-efile** saves the DNA methylation (or gene expression)
data in text format.

```
osca --befile myprofile --make-tefile --out mytprofile.txt 
```
**\--make-tefile** saves the DNA methylation (or gene expression)
data in transposed text format.

**NOTE**: The options in [Manage BOD file(s)](#ManageBODfile(s)) can also be applied.

#### \# Calculate the variance and the mean of probes

```
osca --befile myprofile --get-variance --get-mean --out newprofile 
```

**\--get-variance** calculates the variance of each probe.

**\--get-mean** calculates the mean of each probe.

***newprofile.var.txt***

```
cg00000957 0.000812127
cg00001349  0.00560701
...                 
```

***newprofile.mean.txt***

```
cg00000957 0.901574
cg00001349  0.860279
...                 
```

### BESD format

Results from eQTL analysis will be saved in SMR BESD format [see SMR website for more information](http://cnsgenomics.com/software/smr/#BESDformat).To save the eQTL results more efficiently, we extended the BESD format.

**Note:** The texts below are for advanced users only. 


**BESD dense format 1**: the first 64 Bytes are reserved for the descriptive information which starts with 0x00000005. The data onwards are a vector of effect sizes followed by a vector of SEs of each probe across all the snps. The effect sizes and SEs are saved in single float-precision (4B).

**BESD dense format 2** (only supported in OSCA): the first 64 Bytes are reserved for the descriptive information which starts with 0x00000004. The data onwards are the effect sizes followed by the SEs of each SNP across all the probes. The effect sizes and SEs are saved in single float-precision (4B).

**BESD sparse format**:  the first 64 Bytes are reserved for the descriptive information which starts with 0x00000001. The effect sizes and the SEs as saved in [the CSC format](https://en.wikipedia.org/wiki/Sparse_matrix#Compressed_sparse_column_(CSC_or_CCS))


### Query a BESD file 

This feasuer is memory efficent even to query with huge dense BESD file.

#### \# Command line options for SNPs

To query the eQTL resutls for a single SNP, we could use this command

```
osca --beqtl-summary myeqtl --query 5.0e-8 --snp rs123 --out myquery 
```

**\--query** saves in text format a subset of the eQTL summary
dataset based on the specified eQTL p-value threshold. The default
value is 5.0e-8.

**\--snp** specifies a single SNP.

***myquery.txt***

```
SNP	Chr	BP	A1	A2	Freq	Probe	Probe_Chr	Probe_bp	Gene	Orientation	b	se	p
rs01	1	1001	A	G	0.23	cg01	1	1101	gene1	+	-0.033	0.006	3.8e-08
rs01	1	1001	A	G	0.06	cg02	1	1201	gene2	-	0.043	0.007	8.1e-10
......	
```
To query the eQTL resutls excluding a single SNP, we could use this command

```
osca --beqtl-summary myeqtl --query 5.0e-8 --snp-rm rs123 --out myquery 
```
**\--snp-rm** specifies a single SNP to exclude.

To query the eQTL resutls extracting a subset of SNPs , we could use this command

```
osca --beqtl-summary myeqtl --query 5.0e-8 --extract-snp mysnp.list --out myquery 
```
**\--extract-snp** extracts a subset of SNPs for analysis.

To query the eQTL resutls excluding a subset of SNPs , we could use this command

```
osca --beqtl-summary myeqtl --query 5.0e-8 --exclude-snp mysnp.list --out myquery 
```
**\--exclude-snp** excludes a subset of SNPs from analysis.

To query eQTL resutls for a range of SNPs in a genomic region

```
osca --beqtl-summary myeqtl --query 5.0e-8 --from-snp rs123 --to-snp rs456 --out myquery 
```

**\--from-snp** specifies the start SNP.

**\--to-snp** specifies the end SNP.

**NOTE** : All SNPs should be on the same chromosome.

To query eQTL results for all SNP on a chromosome

```
osca --beqtl-summary myeqtl --query 5.0e-8 --snp-chr 1 
```

**\--snp-chr** specifies a chromosome to select SNPs.

**NOTE** : The probes in the result could be on the other chromosomes if
there are *trans*-eQTLs.

To query SNPs based on physical positions

```
osca --beqtl-summary myeqtl --query 5.0e-8 --snp-chr 1 --from-snp-kb 100 --to-snp-kb 200 --out myquery 
```

**\--from-snp-kb** specifies the start physical position of the
region.

**\--to-snp-kb** specifies the end physical position of the region.

**NOTE** : You will need to specify a chromosome (using the '\--snp-chr'
option) when using this option.

To query based on a flanking region of a SNP

```
osca --beqtl-summary myeqtl --query 5.0e-8 --snp rs123 --snp-wind 50 --out myquery 
```

**\--snp-wind** defines a window centred on a specified SNP.

#### \# Command line options for probes

To query based on a single probe

```
osca --beqtl-summary myeqtl --query 5.0e-8 --probe cg123 --out myquery 
```

**\--probe** specifies a single probe.

To query excluding a single probe

```
osca --beqtl-summary myeqtl --query 5.0e-8 --probe-rm cg123 --out myquery 
```

**\--probe-rm** specifies a single probe to exclude.

To query the eQTL resutls extracting a subset of probes , we could use this command

```
osca --beqtl-summary myeqtl --query 5.0e-8 --extract-probe myprobe.list --out myquery 
```
**\--extract-probe** extracts a subset of probes for analysis.

To query the eQTL resutls excluding a subset of probes , we could use this command

```
osca --beqtl-summary myeqtl --query 5.0e-8 --exclude-probe myprobe.list --out myquery 
```
**\--exclude-probe** excludes a subset of probes from analysis.

To query based on a range of probes

```
osca --beqtl-summary myeqtl --query 5.0e-8 --from-probe cg123 --to-probe cg456 --out myquery 
```

**\--from-probe** specifies the start probe.

**\--to-probe** specifies the end probe.

NOTE : All probes should be on the same chromosome.

To query based on a chromosome

```
osca --beqtl-summary myeqtl --query 5.0e-8 --probe-chr 1 
```

**\--probe-chr** specifies a chromosome to select probes.

**NOTE** : The SNPs in the result could be on the other chromosomes if there
are *trans*-eQTLs.

To query based on physical positions of the probes

```
osca --beqtl-summary myeqtl --query 5.0e-8 --probe-chr 1 --from-probe-kb 1000 --to-probe-kb 2000 --out myquery 
```

**\--from-probe-kb** specifies the start physical position of the
probes.

**\--to-probe-kb** specifies the end physical position of the
probes.

**NOTE** : You will need to specify a chromosome (using the '\--probe-chr'
option) when using this option.

To query based on a flanking region of a probe

```
osca --beqtl-summary myeqtl --query 5.0e-8 --probe cg123 --probe-wind 1000 --out myquery 
```

**\--probe-wind** defines a window centred on a specified probe.

To query based on a gene

```
osca --beqtl-summary myeqtl --query 5.0e-8 --gene gene1 --out myquery 
```

**\--gene** specifies a single gene to select probes.

#### \# Command line option for cis-region

```
osca --beqtl-summary myeqtl --query 5.0e-8 --probe cg123 --cis-wind 2000 --out myquery 
```

#### \# File-list options

To query based on a list of SNPs

```
osca --beqtl-summary myeqtl --extract-snp snp.list --query 5.0e-8 --out myquery 
```

To query based on a list of probes

```
osca --beqtl-summary myeqtl --extract-probe probe.list --query 5.0e-8 --out myquery
```

To qurey based on a list of genes

```
osca --beqtl-summary myeqtl --genes gene.list --query 5.0e-8 --out myquery 
```

**\--genes** extracts a subset of probes which tag the genes in the
list.

***gene.list***
```
gene1
gene2
gene3
...
```
### Manage a BESD file 

#### \# make a subset of data
All the data management options in [Query a BESD file](file:///Users/futao.zhang/Desktop/20171212/osc_doc/build/index.html#QueryaBESDfile) can be here.

for example, To extract a subset of SNPs and/or probes

```
osca --beqtl-summary myeqtl --extract-snp mysnp.list --extract-probe myprobe.list  --make-besd --out mybesd 
```
#### \# tansform to SMR compatible format

```
osca --beqtl-summary myeqtl --make-besd --to-smr --out mybesd 
```
**\--to-smr** tranforms BESD file to SMR compatible format.

#### \# shrink a BESD file

To remove probes without any value across all the SNPs and SNPs without any value across all the probes.

```
osca --beqtl-summary myeqtl --make-besd --besd-shrink --out mybesd 
```
**\--besd-shrink** removes probes and SNPs that have no value.

