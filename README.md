# peptide-imputation-inference

This repository contains codes and pipelines associated with the article [AUGMENTED DOUBLY ROBUST POST-IMPUTATION INFERENCE FOR PROTEOMIC DATA]. 

## General use

A full pipeline for least suare inference for proteomic data with missingness is provided in [`pipeline_peptide_post_imputation_inference.Rmd`].

This pipeline can be applied directly on a custom data set (the default is a simulated toy example), provided that it suits the format as follows:

- `X.na`: confounders. A data.frame of size `#observations x #covariates`. With or without missing values.
- `W`: treatment assignment. A binary vector coded either with `{0,1}` or with `{FALSE,TRUE}` (representing `{control,treatment}`). Without missing values.
- `Y`: observed outcome. A numerical or binary vector (if binary, then coded with `{0,1}`). Without missing values.

