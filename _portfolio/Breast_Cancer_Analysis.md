---
title: "Breast Cancer Analysis"
excerpt: ""
mathjax: "true"
---

# Breast Cancer Analysis
## EDA and Predictive Analytics

### Introduction
Breast cancer is the most common type of cancer among women – 1 in 8 women in the United States will be diagnosed at some point in their life. Mammographic images are used to detect abnormal masses in breast tissue. Based on the observed attributes of the mass, a physician may recommend a biopsy to determine a diagnosis. A fine needle aspiration (FNA) biopsy is a common form of the procedure, in which a physician uses a needle attached to a syringe to withdraw tissue or fluid from the mass. Mammographic images and FNA biopsies tend to have diagnosis inaccuracies, yielding false negative rate of 20% and 12%, respectively. False negative, or Type II, diagnosis results are the most damaging as they allow breast cancer to remain undetected and treatment to be delayed. Delays in treatment increase the risk of metastasis, which can reduce life expectancy. I used the Haberman’s Survival dataset to determine which variables are most significant to the survival of a patient. Then, I used the Mammographic Imaging and Biopsy datasets to determine which variables are most significant to predict breast cancer with high accuracy and perfect recall, avoiding any false negative prediction to ensure breast cancer does not go undetected, thus increasing survival.


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
