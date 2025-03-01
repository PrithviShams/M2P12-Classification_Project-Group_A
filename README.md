# M2P12-Classification_Project-Group_A

## Introduction

In this project, we use a dataset of mostly categorical features to predict customer churn probability of a telecom company.

The dataset contained around 7000 data points of customers in California, United States. Clearly irrelevant features were dropped from the dataset before preprocessing. It was not clear from the data dictionary what exactly was meant by the categorical value "No phone service", so we simply assumed that this meant the customer was not a subscriber of the corresponding service. The categorical values were standardized to limit them to 2 or 3 values. All but one of the categorical features were encoded as nominal variables.

Latitude and longitudinal coordinates were standardized to mitigate their periodic trends, then encoded using K-means clustering into a categorical feature that would express the impact of geographic location on the churn probability. While there are better technics for encoding geographic data, we chose K-means clustering and the elbow method to find the optimum value of K for the sake of simplicity. 

Before encoding the categorical variables, the correlation chart of the numeric features with churn value shows a strong positive correlation between churn probability & churn value, and a strong negative correlation between Total Charges and Tenure Months. The correlation chart including the encoded categorical features adds fiber optic internet service as another feature with strong positive correlation to churn probability. This could be explained by the fact that the market for fiber optic internet service is very competitive, so there's little cost to switching and low incentive for the customer to retain their internet service for long periods. The contrast between the correlation charts before and after including the encoded categorical features is an interesting illustration of how certain unsuspect features can turn out to be influential after all!

## Analysis
### Churn Value Correlations
Strong Positive Relations:
- Churn Score (+0.66) - A higher Churn Score indicates a higher likelihood of churn. 
- Internet Service_Fiber optic (+0.31) - Customers with fiber optic internet tend to churn more. This could be due to higher costs or service issues.
 
Strong Negative Relations:
- Contract_encoded (-0.40) - Customers with long-term contracts churn less.
- Tenure Months (-0.35) - The longer a customer stays, the less likely they are to churn.
- Dependents_Yes (-0.25) - Customers with dependents are less likely to churn, possibly because their families rely on the service or losing the service has a negative impact.
- Internet Service_No (-0.23) - Those who do not have internet churn less.
- Total Charges (-0.20) - Higher total spending is linked to lower churn.

### Model 1 - Logistic Regression Model
Logistic regression was used to identify the key features contributing to churn probability.

<img width="690" alt="image" src="https://github.com/user-attachments/assets/651baf0a-4570-4b62-a809-c2e750713d6c" />

Features found That Increase Churn Probability:
- Internet Service_Fiber optic
- Senior Citizen_Yes
- Churn Score
- Total Charges (Higher values)

Features found That Reduce Churn Probability:
- Contract_encoded: Longer contracts reduce churn.
- Dependents_Yes and Partner_Yes: Customers with dependents or a partner are less likely to churn.
- Tech Support_Yes and Online Security_Yes: These services improve customer retention, reducing churn probability.

Classification Report:

No Churn:
- Precision = 95% - When the model predicted No Churn, it was correct 95% of the time.
- Recall    = 94% of the No Churn cases were correctly identified.
  
Churn:
- Precision = 83% - When the model predicted Churn, it was correct 83% of the time.
- Recall    = 86% of the Churn cases were correctly identified.

Overall Accuracy: 92% - The model correctly classified 92% of the cases.

### Model 2 - SVM (Support Vector Machines) + GridSearchCV
We also implemented an SVM model with GridSearchCV for hyperparameter tuning.

Classification Report for SVM:

No Churn:
- Precision = 95% - When the model predicted No Churn, it was correct 95% of the time.
- Recall = 95% - 95% of the No Churn cases were correctly identified.
  
Churn:
- Precision = 88% - When the model predicted Churn, it was correct 88% of the time.
- Recall = 86% - 86% of the Churn cases were correctly identified.

Overall Accuracy: 93% - The model correctly classified 93% of the total cases.
