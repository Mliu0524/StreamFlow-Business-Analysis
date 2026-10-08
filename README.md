# StreamFlow-Business-Analysis

Project Overview:
StreamFlow is a subscription-based streaming company that's similar to companies like Netflix and Hulu. The executives at StreamFlow want to understand how the company is doing 
This Project Demonstrates end-to-end buiness analysis including:
Data Modeling, SQL calculation and data processing, Tableau visualization/ dashboard, Marketing Analytics, Predictive Modeling with Python
Additional information:
Timeframe for this project is from 01/01/2023 to 09/30/2026.

Data Architectures:
<img width="1805" height="664" alt="image" src="https://github.com/user-attachments/assets/992479cd-2a0d-4177-8bfa-c260fa7e7587" />


Key Business Questions:
1.Why we spot revenue dropping since May 2025? What contributed the huge revenue dip in March 2026?
What the subscriber's growth trend looking like?
What drives customer churn?
Which marketing campaigns generate the highest ROAS?
How much a customer worth over their lifetime with the company?
Can customer churns be predicted before they take actions?


SQL Findings:
1. Since revenue = active subscriber count * ARPU, revenue decrease has to be either caused by drop in active subscribers or ARPU or both
   <img width="997" height="813" alt="image" src="https://github.com/user-attachments/assets/1cf16260-27f6-4633-8109-18e757010c5a" />
After comparing the trend of revenue, ARPU and monthly active subscribers, ARPU stays steady and revenue moves in the similar speed as active subscribers.
Notice how revenue May 2025 peak aligns with the peak in active subscriber June 2025,
as most of the active subscribers June 2025 contributes to revenue in May 2025. We can confidently say that loss of active subscribers caused revenue drop.
Hence, we should collaborate with marketing team to find creative methods to drive active subscribers' growth.


2. Subscriber Growth Analysis
 <img width="1033" height="792" alt="image" src="https://github.com/user-attachments/assets/ea1eecd7-680a-4b30-a7aa-21a4b01dab59" />

Findings:
Streamnflow has been gaining new subscribers on a steady pace around 600-700 new subscribers monthly since 2023. A crash in new subscribers happened from March 2026 till May 2026 when it comes to bringing new customers in.
Around the same time, we also witness the number of customers leaving reaching first time high. These findings confirmed the huge dip in revenue March 2026. Since 2023, Streamflow obtains positive net subscriber growth 
until October 2025. October 2025, we witness net subscriber reaches 0, we started to see net subscriber count becoming positive due to churned customer started to drop after March 2026(Postive) However, Streamflow still needs to discover the root cause of trouble gaining new subscribers.
Sugguestions: 
Collaborate with other teams such as marketing team and IT team to understand if the decrease in CTR, conversion rate and customer support satisfaction has played a huge part in revenue dropping.



Create date table with first day of the month starting 01/01/2023 to 09/30/2026 so we can analyze data by month:

<img width="518" height="457" alt="image" src="https://github.com/user-attachments/assets/72461075-3bae-45c9-8238-3f733a68a880" />

Calculate the numbers of subscribers every beginning of the month:

<img width="529" height="514" alt="image" src="https://github.com/user-attachments/assets/4d790e13-e361-432d-a1db-9a36b63fbbef" />

Calculate churned customers at beginning of the month:

<img width="491" height="559" alt="image" src="https://github.com/user-attachments/assets/0ca880b6-b684-47c9-8346-fa6a59c6b1eb" />

Calculate monthly revenue:
<img width="944" height="558" alt="image" src="https://github.com/user-attachments/assets/17d4e3ff-a33c-4e92-b5b2-db1af43fab81" />

This is an initial EDA to spot trends and outliers. Will demonstrate usage in Tableau to further analyze.


Note: Notice that revenue and marketing metrics we collected is not suitable for data processing and data visualization. The raw data in Fact revenue table and marketing table has start date and end date, since we need to analyze data on monthly basis, we're going to slice and dice the data combined with date dimension. We're going to look at by each customer each month, so we can compare start date and end date with month start (date dim table), and use ActiveBOM(start of month) and ActiveEOM(end of month), ActiveBOM and ActiveEOM will be assigned to either 1 or 0 depends on whether a customer churns by start of the month and end of the month


