# A reproducible workflow for identifying and predicting broiler gut microbiota developmental stages using Dirichlet Multinomial Mixture (DMM) modelling.

This repository gives example code on how to predict the git microbiota (GM) maturation stage of broiler caecum samples, as was used in Cleiren *et al.* (https://doi.org/10.21203/rs.3.rs-11229652/v1). 

## Data

Two longitudinal datasets of the caecal microbiota (16S rRNA gene amplicon sequencing) are included.

**Reference dataset**

The reference dataset contains caecal 16S rRNA gene amplicon sequencing data from Ross 308 broilers sampled between 2 and 29 days post-hatch. This is the main dataset used by Cleiren *et al.* to identify GM developmental stages.

**Early feeding dataset**

The early feeding dataset contains caecal 16S rRNA gene amplicon sequencing data from two broiler breeds: Ross 308 and Hubbard Redbro. Two feeding groups are included: 

- **Early fed (EF):** immediate access to feed and water after hatch.
- **Delayed fed (DF):** 48-hour feed and water deprivation after hatch. 

The datasets are provided as:

- **Metadata:** sample information, including bird age, breed and treatment group.
- **ASV abundance table:** read counts per ASV after preprocessing.
- **Taxonomy table:** taxonomic classification of each ASV.
- **Representative sequences:** nucleotide sequences of the ASVs

Raw sequencing reads are not included, but can be downloaded from NCBI SRA under BioProject PRJNA1520313 (reference dataset) and PRJNA1520349 (early feeding dataset). The workflow starts from processed ASV tables.

## Requirements for combining datasets

When combining microbiome datasets or applying an existing DMM model to new samples, consistency in the laboratory and bioinformatics workflows is essential.

**DNA extraction and library preparation**

New datasets should be generated using the same DNA extraction protocol and 16S rRNA gene target region and primer pair as the reference dataset. The library preparation protocol should also be consistent.

Differences in these procedures can introduce technical variation that affects the observed microbial community composition and may compromise comparisons between datasets.

**Taxonomic classification**

All datasets must be classified using the same reference taxonomy database and version. The datasets in this repository were classified using SILVA v138.2.

If a different taxonomy database or version is used, taxonomy should be reassigned consistently across all datasets before genus-level abundance tables are generated.

Representative ASV sequences are provided to allow taxonomic reassignment when needed.

**Abundance data**

DMM modelling is performed on genus-level abundance count data. Therefore, ASV tables must be aggregated to the genus level using consistent taxonomic assignments and filtering criteria.

For prediction using an existing model, the genus-level abundance table of the new samples must contain the same genera, in the same order, as the dataset used to train the model. Genera absent from the new dataset should be represented by zero counts.

Example code on how to achieve this is included in the provided scripts.

## Scripts

The code is written in R and provided as R Markdown files. Before running the scripts, set the working directory to the repository location.

Two scripts are provided:

1. **01_reference_DMM.Rmd**: Demonstrates how to perform DMM modeling on a dataset. The reference dataset is used as an example to identify GM maturation stages. 

2. **02_AddSamplesToRef_DMM.Rmd**: Demonstrates two approaches for incorporating new samples into a reference framework: 
    - **Expand the reference dataset:** Add new samples to the reference dataset and refit the DMM model. This approach was used in the manuscript.
    - **Predict using an existing model:** Apply a previously trained DMM model to new samples to predict their GM maturation stage, without refitting the model.

## Results

Example output is shown in the `results` folder.

![Reference dataset GM maturation stages](./results/reference/Bubble_ref_DMM.png)

*Graphic representation of the microbiota maturation over time. Nodes are ordered based on age of the birds and labelled to include the number of samples per timepoint allocated to each GM maturation stage.*