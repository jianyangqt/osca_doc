
## eQTL/mQTL Analysis {: .expand}

#### \# basic option 

```
osca --eqtl --bfile mydata --befile myprofile --out myeqtl
```
**\--eqtl** turns on eQTL analysis.

**\--bfile** reads individual-level SNP genotype data (in PLINK binary format) from a reference sample for LD estimation, i.e. .bed, .bim, and .fam files.

#### \# compute with multi-tasks 
```
osca --eqtl --bfile mydata --befile myprofile --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
**\--task-total** specifies the total task number to patition computation by probes.

**\--task-id** specifies the current task ID which ranges form 1 to the total task number.

**\--thread-num** specifies the number of OpenMP threads for parallel computing. The default value is 1.

#### \# include covariates

```
osca --eqtl --bfile mydata --befile myprofile --covar mycovar --qcovar myqcovar --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
#### \# include data management options

```
osca --eqtl --bfile mydata --befile myprofile --extract-snp mysnp.list --maf 0.01 --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
**\--maf** removes SNPs based on a minor allele frequency (MAF) threshold in the individual-level SNP genotype data.

#### \# save result in [BESD dense format 2](#BESDformat)

The options above suffer from repeated recoding the genotype. This could be aggravated as the probe number increase. THis option could alleviate the situation a little bit.

```
osca --eqtl --bfile mydata --befile myprofile --besd-snp-major --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
**\--besd-snp-major** conducts eQTL analysis SNP by SNP across all the probes and saves the result in [BESD dense format 2](#BESDformat).

#### \# fast eQTL analysis

The options above fit the covariates in the model as y=xb+C&beta;+e. It is equivalent to y<sup>'</sup>=y-C&beta;<sup>^</sup>, x<sup>'</sup>=x-C&beta;<sup>^</sup>, y<sup>'</sup>=x<sup>'</sup>b. 

```
osca --eqtl --bfile mydata --befile myprofile --fast-eqtl --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
**\--fast-eqtl** runs fast eQTL analysis.
