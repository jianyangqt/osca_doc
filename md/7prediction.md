
## Prediction Analysis {: .expand}

```
osca --reml --orm myorm --pheno my.phen --reml-pred-rand --out myblp
```
**\--reml-pred-rand** predicts the random effects by the BLUP (best
linear unbiased prediction) method. This option is to estimate the
aggregated effect of all the probes (used to compute the ORM) to the
phenotype of an individual. The aggregated omics effects of all the
individuals will be saved in a plain text file **\*.indi.blp**.

***myblp.indi.blp***
```
R06C01 R06C0   1.02275 0.07065 1.05692 1.05692
R05C02  R05C02  0.18653 0.27059 0.86650 0.86650
R04C02  R04C02  -0.1982 -0.1673 -0.9209 -0.9209
...                    
```
This is a text file with no headers. Columns are family ID, individual
ID, an intermediate variable, the aggregated omics effect, another
intermediate variable and the residual effect.
```
osca --befile myprofile --blup-probe myblp.indi.blp --out myblp
```
**\--blup-probe** calculates the BLUP solutions for the probe
effects.

***myblp.probe.blp***
```
cg04584301 -0.000654646
cg04839274  0.000602484
cg16648571  -4.70356e-05
...                    
```
This is a text file with no headers. Columns are probe ID and BLUP of
the probe effect.
```
osca --befile myprofile --score myblp.probe.blp --out myscore
```
```
osca --befile myprofile --score myblp.probe.blp 1 2 --out myscore
```
**\--score** reads score files for probes and generates predicted
omics profiles for individuals. (Note that this option largely
follows the \--score option in PLINK.) It allows users to specify
the column numbers for probe ID and score (the default values are 1
and 2 as shown in the example above).

***myscore.profile***
```
FID    IID PHENO   CNT SCORE
131000028   422572  -9  20000   -7.269198e-07
131000031   243421  -9  20000   9.322096e-06
131000179   338728  -9  20000   -1.250443e-05
...                    
```
This is a text file with headers. Columns are family ID, individual ID,
phenotype, Number of non-missing probes and score.

```
For example
In the score file:
cg04584301  -0.065
cg04839274  0.060
cg16648571  -1.03

In the DNA methylation data:
FID IID cg04584301  cg04839274  cg16648571
R05C02  R05C02  0.18653 0.27059 0.86650

The score should be:
( 0.18653*(-0.065) + 0.27059*0.060 + (-1.03)*0.86650 ) / 3 = (-0.8883841) / 3 = -0.296
```
```
osca --befile myprofile --score myblp.probe.blp --score-has-header --out myscore
```
**\--score-has-header** indicates probe score file has headers.

