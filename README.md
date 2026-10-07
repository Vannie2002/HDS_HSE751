# **AUTOMATED ANALYSIS PIPELINE NOTEBOOK - DIABETES PREDICTION & AUTOMATED ANALYSIS**
---
## **Project Overview**

This project explores an automated analysis pipeline using the Pima Indians Diabetes Database. The notebook demonstrates how data exploration, data cleaning, statistical analysis, and machine learning can be organized into a reproducible workflow.

The main prediction task is to classify whether a participant has diabetes based on available clinical and demographic predictors.

The project focuses on understanding how an automated analytical workflow responds to the characteristics of a dataset, rather than only building a predictive model. Throughout the notebook, we examine the data, identify potential data-quality issues, run statistical analyses, train machine learning models, and modify selected parts of the pipeline.

---
## **Dataset**

### **Pima Indians Diabetes Database**

Pima Indians Diabetes Database

The dataset contains diagnostic measurements from 768 women who are at least 21 years old and of Pima Indian heritage. The dataset is commonly used for demonstrating classification and machine learning methods.

The outcome variable is:

Outcome = 0: No Diabetes
Outcome = 1: Diabetes

The predictor variables include:

- Pregnancies	(Number of pregnancies)
- Glucose	(Plasma glucose concentration)
- Blood pressure	(Diastolic blood pressure)
- Skin thickness	
- Insulin	
- Body mass index (BMI)
- Diabetes pedigree function	
- Age	(Age in years)
- Outcome	(iabetes outcome (0/1))

The dataset is used for educational and demonstration purposes. It should not be interpreted as a clinical diagnostic dataset or used to make medical decisions.

### **Dataset Source**

The dataset is associated with the National Institute of Diabetes and Digestive and Kidney Diseases (NIDDK) and is widely distributed through machine-learning repositories and educational resources.

Because the same dataset can be downloaded from different sources, the file format and column names may differ slightly depending on where the dataset is obtained. Check the dataset before running the notebook.

---

## **How to Get and Load the Dataset**

Dataset is included in this repository, so download the dataset directly from the repository and make sure the notebook's file path points to the correct location as well as the dataset's name. 

Follow the code provided on the notebook and upload the dataset when prompted.

***Check the dataset after loading***

- Before continuing with the pipeline, check that the data loaded correctly:

print(df.shape)

print(df.columns.tolist())

df.head()

- The original dataset should contain: 768 observations, 9 variables

- If the number of rows, columns, or variable names looks different, stop and check the file before continuing.

***Column Names May Differ if you use dataset from a different source!***

Column names may not be exactly the same across different versions of the dataset.

- For example, one version may use:

Blood pressure

Skin thickness

Body mass index

while another version may use:

BloodPressure

SkinThickness

BMI

- The analysis code depends on the column names, so the variable names in the notebook need to match the actual dataset.

- You can check the names with:  df.columns.tolist()

- If your dataset uses different names, update the relevant code before running the pipeline.

---

## **Project Purpose**

The purpose of this project is to explore how a structured and automated analytical workflow can combine:

- Data ingestion
- Data-quality checks
- Missing-value identification
- Data preprocessing
- Exploratory data analysis
- Correlation analysis
- Inferential statistics
- Classification modeling
- Model evaluation
- Model tuning
- Model interpretation

The project also demonstrates how conditional logic can allow a pipeline to make analytical decisions based on the characteristics of the dataset.

The goal is not simply to run the pipeline from beginning to end. I also examine the reasoning behind each stage and modify selected components to better understand how those changes affect the analysis.

---

## **General Workflow**

1. Load data
2. Inspect dataset
3. Identify invalid/missing values
4. Clean and preprocess data
5. Exploratory data analysis
6. Correlation analysis
7. Inferential statistics
8. Configure outcome and predictors
9. Train/Test Split
10. Preprocessing pipeline
11. Train classification models
12. Evaluate model performance
13. Tune models
14. Interpret model results

---

## **Common Issues and Troubleshooting**

1. Column names not matching - Pay attention to column names if dataset is loaded from a different source.
2. NaN values - Some zero values are converted to NaN because they represent missing or physiologically implausible measurements. The machine learning pipeline later handles these missing predictors through median imputation.
3. The pipeline says predictors must be numeric - Make sure to identify non-numeric columns before working on the model.

---

## **Tools and Libraries**

This project was completed using Python in Google Colab.

Main libraries include:

- pandas — data manipulation
- numpy — numerical operations
- matplotlib — visualization
- seaborn — statistical visualization
- scipy — statistical tests
- statsmodels — statistical modeling and ANOVA
- scikit-learn — preprocessing, machine learning, model evaluation, and cross-validation
- phik — Phi-K correlation analysis

---
## **Workflow Reflection**

This assignment helped me understand how an automated data analysis and machine learning pipeline moves from raw data to model evaluation. The workflow started with examining the dataset and its descriptive statistics to understand the variables, their distributions, and the outcome variable. This was followed by data cleaning and preprocessing, including identifying values that were technically recorded as zeros but were not realistic measurements for certain clinical variables. These values were converted to missing values so they could be handled appropriately before modeling.

The next part of the workflow focused on understanding the relationships within the data through correlation analyses and visualizations. We used Pearson, Spearman, and Phi-K correlations, along with histograms, boxplots, scatterplots, violin plots, and other visualizations. These steps helped me see that exploratory data analysis (EDA) help identify unusual values, understand distributions, recognize potential relationships between predictors and the outcome, and make better decisions about how the data should be prepared for modeling.

The pipeline then moved into inferential statistics. We used one-sample and independent-samples t-tests, ANOVA, and a chi-square test to examine whether differences or associations observed in the data were statistically significant. This allowed me to better understand the difference between simply observing a pattern in the data and formally testing whether there is evidence of an association or difference.

After the exploratory and statistical analysis, the data was prepared for machine learning. The outcome was checked to make sure it was coded as 0 and 1, and non-predictor columns such as Outcome_label were removed before splitting the data. The data was then divided into training and test sets using stratification so that both sets maintained a similar distribution of the two outcome classes.

The machine learning portion began with Logistic Regression and a Decision Tree. Missing predictor values were handled using median imputation, and standardization was applied to Logistic Regression. An important lesson from this step was that preprocessing should be learned from the training data rather than the entire dataset. This helps prevent data leakage, where information from the test data unintentionally influences the model.

The models were then evaluated using several performance measures, including accuracy, recall, precision, F1 score, and ROC AUC. I learned how to interpret confusion matrices by looking at true positives, true negatives, false positives, and false negatives. This was especially useful for understanding that accuracy alone does not tell the entire story of a classification model. In a health-related prediction problem, the type of error can be just as important as the overall percentage of correct predictions.

Another important part of the workflow was adjusting the Logistic Regression classification cutoff. Instead of automatically using the default 0.50 threshold, the pipeline selected a cutoff of 0.443 using cross-validation and Youden's J statistic. This showed that model performance can depend not only on the model itself, but also on how its predicted probabilities are converted into final classifications.

Finally, the Decision Tree was tuned using GridSearchCV and stratified cross-validation. The tuning process tested different combinations of tree depth, leaf size, number of leaf nodes, and class weights. The final tree was then evaluated on the test set and visualized to better understand how it made predictions. Feature importance showed that Glucose, BMI, and Age contributed the most to the decisions made by the fitted tree.




