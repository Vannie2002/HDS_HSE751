# **INITIAL EXPLORATORY ANALYSIS - Vannie Nguyen**

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

---
The dataset selected for this project is the 2023 Medical Expenditure Panel Survey (MEPS) Full-Year Consolidated Data File (HC-251) from the Agency for Healthcare Research and Quality (AHRQ). MEPS is a nationally representative survey of the U.S. civilian noninstitutionalized population and contains information on healthcare access, utilization, health insurance, health stauts, demographics, income, and healthcare expenditures. The 2023 Full-Year Consolidated File contains data from 2023 and includes respondents from MEPS Panels 27 and 28.

This dataset was selected because it aligns closely with my academic and professional interests in healthcare access, health disparities, and health data. Satisfying the required criteria, this dataset provides an appropriate binary outcome for examining whether demographic, socioeconomic, and health-related characteristics can be used to predict delayed medical care.

The dataset satisfies the required criteria, including:
- *Binary classification*: The target variable can be recorded into a binary outcome where respondents who reported delaying medical care because of cost are coded as 1 and those who did not are coded as 0.

- *Minimum of 200 observations*: The detaset contains 18,919 observations, which is substantially greater than the required minimum of 300 observations.

- *Minimum of 10 predictor variables*: The MEPS Full-Year Consolidated File contains 1,374 variables in the version used for this project, providing substantially more than the required minimum of 10 potential predictor variables. Candidate predictors for this project include health insurance coverage, income/poverty category, age, sex, health status, and potentially health-related characteristics.

- *Alignment with academic interests*: MEPS provides data related to healthcare access and utilization, which aligns with my interests in public health, healthcare data science, and understanding factors associated with barriers to healthcare.


## **Dataset Exploration**

### **Target variable:** **DLAYCA42**

The target variable for this classification project is DLAYCA42, which measures whether a respondent delayed medical care because of cost. The variable is coded as 1 = YES an d 2 = NO. MEPS includes special codes for Don't Know (-8), Refuse (-7), and Inapplicable (-1). These special codes will be treated as missing values during data processing. Among the 18,919 observations, 1156 respondents reported delaying medical care because of cost, while 17,436 reported that they did not.

Among respondents with valid responses for DLAYCA42, 6.22% reported delaying medical care because of cost, while 93.78% reported that they did not delay medical care because of lost. This indicates that the target variable is highly imbalanced, with substantially fewer respondents in the delayed-care group. Class imbalance will therefore be considered when evaluating the classification models.

### **Descriptive stats for the main predictors:** **INSCOV23**, **POVCAT23**

Among the 18,919 respondents, 58.4% had private health insurance, 34.8% had public insurance only, and 6.9% were uninsured. Regarding family income relative to the federal poverty line, 39.0% were categorized as high income and 27.9% as middle income, while 15.2% were categorized as poor/negative, 13.1% as low income, and 4.7% as near poor.


**### Descriptive stats for other predictors:**

**AGE23X** - Respondent's age in years.
Among respondents with valid age information, the mean age was 43.5 years and the median was 44 years. Because the project focuses on adults, age will be reassessed after restricting the dataset to respondents aged 18 or older.

---

**SEX** - Respondent's sex.
The sample consisted of 47.6% males and 52.4% females. This variable is included as a demographic characteristic that may be associated with healthcare access and utilization.

---

**RACETHX** - Race and ethnicity classification.
The largest group was non-Hispanic White respondents (54.6%), followed by Hispanic respondents (22.1%), non-Hispanic Black respondents (13.3%), non-Hispanic Asian respondents (6.1%), and other/multiple race respondents (3.8%). This variable allows demographic differences in delayed medical care to be considered.

---

**EDUCYR** - Number of years of education reported when the respondent entered MEPS. Among the 17,713 respondents with valid education information, 4,497 (25.4%) reported 12 years of education, 3,020 (17.0%) reported 16 years, and 2,289 (12.9%) reported 17 or more years. There were also 1,039 (5.5%) respondents with inapplicable values, 128 (0.7%) who reported "don't know," and 39 (0.2%) who refused to answer. These special codes will be treated as missing during preprocessing.

---

**EMPST53H** - Employment status from the latest MEPS round. Among the full sample, 8,726 (46.1%) respondents were employed, 6,845 (36.2%) were not employed, and 50 (0.3%) reported having a job to return to. There were 3,298 (17.4%) inapplicable responses. Employment status was included because employment may be related to income and access to health insurance.

---

**MARRY23X** - Marital status as of Dec 31, 2023. 7,553 (39.9%) respondents were married, 4,611 (24.4%) had never been married, 1,951 (10.3%) were divorced, 1,299 (6.9%) were widowed, and 344 (1.8%) were separated. There were 3,153 (16.7%) respondents coded as under age 16/inapplicable, along with 8 responses coded as refused or don't know. The inapplicable category will not be treated as a marital-status category in the adult analysis.

