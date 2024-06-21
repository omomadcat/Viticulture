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
### Resources/
- countries_production.csv
  - All countries that have, or are, currently producing wine, for coding purposes.

- country_weather_adj.csv
  - Cleaned version of weather_all_country_codes3.csv
    - Create new columns for year, country code
    - Create logic to calculate average where there are multiple records for year/country code key
    - Remove original records used in calculated average
    - Append averaged records to dataset
    - Format the dataset to create new columns for datatypes
    - Export to resources folder to validate output

- DataType_Glossary.md 
  - Metadata for pulled climate values that were used in project
  
- ghcnd_country_codes.csv 
  - all the country codes that exist in the NCEI GSOY database

- ghcnd-countries.csv
  - Country codes paired with country name.

- GSOM_documentation.pdf
  - Glossary of all available climate values.

- GSOM_GSOY_Description_Document_v1.0.2_20200219
  - Full documentation of climate data available in the GSOM and GSOY databases.

- stationcodes.txt
  - Station code definitions, including lat, long, and city.

- weather_all_country_codes3.csv
  - Initial mostly raw data from RetrieveClimateData.ipynb

- Wine_data_all_1.xlsx
  - Initial import of data from the International Organization of Vine and Wine dataset
    - Data  pulled for Wine: production, export, imports, consumption 
      - Attributes: Continent, Region/Country, Product, Variable, Year, Unit
    - Metrics: Quantity (1000hl)
    - Pivot table on fist tab to start parsing the data
    - Base dataset
    - Assign country code mapping from ghcnd-countries.csv joined on country name
    - Manually assign country code where country names were slightly different 

- Wine_data_all_2.xlsx
  - This is the same as Wine_data_all_1.xlsx, but with addition of separate tabs for each wine variable, for the purpose of converting to .csv files if needed for coding purposes.
    - Attributes: Continent, Region/Country, Product, Variable, Year, Unit
    - Metrics: Quantity (1000hl)
  - Base dataset
  - Assign country code mapping from ghcnd-countries.csv joined on country name
  - Manually assign country code where country names were slightly different 

- wine_country_data_code_mapping.csv
  - result of updated data frame processing to include country code mapping.

### Main  
- Country_weather_cleaning.ipynb
  - Jupiter lab notebook with python code to produce country_weather_adj.csv

- Wine_Country_Weather_Data_adj.xlsx
  - Cleaned and merged version of Wine_data_all_1.xlsx and country_weather_adj.csv
  - Merged on year and country code key
  - Combined wine data with climate data
  
- Wine_Project_Solution_main.ipynb
  - Jupiter lab notebook with python code which sources Wine_Country_Weather_Data_adj.xlsx
  - Converts quantity (1000hl) to gallons and creates new column called quantity (gallons)
  - Formats the sequence of columns
  - Delete records where country code is null
  - Finalized data frame as starter code to start analysis

- PrepareCountryCodes.ipynb
  - short code to prepare the country codes to be pulled in and used for climate data retrieval

- RetrieveClimateData.ipynb
  - Code for using API to fetch data from the NOAA NCEI GSOY database.
    - Working in 10-year data chunks, from 1995-01-01 to 2023-12-31, loops through the ghcnd_country_codes.csv file to grab all available weather stations.
      - retrieves data for the variables DP10, DP1X, DT32, DX70, DX90, PRCP, RHAV, TAVG, TMAX, EMXT, EMNT, HTDD, EMXP, MNPN, MXPN, HXyz, HNyz
    - Exports created data frame to weather_all_country_codes3.csv.
   
### Conclusions
![image](https://github.com/omomadcat/Viticulture/assets/114450824/c256d8a5-8a8e-4093-87e4-8f29dc0d6587)
Based on the above graph, our data shows the following:
- Wine Production Trend: There is a significant decreasing trend in wine production in France over the years.
- Temperature Trend: There is an increasing trend in the mean maximum temperature, but the relationship is not statistically significant.
