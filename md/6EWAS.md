
## EWAS {: .expand}

### MOMENT
#### \# MOMENT (Multi-cOmponent Mlm-based association ExcludiNg the Target)
```
osca --moment --befile myprofile --pheno my.phen --out my
```
**\--moment** initiates a multi-component MLM based association analysis excluding
the target probe (the probe to be tested for association) and the probes in its flanking region from the
ORM (the size of flanking region can be modified by --moment-wind). The results will be saved in a plain text file with *.mlma.
as the filename extension.

```
osca --moment --befile myprofile --pheno my.phen --moment-wind 100 --out my
```
**\--moment-wind** specifies a flanking region to exclude probes from the ORM. The default value is 100 Kb (i.e. a 100 Kb region centred at the probe to be tested).

***my.mlma***
```
Chr    Probe   bp  Gene    Orientation b   se  p
1   cg00003287  201346149   TNNT2   -   -0.156  0.597   0.794
1   cg00008647  207082900   IL24    +   0.032   0.354   0.926
1   cg00009292  50882082    DMRTA2  -   0.120   1.182   0.919
...                    
```
This is a text file with headers. Columns are chromosome, probe, probe
BP, gene, orientation, effect size, standard error and p-value.

**NOTE:** Sometimes the MLM estimation process in the EWAS analysis does not work (the REML iteration cannot converge or an estimate hits the boundaries of parameter space) especially when the sample size is small. In such case we switch MLMA to standard PC based linear regression analysis. We have implemented a strategy to identify the number of PCs iteratively until the genomic inflation factor (lambda value) falls into a user-defined range, or the number of PCs reaches the lower (0) or upper boundary (half of the sample size). The range size for lambda can be specified by the option **\--lambda-range**


```
osca --moment --befile myprofile --pheno my.phen --lambda-range 0.05 --out my
```
**\--lambda-range** specifies a range for the lambda value. The default value is 0.05. This option only works when the MLM estimation process fails.

**NOTE:** The analysis becomes slower as the number of PCs becomes larger. The option **\--fast-linear** can accelerate the analysis by pre-adjusting both the trait and gene expression (or DNA methylation) value by the PCs. In this case, all the missing gene expression (or DNA methylation) values will be replaced by the mean. It should be noted that if the proportion of missing values in the gene expression (or DNA methylation) data is large, this accelerated analysis may lead to substantial differences in results.

```
osca --moment --befile myprofile --pheno my.phen --fast-linear --out my
```
**\--fast-linear** runs a fast linear regression analysis. This flag can also be used in the [Fast Linear Regression analysis module](#FastLinearRegression)


### MOA
#### \# MOA (MLM-based Omic Association)
```
osca --moa --befile myprofile --pheno my.phen --out my
```

If you have already computed the ORM

```
osca --moa --befile myprofile --pheno my.phen --orm myorm --out my
```
**\--moa** initiates an MLM based association analysis including
the target probe (the probe to be tested for association) in the
ORM. The results will be saved in a plain text file with **.mlma**
as the filename extension.

### Linear Regression

```
osca --befile myprofile --pheno my.phen --linear --out my
```
```
osca --befile myprofile --pheno my.phen --qcovar my.qcovar --covar my.covar --linear --out my
```
**\--linear** saves linear regression statistics to a plain text file.

***my.linear***

```
probeChr   ProbeID Probe_bp Gene    Orientation   BETA    SE  P   NMISS
1   cg00003287  201346149   TNNT2   -   -0.0594 0.531   9.11e-01    1337
1   cg00008647  207082900   IL24    +   0.5003  0.263   5.72e-02    1337
1   cg00009292  50882082    DMRTA2  -    1.0512  1.026   3.06e-01    1337
...                    
```

This is a text file with headers. Columns are chromosome, probe, probe
BP, gene, orientation, effect size, standard error, p-value and number of non-missing
individuals.

### Fast Linear Regression

The options above fit the covariates in the model as y=xb+C&beta;+e. This is equivalent to y<sup>'</sup>=y-C&beta;<sup>^</sup>, x<sup>'</sup>=x-C&beta;<sup>^</sup>, y<sup>'</sup>=x<sup>'</sup>b. This equivalent transformation avoids the repeated computing of the inverse of a (p +1)*(p + 1) matrix where p is the number of covariates.

```
osca --linear --befile myprofile --pheno my.phen --qcovar my.qcovar --covar my.covar --fast-linear --out my
```
**\--fast-linear**  runs a fast linear regression analysis.

### Logistic Regression

```
osca --befile myprofile --pheno my.phen --logistic --out my
```
```
osca --befile myprofile --pheno my.phen --qcovar my.qcovar --covar my.covar --logistic --out my
```
**\--logistic** outputs logistic regression analysis result to a plain text file.

***my.logistic***

```
probeChr   ProbeID Probe_bp Gene    Orientation   OR    SE  P   NMISS
1	cg00297950	110282525	GSTM3	-	0.010953	1.30438	5.386424e-04	1318
1	cg00299820	11943154	NPPB	-	0.0085006	2.77659	8.596523e-02	1318
1	cg00305285	1017115	RNF223	-	8.22097	2.99934	4.824397e-01	1318
...                    
```

This is a text file with headers. Columns are chromosome, probe, probe
BP, gene, orientation, odd ratio, standard error, p-value and number of non-missing
individuals.

**NOTE:** It is allowed to use characters, strings, or numbers as phenotype values in logistic regression but "NA" or "na" will be recognised as a missing value.

### EWAS simulation

The phenotypes are simulated based on a set of real DNA methylation (or
gene expression) data and a simple model y= sum(x<sub>i</sub>b<sub>i</sub>)+ε, where y is
a vector of phenotypes, x<sub>i</sub> is a vector of raw DNA methylation (or gene
expression) profile or standardized profile of the i-th "causal"
probe, b<sub>i</sub> is the effect of the i-th causal probe and ε \~ N(0,var(
sum(x<sub>i</sub>b<sub>i</sub>))(1/h<sup>2</sup>-1) ) is a vector of residual effect.

```
osca --simu-qt --simu-hsq 0.1 --befile myprofile --simu-causal-loci mycausal.list --out mypheno
```
**\--simu-qt** smulates a quantitative trait.

**\--simu-hsq** specifies the proportion of variance in phenotype
explained by the causal probes. The default value is 0.1.

**\--simu-causal-loci** reads a list of probes as causal probes. If
the effect sizes are not specified in the file, they will be
generated from a standard normal distribution.

***mycausal.list***
```
cg04584301 1.55182
cg04839274  -0.106226
cg16648571  0.0257417
...                    
```
This is a text file with no headers. Columns are probe ID and effect
size.
```
osca --simu-qt --simu-hsq 0.1 --simu-eff-mod 0 --befile myprofile --simu-causal-loci mycausal.list --out mypheno
```
**\--simu-eff-mod** specifies whether or not to standardize the
causal probe, 0 for standardized profile and 1 for raw profile. The
default value is 0.

```
osca --simu-cc 100 300 --simu-hsq 0.1 --simu-k 0.1 --befile myprofile --simu-causal-loci mycausal.list --out mypheno
```
**\--simu-cc** simulates a case-control trait and specifies the
number of cases and the number of controls.

**\--simu-k** specifies the disease prevalence. The default value is
0.1 if this option is not specified.

