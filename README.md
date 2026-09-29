# DIABETES RISK FACTOR ANALYSIS
## Project Purpose
This project analyzes patient characteristics associated with diabetes outcomes using a diabetes outcomes using a diabetes risk factor dataset. The purpose is to demonstrate a reproducible data science workflow, including data validation, preparation, descriptive statistics, visualization, correlation analysis, inferential statistics, and logistic regression. 
The notebook is designed so that another data scientist can reproduce the analysis from the project repository without relying on the original analyst's local environment. 

---
## Analysis Overview

The analysis includes:
- Working environment setup
- Dataset validation and quality checks
- Descriptive statistics for patient characteristics
- Distribution visualizations for Glucose and BMI
- Bivariate visualizations examining: (1) Glucose by diabetes outcome and (2) Relationship between Glucose and BMI
- Spearman correlation analysis and heatmap for numerical variables
- Independent-samples t-test comparing mean Glucose between diabetes outcome groups
- Logistic regression examining the association between Glucose and diabetes outcome
- Reproducibility checks using a fixed random seed for random sampling and bootstrap estimation

---
## Dataset Source and Provenance

The project uses the file 'Example Dataset_Diabetes.csv', which is included directly in this repository. 

The dataset contains **768 observations and 9 variables** representing patient characteristics and diabetes outcome. The variables include:
- 'Pregnancies'
- 'Glucose'
- 'D_BP'
- 'Skin_Thickneww'
- 'Insulin'
- 'BMI'
- 'Pedigree'
- 'Age'
- 'Outcome'

The notebook loads the dataset directly from the project's GitHub repository using the raw CSV file URL. This helps avoid dependence on a local file path or the original analyst's computational environment.

---
## Required Software and Libraries

### Software
- Google Colab
- Git/GitHub for accessing the project repository

### Python Libraries
The notebook uses the following Python packages:
- 'pandas' - data loading, cleaning, and analysis
- 'numpy' - numerical operations
- 'matplotlib' - data visualization
- 'scipy' - statistical testing
- 'statsmodels' - logistic regression

Package versions used for this project are documented in 'requirements.txt'

---

## Setup and Installation

### Google Colab

1. Open 'Diabetes_Risk_Factor_Analysis.ipynb' in Google colab from the GitHub repository
2. Sign in Google Colab with a valid Google account
3. Ensure that the notebook has access to the internet so the dataset can be loaded from Github
4. Run the notebook cells from top to bottom by clicking on 'Run all'
5. No local copy of the CSV file is required because the notebook loads the dataset from the project's Github repository.

---
## How to Execute the Notebook

To reproduce the analysis:
1. Open 'Diabetes_Risk_Factor_Analyis.ipynb'
2. Verify the the required Python packages are installed
3. Run the notebook from the first cell through the final cell without skipping cells
4. The dataset will be loaded from the documented Github repository location
5. Review the validation checks before proceeding with the analysis
6. Continue through the descriptive, visualization, correlation, inferential, and regression analyses
7. Review the Results and Conclusions section at the end of the notebook.

---
## Expected Outputs

When the notebook is executed successfully, it should produce:
- Dataset dimensions, variable names, data types, and missing-value checks
- Summary statistics for numerical variables
- Validation checks for expected columns, duplicate observations, outcome coding, and zero values
- Histograms of Glucose and BMI
- A boxplot comparing Glucose by diabetes outcome
- A scatterplot showing the relationship between Glucose and BMI
- A Spearman correlation matrix and heatmap
- Results from an independent t-test
- Results from a logistic regression model, including the Glucose odds ratio and 95% confidence interval
- A reproducible participant sample and bootstrap estimate
- A final summary of results and limitations

---
## Assumptions and Limitations

The analysis has several important limitations:

- The analyses describe associations and do not establish causation.
- The logistic regression model examines Glucose as a predictor of the diabetes outcome and does not account for all other patient characteristics simultaneously.
- Several variables contain zero values that may not represent clinically plausible measurements, particularly Glucose, D_BP, Skin_Thickness, Insulin, and BMI. These values require consideration during data preparation.
- The dataset contains 768 observations, which may limit the generalizability of the findings to other populations.
- The analysis depends on the accuracy and completeness of the underlying dataset and its variable definitions.
- Results may change if the underlying dataset is modified.
- Random sampling procedures use a fixed random seed (random_state = 27) to ensure reproducible results.

---
## Computational Environment

The analysis was developed and tested in Google Colab using Python.
The analysis is intended to be reproducible in a Python 2.x environment with the packages and versions listed in 'requirements.txt'

For reproducibility, the notebook:
- Loads the dataset from the project's Github repository rather than a local file path
- Documents required software and Python packages
- Uses a fixed random seed for random sampling procedures
- Includes dataset validation checks before analysis
- Provides documentation throughout the notebook describing the analytical workflow and expected outputs
































