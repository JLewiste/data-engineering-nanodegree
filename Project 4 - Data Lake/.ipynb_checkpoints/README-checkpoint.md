#S3 DataLake

## Introduction
A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As their data engineer, you are tasked with building an ETL pipeline that extracts their data from S3, processes them using Spark, and loads the data back into S3 as a set of dimensional tables. This will allow their analytics team to continue finding insights in what songs their users are listening to.

You'll be able to test your database and ETL pipeline by running queries given to you by the analytics team from Sparkify and compare your results with their expected results.


## Project Description
In this project, you'll apply what you've learned on Spark and data lakes to build an ETL pipeline for a data lake hosted on S3. To complete the project, you will need to load data from S3, process the data into analytics tables using Spark, and load them back into S3. You'll deploy this Spark process on a cluster using AWS.


## Objective:
The objective of this project is to create an ETL pipeline using the data stored in S3 buckets and process that data into respective Fact and dimentsion tables using spark and then upload the parquet files back to S3.


## Dataset (Public S3 buckets):
Song Data: s3://udacity-dend/song_data 
Log Data Path: s3://udacity-dend/log_data 

<b>Schema </b>

A Star Schema would be required for optimized queries on song play queries

<b>Fact Table</b>

<b>songplays_table</b> - records in event data associated with song plays i.e. records with page NextSong songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

<b>Dimension Tables</b>

<b>users_schema_table</b> - users in the app user_id, first_name, last_name, gender, level

<b>songs_schema_table</b> - songs in music database song_id, title, artist_id, year, duration

<b>artists_schema_table</b> - artists in music database artist_id, name, location, lattitude, longitude

<b>time_schema_table</b> - timestamps of records in songplays broken down into specific units start_time, hour, day, week, month, year, weekday


### Datalake schema

#### Dimension tables

##### TABLE users

~~~~
root
 |-- firstName: string (nullable = true)
 |-- lastName: string (nullable = true)
 |-- gender: string (nullable = true)
 |-- level: string (nullable = true)
 |-- userId: string (nullable = true)
~~~~

##### TABLE songs

~~~~
root
 |-- song_id: string (nullable = true)
 |-- title: string (nullable = true)
 |-- artist_id: string (nullable = true)
 |-- year: long (nullable = true)
 |-- duration: double (nullable = true)
~~~~
partitionBy("year", "artist_id")

##### TABLE artists

~~~~
root
 |-- artist_id: string (nullable = true)
 |-- artist_name: string (nullable = true)
 |-- artist_location: string (nullable = true)
 |-- artist_latitude: double (nullable = true)
 |-- artist_longitude: double (nullable = true)
~~~~

##### TABLE time

~~~~
root
 |-- start_time: timestamp (nullable = true)
 |-- hour: integer (nullable = true)
 |-- day: integer (nullable = true)
 |-- week: integer (nullable = true)
 |-- month: integer (nullable = true)
 |-- year: integer (nullable = true)
 |-- weekday: integer (nullable = true)
~~~~

partitionBy("year", "month")

#### Fact table

##### TABLE songplays

~~~~
root
 |-- start_time: timestamp (nullable = true)
 |-- userId: string (nullable = true)
 |-- level: string (nullable = true)
 |-- sessionId: long (nullable = true)
 |-- location: string (nullable = true)
 |-- userAgent: string (nullable = true)
 |-- song_id: string (nullable = true)
 |-- artist_id: string (nullable = true)
 |-- songplay_id: long (nullable = false)
~~~~
partitionBy("year", "month")


## Pipeline
1.Load the Data which are in JSON Files(Song Data and Log Data)
2.Use Spark to process these JSON files and then generate a set of Fact and Dimension Tables
4.Load back this data to S3


## How to run the code:
1.Provide your AWS IAM credential in the dl.cfg file
2.Run etl.py in terminal