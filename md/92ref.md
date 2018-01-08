## Options Reference 

<table width="1000" border="0" style="font-family:arial; font-size:14px; align-self:center" >
<tr> 
<td align="left"><font color="#993333">--befile</font></td>
<td align="left">
reads a DNA methylation (or gene expression) data file in binary format
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--befile-flist</font></td>
<td align="left">
reads a file to get the full paths of the binary files
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--beta2m</font></td>
<td align="left">
calculates the methylation m value from the methylation beta value
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--blup-probe</font></td>
<td align="left">
calculates the BLUP solutions for the probe effects
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--chr</font></td>
<td align="left">
specifies a chromosome to select probes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--covar</font></td>
<td align="left">
reads discrete covariates from a plain text file
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--detection-pval-file</font></td>
<td align="left">
reads a file that contains DNA methylation detection p-values
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--dpval-mth</font></td>
<td align="left">
specifies a method to do quality control with the detection p-values
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--dpval-thresh</font></td>
<td align="left">
specifies a threshold of detection p-value
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--efile</font></td>
<td align="left">
reads a DNA methylation (or gene expression) data file in plain text format
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--exclude-probe</font></td>
<td align="left">
excludes a subset of probes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--extract-probe</font></td>
<td align="left">
extracts a subset of probes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--from-probe</font></td>
<td align="left">
specifies the start probe
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--from-probe-kb</font></td>
<td align="left">
specifies the start physical position of the probes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--gene</font></td>
<td align="left">
extracts a gene
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--genes</font></td>
<td align="left">
extracts a subset of genes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--gene-expression</font></td>
<td align="left">
indicates gene expression profiles in the file
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--get-mean</font></td>
<td align="left">
calculates the mean of each probe
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--get-variance</font></td>
<td align="left">
calculates the variance of each probe
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--keep</font></td>
<td align="left">
extracts a subset of individuals
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--linear</font></td>
<td align="left">
saves linear regression statistics to a plain text file
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--lower-beta</font></td>
<td align="left">
removes the DNA methylation probes with the mean beta value smaller than a specified threshold
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--lxpo</font></td>
<td align="left">
specifies a percentage of probes to exclude from calculating the ORM
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--m2beta</font></td>
<td align="left">
calculates the methylation beta value from the methylation m value
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--make-bod</font></td>
<td align="left">
saves DNA methylation (or gene expression) data in binary format
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--make-efile</font></td>
<td align="left">
saves the DNA methylation (or gene expression) data in text format
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--make-orm</font></td>
<td align="left">
estimates the omics relationship matrix (ORM) and save the lower triangle elements of ORM to binary files
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--make-orm-bin</font></td>
<td align="left">
estimates the omics relationship matrix (ORM) and save the lower triangle elements of ORM to binary files
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--make-orm-gz</font></td>
<td align="left">
estimates the omics relationship matrix (ORM) and save the lower triangle elements of ORM to compressed plain text files
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--make-tefile</font></td>
<td align="left">
saves the DNA methylation (or gene expression) data in transposed text format
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--merge-orm</font></td>
<td align="left">
reads multiple ORMs in binary format
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--methylation-m </font></td>
<td align="left">
indicates methylation m values in the file
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--methylation-beta</font></td>
<td align="left">
indicates methylation beta values in the file
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--mlma</font></td>
<td align="left">
initiates an MLM based association analysis including the target probe (the probe to be tested for association) in the ORM
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--mlma-loco</font></td>
<td align="left">
initiates an MLM based association analysis with the chromosome where the target probe is located excluded from the ORM
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--mpheno</font></td>
<td align="left">
reads a list of comma-delimited trait numbers if the phenotype file contains more than one trait
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--missing-ratio-probe</font></td>
<td align="left">
specifies a missing proportion threshold to remove probes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--no-fid</font></td>
<td align="left">
indicates data without family ID
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--orm</font></td>
<td align="left">
reads the ORM binary files
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--orm-alg</font></td>
<td align="left">
specifies the algorithm to estimate the ORM
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--orm-cutoff</font></td>
<td align="left">
removes one of a pair of individuals with estimated omics relationships larger than the specified cut-off value
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--out</font></td>
<td align="left">
saves data (or results) in a file
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--pca</font></td>
<td align="left">
conducts principal component analysis and saves the first n (default as 20) PCs
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--pheno</font></td>
<td align="left">
reads phenotype data from a plain text file
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--probe</font></td>
<td align="left">
extracts a specified probe
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--probe-wind</font></td>
<td align="left">
defines a window centred on a specified probe
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--probe-rm</font></td>
<td align="left">
excludes a specified probe
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--qcovar</font></td>
<td align="left">
reads quantitative covariates from a plain text file
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--ratio-probe</font></td>
<td align="left">
specifies a proportion threshold to remove probes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--ratio-sample</font></td>
<td align="left">
specifies a proportion threshold to remove individuals
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--reml</font></td>
<td align="left">
performs REML (restricted maximum likelihood) analysis
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--reml-alg</font></td>
<td align="left">
specifies the algorithm to do REML iterations
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--reml-est-fix</font></td>
<td align="left">
displays the estimates of fixed effects on the screen
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--reml-maxit</font></td>
<td align="left">
specifies the maximum number of iterations
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--reml-no-lrt</font></td>
<td align="left">
turns off the LRT
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--reml-pred-rand</font></td>
<td align="left">
predicts the random effects by the BLUP (best linear unbiased prediction) method
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--remove</font></td>
<td align="left">
excludes a subset of individuals
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--score</font></td>
<td align="left">
reads score files for probes and generates predicted omics profiles for individuals
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--score-has-header</font></td>
<td align="left">
indicates probe score file has headers
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--simu-causal-loci</font></td>
<td align="left">
reads a list of probes as causal probes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--simu-cc</font></td>
<td align="left">
simulates a case-control trait and specifies the number of cases and the number of controls
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--simu-eff-mod</font></td>
<td align="left">
specifies whether or not to standardize the causal probe
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--simu-hsq</font></td>
<td align="left">
specifies the proportion of variance in phenotype explained by the causal probes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--simu-k</font></td>
<td align="left">
specifies the disease prevalence. The default value is 0.1 if this option is not specified
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--simu-qt</font></td>
<td align="left">
simulates a quantitative trait
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--std</font></td>
<td align="left">
removes the probes with the standard deviation smaller than a specified threshold
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--to-probe</font></td>
<td align="left">
specifies the end probe
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--to-probe-kb</font></td>
<td align="left">
specifies the end physical position of the probes
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--update-opi</font></td>
<td align="left">
reads a fully annotated .opi file
</td>
</tr>
<tr> 
<td align="left"><font color="#993333">--upper-beta</font></td>
<td align="left">
removes the DNA methylation probes with the mean beta value larger than a specified threshold
</td>
</tr>
</table>

