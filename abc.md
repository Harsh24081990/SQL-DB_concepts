
# Topic covered:-

### Components of a DBMS:-
- Catalog (System Catalog)
- Databases
- Schema
- Tables 
- Views
- Indexes
- Stored Procedures & Functions
-------------------------------------------------------------------------------------------------

-------------------------------------------------------------------------------------------------
# Catalog
### DB catalogs / System Catalogs / Data Dictionary / Metastore 

* These all are the terms used for a storage system where metadata information of the entire DB is stored. 

- Oracle → Single catalog (Data Dictionary) which covers all the schemas (users). 

- Spark SQL → Single catalog (metastore) per server/workspace, which covers all the databases.

- PostgreS → Multiple catalogs. Each database has its own catalog. 

- MS SQL server → Multiple catalogs. Each database has its own catalog. 

------------------------------------------------------

### Metadata views of various DBMS

### ORACLE:-
- USER_TABLES, ALL_TABLES, DBA_TABLES
- USER_TAB_COLUMNS, ALL_TAB_COLUMNS, DBA_TAB_COLUMNS
- USER_PROCEDURES, USER_OBJECTS
- USER_INDEXES, ALL_INDEXES, DBA_INDEXES
------------------------------------------------------
 
### PostgreS:-
- information_schema.tables
- information_schema.columns
- information_schema.routines
------------------------------------------------------

### SQL Server:-
- INFORMATION_SCHEMA.TABLES
- INFORMATION_SCHEMA.COLUMNS
- INFORMATION_SCHEMA.ROUTINES
 
### Spark SQL:-
- system.information_schema.tables
- system.information_schema.columns
- system.information_schema.routines


-------------------------------------------------------------------------------------------------
# Databases
	- one or multiple named storage containers created inside a DBMS to store and organize related data.
“Each database holds tables, views, and other objects that together represent a specific application or system’s data.”

-------------------------------------------------------------------------------------------------


-------------------------------------------------------------------------------------------------
# Schema
Grouping of related or similar db objects under a common name. 
A schema is a logical container inside a database that groups related objects 
(like tables, views, and procedures) under a single name.
“It helps organize data within a database, similar to folders inside a drive.”

- PG Admin--
	- Servers → Databases → your_database_name → Schemas
	- SELECT schema_name FROM information_schema.schemata;

-------------------------------------------------------------------------------------------------



-------------------------------------------------------------------------------------------------
# Tables
-------------------------------------------------------------------------------------------------



-------------------------------------------------------------------------------------------------
# Views
-------------------------------------------------------------------------------------------------



-------------------------------------------------------------------------------------------------
# Indexes
-------------------------------------------------------------------------------------------------



-------------------------------------------------------------------------------------------------
# Stored Procedures & Functions
-------------------------------------------------------------------------------------------------

