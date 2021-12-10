# DSCI6612-Final-Project
# COMPARISON OF MACHINE LEARNING MODELS FOR THE PREDICTION OF CERVICAL CANCER
## INTRODUCTION:
According to WHO, Cervical cancer is the fourth most common cancer in women with an estimated
604,000 new cases and 342,000 deaths worldwide in 2020. Based on NIH statistics the rate of 
new cases of cervical cancer was 7.5 per 100,000 women per year and the death rate was 
2.2 per 100,000 women per year in 2019.

Factors that supposedly influence the survival of cervical cancer patients include age, 
anemia status, stage, type of treatment, complications and secondary disease. Age being 
one of most important factors as cervical cancer is most frequently diagnosed in women 
between the ages of 35 and 44 with the average age at diagnosis being 50. 
Almost all cervical cancer cases (99%) are linked to infection with high-risk 
human papillomaviruses (HPV), an extremely common virus transmitted through sexual contact.  
Cigarette smoking, contraceptives using, multiple pregnancies and some other factors may cause 
cervical cancer as well. The symptom-less nature of the cervical cancer has become challenging 
for the researchers and practitioners to predict the disease at early stage which is why its 
diagnosis at its early stages with ML models is very important to improve its cure and survival ratios.
## STATEMENT OF PURPOSE:
Comparing three different machine learning algorithms capable of diagnosing cervical cancer 
with high accuracy and sensitivity.
## APPROACH:
### GET DATA:
**Loading the data:**
The data is downloaded from Cervical cancer dataset from UCI ML repository 
(https://archive.ics.uci.edu/ml/datasets/Cervical+cancer+%28Risk+Factors%29). 
The dataset was collected at 'Hospital Universitario de Caracas' in Caracas, Venezuela. 
Has 35 features for 858 patients. Contains missing values as several patients decided not 
to answer some of the questions because of privacy concerns.

**Source:Creators of database:**
S.E. Golovenkin, V.A. Shulman, D.A. Rossiev, P.A. Shesternya, S.Yu. Nikulina, Yu.V. Orlova: Professor V.F. Voino-Yasenetsky Krasnoyarsk State Medical University;
A.N. Gorban, E.M. Mirkes: University of Leicester.

Database donator:
E.M. Mirkes, School of Mathematics and Actuarial science, University of Leicester, Leicester, LE1 7RH, UK, em322 '@' le.ac.uk
### DATA CLEANING & EDA:
**Missing values:** 
2 features: STDs: Time since first diagnosis & STDs: Time since last diagnosis, 
have missing values for over 90% of the records.

**Imputation of missing values:** 
Mean imputation (replacing the missing values of a certain variable 
by the mean of non-missing cases of that variable) was performed to replace the missing values.

Identify the collinearity factors using correlation matrix: Plot the correlation matrix as heatmap 
to show the correlation values of the variables in the dataset.  Also, plot heatmap of correlation 
matrix of the top 12 factors to the target variable (Biopsy).

**Check for data imbalance:**
Since Imbalance data can hamper model accuracy big time, 
check for the target variable (biopsy) imbalance.

**PCA analysis to extract highly correlated risk factors:**
Perform PCA analysis over the dataset and selected the number of PCs that explain almost the 95% of the variance. 

Also, get the most important features on the PCs with names and save them into a pandas dataframe.
### TRAIN MODELS:
**Train and Test sets:**
Separate the dataset into the predictive factors and the target variable 
& Preprocessing with StandardScaler and split the predictive factors and target variable into 
train & test datasets.

Balance the data using SMOTE on training set: Using Synthetic Minority Oversampling Technique (SMOTE) 
on training dataset helps to overcome the overfitting problem posed by random oversampling. 

**ML Models: Three ML models used are**
1. Logistic Regression
2. Random Forest 
3. Super learner Ensemble method (Base learners:Decision Tree & Bagging & XGBoost as meta learner)

**Predictive Models: For each ML model, 3 predictive models were build:**
1. Model without PCA & SMOTE
2. Model with PCA only
3. Model with SMOTE only
### EVALUATE & COMPARE MODELS
Assess the accuracy and sensitivity of the three ML models:
1. Confusion matrix: sensitivity (recall), specificity, F1-score, positive predictive accuracy (PPA) 
& negative predictive accuracy (NPA)
2. Receiver operating characteristic (ROC) curve & area under curve (AUC)

Compare the predictive models for each ML models based on evaluation metrics
Compare all the 3 ML models to see which models correctly predicts the incidence of the disease 
with high accuracy & sensitivity
# RESULTS
### Super learner Ensemble method (Base learners:Decision Tree & Bagging & XGBoost as meta learner)
|     | Accuracy | Precision | Recall | ROC score | 
| --- | --- | --- | --- | --- | 
| 1. Model without PCA & SMOTE | 97% | 0.88| 0.57 | 0.93 | 
| 2. Model with PCA only | 96% | 0.78 | 0.54 | 0.87 | 
| 3. Model with SMOTE only | 100%| 1.0 | 1.0 | 1.0 | 

### Logistic Regression
|     | Accuracy | Precision | Recall | ROC score | 
| --- | --- | --- | --- | --- | 
| 1. Model without PCA & SMOTE | 94% | 0.4 | 0.44 | 0.97 | 
| 2. Model with PCA only | 95% | 0.4 | 0.44 | 0.96 | 
| 3. Model with SMOTE only | 95% | 0.5 | 1.0 | 0.98 | 

### Random Forest 
|     | Accuracy | Precision | Recall | ROC score | 
| --- | --- | --- | --- | --- | 
| 1. Model without PCA & SMOTE | 96% | 0.5 | 0.44 | 0.55 | 
| 2. Model with PCA only | 95% | 0.45 | 0.44 | 0.55 | 
| 3. Model with SMOTE only | 100% | 1.0 | 1.0 | 1.0 | 

# CONCLUSION

It is found that both Custom Ensemble model & Random Forest with SMOTE had 100% accuracy and high sensitivity in predicting cervical cancer through biopsy, however we believe that there may be some overfitting happening. It is recommended that some additional steps be taken like feature engineering to get a deeper look into this. The second best model was the ensemble method without PCA and SMOTE.
**BEST MODEL?**: 
**BEST MODEL:** Custom Ensemble Model: Super learner Ensemble method (Base learners:Decision Tree & Bagging & XGBoost as meta learner) without PCA & SMOTE with 97% accuracy and AUC-ROC -score of 0.93.

**Recommendation to improve the model:** Use Weighted XGBoost for Class Imbalance by tuning scale_pos_weight hyperparameter
