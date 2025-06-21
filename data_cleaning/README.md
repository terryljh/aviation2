# Data Cleaning

Data is from Aviation Safety Reporting System (ASRS) online database: https://asrs.arc.nasa.gov/search/database.html

Rather than creating new CSV's, we cleaned the dataframe inside the notebook file directly. A quick summary of some data cleaning we did:

- The dataset has headers, then the first row is the actual headings, so we replace headers with the first row.
- A small number of aviation incidents had mulitple reports for the same incident. We cleaned the data to only consider the first report for some columns, since we don't want repeated columns in the dataset, to simplify things. For some incidents (likely involving multiple aircraft in different categories), the reports contained two different types in some categories. For FAR Parts (meaning commerical aviation, general aviation, etc) , we excluded the small number with multiple different FAR Parts.
- Since our time series was based on dates, we had to remove some entries entered with obviously incorrect dates (e.g. 0 BC).
- FAR Parts of type e.g. 121; 121 were converted to 121, and similarly for the 'Light' Column.
- The airspace class column was later anonymised more, so early incidents contain information about the airport, but later incidents always have airport.zzz. We cleaned it so that all airports are renamed zzz. An earlier analysis was excluding some entries from 2005-2007 before the data was fully anonymised, and lead to some strange results.
- There were a few columns where certain things could be written in a few different ways, e.g. 'Day', 'day' and 'Daylight' in the 'Light' Column, and we cleaned these to be consistent. 
