
## ORM {: .expand}

### estimate ORM

```
osca --befile myprofile --make-orm --out myorm
```

```
osca --befile myprofile --make-orm-bin --out myorm
```
**\--make-orm** or **\--make-orm-bin** estimates the omics relationship matrix (ORM) between pairs of individuals from a set of probes and save the lower triangle elements of ORM to binary files. This format is compatible with the [GRM](http://cnsgenomics.com/software/gcta/#MakingaGRM) in the [GCTA](http://cnsgenomics.com/software/gcta/) software.

```
osca --befile myprofile --make-orm-gz --out myorm
```

**\--make-orm-gz** estimates the ORM and save the lower triangle
elements of ORM to compressed plain text files.

```
osca --befile myprofile --make-orm --orm-alg 1 --out myorm
```

**\--orm-alg** specifies the algorithm to estimate the ORM. 1 for
standardized data of each probe, 2 for centred data of each probe
and 3 for iteratively standardizing probes and individuals. The default option
is 1.

Note that although we describe the options above using DNA methylation
and gene expression data, all the options can be applied to any other
source of omics data mentioned above.

### Principal Component Analysis

```
osca --orm myorm --pca 20 --out mypca
```

**\--orm** reads the ORM binary files.

**\--pca** conducts principal component analysis and saves the first n (default as 20) PCs.

***mypca.eigenval***

```
122.014
95.3064
70.8055
...                    
```
***mypca.eigenvec***

```
R06C01 R06C01  0.012637    -0.00328532 0.0263842   -0.00595246
R05C02  R05C02  0.0106692   -0.0184545  -0.0159826  0.013951
R04C02  R04C02  0.0024727   -0.0118185  -0.0256503  -0.0106235
...                    
```

Users can also manipulate the ORM in the analysis.

```
osca --orm myorm --keep indi.list --pca 20 --out mypca
```
```
osca --orm myorm --remove indi.list --pca 20 --out mypca
```
```
osca --orm myorm --orm-cutoff 0.05 --pca 20 --out mypca
```

**\--orm-cutoff** removes one of a pair of individuals with
estimated omics relationships larger than the specified cut-off
value.

```
osca --multi-orm myorm.flist --pca 20 --out mypca
```

**\--multi-orm** reads multiple ORMs in binary format.


