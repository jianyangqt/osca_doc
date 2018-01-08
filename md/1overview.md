## Overview {: .expand}

### About

**OSCA** (OmicS-data-based Complex trait Analysis) is a software tool
written in C/C++ for the analysis of complex traits using multi-omics
data. It is developed by [Futao Zhang](http://researchers.uq.edu.au/researcher/12709), [Zhihong Zhu](http://researchers.uq.edu.au/researcher/3051) and [Jian Yang](http://researchers.uq.edu.au/researcher/2713) at Institute for Molecular Bioscience, The University of Queensland. Bug reports or questions: Jian Yang <<jian.yang@uq.edu.au>\>.

Functions currently supported are:

-   Estimating the epigenetic (or transcriptomic) relationships between individuals from genome-wide DNA methylation (or gene expression) data.

-   Estimating the proportion of phenotypic variance for a complex trait can be "explained" by all DNA methylation (or gene expression) probes.

-   Mixed linear model based analysis to test for associations between DNA methylation (or gene expression) probes and complex traits.

-   Estimating the joint "effects" of all methylation (transcription) probes on a phenotype (e.g. BMI) in a mixed linear model (analogous to BLUP). These estimated effects can be used to predict the phenotype in a new independent sample.

-   eQTL/mQTL analysis with linear regression model. The model can adjust for the relevant covarites. The results are saved in [SMR dense BESD format](http://cnsgenomics.com/software/smr/#DataManagement).

-   vQTL analysis to test the homogeneity of variance. Three algorithms have been implemented (Bartlett’s test, Levene’s test and Brown–Forsythe test, Fligner-Killeen test). The results are saved in [SMR dense BESD format](http://cnsgenomics.com/software/smr/#DataManagement).

**Note:** Although this software tool is designed for gene expression and DNA methylation data, it can be applied to any other source of omics data including microbiome, proteome and brain connectome.


### Credits 

[Futao Zhang](http://researchers.uq.edu.au/researcher/12709) and [Jian Yang](http://researchers.uq.edu.au/researcher/2713) developed the methods, software and webpage. [Zhihong Zhu](http://researchers.uq.edu.au/researcher/3051) contributed to the development of the ORM and OREML methods. [Ting Qi](http://researchers.uq.edu.au/researcher/15871) contributed to MeCS method. [Huanwei Wang](mailto:huanwei.wang@imb.uq.edu.au) contributed to vQTL method. [Zhili Zheng](mailto:zhili.zheng@imb.uq.edu.au) provided the template of the website.


### Questions and Help Requests 
Bug reports or questions to Jian Yang (<jian.yang@uq.edu.au>) at
Institute for Molecular Bioscience, The University of Queensland.


### Citations 

**EWAS method:**
Zhang, F. et al. (2017) OSCA: a tool for omics-data-based complex trait
analysis. In preparation.

