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




