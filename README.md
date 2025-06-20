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
- 
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






