
## eQTL/mQTL Analysis {: .expand}

This is a module in OSCA to perform a standard eQTL mapping analysis. We describe the module for eQTL mapping but it can be applied to genetic association analysis for all kinds of molecular traits (e.g. DNA methylation, histone modification, metabolites and Microbiome)

#### \# basic option 

```
osca --eqtl --bfile mydata --befile myprofile --out myeqtl
```
**\--eqtl** enables the eQTL mapping analysis.

**\--bfile** reads individual-level SNP genotype data (in PLINK binary format), i.e. .bed, .bim, and .fam files.

By default, the results will be saved in [BESD dense format 1](#BESDformat) (probe-major). This is the format to be used in the SMR software.

#### \# Multi-threading computation
```
osca --eqtl --bfile mydata --befile myprofile --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
**\--task-total** specifies the total number of tasks to partition the computation by probes.

**\--task-id** specifies the task IDs form 1 to the total task number.

**\--thread-num** specifies the number of threads for parallel computing. The default value is 1.


#### \# Using other data management options

```
osca --eqtl --bfile mydata --befile myprofile --extract-snp mysnp.list --maf 0.01 --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
**\--maf** filters SNPs based on the specified MAF threshold.

#### \# Saving the result in [BESD dense format 2](#BESDformat) (SNP-major)

```
osca --eqtl --bfile mydata --befile myprofile --besd-snp-major --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
**\--besd-snp-major** saves the result in [BESD dense format 2](#BESDformat). This option can accelerate the computing because it avoids the repeated recoding of SNP genotypes.

#### \# Fitting covariates

```
osca --eqtl --bfile mydata --befile myprofile --covar mycovar --qcovar myqcovar --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```

#### \# Fast eQTL analysis

The options above fit the covariates in the model as y=xb+C&beta;+e. This is equivalent to y<sup>'</sup>=y-C&beta;<sup>^</sup>, x<sup>'</sup>=x-C&beta;<sup>^</sup>, y<sup>'</sup>=x<sup>'</sup>b. This equivalent transformation avoids the repeated computing of the inverse of a (p +1)*(p + 1) matrix where p is the number of covariates.

```
osca --eqtl --bfile mydata --befile myprofile --fast-eqtl --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
**\--fast-eqtl** runs the fast eQTL analysis.
