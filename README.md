Project Goal 
The goal of a project is to predict wheter a bank customer will subscribe to a term deposit based on 
demographic data and historical marketing campaign interactions. By identifying the most likely subscribers,
a bank can optimize its marketing resources, improve conversion rates, and reduce spendings on unnecessary phone calls to uninterested leads

Data Source 
https://www.kaggle.com/datasets/henriqueyamahata/bank-marketing

Project Workflow

1. Data Preprocessing
Leakage Prevention: Removed the duration feature as this variable is only known after a call ends

Feature Engineering: Created variable was_contacted from the pdays variable where 999 signified no prior contact to avoid misleading the model in treating 999 value as amount  of days 

Standardization: Applied StandardScaler to numerical inputs to ensure coefficients were comparable and the models converged efficiently

2. Handling of Class Imbalance
With only ~11% of customers subscribing, the data is highly skewed. The issue is solved through:

Implementation of  class_weight='balanced' 

Implementation of classification cutoff to 0.3 for the Tuned Random Forest

3. Comparison of two Random Forests
I implemented two distinct Random Forest approaches to compare different business strategies:

The Baseline Forest (Precision-Focused): 
Goal: Efficiency.
 Yielded higher Precision (~0.41). This model is best if the bank has a limited budget and needs to ensure that every call made has a higher probability of success, minimizing "wasted" effort

The Tuned Forest with GridSearchCV (Recall-Focused):

Goal: Sales increase , for Banks with bigger budgets 

Through hyperparameter tuning and threshold adjustment, pushed Recall to ~0.71.
While this lowered precision, it is the superior strategy for a bank aiming to capture 71% of all possible subscribers, accepting the higher cost of calls to ensure maximum conversion

4. Feature Insights
   Analyzed the model coefficients to identify the strongest drivers of customer subscriptions:
Positive Drivers - Success is most highly correlated with the month of March, my engineered was_contacted feature, and the Consumer Price Index
Negative Drivers - High economic volatility (emp.var.rate) and landline contact 
