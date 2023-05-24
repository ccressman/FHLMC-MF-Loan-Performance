Multifamily Loan Performance: Prospective Predictive Models


The goal of this project is to create a model that will evaluate a multifamily loan profile and predict whether it will perform well or represents significant default risk.


Our dataset was obtained from FreddieMac’s Multifamily Loan Performance Database, which provides historical information on a subset of the Freddie Mac Multifamily Whole Loan Portfolio from 1994-2022.
Data Source: https://mf.freddiemac.com/investors/dat



OUR VARIABLES:

Mortgage Term

Original Loan to Value

Count of Residential Units

Fixed vs. Variable Interest Rate

Original Debt Service Coverage

Interest Rate

Interest Only Period

Fixed to Float feature 

Balloon Term feature 



OUR DATASET
Within our dataset there are over 25,000 loans that are categorized as "current" or "less than 60 days delinquent". This indicates that a significant portion of the loans in the dataset are in good standing and being paid on time. Additionally, there are over 25,000 loans that are classified as "closed". This suggests that a substantial number of loans have reached the end of their term or have been fully paid off. The balance of our data after the closed loans are dropped is as follows: 

![image](https://github.com/ccressman/FHLMC-MF-Loan-Performance/assets/119253324/d83cc1b1-0c7d-4fe0-a27e-5cd3b34b0831)



IMBALANCED DATA SUMMARY:

Checking the balance of our target variable, mortgage status, revealed great imbalance within the dataset. That is, it contains almost 28 thousand instances of performing loans versus just over 200 loans in some form of default. Given this disparity, the data will need to be rebalanced prior to training and testing the model. Several methods, including RandomOverSampler from Imbalanced Learn and SMOTE-ENN (Synthetic Minority Over-Sampling Technique), will be used to determine which method performs best.



SUMMARY OF DATA DISTRIBUTION

Analysis of feature distribution indicates highly skewed data. Since the data does not have a Gaussian distribution, MinMax Scaler should perform well in scaling the data while preserving the shape of the distribution. This contrasts with alternative methods, like StandardScaler, which use Z-score normalization and should therefore perform best on datasets with a Gaussian distribution. Graphical representation of our data distribution is below:

![image](https://github.com/ccressman/FHLMC-MF-Loan-Performance/assets/119253324/62b63f75-39ac-42ba-a981-214d0f133cd4)



Correlation Matrix Results

The variables of the Mortgage Term and whether the mortgage has a Fixed to Float feature appear to be highly correlated (0.85), indicating that as the mortgage term increased the likelihood of having a fixed to float mortgage also increased. Although the two features are highly correlated, they represent significantly different measures, therefore the Fixed to Float loan feature will be included in our model.

Based on the correlation values, it appears that there are no strong correlations (above 0.5 or below -0.5) between the features and the target variable.

![image](https://github.com/ccressman/FHLMC-MF-Loan-Performance/assets/119253324/93a9784f-59a6-4816-8981-80473e6d63ea)


MODELING TECHNIQUES USED:

Different modeling techniques used within our project include: 

1. Logistic Regression

2. Histogram-Based Gradient Boosting Model

3. Random Tree Forest

4. Neural Network


MODELING TECHNIQUE ONE: LOGISTIC REGRESSION
The first method we evaluated was logistic regression due to its aptitude for binary classification tasks. However, the results were ultimately underwhelming (cross-validation, accuracy, and balanced accuracy scores were 76%). During this step, we built four different models, which used separate resampling and scaling methods. The highest performing used SMOTE-ENN for resampling and MinMax Scaler. Given the low level of correlation exhibited across features as well as the discrepancies between the coefficient and permutation scores generated for these models, logistic regression does not appear to be the optimal modeling technique to achieve this project's goal.  


MODELING TECHNIQUE TWO: HISTOGRAM-BASED GRADIENT BOOSTING
Data analysis indicates that our features do not maintain a strong linear relationship. This is underlined by the relatively poor performance of our logistic regression models.

A more complex model, like Gradient Boosting Classification (GB), that is able to account for non-linear relationships is therefore a more appropriate model. 

Due to the large size of the dataset being evaluated (>50,000 rows), a histogram-based gradient boosting model was selected over a gradient boosting classifier. Model training is accelerated with this modeling technique by its use of discretizing, or binning, the input features to a few hundred unique values. 

Ultimately, model performance increased significantly. Our highest performing model, which used RandomOverSampler and Standard Scaler, achieved average cross-validation and accuracy scores of 99% and minimized type two error when predicting loan default, which achieves our objective. 

Given the high performance of the model, we took a look at permutation importance, which designates "Interest Rate" as the most important feature, meaning the most influential in predicting performance as calculated by this model. 

Graphical respresentation of model performance results are below: 
![image](https://github.com/ccressman/FHLMC-MF-Loan-Performance/assets/119253324/9d798fa5-22b6-45f7-8f2e-ddb1963fd3b6)

![image](https://github.com/ccressman/FHLMC-MF-Loan-Performance/assets/119253324/4cf4a1be-be31-4463-8f52-92aaa0ccb368)

![image](https://github.com/ccressman/FHLMC-MF-Loan-Performance/assets/119253324/47c26f2c-0f1a-4ad8-ba80-5f1a47625935)


MODELING TECHNIQUE THREE: RANDOM FOREST

We reviewed Random Forest model to predict loan success. Though the model had a 99.4% Accuracy Score it scored low in precision, recall, and f1-score.

The Random Forest model showed 23 - True Positives / 38 - False Positives  / 4 - False Negatives / 6926 - True Negatives. Due to the high False Positives (out weighing the True Positives) we believed the Random Forest model would not be the best model to prejudice loan investment success.  

![Screenshot 2023-05-24 at 7 16 58 PM](https://github.com/ccressman/FHLMC-MF-Loan-Performance/assets/47072092/34cc9cb0-9c49-4b7d-95ea-0d0b5f0c107a)

The 10 most Important Features that were discovered during the Random Forest Model are show. The top 3 making an impact of 20% or more on the model 1.) Debt ratio rate, 2.) Interest rate, 3.)  Loan to value ratio

![Screenshot 2023-05-24 at 7 17 28 PM](https://github.com/ccressman/FHLMC-MF-Loan-Performance/assets/47072092/92214c4c-115f-4881-b7b4-ff470ceb6716)


MODELING TECHNIQUE FOUR: NEURAL NETWORK

Neural Network was then reviewed with a high Accuracy rate of 99.1% and Loss rate of 4.5% it was discovered that mortgage rate term and fixed to float loans (whether loans were fixed rate or float rate) had the highest correlation in this model.

In the correlation matrix you can see fixed to float loan rate and mortgage term had the strongest correlation when predicting multifamily loan success. It is interesting to note that these to inputs where also in the top ten features for the Random Forest model at 7.7% importance for mortgage term and 3.7% importance for fixed to float loan.

![Screenshot 2023-05-24 at 7 19 58 PM](https://github.com/ccressman/FHLMC-MF-Loan-Performance/assets/47072092/2704ef8a-5ce7-4c41-8a5c-0c17dbf4eb9c)


