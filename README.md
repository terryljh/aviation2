# Proposal, KPI's, stakeholders, datasets

## Datasets

- Aviation Safety Reporting System (ASRS) online database: https://asrs.arc.nasa.gov/search/database.html
- National Transportation Safety Board (NTSB) aviation accident database [https://www.ntsb.gov/Pages/AviationQueryv2.aspx](https://data.ntsb.gov/avdata)

## KPI's
- Identify trends in how aviation safety has evolved over time and explore the causes of these trends,
- Identify interventions that could improve aviation safety.
- Gain insights into aviation accidents in 2024-2025 compared to previous years. One goal is to develop a model that either:
  - Rejects the null hypothesis that air travel safety in 2024-2025 is comparable to previous years, or
  - Does not reject the null hypothesis, but after a more refined analysis, successfully explains the discrepancy between public perception of air travel safety versus the actual data. For instance, the ASRS allows database searches to restrict to certain incident types, such as those related to air traffic controllers (ATC), and it may be that such incidents receive more media coverage than other types. 

## Stakeholders

- Passengers
- Policymakers and government officials
- Airlines and aircraft operators

# Meeting 6/2

- (From what I can remember) The main question we agreed on is ``which factors influence aviation safety across time''. But we also discussed whether we are interested in an explanatory model versus a predictive model, and most voted on a predictive model.

# Some notes about data so far
All train test splits use random seed 945. 
- If we regress yearly number of accidents (target) as a function of the year (predictor), from 2006 through 2024, the accidents decrease over time; the test rejects null hypothesis that coefficient of year is zero, with $p = 0.023$. The $R^2$ value is 0.337, adjusted $R^2$ is 0.286. This uses very few observations so may be unreliable. 
- If we do an ordinary linear regression with year as a feature variable and months as categorical variables, with "number of accidents per month" as the target variable, a 95% confidence interval for the coefficient of year is $[-8.108,-3.923]$, so accidents are definitely decreasing yearly. The adjusted $R^2$ for this model is 0.208. In comparison to January (the baseline month), June, July, August, and February have positive coefficients ($p < 0.05$), so we expect more accidents in these months compared to January. 
- If we add in the percentage of accidents due to human factors in each month as a feature variable. The coefficient of "year" becomes positive. If we look at the correlation between "year" and "percentage of accidents due to human factors", there is a negative correlation -0.328, which means that the percentage of accidents due to human factors has decreased over time. I think this means that much of the decrease in total accidents may be due to the decrease in accidents due to human factors. The main other "Primary Problem" for accidents other than human factors is "Aircraft", so maybe it could be interesting if we could conclusively say e.g. that human errors in aviation safety have decreased over time, but aircraft problems have increased. If true, we could further try to identify the problem to then make safety recommendations. 
- If we further add in "percentage of accidents FAR 91", it becomes more complicated.
- We did a time series forecast using ARIMA/SARIMA, and some other plots.






