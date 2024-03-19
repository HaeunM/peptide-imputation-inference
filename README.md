# peptide-imputation-inference

This repository contains codes associated with the paper [AUGMENTED DOUBLY ROBUST POST-IMPUTATION INFERENCE FOR PROTEOMIC DATA]. 

## General pipeline

A full pipeline for least suare inference for proteomic data with missingness is provided in [`pipeline_peptide_post_imputation_inference.Rmd`].

This pipeline can be applied to a custom dataset, provided that it conforms to the following format:

- `raw.pep`: high-dimensional peptide data outcome with missing values. (A matrix #observations x #peptides)
- `covariate`: A low-dimensional covariate without missing values. (A data frame #observations x #covariates)
- `missing_pattern`: A missing pattern of `raw.pep`. Either `MAR` or `MCAR`.

## VAEIT 

The method involves regressing each column of `raw.pep` on both the `covariate` and the other peptides as the high-dimensional auxiliary variables. An addi-
tional challenge is that each column of Y has many missing entries, even when used as a covariate in the regression problem. To address this, we use variational auto-encoder,
a deep neural network tool that allows for flexible input and simultaneous estimation of the multi-response regression. Our pipeline uses an algorithm called `scVAEIT' that is designed for addressing the specific structures of single cell data. We use this algorithm both for single-cell and bulk-cell applications. 

A code for `scVAEIT` can be found on a repository jaydu1/scVAEIT. We recommend downloading the newest version of the code from the repository. Here, we provide version v0.2.0, which was used for the analysis in the paper. Additionally, we provide an R wrapper function `R_wrapper_VAE.R`, written by Jin-Hong Du. Both `scVAEIT` and `R_wrapper_VAE.R` should be located in the same folder to make the pipeline code work.

The use of `scVAEIT` also requires setting up dependencies for python packages. Terminal code written by Jin-Hong Du is provided for this setup (see `setup_dependency.txt`).

## Reproducibility materials

We provides codes for reproducing the results presented in the paper.  

A folder `scpdata` contains codes for reproducing the result in Section 4. The data used for this analsysis is the single-cell proteomic data measured by leduc, and can be downloaded from a bioconductor packages `scpdata`. A file `scpdata_reproduce_figures.Rmd` reproduce figures in the main text and the supplementary material. A file `scpdata_reproduce_main_results.Rmd` reproduce the peptide discovery results. A file `scpdata_reproduce_realistic_simulation1.Rmd` and `scpdata_reproduce_realistic_simulation2.Rmd` reproduce the realistic simulation result presented in Section 4.1.

A folder `ADdata` contains codes and data for reproducing the result in Section 5. The data used for this analsysis is the bulk-cell data related to Alzheimer's Diseases. The file `meta.csv' was downloaded from 
https://panoramaweb.org/Panorama%20Public/2022/MacCoss%20-%20Human%20AD%20Clean%20Diagnosis%20DIA%20Data/SMTG/wiki-page.view?name=SMTG%20Metadata. Other files for peptide data on each brain region was downloaded from
https://panoramaweb.org/Panorama%20Public/2022/MacCoss%20-%20Human%20AD%20Clean%20Diagnosis%20DIA%20Data/project-begin.view
with a selection of Level3A. 

For running the codes, both 'scVAEIT' and 'R_wrapper_VAE.R' should be located in the same folder to make the reproducing codes work.



