# GRL_binary
# 1. Getting started
## 1.1	Downloading GRL_binary
GRL_binary can be downloaded https://github.com/RunKingProgram/GRL_binary. It can be installed as a regular R package.
## 1.2	Installing GRL_binary
GRL_binary links to R packages Rcpp, RcppEigen, RcppArmadillo, BEDMatrix and data.table. These dependencies should be installed before installing GRL_binary. In addition, GRL_binary requires a recompiled PLINK2.0 Software (http://www.cog-genomics.org/plink/2.0/) with name “plinkoffset” under your working directory. Here is an example for installing GRL_binary and all its dependencies in an R session(assuming none of the R packages other than the default has been installed):
```
install.packages(c("BEDMatrix ", " data.table ", "Rcpp", " RcppEigen ", " RcppArmadillo "), repos = "https://cran.r-project.org/")
system(“R CMD install GRLbinary_1.0.tgz”)
```
# 2. Input
GRL_binary requires the phenotype and genotype files in an PLINK BED data frame which also called PLINK 1 binary file and the structure of these files is described in http://www.cog-genomics.org/plink/1.9/formats#bed. How to prepare these data are describe below.
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
Numeric. Takes effect only when heritability is estimated.
## 3.3 GRL_binary
#### Usage
```
Grl_binary (Grammar, Test, QQ,Manh)
```
#### Arguments
#### Grammar  
An object class of list generated from the **Grammar_binary** function.
#### Test   
An optional for association test, a test at once or joint analysis. You can choose “Separate” for a test at once and “Joint” for further joint analysis based on the result of “Separate”.
#### QQ   
logicals. If TURE, Q-Q plot would be drawn.
#### Manh   
logicals. If TURE, Q-Q plot would be drawn.

#### 4.Example

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
