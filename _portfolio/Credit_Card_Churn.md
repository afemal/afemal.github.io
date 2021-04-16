---
title: "Credit Card Churn"
excerpt: ""
mathjax: "true"
---

### Introduction
Credit card companies generate most of their revenue through fees charged to their cardholders. These fees may include interest charged to balances carried over from the previous month, late fees if the minimum payment amount is not paid by the due date, an annual fee to keep the account open, cash advance fees charged when cards are used to obtain cash, balance transfer fees charged when the balance of one card is transferred to another, etc. In 2019, U.S. credit card companies made approximately $180 billion through customer fees alone (Egan, 2020). 

### Business Problem
Customer attrition, or customer churn, can be defined as the rate at which customers stop doing business with a company. Customer churn is an important metric to consider since it is generally more expensive to acquire new customers than to retain existing customers. By determining which factors contribute to customer churn, the company can identify individual cardholders who are likely to cancel their credit card. In turn, the company can extend a retention offer to these customers to encourage them to retain their card. 

### Methods
I obtained the [Credit Card Customers](https://www.kaggle.com/sakshigoyal7/credit-card-customers) dataset from Kaggle, which contained over 10,000 credit cardholder records. It contained 20 variables, including the target variable Attrition_Flag – a categorical variable with binary classes, Existing Customer and Attrited Customer. First, I split the data into a training, validation, and test sets. The training set contained 70% of the data and the remaining 30% was split evenly between the validation and test sets. After converting the categorical variables (Gender,  Education_Level, Marital Status, Income_Category, Card_Category), I used the training data and a decision tree to determine variable importance. The selected the variables that represented 97% importance, as seen in *Figure 1*. Using these variables, I trained and fit five different classification models on the validation data. To evaluate the models, I used the Area Under the Precision-Recall Curve and Negative Log-Loss. The Area Under the Precision-Recall Curve is stable under class-imbalance. Therefore, if the number of cardholders who cancel their account makes up a small percentage of the dataset, this metric will allow me to focus on the trade-off of precision and recall instead of giving credit for true negative predictions that often overwhelm the set of predictions. This allows for additional requirements to potentially quantify the impact of Type 1 (customers predicted to cancel their card but do not) and Type 2 (customers predicted to keep their card but cancel) errors to set a threshold of prediction. Average precision is a metric with scores between 0 and 1, where higher is better. Negative Log-Loss uses calibrated probabilities to assess how confident and correct the model is on average. It heavily penalizes confident and wrong predictions. Negative Log-Los is a metric of positive numbers, where lower is better. I also noted the accuracy of each model. The results can be seen in *Table 1*. 

<figure>
  <figcaption>Figure 1: Variables with top 97% importance</figcaption>
  <img src="https://user-images.githubusercontent.com/61814648/114959094-31b13480-9e19-11eb-939c-fdd5ce1599fa.png" style="width:100%">
</figure>

<figure>
  <figcaption>Table 1: Evaluation metric values for each classification model</figcaption>
  <img src="https://user-images.githubusercontent.com/61814648/114947818-a6c53f80-9e02-11eb-8a60-a455eb6ac929.png" style="width:100%">
</figure>

### Results
The eXtreme Gradient Boosting classification model performed better than the other models. Therefore, I concatenated the training and validation data and performed a cross-validation randomized grid search to choose the best parameters. The fine-tuned eXtreme Gradient Boosting model was fit on the test data and produced the results seen in *Table 2*. 

<figure>
  <figcaption>Table 2: Evaluation metric values after parameter tuning</figcaption>
  <img src="https://user-images.githubusercontent.com/61814648/114947954-e7bd5400-9e02-11eb-8a2f-444d3d736d4d.png" style="width:100%">
</figure>

The classification results can be observed in the confusion matrix, *Figure 2*. Of the 1520 records in the test data, 209 customers were correctly classified and 9 were incorrectly classified as closing their account. Furthermore, 34 customers were incorrectly classified as existing cardholders but have closed their account. However, approximately 86% of customers at risk of churn were identified. The credit card company can extend retention offers to these cardholders; however, the additional 14% represents missed opportunity. The Area Under the Precision-Recall Curve can be seen in *Figure 3*.

<figure>
  <figcaption>Figure 2: Confusion matrix of results</figcaption>
  <img src="https://user-images.githubusercontent.com/61814648/114949730-72ec1900-9e06-11eb-8646-d33c1e2cbc54.png" style="width:85%">
</figure>

<figure>
  <figcaption>Figure 3: Area under the precision-recall curve</figcaption>
  <img src="https://user-images.githubusercontent.com/61814648/114949788-97e08c00-9e06-11eb-8de3-be9a2449f44b.png" style="width:100%">
</figure>

### Conclusion
Once cardholders that have been identified as Attrited Customers, the company must decide how they will proceed with extending retention offers. It may choose one or multiple approaches to compare the effectiveness of each. Based on the responses of each cardholder, further analysis through uplift modeling can be conducted to determine which customers are most likely to respond to the retention offer.  During my research, I discovered two groups of cardholders to which company may not wish to extend retention offers: inactive cardholders and “churners”. First, credit card companies can cancel customer accounts due to inactivity. This is because they only have so much credit they can extend to their customers. They cannot simply give lines of credit to new customers without canceling others (Rathner, 2020). Therefore, the company may also be contributing to customer churn. Second, there are some customers who actively use credit card churn as a strategy to take advantage of card benefits. They open new credit cards accounts to take advantage of the initial signup benefits, cancel their card once the benefit is received, open a new account, and repeat the process. Prior to making a retention offer, the company may want to exclude cardholders who fall into one of these two groups. 

### Presentation
[![IMAGE ALT TEXT](https://user-images.githubusercontent.com/61814648/114291299-2f2a9580-9a3b-11eb-9b9c-5cecfccf47fe.png)](https://youtu.be/cV5D9zP-ze0)

### References
Alpine Jennings, P. (2015, December 25). The 4 D's of Customer Attrition. Retrieved March 17, 2021, from <a>https://thefinancialbrand.com/55772/banking-customer-attrition-analysis/</a> 

Egan, J. (2020, July 03). How Do Credit Card Companies Make Money? Retrieved March 18, 2021, from <a>https://www.creditcards.com/credit-card-news/how-credit-card-companies-make-money/</a>

Goyal, S. (2020, November 19). Credit Card Customers. Retrieved March 17, 2021, from <a>https://www.kaggle.com/sakshigoyal7/credit-card-customers</a>

Hurd, E. (2021, February 16). Should I Try Credit Card Churning? Retrieved March 17, 2021, from <a>https://www.nerdwallet.com/article/credit-cards/credit-card-churning</a>

Hurwood, J. (2016, November 30). Credit Card Colour Comparison: What's The Difference? Retrieved March 26, 2021, from <a>https://www.canstar.com.au/credit-cards/colour-credit-card-mean/</a>

Irby, L. (2020, October 7). What is the credit utilization ratio? Retrieved April 03, 2021, from <a>https://www.thebalance.com/what-is-a-good-credit-utilization-ratio-960548</a>

Johnson, H. (2020, February 27). What is Credit Card Churning? Retrieved March 17, 2021, from <a>https://www.bankrate.com/finance/credit-cards/what-is-credit-card-churning-and-how-does-it-affect-your-credit-score/</a>

Johnson, H. (2020, April 21). Before You Cancel Your Premium Credit Card, Ask About a Retention Offer of Bonus Points or a Reduced Annual Fee. Retrieved March 18, 2021, from <a>https://www.businessinsider.com/personal-finance/credit-card-retention-offers</a>

Lambarena, M. (2020, December 08). How Do Credit Card Companies Make Money? Retrieved March 18, 2021, from <a>https://www.nerdwallet.com/article/credit-cards/credit-card-companies-money</a>

Rathner, S. (2020, September 22). Credit Card Closed for Inactivity? What You Need to Know. Retrieved March 18, 2021, from <a>https://www.nerdwallet.com/article/credit-cards/credit-card-cancelled-due-inactivity</a>

Reducing Attrition Among Credit Card Clients. (n.d.). Retrieved March 17, 2021, from <a>https://www.sas.com/en_nz/customers/tatra-banka.html</a>

Tripathi, S. (2018, November 30). How Can Analytics Help Control Attrition in the Credit Card Industry? Retrieved March 17, 2021, from <a>https://analyticstraining.com/how-can-analytics-help-control-attrition-in-the-credit-card-industry-2/</a>

U.S. News Staff. (2021, March 15). 2019 Credit Card FEE Study: What's Normal and What's Not? Retrieved March 18, 2021, from <a>https://creditcards.usnews.com/articles/fee-survey</a>

### Repository
[Credit Card Churn](https://github.com/afemal/Credit_Card_Churn)
