# MCL Imaging Mass Cytometry Analysis (IMC)
This repository contains all the necessary components and instructions to replicate the entire IMC analysis. Below is a detailed guide on how to set up and run the analysis pipeline, including installing dependencies and understanding the structure of the provided files and directories.

# Note
Due to the large size of the IMC data, if you are interested to reanalyse the data, please email me at: sunandini.sharma@unmc.edu
The codeocean capsule will be also released during time of publication.

# Pipeline Overview
- For this project, we generated a Tissue Microarray (TMA) for Mantle Cell Lymphoma samples and ablated them using the Hyperion™ system. Regions of interest (ROIs) were generated as .txt files for each sample (1-3 ROIs per sample). After segmentation, we produced raw single-cell expression and nearest-neighbor datasets.

- The single-cell data for all markers was normalized using elbow detection to threshold outliers, compressing them with a hyperbolic tangent function. Batch normalization was then performed using the CyCombine R package to harmonize data from different TMAs. Data harmonization was visualized using Uniform Manifold Approximation and Projection (UMAP).

- We conducted a two-stage clustering: hierarchical clustering within samples to a high-resolution set of clusters, followed by Leiden clustering of the hierarchical clusters to phenotype single cells using markers like CD20, CD5, CCND1, SOX11, CD45, CD3, CD4, CD8, FOXP3, CD14, CD11b, CD68, CD163, CD11c, and CD31. Expert reviews annotated these phenotypes, stored in "cluster_phenotype_calling.xlsx", and linked to the expression data frame.

- Finally, we quantified cell interactions by assigning an additive proximity score based on the distance from a cell to all cells of a given phenotype within a defined pixel radius. Neighborhood profiles were generated at 25 and 50 microns, providing an interaction score for each cell.


## Directory Structure

- raw .txt files: Raw data files used as input for the analysis.
- .tiff segmentations: Segmented images used in the analysis. Note that these segmentations are included because they are not directly reproducible due to minor updates in the Mesmer package.
- samples_meta.xlsx: Metadata file containing information about the samples.
- cyCombine_batches.R: R script used for batch normalization.
- utilsimc.py: Python utility script used in the analysis.
- requirements.txt: File listing the Python dependencies required for the analysis.
- fastcluster-1.2.6-cp38-cp38-win_amd64.whl: Wheel file for the fastcluster package, required to be installed after setting up the Python environment.
- Jupyter Notebook: Documentation and steps for the analysis process, including generating diagnostic figures and batch-corrected data.

# Setup and Installation

## Step 1: Python Environment Setup
Create a new Python environment in the Linux terminal using the follwoing command

- python -m venv imc_env
- source imc_env/bin/activate
  
### Install the required Python packages:
- pip install --no-deps -r requirements.txt
- pip install fastcluster-1.2.6-cp38-cp38-win_amd64.whl

## Step 2: Running the Analysis 
Open the provided Jupyter Notebook A00 - MCL Analysis-checkpoint.ipynb in your preferred environment (Jupyter Notebook). Follow the steps documented in the notebook to run the analysis. The notebook provides detailed instructions on generating diagnostic figures and obtaining batch-corrected data.

## Step 3: Running Cycombine for Batch Normalisation in R
Having all the necessary inputs for CyCombine, we will use RStudio to run the script "cycombine_batches.R" inside the "batchnorm" directory. This will correct expression between batches and output diagnostic figures and the corrected dataset as an RDS archive, which we will re-import below.


# Notes

- Reproducibility: The segmentations provided are not directly reproducible due to minor updates in the Mesmer package. However, the included segmentations should suffice for most analysis purposes.
- Optional Re-segmentation: Reviewers can optionally re-run the entire analysis, including segmentation, if they wish to validate the results using the most recent version of the Mesmer package and other dependencies.
By following the above steps, users should be able to replicate the entire IMC analysis pipeline, starting from raw data files to obtaining batch-corrected outputs and diagnostic figures. The provided outputs in the directory can be used as references to ensure the pipeline is running correctly.
