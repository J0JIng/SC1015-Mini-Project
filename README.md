# SC1015: DSAI Mini Project - Predicting Heart Disease

School of Computer Science and Engineering SCSE\
Nanyang Technological University NTU\
Lab: C133 \
Group : 8 

Members: 
1. O Jing ([@J0JIng](https://github.com/J0JIng))
2. Ridhwan Hakim ([@rorodevelopment](https://github.com/rorodevelopment))
3. Vignesh Mani Senthilnathan ([@VigneshManiSenthilnathan](https://github.com/VigneshManiSenthilnathan))


---
### Description:
This repository contains the project files for the SC1015 mini-project developed by students from the SCSE at NTU. Listed here are the ipynb files used, which should be viewed in numerical order:
1. [EDA and Data processing](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/EDA%26Datapreprocess.ipynb)
2. [Multivariate Decision Tree model](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/DecisionTree.ipynb)
3. [Random Forest model](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/RandomForest.ipynb)
4. [Logistic regression model](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/LogisticRegresssion.ipynb)
5. [Support vector machine (SVM) model](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/SVM.ipynb)
6. [Model Comparision](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/Model%20comparison.ipynb)
---
### Table of Contents:
1. [Introduction and Problem Formulation](#1-Introduction-and-Problem-Formulation)
2. [Exploratory Data Analysis and Data Preparation](#2-Exploratory-Data-Analysis-and-Data-Preparation)
3. [Methodology](#3-Methodology)
4. [Experiment](#4-Experiment)
5. [Data Driven Insights and Conclusion](#5-Data-Driven-Insights-and-Conclusion)
---
## 1. [Introduction and Problem Formulation]

**Our Dataset:** [Heart Failure Prediction Dataset on Kaggle](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/heart.csv) \
**Problem Statement:** Discovering the key features or symptoms that determine the patient's likelihood of heart diseases

**Introduction:**
Heart disease is a major health concern that affects a significant portion of the population. In this project, we aim to identify the most important features that contribute to the prediction of heart disease in patients.

**Significance:**
By identifying the most important features that contribute to heart disease, we can develop more accurate and efficient predictive models that can be used to improve patient outcomes. Additionally, our findings could help healthcare professionals prioritise certain risk factors when diagnosing and treating heart disease.

## 2. [Exploratory Data Analysis and Data Preparation]()
Exploratory Data Analysis (EDA) is a crucial step in gaining a deeper understanding of the data and making informed decisions about how to preprocess the data before modelling. EDA uncovers patterns, trends, and relationships in data and helps detect outliers and anomalies.

In this phase, we performed the following steps:

1. Explored categorical features with respect to the target variable, **'HeartDisease'**. We analysed the distribution of each category and checked whether the feature is a predictor of the target variable.
2. Explored numerical features with respect to the target variable, **'HeartDisease'**. We analysed the distribution of each feature, checked for outliers, and checked whether the feature is a predictor of the target variable.
3. Visualiaed the data using various charts and plots, such as histograms, box plots, and correlation matrix. We used these visualisations to identify patterns and trends and to detect outliers and anomalies.

Key Findings :
1. The Distribution of **'Heart Disease'** is balanced 
2. **'Age' , 'MaxHR' and 'Oldpeak'** has the **stronger correlation** to 'HeartDisease'.
3. **'RestingBP' and 'Cholesterol'** seems to be a **weaker correlation** to 'HeartDisease'
4. Presence of 172 "Missing" values in 'Cholesterol' (imputed with zero)
5. Presence of one "Missing" values in 'RestingBP' (imputed with zero)


For further findings and explanations, please refer to the Jupyter Notebook on EDA.

After performing EDA, we prepared the dataset by the following steps:

1. **Imputed the missing values**. We used the best imputation method that yielded the most accurate results, based on the comparison of six separate data frames. The six data frames consisted of three with different imputation methods (zero imputation, mean imputation, and median imputation) and with or without outliers. 
2. **Removed outliers**. The data frames without outliers were removed using interquartile range (IQR) method. This is important as outliers can skew the distribution of the data and affect the accuracy of the model.

We want to chose the best imputation method to ensure that the dataset has minimal missing values and accurate data, which helps improve the accuracy of the model. Removing outliers helps ensure that the distribution of the data is normal and that the model is not affected by extreme values. This will be important for feature pruning. 

## 3. [Methodology]

To find the best imputation method, we ran the six separate dataframes on each of the four machine learning (ML) models. We compared the accuracy of each data frame within each model by measuring metrics such as precision, recall and F1 score. How these metrics are chosen are explained later in [Experiment].

### The four machine learning models used to classify heart disease are as follows: 
1. [Decision Tree](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/DecisionTree.ipynb)
2. [Random Forest](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/RandomForest.ipynb)
3. [Logistic Regression](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/LogisticRegresssion.ipynb)
4. [Support Vector Machine (SVM)](https://github.com/J0JIng/SC1015-Mini-Project/blob/main/SVM.ipynb)

### Baseline Model - Decision Tree model
The Decision Tree model is a simple yet powerful algorithm that uses a tree-like structure to classify data based on a set of rules. It is often used as a baseline model for classification tasks. However, we found that the Decision Tree model yielded subpar results for our dataset, indicating that a more complex model was needed.

### Random Forest model
The Random Forest model is an ensemble learning algorithm that combines multiple decision trees to improve accuracy and generalization by reducing variance and preventing overfitting. It works by creating a random subset of features for each tree and aggregating their predictions. We chose this model to improve the performance of our baseline model and prevent overfitting.

We used GridSearchCV to tune the following hyperparameters for the Random Forest model:

* n_estimators: the number of trees in the forest
* max_depth: the maximum depth of each tree

We trained the Random Forest model using GridSearchCV with 5-fold cross-validation and selected the best hyperparameters based on the F1 score.

### Logistic Regression model
Logistic Regression is a linear model that predicts the probability of an event occurring based on a set of input features. It can achieve comparable or better performance compared to tree models, especially when the number of features is small or when the relationships between features and outcomes are linear or additive. We chose this model to compare its performance with the tree-based models and evaluate its ability to identify significant predictors of heart disease.

We used GridSearchCV to tune the following hyperparameters for the Logistic Regression model:

* C: the inverse of regularization strength
* solver: the optimization algorithm used to fit the model
We trained the Logistic Regression model using GridSearchCV with 5-fold cross-validation and selected the best hyperparameters based on the F1 score.

### Support Vector Machine (SVM) model
SVM is a powerful algorithm that can transform the data into higher-dimensional spaces to identify complex decision boundaries, making it useful for feature selection in classification problems with non-linear relationships. It can identify the most significant features that separate the data into different classes, making it a useful tool for feature selection in identifying predictors of heart disease. We chose this model to evaluate its ability to identify the most important predictors of heart disease.

We used GridSearchCV to tune the following hyperparameters for the SVM model:

* kernel: the kernel function used to transform the data into higher-dimensional spaces
* C: the inverse of regularization strength
* gamma: the kernel coefficient for 'rbf', 'poly' and 'sigmoid'
We trained the SVM model using GridSearchCV with 5-fold cross-validation and selected the best hyperparameters based on the F1 score.

### Feature pruning
After finding what is the best imputation method for that particular model.
To find the best features and model in predicting heart dieases 

We performed the following:
1. Find the best feature within each model (with the best imputation method) via feature pruning which involves selecting the most relevant features that contribute to the accuracy of the model
2. Feature pruning done by analysing the change in F1 Score as the features are removed. The top 3 features for any model is preserved. Other features are considered important based on the evaluation of the change in F1 Score.
3. Create the best model using the best features.
More of this is explained in [Experiment].

## 4. [Experiment]

### Performance Metrics used to evaluate the accuracy of the Model:
To evaluate the performance of our model in predicting the presence or absence of a **'HeartDisease'** response variable, We generated a classification report and the confusion matrix:

| Confusion Matrix  |       |        |        |      
| :---              | :---: | :----: | :----: |         
| Actual Negative   |  (0)  |   TN   |   FP   |             
| Actual Positive   |  (1)  |   FN   |   TP   |       
|                   |       |   (0)   |   (1)   |       
|                   |       | Predicted Negative    |   Predicted Postitive  |     

The confusion matrix is a table that summarises the predictions made by the model, where the rows represent the actual classes, and the columns represent the predicted classes.

The classification report generates the following metrics: precision, recall, and F1 score. We will be using the macro average since the classes are not imbalanced as shown in the EDA.

Performance Metrics:

* **Precision**: Measures the correctness of positive predictions. In the context of this model, precision refers to the model's ability to predict that a patient has 'HeartDisease' (positive prediction) and to make this prediction accurately. A precision score of 1.0 means that the model made no false positive predictions,

* **Recall**: Measures the identification of positive instances. In the context of this model, positive instances refer to patients who have 'HeartDisease' that the model is trying to predict. Recall score of 1.0 means that the model correctly identified all positive instances

* **F1 score**: Balances precision and recall. F1 score is the harmonic mean of precision and recall. It provides a single score that takes into account both precision and recall. F1 score of 1.0 means that the model has both high precision and high recall

* **ROC-AOC Score**: metric used to evaluate the quality of binary classification models. It is a plot of True Positive Rate (TPR) against False Positive Rate (FPR) for varying classification thresholds. A model with an AUC of 1.0 indicates perfect classification performance.

In the case of predicting heart disease, the cost of false negatives' and false postives' might be equally high as. In the case of a false negative where 
a patient is predicted to not have 'HeartDisease' could be potentially fatal and similarly, a patient falsely predicted to have 'HeartDisease' could take up valuable resources that could be used on patients that actually requires it. Therefore, the **F1 score might be the most reasonable metric as it balances both precision and recall**.

However, in the case whereby there are similar F1 score , we would use ROC-AOC score to determine which model is better.

### Introducing baseline

In this study, we compare our ML models against the decision tree model. This baseline help us to assess the performance of our other models relative to the decision tree model.

### Detailed comparison of the imputation method:

Firstly, we compare the F1 score, recall, and precision of the six imputation methods described above to select the best imputation method. We then select the best-performing imputation method and perform feature pruning to obtain the essential features for that particular imputation method. We repeat this process for all four ML models used in this study, including the multivariate decision tree, random forest, logistic regression, and SVM models. For each model, we used GridSearchCV to select the best-performing configuration. We compared the performance of each model to the baselines described earlier to assess the relative performance of our models. 

The following table shows the best imputation method across all four ML models and its respective F1 Score:

| Models     |       Imputation Type       |  F1 Score      |      
| :---                 | :----:                      | :----: |         
| Decision Tree        |   Zero Imputation without Outliers                    |   0.89   |             
| Random Forest        |     Median Imputation                     |   0.89    |       
| Logistic Regression  |         Median Imputation             |   0.89     |       
|        SVM           |  Mean Imputation       |   0.88  |     

Our analysis suggests that the imputation technique does not significantly impact the F1 score, as all ML models have similar F1 scores ranging from 0.88-0.89. We expected this conclusion, as in the EDA, we found that **'Cholesterol'** is not an important feature. Regardless, with the best-performing imputation method, we performed feature pruning to obtain the most important features for that particular model.

### Detailed comparison of the Feature importance:

Secondly, to select the best feature, we compared the bSecondly, to select the best feature, we compared the best features obtained from each respective ML model with the baseline.

The following table shows the most important features across all four ML models:

| Models               | Important Features                                                                                                        | F1 Score before feature pruning | F1 Score after feature pruning |
| :-------------------| :-------------------------------------------------------------------------------------------------------------------------| :------------------------------:| :-----------------------------:|
| Decision Tree        | 'MaxHR', ,'Sex_F' 'ChestPainType_ASY', 'ST_Slope_Up'                                                                       |             0.89               |                       0.85          |
| Random Forest        | 'RestingECG_Normal', 'Sex_M', 'Sex_F', 'ChestPainType_ATA', 'ChestPainType_ASY', 'ST_Slope_Flat', 'ST_Slope_Up'          |             0.89               |                        0.84         |
| Logistic Regression  | 'Age' , 'Oldpeak', 'Sex_M', 'ChestPainType_ASY', 'ExerciseAngina_Y' , 'ST_Slope_Up' , 'ST_Slope_Flat'                      |             0.89               |                     0.86           |
| SVM                  | 'Oldpeak', 'Sex_F', 'ChestPainType_ASY', 'ExerciseAngina_N', 'ST_Slope_Up'                                                 |             0.88               |                    0.87             |
  

The first observation is that all models have similar F1 scores before feature pruning, indicating that all models are initially performing well and have equal predictive power. After feature pruning, we see a decrease in the F1 score for all models, ranging from 0.84 to 0.87. However, the reduction in the F1 score is insignificant, suggesting that the models were likely overfitting some of the removed features. Therefore, removing these features makes the model less prone to overfitting, allowing it to generalise better to new data.

We find that the non-tree models had better F1 scores after feature pruning, with SVM having the best F1 Score of 0.87 in comparison to our baseline of 0.85. We expected this conclusion as we knew that SVM could transform the data into higher-dimensional spaces to identify complex decision boundaries, making it useful for feature selection in classification problems with non-linear relationships. The 'kernel': 'rbf' hyperparameter chosen performed the best as it is more complex and efficient at the same time that it can combine multiple polynomial kernels multiple times of different degrees to project the non-linearly separable data into higher dimensional space so that it can be separable using a hyperplane.

This further suggests that SVM is the best ML model to predict for **'HeartDisease'**. 

The second observation we can make is that across all four ML models, the most critical feature across all models is **'ChestPainType_ASY'**, which appears in the top features of all four models. This suggests that this feature is strongly correlated with the target variable and plays a significant role in predicting the presence of heart disease. Again, We expected this conclusion, as in the EDA, we found that Individuals with **'ChestPainType_ASY'** are most likely to get Heart Disease.

Other features that appear in multiple models include **'ST_Slope_Up'**,**'Sex_F'**,**'Oldpeak'**,**'ExerciseAngina_N'**, which may also be important predictors of heart disease. 

Hence we identified the most important features that are consistently important across multiple modelling techniques
| Most Important Feature    |     
| :---                 |       
| ChestPainType_ASY       |       
| ST_Slope_Up       |    
| Sex_F  |  
|       Oldpeak           | 
|       ExerciseAngina_N          | 

### Detailed comparison of the models with the best features:

The ML models are once again trained with only the most important features. Since the imputation technique is optional, we would be omitting it.  

| Models     |       F1 Score      |  ROC - AOC      |      
| :---                 | :----:    | :----: |         
| Decision Tree        |     0.870  |   0.940 |             
| Random Forest        |     0.870  |   0.941 |       
| Logistic Regression  |     0.870  |   0.938 |       
|        SVM           |     0.870  |  0.948 |     


We found that all four models have relatively similar performance, with F1 scores ranging from 0.87 to 0.88 and ROC-AUC scores ranging from 0.938 to 0.948. This suggests that the models trained using the most important features can make accurate predictions. In this case, SVM is shown to be marginally better as it has the highest ROC-AOC score of 0.948, making it the best ML model to predict if a patient has heart disease. 


We can compare the ML models before feature pruning had a score of 0.88-0.89. After re-training all four models, this slight decrement in the F1 score 0f 0.87 affirms that the selected features are the most important predictors. 


### 5. [Data Driven Insights and Conclusion]

Based on our findings, we found that 'ChestPainType_ASY', 'ST_Slope_Up', 'Sex_F', 'Oldpeak', and 'ExerciseAngina_N' are the top priority risk factors that healthcare professionals should consider when diagnosing and treating heart disease. Additionally, we determined that SVM is the most effective ML model for predicting the presence of heart disease.

However, our current model has a limitation in that it only uses one feature selection technique, feature pruning. To improve the model's performance, we suggest exploring other feature selection techniques such as Principal Component Analysis (PCA), Recursive Feature Elimination (RFE), and further feature importance analysis to identify the most significant features. Despite this limitation, our current models serve as a strong benchmark for future models with more complex feature selections.

