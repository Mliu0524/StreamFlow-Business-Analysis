# StreamFlow-Business-Analysis







1. The most recent data StreamFlow has is till September, 2026. The VP of revenue and operations wants to know what's the revenue forecaste is going to be for October, 2026.
First, I used SQL to do data aggregation, so we have a dataset that's ready to use for statistical analysis.
I chose multiple linear regression here, using number of subscribers at start and churn rate to predict revenue. Then fit the model.
Coefficients:
[58.70180039, -9218.27815481]
Intercept:
-48529.451345181194
Interpretation: we get 58.7 dollars increase in revenue when we gain 1 active subscriber. We get 92.18 dollars decreased in revenue
when we lose 1 subscriber. Explaining intercept won't be useful here as we will never have 0 subscriber and 0 churn rate.
Now let's look at R^2. print(model.score(X, y)) we get R^2 =0.399650049697893
Interpretation: About 40% of the variation in Monthly Revenue can be explained by ActiveAtStart and ChurnRate.
RMSE: 45940.137062642425 and our average monthly revenue is 69834.27422222222. average monthly revenue/RMSE = 0.658 which is bad
How far off your predictions are from actual revenue, on average. So the model's typical error is about 66% of the average monthly revenue.

Final thoughts: The model explains some relationship between revenue, active subscribers, and churn rate, but it's not very good at accurately predicting revenue.
