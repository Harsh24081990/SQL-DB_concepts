# **To run shell script and sql script :**

```bash
# Run shell script
sh script.sh

# Run SQL script
sqlplus user/pass@DB @script.sql
```

# **Run .sql from inside .sh:**

```bash
#!/bin/bash
sqlplus user/pass@DB @/path/to/script.sql
```

# **Run .sh from inside .sql:** *(via SQL*Plus host command)*

```sql
HOST sh /path/to/script.sh;
```

👉 `.sh` = run in shell
👉 `.sql` = run in SQL*Plus

--------------

### You can write and run a single SQL query inside a shell script using a **here-document** with `sqlplus`. Example:

```bash
#!/bin/bash
sqlplus -s user/pass@DB <<EOF
SET HEADING OFF;
SELECT COUNT(*) FROM employees;
EXIT;
EOF
```

**Explanation:**

* `sqlplus -s` → runs SQL*Plus in silent mode (no banners).
* `<<EOF ... EOF` → passes SQL commands directly to SQL*Plus.
* `EXIT;` → closes SQL*Plus session.

### You can also capture query output in a variable:

```bash
#!/bin/bash
count=$(sqlplus -s user/pass@DB <<EOF
SET HEADING OFF FEEDBACK OFF;
SELECT COUNT(*) FROM employees;
EXIT;
EOF
)
echo "Total Employees: $count"
```
# In an Oracle `.sql` script, you can run Unix commands using the SQL*Plus **`HOST`** (or `!`) command.

**Examples:**

```sql
-- Method 1
HOST ls -l

-- Method 2 (short form)
!pwd

-- Method 3: run a shell script
HOST sh /path/to/script.sh
```

✅ **Notes:**

* Works only in SQL*Plus or SQLcl (not inside pure PL/SQL blocks).
* The command executes in the OS shell and returns output to SQL*Plus.
* Common use: creating/removing files, calling shell scripts, etc.
