
## EWAS {: .expand}

### Mixed Linear Model Association

```
osca --mlma --befile myprofile --pheno my.phen --out my
```

If you have already computed the ORM

```
osca --mlma --befile myprofile --pheno my.phen --orm myorm --out my
```
**\--mlma** initiates an MLM based association analysis including
the target probe (the probe to be tested for association) in the
ORM. The results will be saved in a plain text file with **.mlma**
as the filename extension.

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

```
osca --mlma-loco --befile myprofile --pheno my.phen --out my
```
**\--mlma-loco** initiates an MLM based association analysis with
the chromosome where the target probe is located excluded from the
ORM. The results will be saved in a plain text file with
**.loco.mlma** as the filename extension.

```
osca --mlma --lxpo 0.1 --befile myprofile --pheno my.phen --out my
```
```
osca --mlma-loco --lxpo 0.1 --befile myprofile --pheno my.phen --out my
```
**\--lxpo** specifies a percentage of probes to exclude from
calculating the ORM. This option should accompany **\--mlma** or
**\--mlma-loco**. It will first conduct a linear-regression-based
association analysis and then excludes a percentage of top
associated probes from the ORM.

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
probeChr   ProbeID Probe_bp    BETA    SE  P   NMISS
1   cg00003287  201346149   -0.0594 0.531   9.11e-01    1337
1   cg00008647  207082900   0.5003  0.263   5.72e-02    1337
1   cg00009292  50882082    1.0512  1.026   3.06e-01    1337
...                    
```

This is a text file with headers. Columns are chromosome, probe, probe
BP, effect size, standard error, p-value and number of non-missing
individuals.

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

