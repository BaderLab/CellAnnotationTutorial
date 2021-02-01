# Annotating single cell transcriptomic maps using automated and manual methods

Single-cell transcriptomics can profile thousands of cells in a single experiment and identify novel cell types, states and dynamics in a wide range of tissues and organisms. Standard experimental protocols and analysis workflows have been developed to create single-cell transcriptomic maps from tissues. This tutorial focuses on how to interpret these data to identify cell types, states and other biologically relevant patterns with the objective of creating an annotated map of cells.

In the written tutorial, we recommend a three step workflow including automatic cell annotation tools, manual cell annotation and verification. Frequently encountered challenges and strategies to address them are discussed. Guiding principles and specific recommendations for software tools and resources that can be used for each step are covered.

## Accompanying code

To make recommendations by the tutorial more accessible, we have provided an R Notebook that guides the user through specific tools. Realistically, every single-cell map annotation case will be different and will likely not require the usage of all of these tools. For the purposes of this tutorial, the tools make use of publicly available available data and cover reference- and marker-based automatic annotation, manual annotation, and how to build a consensus set of cluster annotations. The R Notebook file can be downloaded and run on your own RStudio system. This will allow you to run through the steps interactively and at your own pace, with a full run of the file also creating a human-readable HTML file on your system.

## Installation instructions

This code has been successfully run using `R 4.0.2` and the following packages:
```
SingleCellExperiment_1.11.7*
Seurat_3.2.1
scater_1.17.5*
SCINA_1.2.0
dplyr_1.0.2*
scmap_1.11.0*
celldex_0.99.1*
SingleR_1.3.8*
ggplot2_3.3.2
harmony_1.0*
cerebroApp_1.2.2*
msigdb_0.2.0
```
Further testing has been done with `R 4.0.3`, for which Harmony is unfortunately not available. 

If you haven't yet installed R on your system, you can install R at https://cran.r-project.org/ and R Studio at https://rstudio.com/products/rstudio/download/.

Packages can be installed with `install.packages("package")`. Packages with * must be installed using BiocManager by running `BiocManager::install("package")` instead of `install.packages("package")`. msigdb can be installed directly from Github using the package `devtools`: `devtools::install_github("mw201608/msigdb")`.

This tutorial takes advantage of open source data, and requires the downloaded folders to be in certain relative file paths to the code in order for it to be read in properly. The "query dataset" that we are annotating is available from 10X Genomics at https://cf.10xgenomics.com/samples/cell-exp/1.1.0/pbmc3k/pbmc3k_filtered_gene_bc_matrices.tar.gz. Clicking on the link will automatically download the data. Move the downloaded zipped file to the same directory that the R Notebook code is in (`CodingBlocks.rmd`) and unzip it there. The data we are using will now be in the relative file path: `./filtered_gene_bc_matrices/hg19/`. An alternative is to use wget or curl on the command line in the same directory as `CodingBlocks.rmd`.

Mac or Linux:
```
wget https://cf.10xgenomics.com/samples/cell-exp/1.1.0/pbmc3k/pbmc3k_filtered_gene_bc_matrices.tar.gz
tar -xvzf pbmc3k_filtered_gene_bc_matrices.tar.gz
```

Windows:

```
curl.exe -o pbmc3k_filtered_gene_bc_matrices.tar.gz
tar -xvzf pbmc3k_filtered_gene_bc_matrices.tar.gz
```

For marker-based automatic annotation, a list of marker genes is available from [Diaz-Mejia JJ et al.](https://zenodo.org/record/3369934#.X2PWty2z1QI) at `https://zenodo.org/record/3369934/files/pbmc_22_10x.tar.bz2`. The data can be gathered directly by downloading and extracting the pbmc_22_10x.tar.bz2 file in the same directory as `CodingBlocks.rmd`. Alternatively, this can also be done on the command line.

Mac or Linux:
```
wget https://zenodo.org/record/3369934/files/pbmc_22_10x.tar.bz2
tar -xvjf pbmc_22_10x.tar.bz2
```
Windows:
```
curl.exe -o pbmc_22_10x.tar.bz2 https://zenodo.org/record/3369934/files/pbmc_22_10x.tar.bz2
```
For Windows, the bz2 compression may require the installation of additional software such as [7-zip](https://www.7-zip.org/).

The extracted data will by located in the following relative file path:
```
./MY_PAPER/SUPPLEMENTARY_DATA/pbmc_22_10x/pbmc_22_10x_cell_type_signature_gene_sets.gmt
```
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
