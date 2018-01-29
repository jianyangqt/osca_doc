
## vQTL Analysis {: .expand}

#### \# basic option for variance QTL analysis

```
osca --vqtl --bfile mydata --befile myprofile --out myvqtl
```
**\--vqtl** turns on vQTL analysis.

#### \# compute with multi-tasks 
```
osca --vqtl --bfile mydata --befile myprofile --task-total 1000 --task-id 1 --thread-num 10 --out myvqtl
```
#### \# specify the algorithm to analyse the homogeneity of variance

We provide 4 methods to run vQTL analysis. 0 for [Bartlett’s test](https://en.wikipedia.org/wiki/Bartlett%27s_test); 1 for [Levene’s test](https://en.wikipedia.org/wiki/Levene%27s_test) with mean; 2 for [Levene’s test](https://en.wikipedia.org/wiki/Levene%27s_test) with median; 3 for [Fligner-Killeen test](http://www.cookbook-r.com/Statistical_analysis/Homogeneity_of_variance/#fligner-killeen-test).

```
osca --eqtl --bfile mydata --befile myprofile --vqtl-mtd 0 --task-total 1000 --task-id 1 --thread-num 10 --out myvqtl
```
**\--vqtl-mtd** specifies the algorithm to analyse the homogeneity of variance. The default option is 0.

#### \# include data management options

```
osca --vqtl --bfile mydata --befile myprofile --extract-snp mysnp.list --maf 0.01 --task-total 1000 --task-id 1 --thread-num 10 --out myvqtl
```

#### \# save result in [BESD dense format 2](#BESDformat)

```
osca --vqtl --bfile mydata --befile myprofile --besd-snp-major --task-total 1000 --task-id 1 --thread-num 10 --out myvqtl
```

#### \# vQTL analysis in cis-regions

Conduct the vQTL analysis only in cis-regions. The result will be saved in [BESD sparse format 2](#BESDformat).

```
osca --vqtl --bfile mydata --befile myprofile --cis-wind 2000 --task-total 1000 --task-id 1 --thread-num 10 --out myeqtl
```
**\--cis-wind** defines a window centred around the probe to select SNPs for the vQTL analysis. The default value is 2000Kb.
