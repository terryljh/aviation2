# Exploratory Data Analysis
First we began by exploring the data by looking at the following features:
- accidents over time
- accidents per state
- accidents in the top 3 states over time 
- accidents per country
- accidents by FAR 121 and Airspace Category
- accidents by different FAR parts
- accidents by time of day


## Accidents over Time
From the scatterplot, accidents appear to be decreasing over time, although it is not super clear and further investigation is needed. 
![Accidents per Year](accidents_per_year.png)
## Accidents per State
In accidents per state we can see that the top 3 states for accidents included California, Texas, and Florida. 
![Accidents per State](accidents_per_state.png)

## Accidents per Top 3 States Over Time
In accidents per state we can see that the top 3 states for accidents have been decreasing over time, especially since the year of 2015, where accident rates where at their peak. 
![Accidents per top 3 states](accidents_per_top_3_states.png)

## Accidents per Country
This dataset was of flights coming from the United States to a different country so it makes sense that the United States had the highest incident rate, followed by the Philippines
![Accidents per Country](accidents_per_country.png)

## Accidents by FAR 121 and Airspace Category

We examined how accidents under **FAR 121 (commercial operations)** were distributed across different types of airspace. Below are the scatterplots broken down by airspace classifications A through E.

### Overall Accidents Under FAR 121
This chart shows total accident counts for FAR 121, regardless of airspace.

![Accidents FAR 121](accidents_far_121.png)


### Accidents in Airspace A
![Accidents Airspace A](accidents_FAR_121_Airspace_A.png)

### Accidents in Airspace B
![Accidents Airspace B](accidents_FAR_121_Airspace_B.png)

### Accidents in Airspace C
![Accidents Airspace C](accidents_FAR_121_Airspace_C.png)

### Accidents in Airspace D
![Accidents Airspace D](accidents_FAR_121_Airspace_D.png)

### Accidents in Airspace E
![Accidents Airspace E](accidents_FAR_121_Airspace_E.png)

## Accidents by Time of Day

We also examined when accidents occurred across different times of day. This plot helps highlight any trends associated with daylight vs night operations.

![Accidents by Time of Day](accidents_by_time_of_day.png)

---

## Accidents by FAR Part

The Federal Aviation Regulations (FARs) categorize aviation operations into different parts. Below we show how accident counts differ across **Part 91**, **Part 121**, and **Part 135** operations.

### Part 91: General Aviation (non-commercial)

![Accidents FAR 91](accidents_FAR_91.png)

---

### Part 121: Scheduled Air Carriers (e.g., airlines)

![Accidents FAR 121](accidents_far_121.png)

---

### Part 135: On-Demand Charter, Air Taxi, etc.

![Accidents FAR 135](accidents_FAR_135.png)


