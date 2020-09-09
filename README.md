# Data-Pipelines-with-Airflow
This project aims to create a high-grade data pipelines with airflow, This pipeline is built from dynamic and reusable tasks, Implementing the data quality checks to catch the data discrepancies and can be monitored and allow easy backfills. 

## Overview
This project builds a data pipeline for Sparkify using Apache Airflow that automates and monitors the running of an ETL pipeline.

The ETL loads song and log data in JSON format from S3 and processes the data into analytics tables in a star schema on Reshift. A star schema has been used to allow the Sparkify team to readily run queries to analyze user activity on their app. Airflow regularly schedules this ETL and monitors its success by running a data quality check.


## Datasets
The log data is located at ``` s3://udacity-dend/log_data``` and the song data is located in ```s3://udacity-dend/song_data```.

## Structure

* ``` udac_example_dag.py``` Tasks and dependencies of the DAG are defined here. This is present in dags directory.
* ``` create_tables.sql``` SQL queries for creating all the required tables in Redshift are listed here. This is also present in the dags directory.
* ``` sql_queries.py```  SQL queries for data transformation which are used in the ETL process are listed here. This is present in the plugins/helpers directory.


The following operators should be placed in the plugins/operators directory of your Airflow installation:

* ```stage_redshift.py``` StageToRedshiftOperator is defined here, which copies JSON data from S3 to staging tables in the Redshift data warehouse.
* ```load_dimension.py``` LoadDimensionOperator is defined here, this executes the transformation queries to load the data in dimension tables from the staging tables.
* ```load_fact.py``` LoadFactOperator is defined here, this executes the transformation queries to load the data in fact tables from the staging table.
* ```data_quality.py``` DataQualityOperator is defined here, which runs a data quality check by passing table name in SQL queries, Task fails if the results don't match.



## Configuration
Create the following connections in Airflow admin:

* ```aws_credentials``` is created with access key and secret key to connect to S3.
* ```redshift``` is created to connect with Redshift cluster and Redshift data warehouse. 


Check the [aws_credentials](https://github.com/himanshu1612/Data-Pipelines-with-Airflow/blob/master/aws_credentials.png), [redshift](https://github.com/himanshu1612/Data-Pipelines-with-Airflow/blob/master/redshift.png) images for reference.
