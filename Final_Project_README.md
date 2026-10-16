# **FINAL PROJECT - Vannie Nguyen**

# **Predicting Cost-Related Delays in Medical Care Using MEPS 2023**

## **Project Overview**

This project examines whether health insurance coverage, poverty category, demographic characteristics, and health-related factors can help predict whether adults delay medical care because of cost.

Using the 2023 Medical Expenditure Panel Survey (MEPS), we developed and compared two supervised machine learning classification models: logistic regression and random forest. We evaluated their performance with multiple metrics because the outcome was imbalanced, with relatively few respondents reporting delayed medical care due to cost.

This project was completed for HSE751: Programming for Health Data Science as part of the Dartmouth College MS in Health Data Science program.

## **Research Question**

Can health insurance status, income, and selected demographic and health characteristics predict whether an adult delays medical care because of cost?

## **Data Selection**

**Dataset**: 2023 Medical Expenditure Panel Survey (MEPS) Full-Year Consolidated Data File (HC-251)

**Source**: Agency for HealthcareResearch and Quality (AHRQ), Medical Expenditure Panel Survey (MEPS)

**Source URL**: https://meps.ahrq.gov/mepsweb/data_stats/download_data_files_detail.jsp?cboPufNumber=HC-251

**Note for downloading the dataset**: The raw dataset is not included in this repository because of its file size. Download the data as 'MEPS2023'
1. Visit the official MEPS HC-251 download page:
   https://meps.ahrq.gov/mepsweb/data_stats/download_data_files_detail.jsp?cboPufNumber=HC-251

2. Under the **Data File, XLSX format** option, download the **ZIP**
   file.

3. Extract/unzip the downloaded file.

4. Rename the extracted Excel file to:
   `MEPS2023.xlsx`

5. Upload `MEPS2023.xlsx` when prompted by the Google Colab notebook.
The notebook expects the dataset to be named `MEPS2023.xlsx`.

Please allow approximately 10 minutes for the dataset to fully load in Google Colab. Loading time may vary depending on your internet connection and Colab's available resources.

## How to Run the Project - Run Locally

1. Clone the repository.
2. Download and prepare the MEPS dataset as described above.
3. Install the required Python libraries.
4. Update the notebook's dataset path to point to your local copy of `MEPS2023.xlsx`.
5. Run the notebook using Jupyter Notebook, JupyterLab, or another compatible environment.

## Requirements

The project uses Python and the following libraries:

- `pandas` — data manipulation and analysis
- `numpy` — numerical operations
- `matplotlib` — data visualization
- `seaborn` — exploratory visualization
- `scikit-learn` — preprocessing, model training, and evaluation
- `openpyxl` — reading Excel workbooks

## Reproducibility

To improve reproducibility, the project uses:

- A fixed random seed (`random_state=42`) for the train-test split and model settings where applicable.
- Stratified train-test splitting to preserve the outcome proportions.
- Scikit-learn pipelines to combine preprocessing and model training.
- Training data to fit preprocessing transformations before applying them to the test data.
- The same testing dataset for comparing both models.

Model results may vary slightly across software versions or changes to the dataset, preprocessing, or model configuration.

---

The dataset selected for this project is the 2023 Medical Expenditure Panel Survey (MEPS) Full-Year Consolidated Data File (HC-251) from the Agency for Healthcare Research and Quality (AHRQ). MEPS is a nationally representative survey of the U.S. civilian noninstitutionalized population and contains information on healthcare access, utilization, health insurance, health stauts, demographics, income, and healthcare expenditures. The 2023 Full-Year Consolidated File contains data from 2023 and includes respondents from MEPS Panels 27 and 28.

This dataset was selected because it aligns closely with my academic and professional interests in healthcare access, health disparities, and health data. Satisfying the required criteria, this dataset provides an appropriate binary outcome for examining whether demographic, socioeconomic, and health-related characteristics can be used to predict delayed medical care.

The dataset satisfies the required criteria, including:
- *Binary classification*: The target variable can be recorded into a binary outcome where respondents who reported delaying medical care because of cost are coded as 1 and those who did not are coded as 0.

- *Minimum of 200 observations*: The detaset contains 18,919 observations, which is substantially greater than the required minimum of 300 observations.

