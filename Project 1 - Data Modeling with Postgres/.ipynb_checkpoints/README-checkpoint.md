# Udactity-Data-Modeling-with-Cassandra

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analysis team is particularly interested in understanding what songs users are listening to. Currently, there is no easy way to query the data to generate the results, since the data reside in a directory of CSV files on user activity on the app.

They'd like a data engineer to create an Apache Cassandra database which can create queries on song play data to answer the questions, and wish to bring you on the project. Your role is to create a database for this analysis. You'll be able to test your database by running queries given to you by the analytics team from Sparkify to create the results.

### Datasets
1. Song Dataset - Complete details and metadata about the song
2. Log Dataset - User activity log

### Database Schema 
Here we are using "Star Schema" to model this dataset by dividing them into facts and dimensions so that it is in a structured manner. 

##### Fact Table
Fact table is going to be "songplays" table which contains the metadata of the complete information about each user activity. Many dimension tables are connected to one fact table.

##### Dimension Tables
Here "users","songs","artists","time" are going to be dimension tables. These tables will be having detailed information about a single row from facts table.

### ETL Pipleline
I have created an ETL pipeline which collects data from the json log files and then inserts them into respective tables. "etl.py" file consists of the complete pipeline

#### Files Explained
There are 7 files in this project. 
1. data - This folder contains the log and song datasets.
2. etl.ipynb - This is a jupyter notebook which I used to create the skeleton for the pipeline. It is kind of a workbook.
3. test.ipynb - This jupyter notebook checks whether the written scripts for creating tables and inserting data are working fine or not.
4. create_tables.py - This program contains postgresql queries for creating the database and tables.
5. etl.py - This script contains the complete ETL pipeline for the project.
6. Readme.md - Documentation regarding the project.
7. sql_queries.py - This python script contains the create and insert contains for the database.

### How to run the project ?
1. To run the project, make sure you have all the above files at a single place.
2. Go to terminal and first run create_tables.py script by typing "python create_tables.py" in the terminal. This will make sure that all the previous databases are dropped and new database with tables are created.
3. Go ahead and run etl.py script by typing "python etl.py". This will run the etl pipeline and extract data from the log files and insert them into the facts and dimension table.s