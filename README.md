# StreamFlow-Business-Analysis







1. The most recent data StreamFlow has is till September, 2026. The VP of revenue and operations wants to know what's the revenue forecaste is going to be for October, 2026.
First, I used SQL to do data aggregation, so we have a dataset that's ready to use for statistical analysis.

I first started with multiple linear regression, using number of subscribers at start, marketing spends and churn rate to predict revenue. Then fit the model.
Coefficients:[58.70180039, -9218.27815481]
Intercept:-48529.451345181194
R^2 =0.399650049697893
RMSE: 45940.137062642425
Interpretation: we get 58.7 dollars increase in revenue when we gain 1 active subscriber. We lose 92.18 dollars in revenue
when we lose 1 subscriber. Explaining intercept won't be useful here as we will never have 0 subscriber and 0 churn rate. 
**However, this model only explains about 39& of revenue change, and on average the revenue is predicted off by $45940.138 which is not solid as forecasting guide. 
Moving onto a different model, which is decision tree

Decision tree model:
I first split the data into 2 parts, 1 for training the other for testing.
New R^2 = 0.820991019150182
RMSE: 28085
ActiveAtStart: 0.691935769581
MarketingSpend: 0.27737278224
Churn rate: 0.030691448184
Interpretation: Active subscribers beginning of the month plays the most important role in predicting revenue, which is 
69%. Streamflow's revenue is primarily driven by size of the active subscriber base. Marketing investment plays a meaningful role in influencing revenue, although its impact is much smaller than the size of the subscriber base. ChurnRate only helped explain about 3% of the model's revenue predictions.

Summary: The Decision Tree identified Active Subscribers as the primary driver of monthly revenue, accounting for roughly 69% of the model's predictive power. Marketing Spend contributed about 28%, while Churn Rate contributed only 3%. This suggests that subscriber volume and marketing activity had stronger short-term impact to revenue than churn rate in this dataset. This model achieved an R² of 0.82 compared to 0.40 for Linear Regression, indicating that revenue relationships were nonlinear and better captured by a tree-based approach.







Final thoughts: The model explains some relationship between revenue, active subscribers, and churn rate, but it's not very good at accurately predicting revenue.
