# Modeling and Results

To better understand trends in aviation accidents, we applied both linear regression models (OLS) and seasonal time series models (SARIMA). The OLS models were used to examine overall trends in accident counts over time, such as whether incidents have increased or decreased by year or month. In contrast, SARIMA models were used to forecast future accident patterns by accounting for both trend and seasonality. These models were applied separately to different regulatory categories (FAR 91, FAR 121, and FAR 135) to explore how accident dynamics differ across types of operations.

## OLS Models

- If we do linear regression on the yearly number of incidents, with year as the "predictor" and "number of accidents" as the target, from 2006 through 2024, the accidents decrease over time ($p = 0.023$). The $R^2$ value is $0.337$, adjusted $R^2$ is $0.286$. Much of the variance is unexplained in this plot, so we explore this further below. 
<p align="center">
  <img src="yearvsincident.png" alt="Trend in incidents" width="400">
</p>

 - If we redo this considering only data from commercial flights (FAR Part 121), there is much less unexplained variance ($R^2 = 0.696$), and there is still a clear decreasing trend over time ($p=0.000$).
<p align="center">
          <img src="yearincidence121.png" alt="Trend in incidents" width="400">
</p>

  - If, still within FAR Part 121, we further restrict incidents according to their "Primary Problem", then:
    - There are no statistically significant trends for:
      - "Procedure" ($\sim 300$ incidents per year, but not introduced as a category until 2009)
      - "Weather" ($\sim 100$ incidents per year)
      - "Environment - Non Weather Related" ($\sim 75$ incidents per year)
      - "ATC Equipment / Nav Facility / Buildings" ($\sim 50$ incidents per year),
      -  "Chart or publication ($\sim 50$ incidents per year)
      -  "Airspace structure ($\sim 20$ incidents per year)
      -  "Software and Automation" ($\sim 20$ incidents per year)
    - Incidents due to "Human Factors" are decreasing yearly ($p = 0.024$, $\sim 1000$ incidents per year, coefficient of year is $-22$).
      <p align="center">
          <img src="humanfactors.png" alt="Trend in incidents" width="400">
      </p>
    - Incidents due to "Aircraft" are decreasing yearly ($p = 0.014$, $\sim 1000$ incidents per year, coefficient of year is $-24.78$),
      <p align="center">
          <img src="aircraft.png" alt="Trend in incidents" width="400">
      </p>
    - Incidents due to "Company Policy" are decreasing yearly ($p = 0.000$, coefficient of year is $-17.23$). On average there were around 100 incidents per year due to "Company Policy", but by 2023 they decreased to effectively zero. This is one of the most significant part of this particular dataset; it seems to suggest that companies are actually responding quite well to feedback, especially considering that the ASRS data is anonymised. The variance is fairly well explained by the linear fit ($R^2 = 0.710$). 
      <p align="center">
          <img src="companypolicy.png" alt="Trend in incidents" width="400">
      </p>
    - At a guess, only 50% of incidents report information about the airspace, but if we restrict incidents to airspace, then:
        - For Classes A, B, E airspace, and for those with airspace not specified, there is clear decrease in the incidents over time.

      <table>
  <tr>
    <td align="center">
      <img src="airspaceA.png" alt="Airspace A" width="300"><br>
      <sub>Airspace A</sub>
    </td>
    <td align="center">
      <img src="airspaceB.png" alt="Airspace B" width="300"><br>
      <sub>Airspace B</sub>
    </td>
  </tr>
  <tr>
    <td align="center">
      <img src="airspaceE.png" alt="Airspace E" width="300"><br>
      <sub>Airspace E</sub>
    </td>
    <td align="center">
      <img src="noairspace.png" alt="No Airspace" width="300"><br>
      <sub>No Airspace</sub>
    </td>
  </tr>
</table>
      
   - For Class C airspace, there is no statistically significant trend. 
   - For Class D airspace, there is an *increase* in incidents over time, but it is only marginally significant ($p = 0.054$), on average around 50 incidents per year.
<p align="center">
          <img src="airspaceD.png" alt="Trend in incidents" width="400">
