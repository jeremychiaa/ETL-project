# ETL-Project
## Victorian Vehicle Accident Data

### Purpose
- To investigate the relationship between the busiest road intersections and the frequency of fatal and injury crashes in Victoria

### The working questions
1. What are the busiest intersections in Victoria?
2. What are the common vehicle types (cars, trucks, motorcycles etc.) involved in fatal and injury crashes in those intersections?
3. What is the age demographics (by suburb) of motorists?

### Team members
1. Alison Beer (AB)
2. Jeremy Chia (JC)
3. Sasith Wijebandara (SW)

### Task breakdown:
- AB will focus on ABS/Census data
- JC will focus on accident data
- SW will focus on traffic volume data
- Datasets will be able to be joined on suburbs or postcodes

### Description and outline
Clean and transform the data sets to allow analysis and relationships to be created between the 3 different data sets. 

### Data Extraction
#### All the data extracted are in a CSV format

#### Victoria Vehicle Accident Data
- https://discover.data.vic.gov.au/dataset/crashes-last-five-years1

#### Victoria Traffic Volume Data
- https://vicroadsopendata-vicroadsmaps.opendata.arcgis.com/datasets/traffic-volume/data?geometry=124.216%2C-39.579%2C166.030%2C-33.402

#### Demographic data from ABS
- Australian Bureau of Statistics (ABS), 2016 census data, csv files downloaded from: https://datapacks.censusdata.abs.gov.au/datapacks/

### Data Transformation
#### Victoria Vehicle Accident Data
Structuring
- The unnecessary columns were removed from the dataset to only maintain the relevant data within the dataset. This restructuring allow users to have more ease of use and analysis
- The dataset was filtered to crash data that occured in 2018

Cleaning
- Missing data were handled by dropping them. As the number of missing data are insignificant in comparison to the number of data points, this option will minimise the skewing of the data
- The columns headers were converted to lowercase

Enriching
- As the dataset consisted of the latitude and longitude data of locations, the suburb and postcodes of those locations were pulled using Google's Reverse Geocoding API. This allows for exploratory analysis to be done specific to suburbs and postcodes.
- The other datasets will be able to merge on the suburbs and postcodes columns for analysis

#### Victoria Traffic Volume Data
- To further our understanding of the Victoria Vehicle Accident Data we wanted to understand the traffic volume of the Victorian postcodes. This would allow us to test the relationship between traffic volume and accidents in certain postcodes.
- The Department of Transport Open Data provides data on traffic volumes for freeways (excluding tolls) and arterial roads in Victoria. Annual average daily traffic volume is provided with values derived from traffic surveys or estimates for the current year. 

Structuring
- Postcode data is not provided in this dataset; however, the dataset did provide the TIS_ID (Traffic Information System Id) which is used for joining on to spatial datasets within The Department of Transport Open Data. Joining the Traffic Volume dataset to the homogenous traffic flow data set on TIS_ID, data extracted from the Traffic Information System, outputted data on the Latitude and Longitude of Midpoint of Length Segment for each TIS_ID.
- Using the Latitude and Longitude data the cordinates were reverse geocoded using Google Maps API to output data on the suburb and postcode.
- The final step of transforming this dataset was to group the data by postcode so traffic volume data was represented for each post code in the dataset.

Cleaning
- Postcode and suburb data were missing for an insignificant number of cordinates as a result of the reverse geocoding. This missing data was handled by dropping them.
- Column headers were renamed to more appropriate callings.

Enriching
- The other datasets will be able to merge on the postcode column for analysis

#### Demographic data from ABS
- 2016 census data from the ABS was used to provide a picture of the population, by age and sex, for each postcode. 
- The ABS data consisted of three csv files. 
- Two csv's contained the demographic data in four year age groups, by gender and for all persons, and Postal Area (POA) classification. 
- POAs enable the comparison of ABS data with other data collected using postcodes. POAs are incorporated into the Australian Statistical Geography Standard (ASGS) as a non-ABS structure. 
- The third csv file provided the ASGS non-ABS structures which included POA classification and postcode. 

Cleaning
- All csv's were imported into Pandas as dataframes for cleaning.
- The two dataframes with the demographic data where merged together using an outer join on the POA code. 
- The columns of non-driving age were removed (0-14 years and 80+ years).
- The ASGS Structure dataframe was filtered to only include the POA classification. This filtered dataframe was then merged with the demographic dataframe using a left join on the POA code. 
- The index of the final dataframe was set to postcode.
- The POA code column was no longer of use and deleted.
- The final dataframe was written to a csv file in preparation for importing into an sql database. 

### Data Loading
- Google Cloud SQL was chosen to store our data as it was convenient for us to load our seperate tables from remote computers to one single database
