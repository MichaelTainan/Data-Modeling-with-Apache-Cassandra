# Project2 Data Modeling with Cassandra

## 1. Goal in the Project
Sparkify's app used CSV format to keep their user's activity when they used the app in period.
They want to find a team or person(like us) to help them.
Help them to create an Apache Cassandra database to analyze their users listen. So for this purpose, we had to design a NoSQL DB and create NoSQL select used table schema data model to ETL these CSV datas into these DB's table to help them reach their goal.

## 2. Part I. ETL Pipeline for Pre-Processing the Files
Follow the template file Project_1B_Project_Templ.ipynb to step by step to get the event_data filepath, then get the filpath csv became a file list, used for loop and csvreader to get full row data list. Finally create a smaller event_datafile_new.csv and load full row data list to write into this new csv file.  
Store the app's user infomation, source is came from log_data, ETL input 96 rows

## 3. Part II. Complete the Apache Cassandra coding portion of my project. Student provides responses to the questions.
Begin create a cluster and a session, then create keyspace and set keyspace.
### 3.1. Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4 
Create a table songs_by_session, set partition key with sessionId, then clustering columns add itemInSession, define these columns to become primary key. Because select column has length, so set it with decimal data type. Before we load CSV data, import Decimal function from Python decimal, then we loaded it into table, changed line[5] to become decimal type. 

result: 1 row
+-----------+---------------------------------+----------+
|   Artist  |               Song              |  Length  |
+-----------+---------------------------------+----------+
| Faithless | Music Matters (Mark Knight Dub) | 495.3073 |
+-----------+---------------------------------+----------+

### 3.2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182
Create a table users, set partition key as composite key with userId and sessionid, then clustering columns add itemInSession, because have to sort by itemInSession, add it in primary key.  

result: 4 rows
+-------------------+------------------------------------------------------+-------------+
|       Artist      |                         Song                         |     User    |
+-------------------+------------------------------------------------------+-------------+
|  Down To The Bone |                  Keep On Keepin' On                  | Sylvie Cruz |
|    Three Drives   |                     Greece 2000                      | Sylvie Cruz |
| Sebastien Tellier |                      Kilometer                       | Sylvie Cruz |
|   Lonnie Gordon   | Catch You Baby (Steve Pitron & Max Sanna Radio Edit) | Sylvie Cruz |
+-------------------+------------------------------------------------------+-------------+

### 3.1. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'
Create a table users_by_song, set partition key with song, then clustering columns add userId, because Primary have to uniquely, add them in primary key.  

result: 3 rows
+------------------+
|       User       |
+------------------+
| Jacqueline Lynch |
|   Tegan Levine   |
|   Sara Johnson   |
+------------------+