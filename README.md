# MCL_IMC_Analysis
This repository contains all the necessary components and instructions to replicate the entire IMC analysis. Below is a detailed guide on how to set up and run the analysis pipeline, including installing dependencies and understanding the structure of the provided files and directories.

Directory Structure

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
- source imc_env/bin/activate  # On Windows use `imc_env\Scripts\activate`

### Install the required Python packages:
pip install --no-deps -r requirements.txt

### Install the fastcluster package:
pip install fastcluster-1.2.6-cp38-cp38-win_amd64.whl

## Step 2: Running the Analysis
Open the provided Jupyter Notebook A00 - MCL Analysis-checkpoint.ipynb in your preferred environment (e.g., JupyterLab, Jupyter Notebook). Follow the steps documented in the notebook to run the analysis. The notebook provides detailed instructions on generating diagnostic figures and obtaining batch-corrected data.

## Step 3: Running Cycombine for Batch Normalisation in R
Having all the necessary inputs for CyCombine, we will use RStudio to run the script "cycombine_batches.R" inside the "batchnorm" directory. This will correct expression between batches and output diagnostic figures and the corrected dataset as an RDS archive, which we will re-import below.


# Notes

- Reproducibility: The segmentations provided are not directly reproducible due to minor updates in the Mesmer package. However, the included segmentations should suffice for most analysis purposes.
- Optional Re-segmentation: Reviewers can optionally re-run the entire analysis, including segmentation, if they wish to validate the results using the most recent version of the Mesmer package and other dependencies.
By following the above steps, users should be able to replicate the entire IMC analysis pipeline, starting from raw data files to obtaining batch-corrected outputs and diagnostic figures. The provided outputs in the directory can be used as references to ensure the pipeline is running correctly.
