# UCB Project 1
Analysis of climate change impact to global wine production (1995 to 20??)

## Team Members
- Brenda McCourt
- Theresa Fregoso
- Rinal Shastri
- Jeff Kim
- Madison Outland


## Research Questions
1. Which were the top wine producing countries in year X?
2. Which are the current top wine producing countries in year Y?
3. What is the correlation between temperature and wine production?
4. What is the correlation between precipitation and wine production?
5. What is the optimal temperature for maximum production?
6. What is the optimal precipitation level for maximum wine production?
7. For which countries has the climate changed to favorably or unfavorably impact wine production?

## Datasets
- International Organization of Vine and Wine
  - [Statistics](https://www.oiv.int/what-we-do/statistics)
  - [Database Discovery Tool](https://www.oiv.int/what-we-do/data-discovery-report?oiv)

- NOAA National Centers for Environmental Information
  - [Climate Data Online: Web Services Documentation](https://www.ncdc.noaa.gov/cdo-web/webservices/v2#gettingStarted)
  - [Data access](https://www.ncei.noaa.gov/access)
  - [NCEI Data Service API User Documentation](https://www.ncei.noaa.gov/support/access-data-service-api-user-documentation)

## Files
- Wine_data_all_1.xlsx
  - Wine production, export, imports, consumption data from International Organization of Vine and Wine dataset
    - Attributes: Continent, Region/Country, Product, Variable, Year, Unit
    - Metrics: Quantity (1000hl)
  - Base dataset
  - Assign country code mapping from ghcnd-countries.csv joined on country name
  - Manually assign country code where country names were slightly different 

- country_weather_adj.csv
  - Cleaned version of weather_all_country_codes3.csv
    - Create new columns for year, country code
    - Create logic to calculate average where there are multiple records for year/country code key
    - Remove original records used in calculated average
    - Append averaged records to dataset
    - Format the dataset to create new columns for datatypes
    - Export to resources folder to validate output
  
- Country_weather_cleaning.ipynb
  - Jupiter lab notebook with python code to produce country_weather_adj.csv

- Wine_Country_Weather_Data_adj.xlsx
  - Cleaned and merged version of Wine_data_all_1.xlsx and country_weather_adj.csv
  - Merged on year and countrycode key
  - Combined wine data with climate data
  
- Wine_Project_Solution_main.ipynb
  - Jupiter lab notebook with python code which sources Wine_Country_Weather_Data_adj.xlsx
  - Converts quantity (1000hl) to gallons and creates new column called quantity (gallons)
  - Formats the sequence of columns
  - Delete records where country code is null
  - Finalized dataframe as starter code to start analysis