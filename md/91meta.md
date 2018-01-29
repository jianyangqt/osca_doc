
## Meta-analysis {: .expand}

### Meta-analysis for data without sample overlap

#### \# Meta for GWAS summary data without sample overlap

```
osca --gwas-flist mygwas.flist --meta --out mymeta
```
**\--meta** implements the conventional inverse-variance-weighted meta-analysis meta-analysis assuming all the cohorts are independent. Pleae refer to [de Bakker PI et al.2008 Hum Mol Genet](https://academic.oup.com/hmg/article/17/R2/R122/2527210) for the details.

**\--gwas-flist** reads a file to get file paths of the GWAS summary data.

***mygwas.flist***

```
Height.01.COJO
Height.02.COJO
Height.03.COJO
...                    
```
This file has no header. 

The input format of the GWAS summary data follows that for GCTA-COJO analysis (
<http://cnsgenomics.com/software/gcta/#COJO>).

***Height.01.COJO***
```
SNP	A1	A2	freq	b	se	p	n
rs1001	A	G	0.8493 	0.0024 	0.0055 	0.6653	129850
rs1002	C	G	0.03606	0.0034	0.0115	0.7659	129799
rs1003	A	C	0.5128	0.045	0.038	0.2319	129830
......
```
Columns are SNP, the effect (coded) allele, the other allele, frequency of the effect allele, effect size, standard error, p-value and sample size. The headers are not keywords and will be omitted by the program. <font color='red'>Important: “A1” needs to be the effect allele with “A2” being the other allele and “freq” needs to be the frequency of “A1”</font>. **NOTE: For a case-control study, the effect size should be log(odds ratio) with its corresponding standard error**.

#### \# meta for eQTL summary data

```
osca --besd-flist mybesd.flist --meta --out mymeta
```
**\--besd-flist** reads a file to get the full paths of the BESD files.

***mybesd.flist***

```
path1/my_besd1
path2/my_besd2
path3/my_besd3
...                   
```
This file has no header. The eQTL summary data should be in [BESD formta](#BESDformat).

### MeCS (meta analysis in correlated sampels)

#### \# MeCS for GWAS summary data with sample overlap

```
osca --gwas-flist mygwas.flist --mecs --out mymecs
```
**\--mecs** implements the MeCS analysis.

Specify the cohort correlation matrix

```
osca --gwas-flist mygwas.flist --mecs --cor-mat cor.mat --out mymecs
```
**\--cor-mat** reads a p-value threshold to exclude the significant SNPs from calculation the cohort correlation matrix. The default value is 0.01. 

***cor.mat***
```
1.000000000 0.03911566 0.001821693 0.021464142 0.017527909
0.039115655 1.00000000 0.010180606 0.016671469 0.017503133
0.001821693 0.01018061 1.000000000 0.001058645 0.004646767
0.021464142 0.01667147 0.001058645 1.000000000 0.034315463
0.017527909 0.01750313 0.004646767 0.034315463 1.000000000
```
This file is a symmetric matrix without header.

Use the z-scores instead of the beta values to estimate the cohort correlation matrix.

```
osca --gwas-flist mygwas.flist --mecs --mecs-mth 0 --pcc-z --out mymecs
```
**\--pcc-z** indicates using z-score to compute the Pearson Correlaton Coefficiet matrix. The default value is false.

Specify a p-value threshold to exclude the significant SNPs from calculating the cohort correlation matrix.
```
osca --gwas-flist mygwas.flist --mecs --pmecs 0.01 --out mymecs
```
**\--pmecs** reads a p-value threshold to exclude the significant SNPs from calculating the cohort correlation matrix. The default value is 0.01. 



#### \# MeCS for eQTL summary data

MeCS is a method that only requires summary-level cis-eQTL data to perform a meta-analysis of cis-eQTLs from multiple cohorts (or tissues) with sample overlaps. It estimates the proportion of sample overlap from null SNPs in the cis-regions and meta-analysed the eQTL effects using a generalized least squares approach. The method can be applied to data from genetic studies of molecular phenotypes (e.g. DNA methylation and histone modification).

**NOTE:**  Only the information in the cis-region would be used.

```
osca --besd-flist mybesd.flist --mecs --out mymecs
```

