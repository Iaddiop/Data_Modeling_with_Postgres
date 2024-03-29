# Data Modeling with Postgres
In this project, we will explain how to load JSON files to a [Posgres database](https://www.postgresql.org/) called Sparkify using Pyhton language programming.
JSON data comes from logs (songs in the streaming app and user data of that app) on the music streaming app called Sparkify.
The database will be used later on analytical dashboards (marketing, financial ...) to understand user behavior and usage habits.

Different steps will be taken in this project:
- Build SQL statements that will be used to create and insert data into tables
- Build an ETL pipeline to feed the data from the log files to the Sparkify database.
- Finally, data integration test in the database.

## About the data :
The data stored in 2 directories file :
- [Log_data](https://github.com/Iaddiop/Data_Modeling_with_Postgres/tree/master/data/log_data/2018/11) : JSON files covered the main activities fo the users of the music app
- [Song_data](https://github.com/Iaddiop/Data_Modeling_with_Postgres/tree/master/data/song_data/A) : in this directory we find others files directories that contains JSON metadata about users

## Data modeling :
We will use the relational database to modeling the data and the star schema concept, like this :

![image info](./Schema.png)

- **Fact Table**

**- songplays** : song plays (we will filtring data for page == NextSong), have these columns :
songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

- **Dimension Tables**

**- users** : users table have this columns : user_id, first_name, last_name, gender, level

**- songs** : songs, have these columns : song_id, title, artist_id, year, duration

**- artists** : artists, have these columns : artist_id, name, location, latitude, longitude

**- time** : timestamps of records in songplays broken down into specific units, have these columns : start_time, hour, day, week, month, year, weekday

Please check `sql_queries.py` to see the details of data type of each columns in the tables.
To learn more about [Data Types Postgres](https://www.postgresql.org/docs/9.5/datatype.html). 

## How to run python scripts :
- Description of the files contents :
`sql_queries.py` : content all queries that we need to create, to drop and insert data in the tables.
`create_table.py` : using sql_queries module to make connection with the database, create and drop the tables.
`etl.py`: the etl pipeline that extract all JSON log files, transmort (format some data as datetime), filtring data, extract all infromation that we need to inset into the tables.

- To run this project, please folowing the below steps :
    - create tables first : run `create_table.py` 
    - then lanch the etl : run `etl.py` to process data (extract, ttansform and insert data to the tables)
    - to test the integration of the data : run `test.ipynb` on Jupyter Notebook 
    

### References :
- Issue : psycopg2: can't adapt type 'numpy.int64' ref to : https://stackoverflow.com/questions/50626058/psycopg2-cant-adapt-type-numpy-int64
- Convert timestamp : https://www.postgresql.org/docs/9.5/datatype-datetime.html
- Schema picture : generated with DBSchema software : https://dbschema.com/?AFFILIATE=96594&__c=1