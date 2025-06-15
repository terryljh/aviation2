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
    -  If we further restrict incidents according to their "Primary Problem", then:
        - There are no statistically significant trends for:
           - "Procedure" ($\sim 300$ incidents per year, but not introduced as a category until 2009)
           - "Weather" ($\sim 100$ incidents per year)
           - "Environment - Non Weather Related" ($\sim 75$ incidents per year)
           - "ATC Equipment / Nav Facility / Buildings" ($\sim 50$ incidents per year),
           -  "Chart or publication ($\sim 50$ incidents per year)
           -  "Airspace structure ($\sim 20$ incidents per year)
           -  "Software and Automation" ($\sim 20$ incidents per year)
        - Incidents due to "Human Factors" are decreasing yearly ($p = 0.024$, $\sim 1000$ incidents per year, coefficient of year is $-22$),
        - Incidents due to "Aircraft" are decreasing yearly ($p = 0.014$, $\sim 1000$ incidents per year, coefficient of year is $-24.78$),
        - Incidents due to "Company Policy" are decreasing yearly ($p = 0.000$, coefficient of year is $-17.23$). On average there were around 100 incidents per year due to "Company Policy", but by 2023 they decreased to effectively zero.
    - At a guess, only 60% of incidents report information about the airspace, but if we restrict incidents to airspace, then:
        - For Class A airspace there is no statistically significant trend, but if we exclude outliers 2006-2008 which seem to have no data, there is clear decrease in the incidents over time ($p= 0.007$, coefficient of year is $-12.14$, around 350 yearly incidents on average).
        - For Class B airspace there is no statistically significant trend, over any range of years (on average around 300 incidents per year).
        - For Class C airspace, (on average around 150 incidents per year), there is a clear *increase* in incidents over time ($p = 0.006$). The coefficient of year is 6.40, with a 95% confidence interval for the year being $[2.267,10.529]$. 
        - For Class D airspace, (on average around 200 incidents per year), there is a clear *increase* in incidents over time ($p = 0.000$). The coefficient of year is 15.73, with a 95% confidence interval for the year being $[10.039,21.417]$. 
-  If instead of commerical flights, we consider Far Part 91 (general aviation, non-commerical flights), accidents counts are *increasing* over time; test rejects hypothesis that coefficient of year is zero with $p < 0.016$. If we restrict to Far Part 135 (other types of commercial flights such as charter flights), it is unclear whether the accidents are increasing or decreasing over time (the test cannot reject hypothesis that coefficient of year is zero ($p > 0.05$)). There is much less data for Part 135 than 121 and 91 (about 60000 Part 121 accidents,  27000 Part 91, 4000 Part 135, 1000 other). 
- If we do an ordinary linear regression with year as a feature variable and months as categorical variables, with "number of accidents per month" as the target variable, only July has a statistically significant positive coefficient, meaning that more accidents are expected in July than January. If we specialise this to just Part 121 flights, the only statistically significant month is February which has a negative coefficient (less accidents in February versus January), which could even be due to February having the least number of days. If we specialise instead to Part 91 flights, than almost every non-Winter month has a statistically significant positive coefficient (this is likely because far fewer Part 91 flights occurr during the Winter, whereas Part 121 flights continue throughout Winter). So it seems that months are important to use as categorical variables for Part 91 flights, but not necessarily for Part 121 flights. 
- The correlation coefficient between "year" and "pct_human_factors" (percent of accidents/incidents due to human factors) is $-0.328$, so "pct_human_factors" has decreased over time. Some of the decrease in monthly accidents over time is probably due to the decrease in accidents due to human factors. The main other "Primary Problem" for accidents other than human factors is "Aircraft". The correlation between "Year" and "pct_aircraft" (problems due to aircraft) is $+0.138$, so there is a slight increase in *percentage* of accidents due to aircraft problems over time. The $p$-values for these correlation coefficients have $p < 0.01$.  For the *total* monthly number of accidents due to "aircraft" instead of percentage, there is a slight negative correlation with year, so accidents due to aircraft have decreased over time, just less so compared to other categories, and the $p$-value for the correlation is not significant ($p \approx 0.08$).
- If we redo the above but restrict to commercial flights (FAR Part 121), the accidents due to human factors are decreasing over time (both percentage and number), and the number of accidents due to aircraft is decreasing over time. We cannot reject the null hypothesis that the proportion of accidents due to aircraft has remained constant over time ($p \approx 0.72$). 
- We did a time series forecast using ARIMA/SARIMA, and some other plots.

# Some suggestions copy-pasted from slack
- We'd like to continue with predictive modeling, answering some questions like:
  - Can we predict the number of aviation incidents over the next year? (Mean, variance; probably not exact number)
  - Is the number of incidents on the rise?

- Some ideas for timeseries analysis:
  - Month-by-month
  - Bin by year
  - Bin by larger concrete chunks (decade? 5-year periods?)

- We'd also like to understand the drivers of incidents over the study period. Some ideas include,
  - How do the primary causes of incidents change over time? Human factors, ATC, aircraft failure, weather? 
  - Where are accidents occurring in airspace?
  - Where are accidents occurring geographically?
  - What type of aircraft are experiencing the most incidents? (Are Boeing aircraft, as public perception seems to indicate, less safe than Airbus/Embraer/other aircraft?)






