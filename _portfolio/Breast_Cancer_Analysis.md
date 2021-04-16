---
title: "Breast Cancer Analysis"
excerpt: ""
mathjax: "true"
---

### Introduction
Breast cancer is the most common type of cancer among women – 1 in 8 women in the United States will be diagnosed at some point in their life. Mammographic images are used to detect abnormal masses in breast tissue. Based on the observed attributes of the mass, a physician may recommend a biopsy to determine a diagnosis. A fine needle aspiration (FNA) biopsy is a common form of the procedure, in which a physician uses a needle attached to a syringe to withdraw tissue or fluid from the mass. Mammographic images and FNA biopsies tend to have diagnosis inaccuracies, yielding false negative rate of 20% and 12%, respectively. False negative, or Type II, diagnosis results are the most damaging as they allow breast cancer to remain undetected and treatment to be delayed. Delays in treatment increase the risk of metastasis, which can reduce life expectancy. 
I will use the Haberman’s Survival dataset to determine which variables are most significant to the survival of a patient. I will use the Mammographic Imaging and Biopsy datasets to determine which variables are most significant to predict breast cancer with high accuracy and perfect recall, avoiding any false negative predictions. This will ensure breast cancer does not go undetected and increases survival.


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

### Data
All datasets were obtained from Kaggle.com and include the following information:

