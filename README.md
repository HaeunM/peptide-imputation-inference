# peptide-imputation-inference

This repository contains codes and pipelines associated with the article [AUGMENTED DOUBLY ROBUST POST-IMPUTATION INFERENCE FOR PROTEOMIC DATA]. 

## General use

A full pipeline for least suare inference for proteomic data with missingness is provided in [`pipeline_peptide_post_imputation_inference.Rmd`].

This pipeline can be applied directly on a custom data set (the default is a simulated toy example), provided that it suits the format as follows:

- `raw.pep`: A high dimensional peptide data with missingness. A matrix `#observations x #peptides`. 
- `W`: A low-dimensional covariate without missingness `#observations x #covariates`. 

## Package Dependency

The proposed method uses a variant of VAE models called VAEIT (Du et al., 2022) to fit the outcomes. The dependencies can be installed via the following commands:
