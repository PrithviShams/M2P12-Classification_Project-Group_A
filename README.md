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
We also implemented an SVM model with GridSearchCV for hyperparameter tuning and found Linear model was the best Fit.

Classification Report for best fit model (Linear):

No Churn:
- Precision = 95% - When the model predicted No Churn, it was correct 95% of the time.
- Recall = 95% - 95% of the No Churn cases were correctly identified.
  
Churn:
- Precision = 88% - When the model predicted Churn, it was correct 88% of the time.
- Recall = 86% - 86% of the Churn cases were correctly identified.

Overall Accuracy: 93% - The model correctly classified 93% of the total cases.

### Model 3 - Random Forest Classification with Cross Validation
For this Random Forest Classification Model, the test size was decided was decided based on trial and error using cross validation to find the highest accuracy score of the specific models. The number of decision trees then needed to be chosen. Due to this being a smaller dataset, it was possible to iterate over a number of different decision trees to compare cross validation score with a focus on the Mean Accuracy. It appeared that 400 decision trees produce the best results with 150 almost identical. Anything over 400 was outputting very similar results with the cost of higher computing time.

No Churn:
- Precision = 97% of the time when the model predicted No Churn, it was correct.
- Recall    = 97% of the No Churn cases were correctly identified.

Churn
- Precision = 93% of the time when the model predicted Churn, it was correct.
- Recall    = 91% of the Churn cases were correctly identified.

Model accuracy score with 400 decision-trees : 95.53%

This was chosen to be our final model due to the high accuracy.

### Final Model Selected Features

The method of feature importance was used to find the non-linear relationships between features in the modle and ranks them on how important they are to the target of the model.

![Feature scores](https://github.com/user-attachments/assets/ae08cf23-f897-494b-a5c7-38c222e00949)

Several features were dropped based on their importance to the model. While not applicable to this dataset due to its small size, removing irrelevant features to increase the efficiency of a model can be an effective method of maintaining accuracy while reducing computing time. Using an efficient number of decision trees without sacrificing training speed would also need to be considered when weighing the model accuracy vs efficiency.

Model accuracy score with 400 decision-trees and Selected Features : 95.21%

### Final Model with Simulated Inputs

The model is still accurate but this is only based on the semi-random simulated data that was created.

Model accuracy score with 400 decision-trees and simulated imputs : 94.00%

## Conclusion

All of our models performed well with Random Forest standing out as the star performer. This validates our assumptions in the EDA phase, though we could potentially include additional features like billing method to verify whether our assumption about this feature held up or not. The model was trained on a dataset of a single State of a single country. It would be interesting to include data from different states and countries having the same demographic parameters and explore if churn behvavior varies with the country. The model can be further improved by including more features and allowing for additional processing time to allow more complicated models to run.











