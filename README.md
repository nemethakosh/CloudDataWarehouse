# CloudDataWarehouse
In this repository I create an ETL pipeline for a database hosted on Redshift.

My name is Akos Nemeth, Data Engineer, and I provided a solution of building an ETL pipeline that extracts data from S3, stages them in Redshift, and transforms data into a set of dimensional tables. 

Since the data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app, I check the data in S3 through AWS.

I used the log_data and song_data and created the following staging tables :
- staging_events which contains : artist, auth, firstName, gender, ItemInSession, lastName, length, level, location, method, page, registration, sessionId, song, status,  ts, userAgent and userId
- staging_songs which contains : song_id, artist_id, artist_latitude, artist_longitude, artist_location, artist_name, duration, num_songs, title and year 

With the etl.py I loaded data from S3 to these two staging tables on Redshift.

I also created a final start schema, with the following fact table:
- songplays which contains: songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location and user_agent

The dimension tables are the following:
- users which contains: user_id, first_name, last_name, gender and level
- songs which contains: song_id, title, artist_id, year and duration
- artists which contains: artist_id, name, location, lattitude and longitude
- time which contains: start_time, hour, day, week, month, year, weekday

After creating the fact and dimension tables, I loaded the data from staging tables to analytics tables on Redshift, so you have now the start schema where you can analyse the data further.

In the material, I created, there are three py files. First, the create_tables.py file has to be run, in order for the tables to be created. The py file can be run in the terminal by writing 'python create_tables.py'.
The second step is to run the 'etl.py' file, which runs the ETL pipelines I built :  'python etl.py' . It will load the log_data and song_data from S3 to staging tables and then from staging tables to analytics tables.
