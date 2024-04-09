# dataprox
How to create migration files for MySQL

Step1
create one folder and name it DBops2

 

Dbops:
•	This is the main folder where you'll organize your database operation files.
•	The name Dbops suggests it's a place where you'll keep scripts and files related to database operations.

Step2
 create subfolder folder name it as m1_sprint1 to work as major in the database tbl_version table

 

m1_sprint1:
•	This is a subfolder inside the Dbops folder.
•	The name m1_sprint1 indicates it's related to the first sprint (sprint1) of a project or milestone (m1). which will update the data in major column in tbl_version
•	Within Dbops, subfolders like m1_sprint1 help organize scripts based on project milestones or sprints, making it easier to track changes and manage migrations over time.
Step 3
Now create sql file name it a1.1_create_table.sql in the m1_sprint1 folder this record will be updated as a1.1 in miner column in the tbl_version table

 

•	Responsible for creating a table in the database.
•	Contains a CREATE TABLE statement to define the structure of the table.

Step 4
Write SQL script in SQL file Version tags (#start version:m1.1.1 and #end version:m1.1.1) are added to specify the version of this script.


 

This will update as m1.1.1 in the charge column in the tbl_version table
a1.2_insert_table.sql:
•	Create an SQL file named a1.2_insert_table.sql in the m1_sprint1 folder.

•	Inserts data into the table created by a1.2_insert_table.sql.
•	Contains INSERT INTO statements to add data into the table.
•	Includes version tags (#start version:m1.2.1 and #end version:m1.2.1) to specify the script version.


c1.3_constant_table.sql:
•	Create an SQL file named a1.3_constant_table.sql in the m1_sprint1 folder.

•	This SQL file has the same content scripts as the preview’s script 
•	Contains constant scripts that always execute in the database.
•	The filename starts with "c" to indicate a constant script.
•	Includes version tags (#start version:m1.3.1 and #end version:m1.3.1) to specify the script version.



d1.4_discard_table.sql
•	Create an sQL file named d1.4_discard_table.sql in the m1_sprint1 folder.

•	Contains scripts to delete a table from the database.
•	The filename starts with "d" to indicate a discard script.
•	Includes version tags (#start version:m1.4.1 and #end version:m1.4.1) to specify the script version

 

Running the code by providing the specified folder path.


How to run the code
•	copy the folder path and past it in the -folder path parameters
 


How the code will work for the database
ID: This column represents the unique identifier for each row in the table. It's a sequential number starting from 1, indicating the order in which the scripts were executed.
MAJOR: This column represents the major version of the script. It's derived from the directory name where the script is located. In your example, you have major version "m1".

MINOR: This column represents the minor version of the script. It's derived from the prefix of the script file name. In your example, you have minor versions like "a1.1", "a1.2", "c1.3", and "d1.4".
CHANGE: This column represents the specific change or feature implemented by the script. It's extracted from the script content itself. For example, "m1.1.1", "m1.1.2", etc., represent different changes within the same minor version.
STATUS: This column indicates the execution status of the script. It can have one of the following values:
success: Indicates that the script executed without errors.
skipped: Indicates that the script was skipped due to a matching hash code.
failed: Indicates that the script execution encountered an error.
HASH CODE: This column represents the hash code generated from the script content between (--start version:m1.4.1 and --end version:m1.4.1). It's used to identify if a script has been previously executed to determine if it should be skipped.
EXECUTION TIME: This column represents the timestamp when the script was executed. It shows the date and time in UTC format when the script execution took place.

How the scripts executed in database tbl_version table
Database Connection Establishment
The application establishes a connection to the Cassandra database using the provided host address.
Table Creation (if not exists):
The application checks if the tbl_version table exists in the specified keyspace.
If the table doesn't exist, it creates the table with the following schema:
sql
Copy code
CREATE TABLE IF NOT EXISTS tbl_version (
    id int,
    major text,
    minor text,
    change column text,
    status text,
    hashcode text,
    executiontime timestamp,
    PRIMARY KEY ((major, minor, change column), id)
);
Script Execution and Data Insertion:
•	The application iterates over each script file (*.sql) present in the specified folder.
•	For each script file, it extracts the major version, minor version, change, and script content.
•	It then checks if the script content has been previously executed by generating a hash code from it and comparing it with the hash codes stored in the database.
•	If the script content has not been executed before (or if the script starts with 'c'), it executes the script by splitting it into individual SQL statements and executing each statement separately.
•	After successful execution or if the script was skipped, the application inserts or updates a record in the tbl_version table based on the major version, minor version, and change.
Each record in the table includes the following fields:


 

	id: A UUID generated for each record to serve as a unique identifier.
	major: Represents the major version of the script.
	minor: Represents the minor version of the script.
	change: Represents the specific change or feature implemented by the script.
	status: Indicates the execution status of the script (success, skipped,).
	hashcode: Represents the hash code generated from the script content.
	executiontime: Represents the timestamp when the script was executed.
Table Population:
It will insert only success records if the script has any error(failed) it will not inserted in tbl_version table in status column
When you run the same script for second time it will update the status to skipped which file name does not start with ‘’c’’
As the scripts are executed and records are inserted/updated in the tbl_version table, the table gets populated with data representing the history of script execution along with their versions, execution status, and timestamps.
Overall, this process ensures that the tbl_version table accurately reflects the execution status and history of the scripts, allowing for tracking and management of database schema changes over time.






















How to create migration files for MariaDB
Step1
create one folder and name it DBops2

 

Dbops:
•	This is the main folder where you'll organize your database operation files.
•	The name Dbops suggests it's a place where you'll keep scripts and files related to database operations.

Step2
 create subfolder folder name it as m1_sprint1 to work as major in the database tbl_version table

 

m1_sprint1:
•	This is a subfolder inside the Dbops folder.
•	The name m1_sprint1 indicates it's related to the first sprint (sprint1) of a project or milestone (m1). which will update the data in major column in tbl_version
•	Within Dbops, subfolders like m1_sprint1 help organize scripts based on project milestones or sprints, making it easier to track changes and manage migrations over time.
Step 3
Now create sql file name it a1.1_create_table.sql in the m1_sprint1 folder this record will be updated as a1.1 in miner column in the tbl_version table

 

•	Responsible for creating a table in the database.
•	Contains a CREATE TABLE statement to define the structure of the table.

Step 4
Write SQL script in SQL file Version tags (#start version:m1.1.1 and #end version:m1.1.1) are added to specify the version of this script.


 

This will update as m1.1.1 in the charge column in the tbl_version table
a1.2_insert_table.sql:
•	Create an SQL file named a1.2_insert_table.sql in the m1_sprint1 folder.

•	Inserts data into the table created by a1.2_insert_table.sql.
•	Contains INSERT INTO statements to add data into the table.
•	Includes version tags (#start version:m1.2.1 and #end version:m1.2.1) to specify the script version.


c1.3_constant_table.sql:
•	Create an SQL file named a1.3_constant_table.sql in the m1_sprint1 folder.

•	This SQL file has the same content scripts as the preview’s script 
•	Contains constant scripts that always execute in the database.
•	The filename starts with "c" to indicate a constant script.
•	Includes version tags (#start version:m1.3.1 and #end version:m1.3.1) to specify the script version.



d1.4_discard_table.sql
•	Create an SQL file named d1.4_discard_table.sql in the m1_sprint1 folder.

•	Contains scripts to delete a table from the database.
•	The filename starts with "d" to indicate a discard script.
•	Includes version tags (#start version:m1.4.1 and #end version:m1.4.1) to specify the script version

 

Running the code by providing the specified folder path.


How to run the code
•	copy the folder path and past it in the -folder path parameters
 


How the code will work for the database
ID: This column represents the unique identifier for each row in the table. It's a sequential number starting from 1, indicating the order in which the scripts were executed.
MAJOR: This column represents the major version of the script. It's derived from the directory name where the script is located. In your example, you have major version "m1".

MINOR: This column represents the minor version of the script. It's derived from the prefix of the script file name. In your example, you have minor versions like "a1.1", "a1.2", "c1.3", and "d1.4".
CHANGE: This column represents the specific change or feature implemented by the script. It's extracted from the script content itself. For example, "m1.1.1", "m1.1.2", etc., represent different changes within the same minor version.
STATUS: This column indicates the execution status of the script. It can have one of the following values:
success: Indicates that the script executed without errors.
skipped: Indicates that the script was skipped due to a matching hash code.
failed: Indicates that the script execution encountered an error.
HASH CODE: This column represents the hash code generated from the script content between (--start version:m1.4.1 and --end version:m1.4.1). It's used to identify if a script has been previously executed to determine if it should be skipped.
EXECUTION TIME: This column represents the timestamp when the script was executed. It shows the date and time in UTC format when the script execution took place.

How the scripts executed in database tbl_version table
Database Connection Establishment
The application establishes a connection to the Cassandra database using the provided host address.
Table Creation (if not exists):
The application checks if the tbl_version table exists in the specified keyspace.
If the table doesn't exist, it creates the table with the following schema:
sql
Copy code
CREATE TABLE IF NOT EXISTS tbl_version (
    id int,
    major text,
    minor text,
    change column text,
    status text,
    hashcode text,
    executiontime timestamp,
    PRIMARY KEY ((major, minor, change column), id)
);
Script Execution and Data Insertion:
•	The application iterates over each script file (*.sql) present in the specified folder.
•	For each script file, it extracts the major version, minor version, change, and script content.
•	It then checks if the script content has been previously executed by generating a hash code from it and comparing it with the hash codes stored in the database.
•	If the script content has not been executed before (or if the script starts with 'c'), it executes the script by splitting it into individual SQL statements and executing each statement separately.
•	After successful execution or if the script was skipped, the application inserts or updates a record in the tbl_version table based on the major version, minor version, and change.
Each record in the table includes the following fields:


 

	id: A UUID generated for each record to serve as a unique identifier.
	major: Represents the major version of the script.
	minor: Represents the minor version of the script.
	change: Represents the specific change or feature implemented by the script.
	status: Indicates the execution status of the script (success, skipped,).
	hashcode: Represents the hash code generated from the script content.
	executiontime: Represents the timestamp when the script was executed.
Table Population:
It will insert only success records if the script has any error(failed) it will not inserted in tbl_version table in status column
When you run the same script for second time it will update the status to skipped which file name does not start with ‘’c’’
As the scripts are executed and records are inserted/updated in the tbl_version table, the table gets populated with data representing the history of script execution along with their versions, execution status, and timestamps.
Overall, this process ensures that the tbl_version table accurately reflects the execution status and history of the scripts, allowing for tracking and management of database schema changes over time.






















How to create migration files for PostgreSQL 
Step1
create one folder and name it DBops2

 

Dbops:
•	This is the main folder where you'll organize your database operation files.
•	The name Dbops suggests it's a place where you'll keep scripts and files related to database operations.

Step2
 create subfolder folder name it as m1_sprint1 to work as major in the database tbl_version table

 

m1_sprint1:
•	This is a subfolder inside the Dbops folder.
•	The name m1_sprint1 indicates it's related to the first sprint (sprint1) of a project or milestone (m1). which will update the data in major column in tbl_version
•	Within Dbops, subfolders like m1_sprint1 help organize scripts based on project milestones or sprints, making it easier to track changes and manage migrations over time.
Step 3
Now create sql file name it a1.1_create_table.sql in the m1_sprint1 folder this record will be updated as a1.1 in miner column in the tbl_version table

 

•	Responsible for creating a table in the database.
•	Contains a CREATE TABLE statement to define the structure of the table.

Step 4
Write SQL script in SQL file Version tags (--start version:m1.1.1 and --end version:m1.1.1) are added to specify the version of this script.


 

This will update as m1.1.1 in the charge column in the tbl_version table
a1.2_insert_table.sql:
•	Create an SQL file named a1.2_insert_table.sql in the m1_sprint1 folder.

•	Inserts data into the table created by a1.2_insert_table.sql.
•	Contains INSERT INTO statements to add data into the table.
•	Includes version tags (--start version:m1.2.1 and --end version:m1.2.1) to specify the script version.
 

c1.3_constant_table.sql:
•	Create an SQL file named a1.3_constant_table.sql in the m1_sprint1 folder.

•	This SQL file has the same content scripts as the preview’s script 
•	Contains constant scripts that always execute in the database.
•	The filename starts with "c" to indicate a constant script.
•	Includes version tags (--start version:m1.3.1 and --end version:m1.3.1) to specify the script version.

 

d1.4_discard_table.sql
•	Create an sQL file named d1.4_discard_table.sql in the m1_sprint1 folder.

•	Contains scripts to delete a table from the database.
•	The filename starts with "d" to indicate a discard script.
•	Includes version tags (--start version:m1.4.1 and --end version:m1.4.1) to specify the script version

 

Running the code by providing the specified folder path.


How to run the code
•	copy the folder path and past it in the -folder path parameters
 


How the code will work for the database
ID: This column represents the unique identifier for each row in the table. It's a sequential number starting from 1, indicating the order in which the scripts were executed.
MAJOR: This column represents the major version of the script. It's derived from the directory name where the script is located. In your example, you have major version "m1".

MINOR: This column represents the minor version of the script. It's derived from the prefix of the script file name. In your example, you have minor versions like "a1.1", "a1.2", "c1.3", and "d1.4".
CHANGE: This column represents the specific change or feature implemented by the script. It's extracted from the script content itself. For example, "m1.1.1", "m1.1.2", etc., represent different changes within the same minor version.
STATUS: This column indicates the execution status of the script. It can have one of the following values:
success: Indicates that the script executed without errors.
skipped: Indicates that the script was skipped due to a matching hash code.
failed: Indicates that the script execution encountered an error.
HASH CODE: This column represents the hash code generated from the script content between (--start version:m1.4.1 and --end version:m1.4.1). It's used to identify if a script has been previously executed to determine if it should be skipped.
EXECUTION TIME: This column represents the timestamp when the script was executed. It shows the date and time in UTC format when the script execution took place.

How the scripts executed in database tbl_version table
Database Connection Establishment
The application establishes a connection to the Cassandra database using the provided host address.
Table Creation (if not exists):
The application checks if the tbl_version table exists in the specified keyspace.
If the table doesn't exist, it creates the table with the following schema:
sql
Copy code
CREATE TABLE IF NOT EXISTS tbl_version (
    id int,
    major text,
    minor text,
    change column text,
    status text,
    hashcode text,
    executiontime timestamp,
    PRIMARY KEY ((major, minor, change column), id)
);
Script Execution and Data Insertion:
•	The application iterates over each script file (*.sql) present in the specified folder.
•	For each script file, it extracts the major version, minor version, change, and script content.
•	It then checks if the script content has been previously executed by generating a hash code from it and comparing it with the hash codes stored in the database.
•	If the script content has not been executed before (or if the script starts with 'c'), it executes the script by splitting it into individual SQL statements and executing each statement separately.
•	After successful execution or if the script was skipped, the application inserts or updates a record in the tbl_version table based on the major version, minor version, and change.
Each record in the table includes the following fields:


 

	id: A UUID generated for each record to serve as a unique identifier.
	major: Represents the major version of the script.
	minor: Represents the minor version of the script.
	change: Represents the specific change or feature implemented by the script.
	status: Indicates the execution status of the script (success, skipped,).
	hashcode: Represents the hash code generated from the script content.
	executiontime: Represents the timestamp when the script was executed.
Table Population:
It will insert only success records if the script has any error(failed) it will not inserted in tbl_version table in status column
When you run the same script for second time it will update the status to skipped which file name does not starts with ‘’c’’
As the scripts are executed and records are inserted/updated in the tbl_version table, the table gets populated with data representing the history of script execution along with their versions, execution status, and timestamps.
Overall, this process ensures that the tbl_version table accurately reflects the execution status and history of the scripts, allowing for tracking and management of database schema changes over time.






















How to create migration files for MsSQL
Step1
create one folder and name it DBops2

 

Dbops:
•	This is the main folder where you'll organize your database operation files.
•	The name Dbops suggests it's a place where you'll keep scripts and files related to database operations.

Step2
 create subfolder folder name it as m1_sprint1 to work as major in the database tbl_version table

 

m1_sprint1:
•	This is a subfolder inside the Dbops folder.
•	The name m1_sprint1 indicates it's related to the first sprint (sprint1) of a project or milestone (m1). which will update the data in major column in tbl_version
•	Within Dbops, subfolders like m1_sprint1 help organize scripts based on project milestones or sprints, making it easier to track changes and manage migrations over time.
Step 3
Now create sql file name it a1.1_create_table.sql in the m1_sprint1 folder this record will be updated as a1.1 in miner column in the tbl_version table

 

•	Responsible for creating a table in the database.
•	Contains a CREATE TABLE statement to define the structure of the table.

Step 4
Write SQL script in SQL file Version tags (--start version:m1.1.1 and --end version:m1.1.1) are added to specify the version of this script.


 

This will update as m1.1.1 in the charge column in the tbl_version table
a1.2_insert_table.sql:
•	Create an SQL file named a1.2_insert_table.sql in the m1_sprint1 folder.

•	Inserts data into the table created by a1.2_insert_table.sql.
•	Contains INSERT INTO statements to add data into the table.
•	Includes version tags (--start version:m1.2.1 and --end version:m1.2.1) to specify the script version.
 

c1.3_constant_table.sql:
•	Create an SQL file named a1.3_constant_table.sql in the m1_sprint1 folder.

•	This SQL file has the same content scripts as the preview’s script 
•	Contains constant scripts that always execute in the database.
•	The filename starts with "c" to indicate a constant script.
•	Includes version tags (--start version:m1.3.1 and --end version:m1.3.1) to specify the script version.

 

d1.4_discard_table.sql
•	Create an sQL file named d1.4_discard_table.sql in the m1_sprint1 folder.

•	Contains scripts to delete a table from the database.
•	The filename starts with "d" to indicate a discard script.
•	Includes version tags (--start version:m1.4.1 and --end version:m1.4.1) to specify the script version

 

Running the code by providing the specified folder path.


How to run the code
•	copy the folder path and past it in the -folder path parameters
 


How the code will work for the database
ID: This column represents the unique identifier for each row in the table. It's a sequential number starting from 1, indicating the order in which the scripts were executed.
MAJOR: This column represents the major version of the script. It's derived from the directory name where the script is located. In your example, you have major version "m1".

MINOR: This column represents the minor version of the script. It's derived from the prefix of the script file name. In your example, you have minor versions like "a1.1", "a1.2", "c1.3", and "d1.4".
CHANGE: This column represents the specific change or feature implemented by the script. It's extracted from the script content itself. For example, "m1.1.1", "m1.1.2", etc., represent different changes within the same minor version.
STATUS: This column indicates the execution status of the script. It can have one of the following values:
success: Indicates that the script executed without errors.
skipped: Indicates that the script was skipped due to a matching hash code.
failed: Indicates that the script execution encountered an error.
HASH CODE: This column represents the hash code generated from the script content between (--start version:m1.4.1 and --end version:m1.4.1). It's used to identify if a script has been previously executed to determine if it should be skipped.
EXECUTION TIME: This column represents the timestamp when the script was executed. It shows the date and time in UTC format when the script execution took place.

How the scripts executed in database tbl_version table
Database Connection Establishment
The application establishes a connection to the Cassandra database using the provided host address.
Table Creation (if not exists):
The application checks if the tbl_version table exists in the specified keyspace.
If the table doesn't exist, it creates the table with the following schema:
sql
Copy code
CREATE TABLE IF NOT EXISTS tbl_version (
    id int,
    major text,
    minor text,
    change column text,
    status text,
    hashcode text,
    executiontime timestamp,
    PRIMARY KEY ((major, minor, change column), id)
);
Script Execution and Data Insertion:
•	The application iterates over each script file (*.sql) present in the specified folder.
•	For each script file, it extracts the major version, minor version, change, and script content.
•	It then checks if the script content has been previously executed by generating a hash code from it and comparing it with the hash codes stored in the database.
•	If the script content has not been executed before (or if the script starts with 'c'), it executes the script by splitting it into individual SQL statements and executing each statement separately.
•	After successful execution or if the script was skipped, the application inserts or updates a record in the tbl_version table based on the major version, minor version, and change.
Each record in the table includes the following fields:


 

	id: A UUID generated for each record to serve as a unique identifier.
	major: Represents the major version of the script.
	minor: Represents the minor version of the script.
	change: Represents the specific change or feature implemented by the script.
	status: Indicates the execution status of the script (success, skipped,).
	hashcode: Represents the hash code generated from the script content.
	executiontime: Represents the timestamp when the script was executed.
Table Population:
It will insert only success records if the script has any error(failed) it will not inserted in tbl_version table in status column
When you run the same script for second time it will update the status to skipped which file name does not start with ‘’c’’
As the scripts are executed and records are inserted/updated in the tbl_version table, the table gets populated with data representing the history of script execution along with their versions, execution status, and timestamps.
Overall, this process ensures that the tbl_version table accurately reflects the execution status and history of the scripts, allowing for tracking and management of database schema changes over time.























How to create migration files for Cassandra
Step1
create one folder and name it DBops

 

Dbops:
•	This is the main folder where you'll organize your database operation files.
•	The name Dbops suggests it's a place where you'll keep scripts and files related to database operations.

Step2
 create subfolder folder name it as m1_sprint1  to work as major in the database tbl_version table

 

m1_sprint1:
•	This is a subfolder inside the Dbops folder.
•	The name m1_sprint1 indicates it's related to the first sprint (sprint1) of a project or milestone (m1). which will update the data in major column in tbl_version
•	Within Dbops, subfolders like m1_sprint1 help organize scripts based on project milestones or sprints, making it easier to track changes and manage migrations over time.
Step 3
Now create sql file name it a1.1_create table.cql in the m1_sprint1 folder this record will updated  as a1.1 in miner column in the tbl_version table

 


•	Responsible for creating a table in the database.
•	Contains a CREATE TABLE statement to define the structure of the table.
Step 4
Write CQL script in CQL file Version tags --start version:m1.1.1 and --end version:m1.1.1 are added to specify the version of this script.


 

This will update as m1.1.1 in the charge column in the tbl_version table
a1.2_insert_table.cql:
•	Create an CQL file named a1.2_insert_table.cql in the m1_sprint1 folder.
•	Inserts data into the table created by a1.1_create_table.cql.
•	Contains INSERT INTO statements to add data into the table.
•	Includes version tags (--start version:m1.2.1 and --end version:m1.2.1) to specify the script version.
 

c1.3_constant_table.cql:
•	Create an CQL file named a1.3_constant_table.cql in the m1_sprint1 folder.
•	This CQL file has the same content scripts as the preview’s script 
•	Contains constant scripts that always execute in the database.
•	The filename starts with "c" to indicate a constant script.
•	Includes version tags (--start version:m1.3.1 and --end version:m1.3.1) to specify the script version.

 

d1.4_discard_table.cql
•	Create an CQL file named d1.4_discard_table.cql in the m1_sprint1 folder.
•	Contains scripts to delete a table from the database.
•	The filename starts with "d" to indicate a discard script.
•	Includes version tags (--start version:m1.4.1 and --end version:m1.4.1) to specify the script version

 

Running the code by provided the specified folder path.


How to run the code
•	copy the folder path and past it in the -folder path parameters


 


How the code will works for the database
ID: This column represents the unique identifier for each row in the table. It's a sequential number starting from 1, indicating the order in which the scripts were executed.
MAJOR: This column represents the major version of the script. It's derived from the directory name where the script is located. In your example, you have major version "m1".

MINOR: This column represents the minor version of the script. It's derived from the prefix of the script file name. In your example, you have minor versions like "a1.1", "a1.2", "c1.3", and "d1.4".
CHANGE: This column represents the specific change or feature implemented by the script. It's extracted from the script content itself. For example, "m1.1.1", "m1.1.2", etc., represent different changes within the same minor version.
STATUS: This column indicates the execution status of the script. It can have one of the following values:
success: Indicates that the script executed without errors.
skipped: Indicates that the script was skipped due to a matching hash code.
failed: Indicates that the script execution encountered an error.
HASH CODE: This column represents the hash code generated from the script content between (--start version:m1.4.1 and --end version:m1.4.1). It's used to identify if a script has been previously executed to determine if it should be skipped.
EXECUTION TIME: This column represents the timestamp when the script was executed. It shows the date and time in UTC format when the script execution took place.

How the scripts executed in database tbl_version table
Database Connection Establishment
The application establishes a connection to the Cassandra database using the provided host address.
Table Creation (if not exists):
The application checks if the tbl_version table exists in the specified keyspace.
If the table doesn't exist, it creates the table with the following schema:
cql
Copy code
CREATE TABLE IF NOT EXISTS tbl_version (
    id int,
    major text,
    minor text,
    changecolumn text,
    status text,
    hashcode text,
    executiontime timestamp,
    PRIMARY KEY ((major, minor, changecolumn), id)
);
Script Execution and Data Insertion:
•	The application iterates over each script file (*.cql) present in the specified folder.
•	For each script file, it extracts the major version, minor version, change, and script content.
•	It then checks if the script content has been previously executed by generating a hash code from it and comparing it with the hash codes stored in the database.
•	If the script content has not been executed before (or if the script starts with 'c'), it executes the script by splitting it into individual CQL statements and executing each statement separately.
•	After successful execution or if the script was skipped, the application inserts or updates a record in the tbl_version table based on the major version, minor version, and change.
Each record in the table includes the following fields:

 


	id: A UUID generated for each record to serve as a unique identifier.
	major: Represents the major version of the script.
	minor: Represents the minor version of the script.
	change: Represents the specific change or feature implemented by the script.
	status: Indicates the execution status of the script (success, skipped,).
	hashcode: Represents the hash code generated from the script content.
	executiontime: Represents the timestamp when the script was executed.
Table Population:
It will insert only success records if the script has any error(failed) it will not inserted in tbl_version table in status column
When you run the same script for second time it will update the status to skipped which file name does not starts with ‘’c’’
As the scripts are executed and records are inserted/updated in the tbl_version table, the table gets populated with data representing the history of script execution along with their versions, execution status, and timestamps.
Overall, this process ensures that the tbl_version table accurately reflects the execution status and history of the scripts, allowing for tracking and management of database schema changes over time.












How to create migration files for MongoDB

Creating a folder using mkdir command 
Creating a file using nano command 
Step1
create one folder and name it DBops
Dbops:
•	This is the main folder where you'll organize your database operation files.
•	The name Dbops suggests it's a place where you'll keep scripts and files related to database operations.

Step2
 create subfolder folder name it as m1_sprint to work as major in the database tbl_version table

 

m1_sprint:
•	This is a subfolder inside the Dbops folder.
•	The name m1_sprint indicates it's related to the first sprint (sprint1) of a project or milestone (m1). which will update the data in major column in tbl_version
•	Within Dbops, subfolders like m1_sprint1 help organize scripts based on project milestones or sprints, making it easier to track changes and manage migrations over time.
Step 3
Now create JSON file name it a1.1_create table.json in the m1_sprint folder this record will updated  as a1.1 in miner column in the tbl_version table

 


•	Responsible for creating a table in the database.
•	Contains a CREATE TABLE statement to define the structure of the table.
Step 4
Write JSON script in JSON file Version tags ("_version": "m1.1.1") are added to specify the version of this script.

This will update as m1.1.1 in the charge column in the tbl_version table

a1.2_insert_table.json:
•	Create an JSON file named a1.2_insert_table.json in the m1_sprint folder.

•	Inserts data into the table created by a1.2_insert_table.json.
•	Contains INSERT INTO statements to add data into the table.
•	Includes version tags ("_version": "m1.2.1") to specify the script version.

c1.3_constant_table.json:
•	Create an JSON file named a1.3_constant_table.json in the m1_sprint folder.

•	This JSON file has the same content scripts as the preview’s script 
•	Contains constant scripts that always execute in the database.
•	The filename starts with "c" to indicate a constant script.
•	Includes version tags ("_version": "m1.3.1") to specify the script version.

 

d1.4_discard_table.json
•	Create an JSON file named d1.4_discard_table.json in the m1_sprint1 folder.

•	Contains scripts to delete a table from the database.
•	The filename starts with "d" to indicate a discard script.
•	Includes version tags ("_version": "m1.4.1) to specify the script version

 

Running the code by providing the specified folder path.


How to run the code
•	copy the folder path and past it in the -folder path parameters


 


How the code will work for the database
ID: This column represents the unique identifier for each row in the table. It's a sequential number starting from 1, indicating the order in which the scripts were executed.
MAJOR: This column represents the major version of the script. It's derived from the directory name where the script is located. In your example, you have major version "m1".

MINOR: This column represents the minor version of the script. It's derived from the prefix of the script file name. In your example, you have minor versions like "a1.1", "a1.2", "c1.3", and "d1.4".
CHANGE: This column represents the specific change or feature implemented by the script. It's extracted from the script content itself. For example, "m1.1.1", "m1.1.2", etc., represent different changes within the same minor version.
STATUS: This column indicates the execution status of the script. It can have one of the following values:
success: Indicates that the script executed without errors.
skipped: Indicates that the script was skipped due to a matching hash code.
failed: Indicates that the script execution encountered an error.
HASH CODE: This column represents the hash code generated from the script content between ("_version": "m1.1.1). It's used to identify if a script has been previously executed to determine if it should be skipped.
EXECUTION TIME: This column represents the timestamp when the script was executed. It shows the date and time in UTC format when the script execution took place.

How the scripts executed in database tbl_version table
Database Connection Establishment
The application establishes a connection to the Cassandra database using the provided host address.
Table Creation (if not exists):
The application checks if the tbl_version table exists in the specified keyspace.
If the table doesn't exist, it creates the table with the following schema:
JSON
Copy code
type Collection2Data struct {
	ID            int       `json:"id"`
	Major         string    `json:"major"`
	Minor         string    `json:"minor"`
	Change        string    `json:"change"`
	Status        string    `json:"status"`
	HashCode      string    `json:"hash_code"`
	ExecutionTime time.Time `json:"execution_time"`

Script Execution and Data Insertion:
•	The application iterates over each script file (*.json) present in the specified folder.
•	For each script file, it extracts the major version, minor version, change, and script content.
•	It then checks if the script content has been previously executed by generating a hash code from it and comparing it with the hash codes stored in the database.
•	If the script content has not been executed before (or if the script starts with 'c'), it executes the script by splitting it into individual JSON statements and executing each statement separately.
•	After successful execution or if the script was skipped, the application inserts or updates a record in the tbl_version table based on the major version, minor version, and change.
Each record in the table includes the following fields:

 


	id: A UUID generated for each record to serve as a unique identifier.
	major: Represents the major version of the script.
	minor: Represents the minor version of the script.
	change: Represents the specific change or feature implemented by the script.
	status: Indicates the execution status of the script (success, skipped,).
	hashcode: Represents the hash code generated from the script content.
	executiontime: Represents the timestamp when the script was executed.
Table Population:
It will insert success and failed in tbl_version table in status column
When you run the same script for second time it will update the status to skipped which file name does not start with ‘’c’’
As the scripts are executed and records are inserted/updated in the tbl_version table, the table gets populated with data representing the history of script execution along with their versions, execution status, and timestamps.
Overall, this process ensures that the tbl_version table accurately reflects the execution status and history of the scripts, allowing for tracking and management of database schema changes over time.








