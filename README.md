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

- (From what I can remember) The main question we agreed on is "which factors influence aviation safety across time''. But we also discussed whether we are interested in an explanatory model versus a predictive model, and most voted on a predictive model.

# Some notes about data so far
All train test splits use random seed 945. 
- If we regress yearly number of accidents (target) as a function of the year (predictor), from 2006 through 2024, the accidents decrease over time; the test rejects null hypothesis that coefficient of year is zero, with $p = 0.023$. The $R^2$ value is $0.337$, adjusted $R^2$ is $0.286$. This uses only 15 observations so may be unreliable. 
- If we do an ordinary linear regression with year as a feature variable and months as categorical variables, with "number of accidents per month" as the target variable, a $95$% confidence interval for the coefficient of year is $[-8.108,-3.923]$, so accidents are definitely decreasing yearly. The adjusted $R^2$ for this model is $0.208$. In comparison to January (the baseline month), June, July, August, and February have positive coefficients ($p < 0.05$), so we expect more accidents in these months compared to January. 
- If we introduce "percentage of accidents due to human factors" or "pct_human_factors" as a feature variable, the $95$% confidence interval for the coefficient of year changes to $[-6.399,-2.194]$, which means that increasing "year" now has less of an effect in decreasing accidents. This is because "year" is negatively correlated with "pct_human_factors", which has a positive coefficient, so the decrease in accidents over time is accounted for somewhat by pct_human_factor decreasing over time.  The correlation coefficient between "year" and "pct_human_factors" is $-0.328$, so "pct_human_factors" has decreased over time. Some of the decrease in monthly accidents over time is probably due to the decrease in accidents due to human factors. The main other "Primary Problem" for accidents other than human factors is "Aircraft". The correlation between "Year" and "pct_aircraft" is $+0.138$, so there is a slight increase in *percentage* of accidents due to aircraft problems over time. The $p$-values for these correlation coefficients have $p < 0.01$.  However, if we look at the *total* monthly number of accidents due to "aircraft" instead of percentage, there is a slight negative correlation with year, so accidents due to aircraft have decreased over time, just less so compared to other categories, and the $p$-value for the correlation is not significant ($p \approx 0.08$). The adjusted $R^2$ for this model is $0.296$. 
- If we further add in "percentage of accidents FAR 91" as another predictor, it becomes more complicated.
- We did a time series forecast using ARIMA/SARIMA, and some other plots.






