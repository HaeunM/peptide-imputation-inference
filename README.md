# peptide-imputation-inference

This repository contains codes and pipelines associated with the article [AUGMENTED DOUBLY ROBUST POST-IMPUTATION INFERENCE FOR PROTEOMIC DATA]. 

## General use

A full pipeline for least suare inference for proteomic data with missingness is provided in [`pipeline_peptide_post_imputation_inference.Rmd`].

This pipeline can be applied to a custom dataset, provided that it conforms to the following format:

- `raw.pep`: high-dimensional peptide data outcome with missing values. (A matrix #observations x #peptides)
- `covariate`: A low-dimensional covariate without missing values. (A data frame #observations x #covariates)
- `missing_pattern`: An assumed missing pattern of `raw.pep`. Either `MAR` or `MCAR`.


## Package Dependency

The proposed method uses a variant of VAE models called VAEIT (Du et al., 2022) to fit the outcomes. The dependencies can be installed via the following commands:
