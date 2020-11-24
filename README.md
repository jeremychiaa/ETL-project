# ETL-Project
## Victorian Vehicle Accident Data

### Purpose
- To investigate the relationship between the busiest road intersections and the frequency of fatal and injury crashes in Victoria.

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

#### Demography data from ABS/Census
- 

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
- 

#### Demography data from ABS/Census
- 

### Data Loading
