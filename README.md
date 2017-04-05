# Patch_for_Temporal_Databases_in_PostgreSQL

   The number of applications using RDBMS has grown rapidly over the past few decades,
since its conception by E.F Codd in 1974, touching all domains like Inventories, Supply
chain management, Hospitals, Schools, Libraries,etc where data and historical data are
important. Despite this popularity, there is another type of application that has not been able
to take advantage of this system. This type of application requires temporal support from the
database system.

   ***PostgreSQL*** is a powerful, open source object-relational database system. It has more
than 15 years of active development and a proven architecture that has earned it a strong
reputation for reliability, data integrity, and correctness.
A temporal table is a table that records the period of time when a row is valid. This validity
is checked by looking at two automatically generated columns "From" And "Upto"."From"
gives the time from when a record is valid and "Upto" the time it becomes invalid.
There are two types of periods:

1. The application period (also known as valid-time or business-time)
2. The system period (also known as transaction-time).

System-period data versioning allows you to specify that old rows are archived into another
table (that is called the history table).

Providing Temporal Support in postgreSQL

1. We have to extend create table statement as follows:
  
  ***CREATE TEMPORAL TABLE \<table name\> (column list)***
  
  For this we need to extend the processing of "CREATE TABLE" statement by automat-
  ically including two new columns called "FROM" and "UPTO", both of timestamp
  type.

2. We have to extend the update statements as follows:

***Insert statements :*** It should initialize FROM with current system time and keep
UPTO as very large value (something like ’forever’ time)


***Delete statement :*** Create a trigger that does not delete the tuple(s) but initializes
the UPTO value to the system time

***Update statement :*** Create triggers to add UPTO values in the before−tuple and
add FROM time into the after−tuple (thus producing two tuples in place of just
one for every modified tuple)

***Insertion:***
  
  INSERT INTO TEMPORAL TABLE Student VALUES (’pramay’,’Computer Science’,15);
  
  INSERT INTO TABLE Student VALUES (’xyz’,’Physics’,1);

***Updation:***

  UPDATE Student SET Hostel_Number = 4 WHERE Hostel_Number = 15;

***Deletion:***

  DELETE FROM Student WHERE Hostel_Number = 1 ;

**How to apply PATCH**

1. Download postgreSQL source code from following link:
  https://www.postgresql.org/ftp/source/v9.6.2/

2. Extract this downloaded file in some folder, say \<dir\>

3.  Now cd \<dir\>/postgresql-9.3.5

4. Run the "patch" command as follows:
   
   patch -p1 \< \<path of the patch file>
5. Now install patched postgreSQL setup using given command on PostgreSQL's official site.

***Enjoy***





