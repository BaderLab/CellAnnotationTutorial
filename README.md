# Annotating single cell transcriptomic maps using automated and manual methods

Single-cell transcriptomics can profile thousands of cells in a single experiment and identify novel cell types, states and dynamics in a wide range of tissues and organisms. Standard experimental protocols and analysis workflows have been developed to create single-cell transcriptomic maps from tissues. This tutorial focuses on how to interpret these data to identify cell types, states and other biologically relevant patterns with the objective of creating an annotated map of cells.

In the written tutorial, we recommend a three step workflow including automatic cell annotation tools, manual cell annotation and verification. Frequently encountered challenges and strategies to address them are discussed. Guiding principles and specific recommendations for software tools and resources that can be used for each step are covered.

## Accompanying code

To make recommendations by the tutorial more accessible, we have provided an R Notebook that guides the user through specific tools. Realistically, every single-cell map annotation case will be different and will likely not require the usage of all of these tools. For the purposes of this tutorial, the tools make use of publicly available available data and cover reference- and marker-based automatic annotation, manual annotation, and how to build a consensus set of cluster annotations. The R Notebook file can be downloaded and run on your own RStudio system. This will allow you to run through the steps interactively and at your own pace, with a full run of the file also creating a human-readable HTML file on your system.

## Installation instructions

This code has been successfully run using `R 4.0.3` and the following packages:
```
SingleCellExperiment_1.12.0*
Seurat_4.1.1
scater_1.18.6*
SCINA_1.2.0
devtools_2.4.3
dplyr_1.0.9*
scmap_1.12.0*
celldex_1.0.0*
SingleR_1.4.1*
ggplot2_3.3.6
Harmony_1.0**
cerebroApp_1.3.0**
msigdb_0.2.0**
```
"*" = packages must be installed by running `BiocManager::install("package")` instead of `install.packages("package")`.  
"**" = packages must be installed by from github using devtools (e.g. devtools::install_github("gitRepo/package").

If you haven't yet installed R on your system, you can install R at https://cran.r-project.org/ and R Studio at https://rstudio.com/products/rstudio/download/.

This tutorial takes advantage of open source data: The "query dataset" that we are annotating is available from 10X Genomics at https://cf.10xgenomics.com/samples/cell-exp/1.1.0/pbmc3k/pbmc3k_filtered_gene_bc_matrices.tar.gz. Additionally, for marker-based annotation
we will be using a list of marker genes from [Diaz-Mejia JJ et al.](https://zenodo.org/record/3369934#.X2PWty2z1QI). These datasets are automatically downloaded when the R code is run.

## Content

The code consists of the following sections:

1. Reference-based automatic annotation
This section annotates the query dataset using a previously labeled reference dataset. Many tools exist to do this: we are going over scmap (cell and cluster) and SingleR. We will further explore how to use integration as a form of annotation using Harmony.

2. Refining / Consensus annotations
After finding multiple cell type labels for each cell using reference-based automatic annotation, we will keep the labels that most commonly occur across methods.

3. Marker-based automatic annotation
Instead of using a reference dataset to annotate the query dataset, we will input lists of marker genes associated with specific cell types. The program we have chosen to demonstrate here is SCINA.

4. Manual annotation
Here, we extract marker genes and associated pathways from the query dataset. To determine cell-type labels from this information, we would have to compare our differentially expressed genes and pathways to those described in the literature. To facilitate this process, we use Seurat and cerebroApp.

## Timing

The associated R packages take about 5 minutes to install (R, itself, only takes a couple of minutes), and the code takes about 10 minutes to run.