- *Minimum of 10 predictor variables*: The MEPS Full-Year Consolidated File contains 1,374 variables in the version used for this project, providing substantially more than the required minimum of 10 potential predictor variables. Candidate predictors for this project include health insurance coverage, income/poverty category, age, sex, health status, and potentially health-related characteristics.

- *Alignment with academic interests*: MEPS provides data related to healthcare access and utilization, which aligns with my interests in public health, healthcare data science, and understanding factors associated with barriers to healthcare.

---

## Research Variables

### Target Variable

The target variable is `DLAYCA42`, which identifies whether a respondent delayed medical care because of cost.

| Original value | Meaning | Modeling value |
|---|---|---|
| 1 | Yes, delayed care due to cost | 1 |
| 2 | No, did not delay care due to cost | 0 |
| -1, -7, -8 | Inapplicable, refused, or don't know/not ascertained | Excluded from the valid target sample |

The analysis focuses on adults aged 18 and older with valid target responses.

### Predictor Variables

The project uses the following 11 predictors:

| Variable | Description |
|---|---|
| `INSCOV23` | Health insurance coverage |
| `POVCAT23` | Poverty category |
| `AGE23X` | Age |
| `SEX` | Sex |
| `RACETHX` | Race and ethnicity |
| `EDUCYR` | Years of education |
| `EMPST53H` | Employment status |
| `MARRY23X` | Marital status |
| `RTHLTH53` | Self-reported physical health |
| `MNHLTH53` | Self-reported mental health |
| `DIABDX_M18` | Diabetes diagnosis indicator |

Variable definitions and coding should be checked against the official MEPS codebook and documentation.

## Project Workflow

The notebook follows a reproducible machine learning workflow:

1. **Dataset exploration:** Load the dataset and examine its structure, variables, and descriptive statistics.
2. **Data quality assessment:** Identify missing values, special codes, and potential data quality issues.
3. **Exploratory data visualization:** Examine patterns in delayed care by insurance coverage and age.
4. **Inferential statistics:** Use chi-square tests, a Welch independent-samples t-test, and one-way ANOVA to explore associations and group differences.
5. **Data cleaning and preprocessing:** Restrict the analysis to adults with valid target responses, recode the target, handle applicable special codes, impute missing predictor values, scale numeric features, and encode categorical features.
6. **Train-test split:** Divide the data into training and testing sets using an 80/20 split and stratification to preserve the outcome proportions.
7. **Model training:** Train logistic regression and random forest models using preprocessing pipelines and class weighting.
8. **Model evaluation:** Compare accuracy, precision, recall, F1-score, ROC-AUC, and confusion matrices.
9. **ROC curve analysis:** Compare model discrimination across classification thresholds.
10. **Classification threshold analysis:** Examine how different probability thresholds affect precision, recall, and F1-score for logistic regression.
11. **Feature importance:** Visualize the top 15 random forest features.
12. **Conclusion and limitations:** Summarize the findings and discuss limitations and potential improvements.

## Pipeline Enhancements

**Enhancement 1 - Reusable descriptive summary function**

Repeated frequency and percentage calculations were combined into a reusable function that summarizes categorical variables. This reduces duplicated code, improves notebook organization, and allows additional variables to be analyzed by simple adding them to the variable list.

**Enhancement 2: Automatically assess class imbalance**

An automated check was added to evaluate the distribution of the target classes and flag substantial class imbalance. This was implemented because only 6.2% of valid respondents reported delaying medical care due to cost. The enhancement helps inform the model evaluation strategy by indicating that accuracy alone may not adequately describe model performance.

**Enhancement 3: MEPS-specific data cleaning**

We inspected predictors for MEPS special response codes and converted invalud response codes such as -7, -8, and applicable -1 values into missing values. The standard missing-value checks did not detect these numeric codes, which could otherwise be incorrectly treated as meaningful data. This step makes data cleaning more appropriate for the MEPS dataset while preserving valid values such as 0 years of education and employment category 34.

**Enhancement 4: Stratified, reproducible train-test split**

