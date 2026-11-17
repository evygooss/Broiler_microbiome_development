# A reproducible workflow for identifying and predicting broiler gut microbiota developmental stages using Dirichlet Multinomial Mixture (DMM) modelling.

This repository gives example code on how to predict the git microbiota (GM) maturation stage of broiler caecum samples, as was used in Cleiren *et al.* (https://doi.org/10.21203/rs.3.rs-11229652/v1). 

## Data

Two longitudinal datasets of the caecum microbiota (16S) are included.

The **reference dataset** contains caecal 16S amplicon sequencing data from Ross 308 broilers at age 2 - 29 days post hatch. This is the main dataset used by Cleiren *et al.*

The **early feeding dataset** contains caecal 16S amplicon sequencing data from two breeds: Ross 308 and Hubbard Redbro. This dataset contains two groups: The Early fed (EF) group had immediate access to feed and water, the Delayed fed (DF) group had a 48h feed and water deprivation. 

Data files include:
- metadata file (metadata information per sample)
- abundance file (read count per ASV, after preprocessing as described in the paper)
- taxonomy file (per ASV, taxonomic information)
- sequence file (ASV sequences)

## Scripts

The code is written in R, in a Markdown file. Don't forget to change the working directory before you start.

Two different scripts are given:
1. **01_reference_DMM.Rmd**: Code to perform DMM modeling on a new dataset. Here we use the reference dataset as an example
2. **02_...Rmd**: Two methods to add new samples to a reference dataset are shown. 
    a. Add new samples to an existing dataset and rerun the DMM model. This method was used in the manuscript.
    b. Use a previously trained model and predict the GM maturation stage of the new samples.

## Results

![Reference dataset GM maturation stages](./results/reference/Bubble_ref_DMM.png)
