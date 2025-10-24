
# Topics covered:-

### Components of a DBMS:-
- Catalog (System Catalog)
- Databases
- Schema
- Tables 
- Views
- Indexes
- Stored Procedures & Functions
-------------------------------------------------------------------------------------------------


# Catalog
### DB catalogs / System Catalogs / Data Dictionary / Metastore 

* These all are the terms used for a storage system where metadata information of the entire DB is stored. 

- Oracle → Single catalog (Data Dictionary) which covers all the schemas (users). 

- Spark SQL → Single catalog (metastore) per server/workspace, which covers all the databases.

- PostgreS → Multiple catalogs. Each database has its own catalog. 

- MS SQL server → Multiple catalogs. Each database has its own catalog. 

### Metadata views of various DBMS

### ORACLE:-
- USER_TABLES, ALL_TABLES, DBA_TABLES
- USER_TAB_COLUMNS, ALL_TAB_COLUMNS, DBA_TAB_COLUMNS
- USER_PROCEDURES, USER_OBJECTS
- USER_INDEXES, ALL_INDEXES, DBA_INDEXES
 
### PostgreS:-
- information_schema.tables
- information_schema.columns
- information_schema.routines

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
- “Each database holds tables, views, and other objects that together represent a specific application or system’s data.”

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
# Tables
- A table is the basic unit of data storage in a database where data is organized in a tabular form — rows and columns.
- A table is a data storage object within a schema that holds information in rows and columns.

-------------------------------------------------------------------------------------------------
# Views
• “A view is a virtual table that shows data from one or more tables using a SQL query.”
• “A view doesn’t store data itself — it just displays data fetched from underlying tables.”
Basically these are the pointers to the actual tables.

-------------------------------------------------------------------------------------------------
# Indexes
• An index is a data structure that helps the database find rows faster, improving query performance.”
• “An index works like a book index — it speeds up data retrieval without scanning the entire table.”
• “An index is a performance optimization object that makes searches and lookups quicker in a table.”
you can create an index on that column:
CREATE INDEX emp_id_idx ON employees(employee_id);
Now, when you run
SELECT * FROM employees WHERE employee_id = 105;

-------------------------------------------------------------------------------------------------
# Stored Procedures & Functions
**Stored Procedures:**
A **stored procedure** is a **set of SQL statements saved in the database** that you can run anytime by calling its name.
It’s used to perform tasks like insert, update, or calculations — all in one go.

**Example (practical):**

```sql
CREATE PROCEDURE increase_salary()
AS
BEGIN
  UPDATE employees SET salary = salary * 1.10;
END;
```

Now you can just run:

```sql
EXEC increase_salary;
```

It will give a 10% raise to all employees.

---

**Functions:**
A **function** is similar to a procedure, but it **returns a single value**.
Used when you need a calculation or result in a query.

**Example (practical):**

```sql
CREATE FUNCTION get_bonus(salary NUMBER)
RETURN NUMBER
AS
BEGIN
  RETURN salary * 0.10;
END;
```

You can use it like:

```sql
SELECT name, get_bonus(salary) FROM employees;
```

It returns the 10% bonus for each employee.

-------------------------------------------------------------------------------------------------

