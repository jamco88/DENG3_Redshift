# Project Summary

Sparkify want to perform data analysis on song and user activity data they've collected from their app.

The data is currently in two JSON directories. The aim of the project is to construct a Data Warehouse in AWS Redshift, and feed the data in the json logs into an ETL pipeline designed to populate this database.

The end result is processed data that is ready for analysis, to provide insight into what songs users are listening to.

# Files

* **[create-tables.py](create_tables.py)**: Create and recreate database and tables
* **[sql_queries.py](sql_queries.py)**: SQL statements used in the other scripts
* **[etl.py](etl.py)**: Implements the extraction of data, moves it to the staging area, processes then inserts to the Redshift DB

# How to run

To create tables:
'''bash
python create_tables.py
'''

To fill tables using the etl script:
'''bash
python etl.py
'''

# Database purpose

The database brings together required information from the two separate sources on AWS S3, in json format;

* **Song data**: 's3://udacity-dend/song_data'  - From the million song dataset
* **Log data**: 's3://udacity-dend/log_data' - Generated using an event simulator

By using SQL and the star schema together, we allow quick and easy searching over the records. This would be extremely difficult and clunky if we were for example attempting to query the JSON directly. Moreover, doing the work up front to get the data to conform to our schema can massively decrease query time, particularly as the data scales. 

# Database schema design

The star schema lets the company investigate user behaviour, their area of interest, across several dimensions.

The Fact Table is songplays - this is composed of columns from two intermediate staging tables.

The Dimension Tables are users, songs, artists, and time. 