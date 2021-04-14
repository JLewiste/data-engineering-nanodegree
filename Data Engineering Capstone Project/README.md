### Data Engineering Nanodegree Capstone Project

#### Project Summary
The purpose of this project is to investigate issues that are related to US immigration such as:

1. The gender distribution of the US immigrants.
2. Visa distribution of the US immigrants.
3. Average age per immigrant.
4. Average temperature per month per city.

We will be using three different datasets for this project.

1. I94 immigration dataset from 2016
2. City temperature dataset from Kaggle
3. US city demographic data from OpenSoft.

The end goal of this project is to design four dimension tables and 1 fact table. 

- Dimension tables:
  - Cities
  - Immigrants
  - Monthly average city temperature
  - Monthly averate city time

- Fact table:
  - Immigration.

Spark will be utilized for ETL tasks and the results will be stored in parquet for downstream analysis.

## Datasets

We will be using these three datasets for this project:

1. I94 Immigration dataset: This dataset originated from the US National Tourism and Trade Office. It contains various information regarding international visitors coming to USA. Dataset link: https://travel.trade.gov/research/reports/i94/historical/2016.html

2. World temperature dataset: This dataset originated from Kaggle and contains average weather temperatures by city. Dataset link: https://www.kaggle.com/berkeleyearth/climate-change-earth-surface-temperature-data

3. US city demographic dataset: This dataset originated from Opensoft and contains information about the demographics of all US cities such as average age, male and female population. Dataset link: https://public.opendatasoft.com/explore/dataset/us-cities-demographics/export/

#### Data model
These are the details for the data schema:

**Staging Tables**

- staging_i94_df
  - id
  - date
  - city_code
  - state_code
  - age
  - gender
  - visa_type
  - count
  
- staging_temp_df
  - year
  - month
  - city_code
  - city_name
  - avg_temperature
  - lat
  - long

- staging_demo_df
  - city_code
  - state_code
  - city_name
  - median_age
  - pct_male_pop
  - pct_female_pop
  - pct_veterans
  - pct_foreign_born
  - pct_native_american
  - pct_asian
  - pct_black
  - pct_hispanic_or_latino
  - pct_white
  - total_pop

**Fact Table**

- immigration_df
  - id
  - state_code
  - city_code
  - date
  - count

**Dimension Tables**

- immigrant_df
  - id
  - gender
  - age
  - visa_type

- city_df
  - city_code
  - state_code
  - city_name
  - median_age
  - pct_male_pop
  - pct_female_pop
  - pct_veterans
  - pct_foreign_born
  - pct_native_american
  - pct_asian
  - pct_black
  - pct_hispanic_or_latino
  - pct_white
  - total_pop
  - lat
  - long

- monthly_city_temp_df
  - city_code
  - year
  - month
  - avg_temperature

- time_df
  - date
  - dayofweek
  - weekofyear
  - month

#### Data dictionary 

**Fact Table**

- immigration_df
  - id: id
  - state_code: state code of arrival city
  - city_code: city port code of arrival city
  - date: date of arrival
  - count: count of immigrant's entries into the US

**Dimension Tables**

- immigrant_df
  - id: id of immigrant
  - gender: gender of immigrant
  - age: age of immigrant
  - visa_type: immigrant's visa type

- city_df
  - city_code: city port code
  - state_code: state code of the city
  - city_name: name of the city
  - median_age: median age of the city
  - pct_male_pop: city's male population in percentage
  - pct_female_pop: city's female population in percentage
  - pct_veterans: city's veteran population in percentage
  - pct_foreign_born: city's foreign born population in percentage
  - pct_native_american: city's native american population in percentage
  - pct_asian: city's asian population in percentage
  - pct_black: city's black population in percentage
  - pct_hispanic_or_latino: city's hispanic or latino population in percentage
  - pct_white: city's white population in percentage
  - total_pop: city's total population
  - lat: latitude of the city
  - long: longitude of the city

- monthly_city_temp_df
  - city_code: city port code
  - year: year
  - month: month
  - avg_temperature: average temperature in city for given month

- time_df
  - date: date
  - dayofweek: day of the week
  - weekofyear: week of year
  - month: month

#### Complete Project Write Up
* Clearly state the rationale for the choice of tools and technologies for the project:
    - For this project, I have used Spark since it can easily handle huge datasets that come in multiple file formats. Spark SQL was used to process the input files into dataframes and manipulated via standard SQL join operations to create the tables.
    
* Propose how often the data should be updated and why.
    - The data update cycle is typically chosen on two criteria. One is the reporting cycle, the other is the availabilty of new data to be fed into the system. For example, if new batch of average temperature can be made available at monthly interval, we might settle for monthly data refreshing cycle.
    
### Scenarios
* Write a description of how you would approach the problem differently under the following scenarios:
    1. the data was increased by 100x.
        - Utilize Amazon Redshift service: It is an analytical database that is optimized for aggregation and read-heavy workloads.
    2. The data populates a dashboard that must be updated on a daily basis by 7am every day.
        - Utilize Airflow. We can create DAG retries and emails for the purpose of failure notifications.
    3. The database needed to be accessed by 100+ people.
        - Utilize Redshift. It has auto-scaling capabilities and good read performance, with larger capacity to serve more users, and workload management to ensure equitable usage of resources across users.