We split the 15,000 observations into 12,000 training and 3,000 testing observations using stratify=y and random_state=42. Only 7.25% of adults reported delaying care, so the outcome distribution needed to be preserved across the two sets. This step supports reproducible evaluation and helps ensure that both sets contain a similar proportion of delayed-care cases.

**Enhancement 5: Reusable preprocessing pipeline**

We created reusable scikit-learn pipelines for median imputation and standardization of numeric predictors, plus most-frequent imputation and one-hot encoding of categorical predictors. The variables have different data types and include missing values, so this step automates preprocessing consistently for both models and fits transformations on training data rather than the full dataset, helping prevent data leakage.

**Enhancement 6: Class-weighted model training**

We set class_weight="balanced" in logistic regression and random forest. The outcome is imbalanced, with far fewer delayed-care cases than non-delayed-care cases. This step gives the minority class more weight during training so the models have an incentive to identify delayed-care cases. The results show that this alone did not eliminate the difficulty of predicting the minority class.

**Enhancement 7: Multiple-metric model evaluation**

We compared accuracy, precision, recall, F1-score, ROC-AUC, and confusion matrices for both models. Accuracy can be misleading when the outcome is imbalanced, so this step provides a more complete assessment of model performance. For example, random forest achieved 91.8% accuracy but only 6.4% recall, while logistic regression achieved 65.6% recall.

**Enhancement 8: ROC curve visualization**

We added ROC curves to compare model discrimination across classfication thresholds. A single classification threshold does not show the full trade-off between true-positive and false-positive rates. This makes the comparison more interpretable and shows that logistic regression had a higher ROC-AUC (0.712) than random forest (0.668).



## Key Findings

The final modeling dataset contained **15,000 adults** with valid target responses.

- **Delayed medical care due to cost:** 1,088 respondents (7.25%).
- **No reported delay:** 13,912 respondents (92.75%).

### Model Comparison

| Metric | Logistic Regression | Random Forest |
|---|---:|---:|
| Accuracy | 67.6% | 91.8% |
| Precision | 13.8% | 25.0% |
| Recall | 65.6% | 6.4% |
| F1-score | 0.227 | 0.102 |
| ROC-AUC | 0.712 | 0.668 |

Logistic regression was more effective at identifying respondents who reported delaying medical care due to cost. Although random forest achieved higher accuracy, it identified very few actual delayed-care cases. This illustrates why accuracy alone can be misleading when predicting an imbalanced outcome.

The random forest feature importance analysis ranked age and years of education as the two most important individual features. These scores reflect the model's use of the predictors and should not be interpreted as evidence of causation or the direction of an association.

### Classification Threshold Analysis

We also explored four logistic regression classification thresholds:

- **0.30:** Highest recall (90.4%), but low precision (8.8%).
- **0.40:** Recall of 79.4% and precision of 10.7%.
- **0.50:** Recall of 65.6% and precision of 13.8%.
- **0.60:** Highest F1-score among the tested thresholds (0.239) and precision of 16.0%, with recall decreasing to 46.8%.

These results demonstrate the trade-off between identifying more delayed-care cases and limiting false-positive predictions. The threshold comparison was exploratory because the thresholds were evaluated using the test set.


## Limitations

Several limitations should be considered:

1. **Class imbalance:** Only 7.25% of the modeling sample reported delaying medical care due to cost.
2. **Limited predictors:** The selected variables do not capture every factor that may influence delayed medical care.
3. **Survey design:** The analysis uses standard, unweighted statistical and machine learning methods and does not fully account for the complex MEPS sampling design. The results should not be interpreted as survey-adjusted national estimates.
4. **Predictive interpretation:** The models identify patterns useful for prediction but do not establish causal relationships.
5. **Threshold selection:** Classification thresholds were explored on the test set. Future work should select thresholds using validation data or cross-validation before final evaluation.
6. **Model performance:** Neither model performed strongly across all evaluation metrics. Further validation and improvement would be needed before practical use.

## Future Improvements

Potential next steps include:

- Exploring additional predictors and alternative classification models.
- Using cross-validation or a separate validation set for model and threshold selection.
- Examining precision-recall curves and other metrics suited to imbalanced outcomes.
- Investigating approaches that account for the complex MEPS survey design.
- Evaluating model performance on an independent dataset, if an appropriate dataset is available.

