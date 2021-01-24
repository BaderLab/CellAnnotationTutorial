# Annotating single cell transcriptomic maps using automated and manual methods

Single-cell transcriptomics can profile thousands of cells in a single experiment and identify novel cell types, states and dynamics in a wide range of tissues and organisms. Standard experimental protocols and analysis workflows have been developed to create single-cell transcriptomic maps from tissues. This tutorial focuses on how to interpret these data to identify cell types, states and other biologically relevant patterns with the objective of creating an annotated map of cells.

In the written tutorial, we recommend a three step workflow including automatic cell annotation tools, manual cell annotation and verification. Frequently encountered challenges and strategies to address them are discussed. Guiding principles and specific recommendations for software tools and resources that can be used for each step are covered.

## Accompanying code

To make recommendations by the tutorial more accessible, we have provided an R Notebook that guides the user through specific tools. The tools make use of publicly available available data and cover reference- and marker-based automatic annotation, manual annotation, and how to build a consensus set of cluster annotations. The R Notebook file can be downloaded and run on your own RStudio system. This will allow you to run through the steps interactively and at your own pace, with a full run of the file also creating a human-readable HTML file on your system. Installation requirements for the code to be fully functional are listed at the beginning of the R Notebook.

In this tutorial, many different methods are described in detail to allow the user to see what is possible with these tools. Every single-cell map annotation case will be different and will likely not require the usage of all of these tools. Although some of the downstream code cannot be run without the upstream code, we recommend that users focus on the chunk that is likely to be applicable to their scenario. For example, it would make sense for the user to focus less on the reference-based annotation section if no labeled reference is available for him or her to use.