---

**RTHLTH53** - Self-reported physical health status. 6,159 (32.6%) respondents reported very good health, 5,504 (29.1%) reported good health, and 4,608 (24.4%) reported excellent health. Smaller proportions reported fair health (1,905; 10.1%) or poor health (469; 2.5%). There were 212 (1.1%) inapplicable responses, 48 (0.3%) refusals, and 14 (0.1%) don't-know responses.

---

**MNHLTH53** - Self-reported mental health status. 5,864 (31.0%) respondents reported very good mental health, 5,419 (28.6%) reported good mental health, and 5,416 (28.6%) reported excellent mental health. 1,603 (8.5%) reported fair mental health and 342 (1.8%) reported poor mental health. There were 212 (1.1%) inapplicable responses, 47 (0.2%) refusals, and 16 (0.1%) don't-know responses.

---

**DIABDX_M18** - Whether the respondent reported being diagnozed with diabetes. Among the full sample, 2,154 (11.4%) respondents reported having diabetes, while 16,649 (88.0%) reported that they did not. There were 82 (0.4%) inapplicable responses, 16 (0.1%) refusals, and 18 (0.1%) don't-know responses. Diabetes was included as a health characteristic that may help predict differences in delayed medical care.


### **Exploratory Visualizations**

**Bar chart for delayed medical care by insurance groups**:
The percentage of respondents who reported delaying medical care because of cost varied by insurance coverage. Among respondents with private insurance, 6.0% reported delaying medical care, compared with 4.6% of respondents with public insurance only. The highest percentage was observed among uninsured respondents, with 15.9% reporting delayed medical care due to cost. This difference suggests that insurance coverage may be an important predictor of delayed medical care and will be further examined in the classification models.

**Violin plot for delayed medical care with age distribution**:
Among adults who delayed medical care because of cost, the mean age was 46.5 years and the median age was 45 years. Among adults who did not delay medical care, the mean age was 52.3 years and the median age was 54 years. The violin plot shows that adults who delayed care tended to be younger than those who did not delay care. This difference suggests that age may be an important predictor of delayed medical care and should be considered in the classification models.

## **Data Quality Assessment**

- Identify missing values or improperly coded observations.
- Discuss anticipated preprocessing steps.
- Identify potential challenges associated with the dataset.

The MEPS dataset uses negative values to represent special responses such as inapplicable, refused, and don't know rather than standard missing values. 
- For the target variable DLAYCA42, 327 observations contained these special codes and will be excluded from the classification analysis, leaving 18,592 valid responses. Similar special codes are present among several predictor variables and will need to be recoded as missing before modeling. 
- The analysis will also be restricted to adults aged 18 years and older. Categorical predictors will be appropriately encoded, while age will remain a numeric variable. 
- A major challenge is class imbalance, as only 6.2% of valid respondents reported delaying medical care because of cost. Therefore, model performance will be assessed using ROC-AUC, precision, recall, F1-score, and confusion matrices rather than accuracy alone. 
- Another consideration is that MEPS is a complex survey with sampling weights and design variables, which may need to be considered depending on the modeling requirements.

## **Project Planning**

**Describe**:
- your proposed prediction problem
- the target variable (appropriate for binary classification)
- candidate evaluation metric

**Proposed prediction problem**
The proposed prediction problem is to determine whether selected demographic, socioeconomic, health status, and insurance characteristics can be used to predict whether an adult will delay medical care because of cost. The analysis will use the 2023 Medical Expenditure Panel Survey (MEPS) and focus on adults aged 18 and older. Candidate predictors include health insurance coverage, income level, age, sex, race/ethnicity, education, employment status, marital status, physical health, mental health, and diabetes status. Logistic regression and random forest classification models will be considered.
- Logistic regression provides an interpretable baseline for the binary outcome and allows the relationships between predictors and delayed medical care to be examined. 
- Random forest provides a more flexible machine-learning approach that can capture nonlinear relationships and interactions among predictors. 
- Comparing their performance will help determine whether the added flexibility of the random forest improves prediction over the simpler logistic regression model.

**Target variable**
The target variable is DLAYCA42, which indicates whether a respondent delayed medical care because of cost. The original MEPS coding is 1 = Yes and 2 = No, with negative values representing special responses such as inapplicable, refused, or don't know. For binary classification, the variable will be recoded as 1 = delayed medical care and 0 = did not delay medical care. Among valid responses, approximately 6.2% reported delaying care, while 93.8% did not.

**Candidate evaluation metric**
The primary evaluation metric will be ROC-AUC (Receiver Operating Characteristic–Area Under the Curve) because the target variable is highly imbalanced, with relatively few respondents reporting delayed medical care. ROC-AUC will measure the model's ability to distinguish between adults who delayed medical care and those who did not across different classification thresholds. Additional metrics, including precision, recall, F1-score, accuracy, and a confusion matrix, will also be reported to provide a more complete assessment of model performance.

























