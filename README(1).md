This repository has scripts for specific single cell/single nuclei RNA-seq analyses. Below is more specific information about the types of analyses, why we use them and links to the original repositories for each tool. 

Here is the flow of how I would use these tools 

Pre-workflow (Removal of ambient RNA)

Resource link (SoupX): https://github.com/constantAmateur/SoupX

"SoupX is an R package for the estimation and removal of cell free mRNA contamination in droplet based single cell RNA-seq data. The problem this package attempts to solve is that all droplet based single cell RNA-seq experiments also capture ambient mRNAs present in the input solution along with cell specific mRNAs of interest. This contamination is ubiquitous and can vary hugely between experiments (2% - 50%), although around 10% seems reasonably common. There's no way to know in advance what the contamination is in an experiment, although solid tumours and low-viability cells tend to produce higher contamination fractions. As the source of the contaminating mRNAs is lysed cells in the input solution, the profile of the contamination is experiment specific and produces a batch effect. Even if you decide you don't want to use the SoupX correction methods for whatever reason, you should at least want to know how contaminated your data are."

(1) Seurat workflow

Resource link (Seurat): https://satijalab.org/seurat/articles/get_started.html

Resource link (Harmony): https://portals.broadinstitute.org/harmony/articles/quickstart.html



This will walk you through example code from your processed cellranger file and through seurat clustering, cell type identification, batch correction and even ambient RNA removal if necessary. This code is specific to the 73 sample human postmortem dlPFC experiment but generally follows the Sajita Lab Seurat Workflow in addition to the use of two additional tools for batch correction (Harmony) and ambient RNA removal (SoupX). All these resource links are posted above and provide example code to follow for your specific experiment. The output of your Seurat workflow will be a Seurat object with stored metadata information containing anything from your study (i.e. drinking age, consumption, sex, etc.) and cell type classification data that you have generated from this analysis. The cell type identification for clusters is accomplished by both scType (https://cran.r-project.org/web/packages/scSorter/vignettes/scSorter.html) and scSorter (https://cran.r-project.org/web/packages/scSorter/vignettes/scSorter.html). The subsequent analyses below sometimes require interoperability conversions which is why there is a separte resource in this reposity for example conversions. 


(2) Interoperability conversions to/from Seurat Objects 

Resource linK: https://satijalab.org/seurat/archive/v3.1/conversion_vignette.html

This is a useful resource for converting to/from Seurat Objects as required by some downstream analyses 


(3) Pseudobulking with Libra 

Resource link: https://github.com/neurorestore/Libra

Libra is an R package to perform differential expression on single-cell data. Libra implements a total of 22 unique differential expression methods that can all be accessed from one function. These methods encompass traditional single-cell methods as well as methods accounting for biological replicate including pseudobulk and mixed model methods. The code for this package has been largely inspired by the Seurat and Muscat packages. Please see the documentation of these packages for further information.

The main function of Libra, run_de, takes as input a preprocessed features-by-cells (e.g., genes-by-cells for scRNA-seq) matrix, and a data frame containing metadata associated with each cell, minimally including the cell type annotations, replicates, and sample labels to be predicted. This means that in order to use Libra, you should have pre-processed your data (e.g., by read alignment and cell type assignment for scRNA-seq) across all experimental conditions.


(4) Pseudotime with monocle3

Resource link: https://cole-trapnell-lab.github.io/monocle3/docs/trajectories/

Single-cell transcriptome sequencing (sc-RNA-seq) experiments allow us to discover new cell types and help us understand how they arise in development. The Monocle 3 package provides a toolkit for analyzing single-cell gene expression experiments.

Monocle 3 can help you perform three main types of analysis:
(a) Clustering, classifying, and counting cells. Single-cell RNA-Seq experiments allow you to discover new (and possibly rare) subtypes of cells. Monocle 3 helps you identify them.

(b) Constructing single-cell trajectories. In development, disease, and throughout life, cells transition from one state to another. Monocle 3 helps you discover these transitions.

(c) Differential expression analysis. Characterizing new cell types and states begins with comparisons to other, better understood cells. Monocle 3 includes a sophisticated, but easy-to-use system for differential expression.

Specifically, Monocle introduced the strategy of using RNA-Seq for single-cell trajectory analysis. Rather than purifying cells into discrete states experimentally, Monocle uses an algorithm to learn the sequence of gene expression changes each cell must go through as part of a dynamic biological process. Once it has learned the overall "trajectory" of gene expression changes, Monocle can place each cell at its proper position in the trajectory. You can then use Monocle's differential analysis toolkit to find genes regulated over the course of the trajectory, as described in the section Finding genes that change as a function of pseudotime . If there are multiple outcomes for the process, Monocle will reconstruct a "branched" trajectory. These branches correspond to cellular "decisions", and Monocle provides powerful tools for identifying the genes affected by them and involved in making them. You can see how to analyze branches in the section Analyzing branches in single-cell trajectories.

(5) RNA velocity 

Resource link: https://github.com/velocyto-team/velocyto.R

Velocyto is a library for the analysis of RNA velocity. It includes a command line tool and an analysis pipeline. RNA velocity is the time derivative of the gene expression state-can be directly estimated by distinguishing between unspliced and spliced mRNAs in common single-cell RNA sequencing protocols. RNA velocity is a high-dimensional vector that predicts the future state of individual cells on a timescale of hours. This tool has mainly been used in developmental studies but it as of yet unused in postmortem tissue. 


