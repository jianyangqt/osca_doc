
## OREML

```
osca --reml --pheno my.phen --out myreml
```

**\--reml** performs REML (restricted maximum likelihood) analysis.
This option is usually followed by the option \--orm (one ORM) or
\--merge-orm (multiple ORMs) to estimate the variance explained by
the probes that were used to estimate the omics relationship matrix.

**\--pheno** reads phenotype data from a plain text file. Missing
value should be represented by "NA".

***my.phen***

```
R06C01 R06C01  32.6332
R05C02  R05C02  23.9411
R04C02  R04C02  29.7441
...                    
```

**NOTE:** current version only supports single trait analysis in one
run.

```
osca --reml --orm myorm --pheno my.phen --out myreml
```
```
osca --reml --orm myorm --pheno my.phen --keep indi.list --out myreml
```
```
osca --reml --orm myorm --pheno my.phen --orm-cutoff 0.05 --out myreml
```

With multiple ORMs

```
osca --reml --multi-orm myorm.flist --pheno my.phen --out myreml
```
```
osca --reml --multi-orm myorm.flist --pheno my.phen --reml-alg 0 --out myreml
```
**\--reml-alg** specifies the algorithm to do REML iterations, 0 for
average information (AI), 1 for Fisher-scoring and 2 for EM. The
default option is 0, i.e. AI-REML, if this option is not specified.

```
osca --reml --multi-orm myorm.flist --pheno my.phen --reml-maxit 100 --out myreml
```
**\--reml-maxit** specifies the maximum number of iterations. The
default number is 100 if this option is not specified.

```
osca --reml --orm myorm --pheno my.phen --covar my.covar --out myreml
```
**\--covar** reads discrete covariates from a plain text file.

***my.covar***

```
R06C01 R06C01  F   0
R05C02  R05C02  F   1
R04C02  R04C02  M   1
...                    
```
```
osca --reml --orm myorm --pheno my.phen --qcovar my.qcovar --out myreml
```
**\--qcovar** reads quantitative covariates from a plain text file.

***my.qcovar***

```
R06C01 R06C01  25
R05C02  R05C02  16
R04C02  R04C02  30
...                    
```
```
osca --reml --orm myorm --pheno my.phen --reml-est-fix --out myreml
```
**\--reml-est-fix** displays the estimates of fixed effects on the
screen.

```
osca --reml --orm myorm --pheno my.phen --reml-no-lrt --out myreml
```
**\--reml-no-lrt** turns off the LRT.

