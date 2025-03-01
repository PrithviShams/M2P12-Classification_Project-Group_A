# M2P12-Classification_Project-Group_A

## Introduction

In this project, we use a dataset of mostly categorical features to predict customer churn probability of a telecom company.

The dataset contained around 7000 data points of customers in California, United States. Clearly irrelevant features were dropped from the dataset before preprocessing. It was not clear from the data dictionary what exactly was meant by the categorical value "No phone service", so we simply assumed that this meant the customer was not a subscriber of the corresponding service. The categorical values were standardized to limit them to 2 or 3 values. All but one of the categorical features were encoded as nominal variables.

Latitude and longitudinal coordinates were standardized to mitigate their periodic trends, then encoded using K-means clustering into a categorical feature that would express the impact of geographic location on the churn probability. While there are better technics for encoding geographic data, we chose K-means clustering and the elbow method to find the optimum value of K for the sake of simplicity. 

Before encoding the categorical variables, the correlation chart of the numeric features with churn value shows a strong positive correlation between churn probability & churn value, and a strong negative correlation between Total Charges and Tenure Months. The correlation chart including the encoded categorical features adds fiber optic internet service as another feature with strong positive correlation to churn probability. This could be explained by the fact that the market for fiber optic internet service is very competitive, so there's little cost to switching and low incentive for the customer to retain their internet service for long periods. The contrast between the correlation charts before and after including the encoded categorical features is an interesting illustration of how certain unsuspect features can turn out to be influential after all!
