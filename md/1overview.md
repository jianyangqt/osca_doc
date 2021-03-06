## Overview {: .expand}

### About

**OSCA** (OmicS-data-based Complex trait Analysis) is a software tool written in C/C++ for the analysis of complex traits using multi-omics data. It is developed by [Futao Zhang](https://scholar.google.com/citations?user=lXCr6p4AAAAJ&hl=en&oi=ao) and [Jian Yang](http://researchers.uq.edu.au/researcher/2713) at [Institute for Molecular Bioscience](https://imb.uq.edu.au/), The University of Queensland. Bug reports or questions: Jian Yang <<jian.yang.qt@gmail.com>\> or Futao Zhang <<futoaz@gmail.com>\>.

Functions currently supported are:

-   Estimating the epigenetic (or transcriptomic) relationships between individuals from genome-wide DNA methylation (or gene expression) data.

-   Estimating the proportion of phenotypic variance for a complex trait that can be captured by all DNA methylation (or gene expression) probes.

-   Mixed linear model-based approaches to test for associations between DNA methylation (or gene expression) probes and complex traits (i.e., the MOA and MOMENT methods).

-   Estimating the joint "effects" of all methylation (transcription) probes on a phenotype (e.g. BMI) in a mixed linear model (analogous to BLUP). These estimated effects can be used to "predict" the phenotype in a new independent sample.

-   eQTL/mQTL analysis based on a linear regression model with relevant covarites (results saved in [BESD format](#BESDformat)).

-   vQTL analysis to test for the effects of genetic variants on the variance of a trait. Three algorithms have been implemented (i.e., the Bartlett's test, the Levene's test and the Fligner-Killeen test).

**Note:** although this software tool is designed for gene expression and DNA methylation data, it can in principle be applied to any other source of omic data including microbiome, proteome and brain connectome.


### Credits 

[Futao Zhang](https://scholar.google.com/citations?user=lXCr6p4AAAAJ&hl=en&oi=ao) and [Jian Yang](http://researchers.uq.edu.au/researcher/2713) developed the methods, software and webpage. [Zhihong Zhu](http://researchers.uq.edu.au/researcher/3051) contributed to the development of the ORM and OREML methods. [Ting Qi](http://researchers.uq.edu.au/researcher/15871) contributed to MeCS method. [Huanwei Wang](mailto:huanwei.wang@imb.uq.edu.au) contributed to vQTL method. [Zhili Zheng](mailto:zhili.zheng@imb.uq.edu.au) provided the template of the website.


### Questions and Help Requests 
Bug reports or questions to Jian Yang (<jian.yang.qt@gmail.com>)  or Futao Zhang (<futoaz@gmail.com>) at
Institute for Molecular Bioscience, The University of Queensland.


### Citation 

Zhang F, Chen W, Zhu Z, Zhang Q, Nabais, MF, Qi T, Deary IJ, Wray NR, Visscher PM, McRae AF, Yang J (2019) OSCA: a tool for omic-data-based complex trait analysis. [*Genome Biol, 20:107*](https://genomebiology.biomedcentral.com/articles/10.1186/s13059-019-1718-z).

