## ORACLE Important metadata views:-
- **USER_TABLES, ALL_TABLES, DBA_TABLES**
- USER_TAB_COLUMNS, ALL_TAB_COLUMNS, DBA_TAB_COLUMNS
- USER_PROCEDURES, USER_OBJECTS
- USER_INDEXES, ALL_INDEXES, DBA_INDEXES
------------------------------------------------------

### Query to check all the table names present in a schema.
- It will give all the table names starting with RX_ 
```sql
SELECT table_name
FROM   user_tables
WHERE  table_name LIKE 'RX\_%' ESCAPE '\'
ORDER BY table_name;
```
----------------------
### Query to check all the column names present in a table.
- It will give all the table names starting with RX_ 
```sql
SELECT column_name,
       data_type,
       data_length,
       data_precision,
       data_scale,
       nullable
FROM   all_tab_columns
WHERE  owner = 'SCHEMA_NAME'
AND    table_name = 'YOUR_TABLE_NAME'
ORDER BY column_id;
```
----------------------
### If you only want column names with datatypes, you can query Oracle’s data dictionary views like below:
```sql
SELECT column_name,
       data_type ||
       CASE 
         WHEN data_type IN ('CHAR','VARCHAR2','NCHAR','NVARCHAR2') 
              THEN '(' || data_length || ')'
         WHEN data_type = 'NUMBER' AND data_precision IS NOT NULL 
              THEN '(' || data_precision || ',' || data_scale || ')'
         ELSE '' 
       END AS data_type
FROM   all_tab_columns
WHERE  table_name = 'YOUR_TABLE_NAME'
AND    owner = 'YOUR_SCHEMA_NAME'
ORDER BY column_id;
```
------------------------
Here’s the difference between **USER_TABLES**, **ALL_TABLES**, and **DBA_TABLES** in Oracle 👇

---

### ✅ **Quick Summary Table**

| View          | Shows Tables From      | Privilege Needed          | Typical Use                                 |
| ------------- | ---------------------- | ------------------------- | ------------------------------------------- |
| `USER_TABLES` | Your own schema        | None                      | When working within your schema             |
| `ALL_TABLES`  | All accessible schemas | None                      | When you need to see shared/external tables |
| `DBA_TABLES`  | Entire database        | DBA / SELECT_CATALOG_ROLE | For DBA or admin-level inspection           |

---

