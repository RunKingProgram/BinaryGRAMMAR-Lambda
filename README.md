# GRL_binary
# 1. Getting started
## 1.1	Downloading GRL_binary
GRL_binary can be downloaded https://github.com/YuxinSong-prog/GRL_binary. It can be installed as a regular R package.
## 1.2	Installing GRL_binary
GRL_binary links to R packages Rcpp, RcppEigen and RcppArmadillo, and also imports R packages BEDMatrix and data.table. These dependencies should be installed before installing GRL_binary. In addition, GRL_binary requires a recompiled PLINK2.0 Software (http://www.cog-genomics.org/plink/2.0/) with name “plinkoffset” under your run directory. Here is an example for installing GRL_binary and all its dependencies in an R session(assuming none of the R packages other than the default has been installed):
install.packages(c("BEDMatrix ", " data.table ", "Rcpp", " RcppEigen ", " RcppArmadillo "), repos = "https://cran.r-project.org/")
system(“R CMD install GRLbinary_1.0.tgz”)
## 2. Input
GRL_binary requires the phenotype and genotype files in an PLINK BED data frame which also called PLINK 1 binary file and the structure of these files is described in http://www.cog-genomics.org/plink/1.9/formats#bed. How to prepare these data are describe below.
## 2.1 Phenotype
Phenotype should place in the sixth column of “.fam” file. The missing phenotype value for quantitative traits is -9.
## 2.2 Genotypes
GRL_binary can only take genotype files in “.bed” and “.bim” format.
## 3. Running GRL_binary
If GRL has been successfully installed, you can load it in an R session using:
```
library(GRLbinary)
```
and then loading "BEDMatrix "and " data.table " 
```
library(BEDMatrix)
library(data.table)
```
We provide three functions in GRL_binary: Data function for basic data management including extract phenotypic values, sampling markers, calculate allele frequencies and calculating GRM, saved in an external file, used for GBLUP method or the transformed GRM for large scale dataset; Grammar_binary function for estimating heritability(optional), estimating breading values, association tests using Grammar method and Grl_binary function for adjust statistics using lambda, joint analysis based on the results of Grammar-Lambda, and outputting association result file then drawing Q-Q and Manhattan plot .
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
logicals. If FLASE, entire markers will be used to calculate GRM. If this is unset or for large scale dataset, the “msampling” default is TURE.
Here we provide two simple examples of data management for GRL using Data.
## 3.2 Grammar function
#### Usage
```
Grammar_binary (Data, Estimateh2, prevenlence)
```
#### Arguments
#### Data
An object class of list from the 1st step.
#### Estimateh2 
logicals. If TURE, heritability will be estimated and the estimate would be used for estimating breeding value. If this is unset or for large scale dataset, a moderate heritability is set by default at 0.5.
#### Prevalence 
Takes effect only when heritability is estimated.
## 3.3 GRL_binary
#### Usage
```
Grl_binary (Grammar, Test, QQ,Manh)
```
#### Arguments
#### Grammar  
An object class of list from the 2st step.
#### Test   
An optional for association test, a test at once or joint analysis. You can choose “Separate” for a test at once and “Joint” for further joint analysis based on the result of “Separate”.
#### QQ   
logicals. If TURE, Q-Q plot would be drawn.
#### Manh   
logicals. If TURE, Q-Q plot would be drawn.
