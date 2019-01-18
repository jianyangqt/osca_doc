
## vQTL Analysis {: .expand}

This is a module in OSCA to perform a variance quantitative trait locus (vQTL) mapping analysis and save the results in [BESD format](#BESDformat). We have provided 4 methods to run vQTL analysis, namely [Bartlett’s test](https://en.wikipedia.org/wiki/Bartlett%27s_test), [Levene’s test](https://en.wikipedia.org/wiki/Levene%27s_test) with mean, [Levene’s test](https://en.wikipedia.org/wiki/Levene%27s_test) with median, and [Fligner-Killeen test](http://www.cookbook-r.com/Statistical_analysis/Homogeneity_of_variance/#fligner-killeen-test). In the output file, apart from the vQTL statistic and p-value, we also provide the vQTL effect (i.e., the effect of a SNP on differences in phenotype variance among genotype groups), computed from z-statistic using the method described in [(Zhu et al. 2016 Nature Genetics)](http://www.nature.com/ng/journal/vaop/ncurrent/full/ng.3538.html). Note that the vQTL z-statistic can be computed from p-value and the sign of the slope of regressing phenotype variance against genotypes.

#### \# Basic option

```
osca --vqtl --bfile mydata --pheno mypheno --out myvqtl
```
**\--vqtl** to turn a vQTL analysis.

**\--bfile** to input SNP genotype data.

**\--pheno**  to input phenotype data (see [OREML](#OREML) for the input format).


***myvqtl.vqtl***
```
Chr    SNP    bp    statistic    df    beta    se    P    NMISS
21    rs144022851    14589985    2.98808    1    -0.246533    0.142619    8.387947e-02    1319
21    rs146286292    14592960    2.99122    1    -0.244279    0.141241    8.371710e-02    1319
21    rs2847443    14595264    2.40285    1    -0.209187    0.134949    1.211141e-01    1319
21    rs192179023    14600255    0.00383907    1    0.0357931    0.577678    9.505945e-01    1319
21    rs9984084    14602180    5.21829    2    0.0696413    0.0389252    7.359741e-02    1319
...                    
```
This is a text file with headers. Columns are chromosome, SNP, SNP BP, the statistic, degree of freedom, effect size, standard error,  p-value and number of non-missing individuals.

#### \# Specifying the method to test variance heterogeneity

```
osca --eqtl --bfile mydata --pheno mypheno --vqtl-mtd 1 --out myvqtl
```
**\--vqtl-mtd** to specify the method to test variance heterogeneity. 0 for Bartlett’s test, 1 for Levene’s test with mean, 2 for Levene’s test with median, 3 for Fligner-Killeen test. The default option is 0.


***myvqtl.vqtl***
```
Chr    SNP    bp    F-statistic    df1    df2    beta    se    P    NMISS
21    rs144022851    14589985    2.03194    1    1317    -0.203255    0.142671    0.154261    1319
21    rs188453282    14591213    1.48959    1    1317    1.21945    0.999626    0.222499    1319
21    rs146286292    14592960    1.84845    1    1317    -0.192008    0.141303    0.174196    1319
21    rs2847443    14595264    1.83381    1    1317    -0.182687    0.134978    0.17591    1319
21    rs192179023    14600255    0.00102531    1    1317    0.018494    0.577679    0.974461    1319
21    rs9984084    14602180    1.73809    2    1316    0.0526684    0.0389454    0.176259    1319
...                    
```
This is a text file with headers. Columns are chromosome, SNP, SNP BP, F-statistic, K-1 degrees of freedom, N-K degrees of freedom, effect size, standard error,  p-value and number of non-missing individuals.

#### \# Including data management options

```
osca --vqtl --bfile mydata --pheno mypheno --extract-snp mysnp.list --maf 0.01 --out myvqtl
```
#### \#  Running vQTL analysis for molecular phenotypes 

```
osca --vqtl --bfile mydata --befile myprofile --out myvqtl
```
**\--befile**  to input molecular phenotypes (e.g. DNA methylation or gene expression measures in [BOD format](#BODformat)).

#### \#  Running vQTL analysis for molecular phenotypes in cis-regions

```
osca --vqtl --bfile mydata --befile myprofile --cis-wind 2000 --out myvqtl
```
**\--cis-wind**  to define a window centred around the probe to select SNPs for the vQTL analysis. The default value is 2000Kb.

**Note** that vQTL results for molecular traits will be saved in  [BESD format](#BESDformat) which can be tansformed to text format using [OSCA query](#QueryaBESDfile).

#### \# Multi-threading computation
```
osca --vqtl --bfile mydata --befile myprofile --cis-wind 2000 --task-num 1000 --task-id 1 --thread-num 10 --out myvqtl
```

#### Citation
Huanwei Wang, Futao Zhang, Jian Zeng, Yang Wu, Kathryn E. Kemper, Angli Xue, Min Zhang, Joseph E. Powell, Michael E. Goddard, Naomi R. Wray, Peter M. Visscher, Allan F. McRae, Jian Yang (2019) Genotype-by-environment interactions inferred from genetic effects on phenotypic variability in the UK Biobank. [bioRxiv 519538; doi: https://doi.org/10.1101/519538](https://www.biorxiv.org/content/early/2019/01/14/519538)