</p>
- If instead of commerical flights, we consider Far Part 91 (general aviation, non-commerical flights), incident counts are increasing over time ($p = 0.016$). Because reporting incidents for Part 91 flights is likely less standardised than for commerical flights, it is possible the increasing trend here is result of increased reporting (or just an increased number of flights taken). 
  <p align="center">
          <img src="far91.png" alt="Trend in incidents" width="400">
  </p>
  
- If we restrict to Far Part 135 (other types of commercial flights such as charter flights), there is no statistically significant trend. There is much less data for Part 135 than 121 and 91 (about 60000 Part 121 accidents,  27000 Part 91, 4000 Part 135, 1000 other).

- If we do an ordinary linear regression with year as a feature variable and months as categorical variables, with "number of accidents per month" as the target variable, only July has a statistically significant positive coefficient, meaning that more accidents are expected in July than January. If we specialise this to just Part 121 flights, the only statistically significant month is February which has a negative coefficient (less accidents in February versus January), which could even be due to February having the least number of days. If we specialise instead to Part 91 flights, than almost every non-Winter month has a statistically significant positive coefficient (this is likely because far fewer Part 91 flights occurr during the Winter, whereas Part 121 flights continue throughout Winter). So it seems that months are important to use as categorical variables for Part 91 flights, but not necessarily for Part 121 flights. 
- The correlation coefficient between "year" and "pct_human_factors" (percent of accidents/incidents due to human factors) is $-0.328$, so "pct_human_factors" has decreased over time. Some of the decrease in monthly accidents over time is probably due to the decrease in accidents due to human factors. The main other "Primary Problem" for accidents other than human factors is "Aircraft". The correlation between "Year" and "pct_aircraft" (problems due to aircraft) is $+0.138$, so there is a slight increase in *percentage* of accidents due to aircraft problems over time. The $p$-values for these correlation coefficients have $p < 0.01$.  For the *total* monthly number of accidents due to "aircraft" instead of percentage, there is a slight negative correlation with year, so accidents due to aircraft have decreased over time, just less so compared to other categories, and the $p$-value for the correlation is not significant ($p \approx 0.08$).
- If we redo the above but restrict to commercial flights (FAR Part 121), the accidents due to human factors are decreasing over time (both percentage and number), and the number of accidents due to aircraft is decreasing over time. We cannot reject the null hypothesis that the proportion of accidents due to aircraft has remained constant over time ($p \approx 0.72$).

## SARIMA Model Outputs
We used SARIMA models because they are well-suited for time series data that exhibit trends and non-stationarity. The plots below show the results of a SARIMA model applied to historical aviation incident data. In the SARIMA forecasts below, the blue line represents actual data from approximately 2006 up until 2024, and the green line shows the forecast into 2024 and beyond. The shaded gray area reflects the 95% confidence interval of the forecast.


### SARIMA 121
Here, we conducted the SARIMA with part 121. While the early years (e.g., 2005–2009) saw higher and more volatile accident counts, the SARIMA model predicts that future rates will remain comparatively lower and more stable. This may suggest improvements in safety protocols or technology, though further analysis would be needed to confirm causal factors.
![SARIMA 121](SARIMA_121.png)  
![SARIMA 121 Zoomed](SARIMA_121_Zoomed.png)  

With a five year forecast, it appears that accident rates tend to stay relatively low.
![SARIMA 121_Extended](SARIMA_121_Extended.png) 

## SARIMA 121 in 5 years
![SARIMA Forecast 121](SARIMA_Forcast_121.png)  

## SARIMA 91 
Here, we conducted the SARIMA with part 91. While the early years (e.g., 2005-2009) saw higher and more volatile accident counts, the SARIMA model predicts that future rates will remain comparatively lower and more stable. This may suggest improvements in safety protocols or technology, though again, further analysis would be needed to confirm causal factors.
![SARIMA Forecast 91](SARIMA_Forecast_91.png) 

With a five year forecast, it appears that accident rates tend to stay relatively low.
![SARIMA Forecast 5 Years](SARIMA_Forecast_5_years.png) 

