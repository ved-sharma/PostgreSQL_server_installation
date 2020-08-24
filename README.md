# PostgreSQL Server Installation on a Windows 7, 64-bit computer
- Downloaded the Windows 64 bit installer from postgresql.org
- Installed in the default C: directory with all components including pgAdmin 4
- Selected the data directory location in D:
- entered superuser password for postgres

## Verify PostgreSQL installation or connect to PostgreSQL database server
- open Windows cmd, which opens in D:\Users\ved>  
- run runpsql.bat file by typing  
  \> C:\"Program Files"\PostgreSQL\12\scripts\runpsql.bat  
  accept all the defaults (server:localhost, database:postgres, port:5432, username: postgres).  
  Enter the superuser password. prompt gives a warning and changes to postgres prompt “postgres=#”.    
  Check postgres version by: postgres=# SELECT version();    
  If above returns the postgres version number, then the installation is successful.    
  Type “exit” or “quit” or “\q” to quit the psql command line

## Or, Connect to PostgreSQL database server using pgAdmin
- Click on pgAdmin 4 from the Start menu, or run pgAdmin4.exe from folder: C:\Program Files\PostgreSQL\12\pgAdmin 4\bin  
- pgAdmin will launch in default browser window with the following address:  
  http://127.0.0.1:49280/browser/  
- Might need to enter the super user password or might have to create a new Master password  
- pgAdmin

## Load PostgreSQL Sample Database from dvdrental.tar using psql command line
- enter the postgres command prompt “postgres=#”  
- create a new database named dvdrental  
  postgres=# CREATE DATABASE dvdrental;  
- exit postgres command prompt and go back to Windows cmd. Change to pg_restore.exe directory  
  d:\Users\ved> cd /d C:\Program Files\PostgreSQL\12\bin  
  [/d option is needed when changing from d: to C:]  
- Run the pg_restore command  
  \> pg_restore -U postgres -d dvdrental d:\Users\ved\dvdrental.tar  
  [it’s important that there are no spaces in the directory path to the .tar file]  
  enter the postgres superuser password. It takes seconds to load data stored in the dvdrental.tar file into the dvdrental database.

## Or, Load PostgreSQL Sample Database from dvdrental.tar using pgAdmin
- right click on Databases > Create > Database…, enter database name: dvdrental1 > OK  
- right click on dvdrental1 > Restore…, enter Filename: d:\Users\ved\dvdrental.tar

## Importing CSV file data into a PostgreSQL table
- create a table first using psql or pgAdmin define all the column names and data type, e.g.  
  CREATE TABLE zip_codes  
  (ZIP char(5), LATITUDE double precision, LONGITUDE double precision,  
  CITY varchar, STATE char(2), COUNTY varchar, ZIP_CLASS varchar);  
- Use COPY command to copy data from CSV file to your table, e.g.  
  COPY zip_codes FROM '/path/to/csv/ZIP_CODES.txt' WITH (FORMAT csv);

## Starting, stopping PostgreSQL server on Windows 7
- After installing postgresql server, by default, it is set to automatic start at Windows startup and runs all the time. Check for postgresql entry in the Task Manager > Services tab  
- To make any changes in the settings, go to Start > search for Services > right click and choose Run as admin (if not in admin account) > enter admin password > look for postgresql service  
- Right click and choose to stop, start, restart etc. Change Startup Type from Automatic to Manual to change if the server starts or not at Windows startup

## Acknowledgement
https://www.postgresqltutorial.com/install-postgresql/  
https://www.youtube.com/watch?v=fZQI7nBu32M