**[Haberman Cancer Survival Data](https://www.kaggle.com/krpiku/haberman.csv?select=haberman.csv)**

This dataset was collected by the University of Chicago’s Billings Hospital between 1958 and 1970 from patients who had undergone breast cancer   surgery. The dataset contains 305 observations with four variables: 
* age: age of the patient at the time of surgery
* year: year the surgery was performed
* nodes: number of positive axillary lymph nodes 
* status: status of the patient 5 years post-surgery, where 1 = survived and 2 = died

**[Mammographic Mass Data](https://www.kaggle.com/overratedgman/mammographic-mass-data-set)**

This dataset was collected at the Institute of Radiology of the University Erlangen-Nuremberg between 2003 and 2006 from mammographic images. The original dataset was comprised of 961 observations but attributes with missing values were removed. This dataset includes 830 observations and six variables: 
* BI-RADS: standard system used to describe findings where:
 * 0 = Incomplete - Additional imagining is necessary
 * 1 = Negative - No abnormalities to report
 * 2 = Benign - No cancerous findings
 * 3 = Probably benign finding
 * 4 = Suspicious abnormality 
 * 5 = Highly suggestive of malignancy
 * 6 = Known biopsy-proven malignancy
* age: age of patient
* shape: shape of the mass, where 1 = round, 2 = oval, 3 = lobular, 4 = irregular
* margin: description of the mass’s edge, where 1 = circumscribed, 2 = microlobulate, 3	= obscured, 4 = ill-defined, 5 = spiculated
* density: density of the mass, where 1 = high, 2 = isodense, 3 = low, 4 = fat-contained
* severity: diagnosis of the mass, where 0 = benign, 1 = malignant
	
[Breast Cancer Prediction Dataset](https://www.kaggle.com/merishnasuwal/breast-cancer-prediction-dataset)

This data was collected by Dr. William H. Wolberg, W. Nick Street, Olvi L. Mangasarian in the General Surgery and Computer Science Departments as the University of Wisconsin in 1992 from fine needle aspiration biopsies. The original dataset is comprised of 569 observations with 32 variables. This dataset contains all 569 observations but has been reduced to the following six variables: 
* radius: mean of distances from the center of the cell nuclei to the points on its perimeter
* texture: mean texture of the nuclei, described by the spatial arrangement and variation of grey values observed
* perimeter: mean distance around the nuclei
* area: mean area of the nuclei
* smoothness: mean of the local variation in radius lengths
* diagnosis: diagnosis of the mass, where 0 = malignant, 1 = benign

### Required Packages
I will be using the following R packages to perform the analysis:
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
 
### Plots and Table Needs
I will be using histograms to determine distributions, scatter plots and correlation matrices to identify relationships, density plots and boxplots to compare different groups, and confusion matrices to summarize prediction results.

### Questions for Further Steps
I will conduct further research of classification models to determine which are the most appropriate to use for the datasets. During this course, I have learned about logistic regression and k-nearest neighbors. I will be exploring other classification models, specifically decision tree and random forest models.

### Data Exploration
First, I imported each dataset and looked at the structure and data summary for each. In doing so, I verified no missing data. The summary of the mammographic mass dataset showed an observation that had a value of 55 for BI.RADS. As BI.RADS is an ordinal, categorical variable, I have removed this observations from the dataset. No other outliers were evident in the datasets. I converted categorical variables, indicating ordinal variables where appropriate.  

The clean datasets had the following summaries:

<figure>
  <img src="https://user-images.githubusercontent.com/61814648/114961035-1a744600-9e1d-11eb-9f6c-a723273c268c.png" style="width:100%">
</figure>

The variables have the following distributions:

<figure>
  <img src="https://user-images.githubusercontent.com/61814648/114961282-94a4ca80-9e1d-11eb-876f-a91dfeff2766.png" style="width:100%">
</figure>

<figure>
  <img src="https://user-images.githubusercontent.com/61814648/114961307-a0908c80-9e1d-11eb-91af-358a13aff23b.png" style="width:100%">
</figure>

<figure>
  <img src="https://user-images.githubusercontent.com/61814648/114961332-aa19f480-9e1d-11eb-93fa-c18a37ca9bf1.png" style="width:100%">
</figure>

The variables in the biop and hab datasets have skewed-right distributions. 

**Haberman’s Survival**

First, I will determine which variables are significant in determining the survival status. I will compare the variables between the two groups, died and survived, and use density and boxplots for visual aids.

![hab 1](https://user-images.githubusercontent.com/61814648/114962409-78a22880-9e1f-11eb-832c-59b6bc2de2e1.png)

![hab 2](https://user-images.githubusercontent.com/61814648/114962509-a38c7c80-9e1f-11eb-8959-4b0683d0b7e0.png)

![hab 3](https://user-images.githubusercontent.com/61814648/114962568-c454d200-9e1f-11eb-9e45-0f10cd8dd2a8.png)

Based on the density and boxplots, it appears the only significant variable is nodes. As the variables are skewed-right, I used the Mann-Whitney U Test to verify this claim. 

![hab 4](https://user-images.githubusercontent.com/61814648/114962772-3200fe00-9e20-11eb-83c3-884a4bce8363.png)

The results show that there is a significant difference in nodes between the two groups. It also indicates that there is no difference in age and year. Therefore, I conclude nodes is the only significant factor in the dataset in determining whether a patient will survive longer than five years after breast cancer surgery.

**Mammographic Imaging**

I will determine which variables are significant in determining the diagnosis of breast cancer. I will compare the variables between the two groups, malignant and benign, and use density and boxplots for visual aids.

![mam 1](https://user-images.githubusercontent.com/61814648/114963454-aa1bf380-9e21-11eb-92f3-4a08788e3fa8.png)

It appears that all variables, except Density, are significant variables in predicting Severity. To decide which variables to use in the logistic model, I used all variables in the dataset to determine the most significant. The full model summary indicates Age, Shape, and Margin are the most significant. 

![mam 2](https://user-images.githubusercontent.com/61814648/114963473-b6a04c00-9e21-11eb-812d-d2ff7a044fa9.png)

I used these variables in a new logistic regression model. The AIC is much lower, which indicates this model is a better fit than the full model. 

![mam 3](https://user-images.githubusercontent.com/61814648/114963495-c15ae100-9e21-11eb-81ee-330894bd06d8.png)

I trained the model using training data and ran the test data through the model. Using a decision threshold of 50%, the model provides a prediction accuracy of 80% and a recall of 79%. To eliminate Type II Errors, I have decided to decrease the decision threshold to a value that will produce 100% recall. Using a decision threshold of 6%, the model provides a prediction accuracy of 58.2% but 100% recall. The full decision tree model indicates BI.RADS, Age, Shape, and Margin are the most significant variables. 

![mam 4](https://user-images.githubusercontent.com/61814648/114963526-d172c080-9e21-11eb-8c9b-62a11536a7e5.png)

Using the training and testing data, the decision tree model provides a prediction accuracy of 83.6% and a recall of 79.8%. The k-nearest neighbors model, when k = 29, provides a prediction accuracy of 80% and a recall of 85%. Using cross validation on a random forest model, BI.RADS is indicated as the only significant variable. The random forest model provides a prediction accuracy of 81.8% and a recall of 84.7%. The decision tree model provided the most prediction accuracy; however, the best model is the logistic regression model with decision threshold of 6% with 100% recall, as seen in the table below.

![mam5](https://user-images.githubusercontent.com/61814648/114963556-ddf71900-9e21-11eb-970a-4252322c2344.png)

**Fine Needle Aspiration Biopsy**

I need to decide how to proceed with the radius, perimeter, and area variables. I will begin by using scatter plots to examine the relationship between them.

![biop 1](https://user-images.githubusercontent.com/61814648/114963634-07b04000-9e22-11eb-99fb-8b906f0c663c.png)

The variables are highly correlated, as suspected. To help decide which two variables to removed from the data frame, I will examine their correlation coefficients.

![biop 2](https://user-images.githubusercontent.com/61814648/114963660-15fe5c00-9e22-11eb-8aa5-6cf82d983828.png)

The greatest correlation is between the product of the radius and perimeter variables and the area variable. Therefore, I will remove the radius and perimeter variables. I want to examine the correlation between the remaining variables.

![biop 3](https://user-images.githubusercontent.com/61814648/114963678-20205a80-9e22-11eb-8305-a486e7e37922.png)

None of the remaining variables are highly correlated with the others. Next, I want to compare the variables between the two diagnosis groups, malignant and benign. I will use density and boxplots for visual aids.

![biop 4](https://user-images.githubusercontent.com/61814648/114963701-2e6e7680-9e22-11eb-907c-4f2f68308efe.png)

![biop 5](https://user-images.githubusercontent.com/61814648/114963708-3201fd80-9e22-11eb-8858-52dfc986ba82.png)

![biop 6](https://user-images.githubusercontent.com/61814648/114963725-375f4800-9e22-11eb-85bf-e297db9ba69b.png)

Based on the density and boxplots, it appears there is a significant difference in texture, area, and smoothness between the two diagnosis groups. I will use the Mann-Whitney U Test to show verify.

![biop 7](https://user-images.githubusercontent.com/61814648/114963763-4a721800-9e22-11eb-88cf-d1b955b65665.png)

The Mann-Whitney U Test verifies these claims. I will use these variables in a logistic regression model. 

![biop 8](https://user-images.githubusercontent.com/61814648/114963787-55c54380-9e22-11eb-8c7e-396ba4729922.png)

I trained the model using training data and ran the test data through the models. Using a 50% decision threshold, the logistic regression model provides a prediction accuracy of 92% and a recall of 86.7%. To eliminate Type II Errors, I decreased the decision threshold to 26%.  This provides a prediction accuracy of 94.7% and 100% recall. The decision tree model provides a prediction accuracy of 90.3% and a recall of 83%. The k-nearest neighbors model, when k = 23, provides a prediction accuracy of 86.7% and a recall of 71.4%. The random forest model provides a prediction accuracy of 92.9% and a recall of 90.5%. The logistic regression model with a 26% decision threshold provides the best prediction accuracy with perfect recall, as seen in the table below.

![biop 9](https://user-images.githubusercontent.com/61814648/114963812-64135f80-9e22-11eb-82d2-bd51313fb200.png)

The only variable found to be significant in predicting the survival of a patient was the number of positive axillary lymph nodes. Axillary lymph nodes are taken from the axilla, or the armpit. When cancer cells are detected in the axillary lymph nodes, it indicates metastasis. As observed in the analysis, smaller amounts of positive lymph node increased the probability of surviving for longer than five years after surgery. These finding emphasizes the importance of recall accuracy, early detection, and timely treatment.
The best recall results were obtained by decreasing the decision threshold in the logistic regression models. There may similar methods available to use on the other classification models; however, time limitations did not allow for further methods to be explored. The survival analysis conducted were based on data gathered from patients who had surgery between 1958 to 1970. Using current data would likely produce different results. 
I used this data to find the classification models that predicted a diagnosis with high accuracy and recall. As breast cancer continues to affect so many, I feel further research into risk factors associated with its development would provide some interesting insights. These insights could decrease false negative results and increase survival. 

### Conclusion
By adjusting the decision threshold, I was able to obtain 100% recall using logistic regression with the mammographic and biopsy datasets – resulting in no false negative diagnosis. The prediction accuracy using the mammography dataset was only 58.2%, which would require biopsies for many women with false positive results. However, the prediction accuracy using the biopsy dataset was 94.7%. 

### Repository
[Breast Cancer Analysis](https://github.com/afemal/Breast_Cancer_Analysis)

### References
Bell, D., Weerakkody, Y., et al (2013). Breast imaging-reporting and data system (BI-RADS): Radiology Reference Article. Retrieved July 29, 2020, from <a>https://radiopaedia.org/articles/breast-imaging-reporting-and-data-system-bi-rads?lang=us</a>

Biswas, K. (2019, July 19). Haberman Cancer Survival Data Set. Retrieved July 20, 2020, from <a>https://www.kaggle.com/krpiku/haberman.csv?select=haberman.csv</a>

Limitations of Mammograms: How Often are Mammograms Wrong? (n.d.). Retrieved August 06, 2020, from <a>https://www.cancer.org/cancer/breast-cancer/screening-tests-and-early-detection/mammograms/limitations-of-mammograms.html</a>

Ovsen. (2016, October 31). Mammographic Mass Data Set. Retrieved July 20, 2020, from <a>https://www.kaggle.com/overratedgman/mammographic-mass-data-set</a>

Singh Suwal, M. (2018, September 26) Breast Cancer Prediction Dataset. Retrieved July 20, 2020 from, <a>https://www.kaggle.com/merishnasuwal/breast-cancer-prediction-dataset</a>
