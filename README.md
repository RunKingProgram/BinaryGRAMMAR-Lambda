# GRL-Binary（GRL_binary）
# 1. Getting started
## 1.1	Downloading GRL_binary
GRL_binary can be downloaded https://github.com/RunKingProgram/BinaryGRAMMAR-Lambda. It can be installed as a regular R package.
## 1.2	Installing GRL_binary
GRL_binary links to R packages Rcpp, RcppEigen, RcppArmadillo, BEDMatrix and data.table. These dependencies should be installed before installing GRL_binary. In addition, GRL_binary requires a recompiled PLINK2.0 Software with name “plink2ebv” under your working directory. Here is an example for installing BinaryOpGR and all its dependencies in an R session under Linux，MacOS or Windows Subsystem for Linux:

```
install.packages(c("BEDMatrix", "data.table", "Rcpp", "RcppEigen", "RcppArmadillo"))
system(“R CMD install GRLbinary_1.0_for_MacOS.tgz”)
```
# 2. Input
Input files consist of three PLINK BED files with the same name. For example, Genotype.bed, Genotype.bim and Genotype.fam.

## 2.1 Phenotype
Phenotype should place in the sixth column of “.fam” file.
## 2.2 Genotypes
GRL_binary can only take genotype files in “.bed” and “.bim” format.
# 3. Running GRL_binary
If GRL_binary has been successfully installed, you can load it in an R session using:
```
library(GRLbinary)
```
and then loading "BEDMatrix "and " data.table " 
```
library(BEDMatrix)
library(data.table)
```
We provide three functions in GRL_binary: **Data** function for basic data management including extract phenotypic values, sampling markers, calculate allele frequencies and calculating GRM; **Grammar_binary** function for estimating heritability (optional) and breading values, association tests using GRAMMAR method with Logistic regression and **Grl_binary** function for adjust statistics using *Lambda*, joint analysis based on the results of GRAMMAR-Lambda for binary phenotype, and outputting association result files.
## 3.1 Data function
#### Usage
```
Data (filename, nsmar, msampling)
```
#### Arguments

#### filename
An object class of character: the filename before the suffix of plink files. The three plink file must have a same filename, for example, “filename.bed”, “filename.bim” and “filename.bam”.
#### nsmar 
An optional numeric for the number of sampling markers. If this is unset, the “nsmar” default is 5,000.
#### msampling
logicals. If FLASE, entire markers will be used to calculate GRM. If this is unset, the “msampling” default is TURE. This argument is not suitable for large scale dataset.
## 3.2 Grammar function
#### Usage
```
Grammar_binary (Data, Estimateh2, prevenlence)
```
#### Arguments
#### Data
An object class of list generated from the **Data** function.
#### Estimateh2 
logicals. If TURE, heritability will be calculated for estimating breeding values. If this is unset or for large scale dataset, heritability is set by default at 0.5.
#### Prevalence 
Numeric. Takes effect only when 
```
Estimateh2 = T
```
## 3.3 GRL_binary
#### Usage
```
Grl_binary (Grammar, Test, QQ,Manh)
```
#### Arguments
#### Grammar  
An object class of list generated from the **Grammar_binary** function.
#### Test   
An optional for association test: a test at once or joint analysis.
#### QQ   
logicals. If TURE, Q-Q plot would be drawn.
#### Manh   
logicals. If TURE, Q-Q plot would be drawn.


# 4.Output files


There are the two outputs from the GRL_binary: estimated breeding values（ebv.txt）and association tests(result.PHENO1.glm.logistic). For example, result.PHENO1.glm.logistic:
CHROM|	POS|	ID|	REF|	ALT|	A1|	TEST|	OBS_CT|	OR|	SE|	Z_STAT|	P|	ERRCODE
---- | ----- | ------ | ------| ------| ------| ------| ------| ------| ------| ------| ------| ------
1|	10390|	S1_10390	|G|	A|	A|	ADD|	2648|	0.0784112|	0.238845|	-0.0328293	|0.973813|	|.
1|	10590|	S1_10590	|T|	A|	A|	ADD|	2648|	0.202364|	0.249746|	-0.810281	|0.417852|	|.
1|	128373|	S1_128373|	C|	T|	T|	ADD|	2648|	0.033819|	0.124565|	0.271498	|0.78603|	|.
…

# 5.Example

```
library(GRLbinary)
library(BEDMatrix)
library(data.table)

setwd("./example")
plinkfilename <- "geno"
gdata <- Data(plinkfilename)
grammar <- Grammar_binary(gdata)
Grl_binary (grammar)
```
