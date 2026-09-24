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

What the subscriber's growth trend looking like?

What drives customer churn?

Which marketing campaigns generate the highest ROAS?

How much a customer worth over their lifetime with the company?

Can customer churns be predicted before they take actions?


SQL Findings:

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

