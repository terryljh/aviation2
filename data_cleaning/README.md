# Data Cleaning

Data is from Aviation Safety Reporting System (ASRS) online database: https://asrs.arc.nasa.gov/search/database.html

Rather than creating new CSV's, we cleaned the dataframe inside the notebook file directly. A quick summary of some data cleaning we did:

- The dataset has headers, then the first row is the actual headings, so we replace headers with the first row.
- A small number of aviation incidents had mulitple reports for the same incident. We cleaned the data to only consider the first report for some columns, since we don't want repeated columns in the dataset, to simplify things. For some incidents (likely involving multiple aircraft in different categories), the reports contained two different types in some categories. For FAR Parts (meaning commerical aviation, general aviation, etc) , we excluded the small number with multiple different FAR Parts. 
