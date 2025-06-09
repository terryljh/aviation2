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

- The main question we agreed on is ``which factors influence aviation safety across time''. But we also discussed whether we are interested in an explanatory model versus a predictive model, and most voted on a predictive model.

# Some notes about what data suggests so far
- If we do an ordinary linear regression with time as a feature variable, and months as categorical variables, with "number of accidents per month" as the target variable, the coefficient of "year" is negative (p-value is essentially zero), so accidents are decreasing yearly. If we just do the regression with months or time as a single feature variable, the test is inconclusive (I think this is because there is huge monthly variation within years). 

# Meeting  6/9
- Does airports.csv need to be changed to airport_codes.csv?
- Does it make sense to use percentages as features (e.g. pct human factors, pct FAR 91)?