<img width="818" height="803" alt="image" src="https://github.com/user-attachments/assets/0ccfcdbb-938e-492d-821e-d2d06baef042" />


This prepares data for analyzing in Tableau. Note: for the subscription that's still active, I replaced end date with 9/30/2026 as this is the hard end date for this project.


We notice that revenue has been dropping since May 2025. By looking at the trend for active subscribers every month, we spot active subscribers started dropping since June 2025. I believe active subscribers is one of 
the driving force affecting revenue. But i want to do some exploration to see what other factors we have.

Data preparation:
Query to turn raw data into format that's suitable for fitting regression model
<img width="792" height="737" alt="image" src="https://github.com/user-attachments/assets/91d19559-ae72-4090-ba2f-5c19fc3769dc" />

Now I'm trying with multiple linear regression to fit the model:
<img width="978" height="820" alt="image" src="https://github.com/user-attachments/assets/9b466988-edcb-4b81-a532-69059c4475ba" />
Interpretation: 
Multiple regression analysis found that subscriber-related metrics were the primary drivers of revenue performance. Active subscribers and new subscriber acquisition exhibited positive relationships with revenue, while churn had a negative relationship. Monthly marketing spend showed little direct impact on revenue after accounting for subscriber behavior, suggesting its influence is primarily indirect through customer acquisition and retention.

Also need to look at R^2= 0.583149, which is not bad but I want to try other models to see if we get better results.
<img width="1061" height="535" alt="image" src="https://github.com/user-attachments/assets/f28ca93e-1c34-4a47-8654-2af5d6eb5eb6" />

Try decision tree model:
<img width="934" height="654" alt="image" src="https://github.com/user-attachments/assets/9057ceb0-2c00-41c4-8f12-a3ec21c3499b" />
Train R²: 0.9624216966294823
Test R²: 0.915504271082746

Conclusion: The model explains 96.2% of the revenue variation in the training dataset. The model explains 91.6% of the revenue variation in unseen months.
Churn negatively impacts revenue, but the overall size of the active subscriber base is by far the dominant revenue driver. The Decision Tree attributed over 90% of predictive importance to Active Subscribers, while churn accounted for about 7%.


Combine conclusion above with SQL manipulation, we confidently say the reason why revenue has been dropping since May 2025 is due to active subscriber base shrinking.
I investigated the decline in monthly revenue after May 2025 using correlation analysis, multiple linear regression, and decision tree regression. While linear regression explained 58% of revenue variation, the decision tree achieved a test R² of 0.92, indicating non-linear relationships between business drivers and revenue. Feature importance analysis showed that Active Subscribers accounted for approximately 90.5% of the model's predictive power, far exceeding churn (7.1%), new subscriber acquisition (2.4%), and marketing spend (0%). These findings suggest the revenue decline was primarily driven by contraction of the active subscriber base, with churn contributing indirectly through subscriber loss.



<img width="1170" height="676" alt="image" src="https://github.com/user-attachments/assets/feca7231-da08-400f-9dd4-9f513037d836" />



Revenue and Active Subscriber trends moved closely together throughout most of the analysis period, indicating that subscriber volume was a major revenue driver. Decision Tree Regression confirmed this finding, attributing over 90% of model importance to Active Subscribers. However, the sharp revenue decline observed after the revenue peak was significantly larger than the decline in Active Subscribers, suggesting additional factors such as changes in ARPU, pricing, subscription mix, or revenue recognition may also have contributed to the downturn.



Current Month Revenue KPIs:
<img width="1002" height="798" alt="image" src="https://github.com/user-attachments/assets/a247b353-66ab-4c93-b118-1fcd1181c7b7" />
Summary:
Streamflow September reaches $106.71k in revenue, which is 0.07% lower comparing to previous month. However, ARPU increases by 0.06% which is $17.16 on average. Family plan tops other plans having $37.34k in revenue.
CLV so far reaches $19.49M in revenue.


