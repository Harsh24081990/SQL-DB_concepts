# DB catalogs / System Catalogs / Data Dictionary / Metastore 

* These all are the terms used for a storage system where metadata information of the entire DB is stored. 

- Oracle → Single catalog (Data Dictionary) which covers all the schemas (users). 

- Spark SQL → Single catalog (metastore) per server/workspace, which covers all the databases.

- PostgreS → Multiple catalogs. Each database has its own catalog. 

- MS SQL server → Multiple catalogs. Each database has its own catalog. 





# Metadata views of various DBMS

## ORACLE:-
- USER_TABLES, ALL_TABLES, DBA_TABLES
- USER_TAB_COLUMNS, ALL_TAB_COLUMNS, DBA_TAB_COLUMNS
- USER_PROCEDURES, USER_OBJECTS
- USER_INDEXES, ALL_INDEXES, DBA_INDEXES
------------------------------------------------------
 
## PostgreS:-
- information_schema.tables
- information_schema.columns
- information_schema.routines
------------------------------------------------------

## SQL Server:-
- INFORMATION_SCHEMA.TABLES
- INFORMATION_SCHEMA.COLUMNS
- INFORMATION_SCHEMA.ROUTINES
 
## Spark SQL:-
- system.information_schema.tables
- system.information_schema.columns
- system.information_schema.routines
------------------------------------------------------
