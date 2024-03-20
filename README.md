# peptide-imputation-inference

This repository contains codes associated with the paper [AUGMENTED DOUBLY ROBUST POST-IMPUTATION INFERENCE FOR PROTEOMIC DATA] by Moon et al. (2024). 

## General pipeline

A full pipeline for least square inference for proteomic data with missingness is provided in [`pipeline_peptide_post_imputation_inference.Rmd`].

This pipeline can be applied to a custom dataset, provided that it conforms to the following format:

- `raw.pep`: high-dimensional peptide data outcome with missing values. (A matrix #observations x #peptides)
- `covariate`: A low-dimensional covariate without missing values. (A data frame #observations x #covariates)
- `missing_pattern`: A missing pattern of `raw.pep`. Either `MAR` or `MCAR`.

## scVAEIT 

The method involves regressing each column of `raw.pep` on both the `covariate` and the other columns of `raw.pep`. Each column of Y has many missing entries, even when used as a covariate in the regression problem. We use an algorithm called `scVAEIT', a variant of variational auto-encoder, which is a deep neural network tool that allows for flexible input and simultaneous estimation of the multi-response regression ([Du et al. (2022)](#references)). 

Here, we provide version 0.2.0 of `scVAEIT`, which is the version used for the analysis in the paper [Moon et al. (2024)](#references). For general use, we recommend downloading the newest version of the code from the repository [jaydu1/scVAEIT](https://github.com/jaydu1/scVAEIT). We also provide an R wrapper function, `R_wrapper_VAE.R`, to compile `scVAEIT` in R. <b>Both the folder `scVAEIT` and the file `R_wrapper_VAE.R` should be located in the same directory with a pipeline code.</b>

The `scVAEIT` requires setting up the Python package dependencies. Below are the versions that are used for the analysis in the paper. 

```cmd
python                    3.9.18
scanpy                    1.1.10 
scikit-learn              1.3.2
tensorflow                2.14.0
tensorflow-probability    0.22.1
```

The dependencies can be installed via the following commands:

```cmd
mamba create --name tf python=3.9 -y
conda activate tf
mamba install -c conda-forge "tensorflow>=2.12" "tensorflow-probability>=0.12" pandas jupyter -y
mamba install -c conda-forge "scanpy>=1.9.2" matplotlib scikit-learn -y
```
If you are using `conda`, simply replace `mamba` above by `conda`.


## Reproducibility materials

We provide codes for reproducing the results presented in the paper.  

The `scpdata` folder contains codes for reproducing the result in Section 4. The data used for this analysis is the single-cell proteomic data measured by [Leduc et al. (2022)](#references), and can be downloaded from a Bioconductor package `scpdata`. A file `scpdata_reproduce_figures.Rmd` reproduces figures in the main text and the supplementary material. A file `scpdata_reproduce_main_results.Rmd` reproduces the peptide discovery results. A file `scpdata_reproduce_realistic_simulation1.Rmd` and `scpdata_reproduce_realistic_simulation2.Rmd` reproduce the realistic simulation result presented in Section 4.1.

The `ADdata` folder contains codes and data for reproducing the result in Section 5. The data used for this analysis is the bulk-cell brain data related to Alzheimer's Disease. The file `meta.csv` was downloaded from [url](https://panoramaweb.org/Panorama%20Public/2022/MacCoss%20-%20Human%20AD%20Clean%20Diagnosis%20DIA%20Data/SMTG/wiki-page.view?name=SMTG%20Metadata). Four other files for peptide data on each brain region can be downloaded from [url](https://panoramaweb.org/Panorama%20Public/2022/MacCoss%20-%20Human%20AD%20Clean%20Diagnosis%20DIA%20Data/project-begin.view) with a selection of Level3A.

For running the codes, both 'scVAEIT' and 'R_wrapper_VAE.R' should be located in the same directory.

## References

- Moon, Haeun, Du, Jin-Hong, Lei, Jing, and Roeder, Kathryn. 2024. "Augmented doubly robust post-imputation inference for proteomic data" Arxiv
- Du, Jin-Hong, Cai, Zhanrui, and Roeder, Kathryn. 2022. "Robust probabilistic modeling for single-cell multimodal mosaic integration and imputation via scVAEIT" Proceedings of the National Academy of Sciences, 119(49)
- Leduc, Andrew and Huffman, R Gray and Cantlon, Joshua and Khan, Saad and Slavov, Nikolai. 2022. "Exploring functional protein covariation across single cells using nPOP", Genome Biology, 23(1)



