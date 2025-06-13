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
-  If we redo this restricting to commerical flights (FAR Part 121), the $R^2$ value increased to $0.702$ (adjusted $0.679$), and the $p$ value for the coefficient of year is zero (to 3 decimal places).
-  If instead of commerical flights, we consider Far Part 91 (general aviation, non-commerical flights), accidents counts are *increasing* over time; test rejects hypothesis that coefficient of year is zero with $p < 0.016$. If we restrict to Far Part 135 (other types of commercial flights such as charter flights), it is unclear whether the accidents are increasing or decreasing over time (the test cannot reject hypothesis that coefficient of year is zero ($p > 0.05$)). There is much less data for Part 135 than 121 and 91 (about 60000 Part 121 accidents,  27000 Part 91, 4000 Part 135, 1000 other). 
- If we do an ordinary linear regression with year as a feature variable and months as categorical variables, with "number of accidents per month" as the target variable, only July has a statistically significant positive coefficient, meaning that more accidents are expected in July than January. If we specialise this to just Part 121 flights, the only statistically significant month is February which has a negative coefficient (less accidents in February versus January). If we specialise instead to Part 91 flights, than almost every non-Winter month has a statistically significant positive coefficient (this is likely because far fewer Part 91 flights occurr during the Winter, whereas Part 121 flights continue throughout Winter). 
- The correlation coefficient between "year" and "pct_human_factors" (percent of accidents/incidents due to human factors) is $-0.328$, so "pct_human_factors" has decreased over time. Some of the decrease in monthly accidents over time is probably due to the decrease in accidents due to human factors. The main other "Primary Problem" for accidents other than human factors is "Aircraft". The correlation between "Year" and "pct_aircraft" (problems due to aircraft) is $+0.138$, so there is a slight increase in *percentage* of accidents due to aircraft problems over time. The $p$-values for these correlation coefficients have $p < 0.01$.  For the *total* monthly number of accidents due to "aircraft" instead of percentage, there is a slight negative correlation with year, so accidents due to aircraft have decreased over time, just less so compared to other categories, and the $p$-value for the correlation is not significant ($p \approx 0.08$).
- If we redo the above but restrict to commercial flights (FAR Part 121), the accidents due to human factors are decreasing over time (both percentage and number), and the number of accidents due to aircraft is decreasing over time. We cannot reject the null hypothesis that the proportion of accidents due to aircraft has remained constant over time ($p \approx 0.72$). 
- We did a time series forecast using ARIMA/SARIMA, and some other plots.






