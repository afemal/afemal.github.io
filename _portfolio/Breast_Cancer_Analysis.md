---
title: "Breast Cancer Analysis"
excerpt: ""
mathjax: "true"
---

### Introduction
Breast cancer is the most common type of cancer among women – 1 in 8 women in the United States will be diagnosed at some point in their life. Early detection is important as it provides more treatment options and a better chance for survival. Mammographic images can help doctors look for early signs of cancer. Suspicious mammographic may require a biopsy to determine a diagnosis. Since only approximately 20% of biopsies results in a malignant diagnosis and can be very painful, I would like to use the measurements taken from mammographic images to predict the diagnosis. The results could better determine whether the woman requires a biopsy or further monitoring through follow-up examinations. The only definite way to diagnose breast cancer is through a biopsy; however, fine needle aspiration biopsies also have problems with prediction accuracy, with a 4% false positive rate and 12% false negative rate (Smith, 1997). Therefore, I would also like to use the measurements taken from biopsies to predict and improve the diagnosis accuracy and recall. The accuracy of diagnosis allows for earlier detection, which mean the difference between life and death. Finally, I would like to determine which variables are significant to the survival of a patient diagnosed with breast cancer. 

### Research questions 
Using different datasets, I would like to answer the following questions:
* What measurements taken during a mammographic image are significant to the diagnosis of breast cancer?
* Using these significant measurements, can I use a machine learning model to predict a diagnosis with high accuracy and high recall? 
* What measurements of cell nuclei taken from a fine needle aspiration biopsy are significant to the diagnosis of breast cancer?
* Using these significant measurements, can I use a machine learning model to predict the diagnosis with high accuracy and high recall? Less than 4% false positive and 12% false negative? 
* What characteristics contribute to a patient surviving longer than five years post-surgery? 

### Approach
For each dataset, I will perform exploratory data analysis. I will examine the variables to find which are the most significant in predicting breast cancer and the survival of a patient. I will use different classification models to identify which provides the best accuracy and recall in predicting a diagnosis. 

**How My Approach Addresses the Problem**
Type II errors, or false negatives, allow breast cancer to remain undetected and treatment to be delayed. Delays in treatment increase the risk of metastasis, or the spread of cancer to other parts of the body, which can reduce life expectancy. I will use the survival data to determine which variables contribute most to the survival of a patient. I will use the data from mammographic images and fine needle aspiration biopsies to determine how to predict breast cancer with high accuracy and perfect recall. This will ensure breast cancer does not go undetected and increase the chance of survival.  

### Tools
* R
* Packages
  * ggplot2
  * gridExtra
  * MASS
  * tidyverse
  * caret
  * rpart
  * rattle
  * rpart.plot
  * RColorBrewer
  * Class
  * randomForest
  * caTools
  * mlbench
  * e1071

### Data
[Mammographic Mass Dataset](www.kaggle.com/overratedgman/mammographic-mass-data-set)

[Breast Cancer Prediction Dataset](https://www.kaggle.com/merishnasuwal/breast-cancer-prediction-dataset)

[Haberman Cancer Survival Dataset](www.kaggle.com/krpiku/haberman.csv?select=haberman.csv)

### Modeling Methods
* Logistic Regression
* Decision Tree
* k-Nearest Neighbors
* Random Forest

### Conclusion
By adjusting the decision threshold, I was able to obtain 100% recall using logistic regression with the mammographic and biopsy datasets – resulting in no false negative diagnosis. The prediction accuracy using the mammography dataset was only 58.2%, which would require biopsies for many women with false positive results. However, the prediction accuracy using the biopsy dataset was 94.7%. 

### Repository
[Breast Cancer Analysis](https://github.com/afemal/Breast_Cancer_Analysis)
