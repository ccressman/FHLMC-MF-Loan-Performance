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


MODELING TECHNIQUE THREE: VickyLynn


MODELING TECHNIQUE FOUR: VickyLynn



