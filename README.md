
### Table of Contents

1. [Installation](#installation)
2. [Project Motivation](#motivation)
3. [Installation](#Installation)
3. [Instructions](#instructions)
4. [File Descriptions](#files)
5. [Licensing, Authors, and Acknowledgements](#licensing)


## Project Motivation<a name="motivation"></a>

### Introduction

An imaginary startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis, and bring you on the project. The objective is to create a database schema and ETL pipeline for this analysis.


### Dataset

The Dataset in folder `data` consist of songs and log data:

- `Song Dataset` is a subset of real data from the [Million Song](https://labrosa.ee.columbia.edu/millionsong/) Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. Below is an example of what a single song file, `TRAABJL12903CDCF1A.json`, looks like.

  <img src="/img/song_data.png">


- `Log Dataset` consists of log files in JSON format generated by this [event simulator](https://github.com/Interana/eventsim) based on the songs in the dataset above. These simulate app activity logs from a music streaming app based on specified configurations. The log files in the dataset are partitioned by year and month. Below is an example of single log data file of 2018-11-12-events.json.

  <img src="/img/log_data.png">

### Data Schema

#### Fact Table

`songplay` - records in log data associated with song plays i.e. records with page NextSong
- `songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent`

#### Dimension Tables

`users` - users in the app
- `user_id, first_name, last_name, gender, level`

`songs` - songs in music database
- `song_id, title, artist_id, year, duration`

`artists` - artists in music database
- `artist_id, name, location, lattitude, longitude`

`time` - timestamps of records in songplays broken down into specific units
- `start_time, hour, day, week, month, year, weekday`


## Installation <a name="installation"></a>

1. [Anaconda distribution](https://www.anaconda.com/distribution/) of Python version 3.6 or later
2. [PostgreSQL](https://www.postgresql.org/)
3. [psycorpg2](http://initd.org/psycopg/docs/install.html)
4. [ipython-sql](https://github.com/catherinedevlin/ipython-sql)


## Instructions<a name="instructions"></a>

Run the following command in the root directory to run the ETL.

`python etl.py`

To check the result, open and run cells in `test.ipynb`

The result should be like the below screenshot.

**Songplay Table**

<img src="/img/songplay_table_example.png">

**Users Table**

<img src="/img/user_table_example.png">

**Artists Table**

<img src="/img/artist_table_example.png">

**Songs Table**

<img src="/img/song_table_example.png">

**Time Table**

<img src="/img/time_table_example.png">

## File Descriptions <a name="files"></a>

Other than dataset, the main files consist of :
- `test.ipynb` displays the first few rows of each table to let you check your database.
- `create_tables.py` drops and creates your tables. Run this file to reset tables before each time running ETL scripts.
- `etl.ipynb` reads and processes a single file from song_data and log_data and loads the data into your tables.
- `etl.py` reads and processes files from song_data and log_data and loads them into your tables.
- `sql_queries.py` contains all sql queries, and is imported into the last three files above.


## Licensing, Authors, Acknowledgements<a name="licensing"></a>

Must give credit to Udacity as part of Data Engineering NanoDegree Program
