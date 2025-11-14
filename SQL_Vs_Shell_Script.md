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

--------------

Yes, you **can do everything in ONE SQL script** — including:

1. **Generate the touch commands**
2. **Save them to a .sh file**
3. **Make the .sh executable**
4. **Execute the .sh file**
5. **Create all trigger (.trg) files**

This is the **only fully-working method** using a **single SQL script**, because SQL*Plus allows `HOST` commands (but PL/SQL does NOT).

Below is the template you need.

---
---
----
-----
-----
# ✅ **FINAL WORKING ONE-SCRIPT SOLUTION --> create trigger files from SQL script itself. **

### **create_trg_files.sql**

```sql
-- 1. Generate the shell script with touch commands
SPOOL /tmp/create_trg_files.sh

SELECT 'touch /your/unix/path/' || LOWER(table_name) || '.trg'
FROM control_table
WHERE load_ind = 'Y';

SPOOL OFF


-- 2. Make it executable (SQL*Plus HOST command)
HOST chmod +x /tmp/create_trg_files.sh


-- 3. Execute the shell script to create the trigger files
HOST sh /tmp/create_trg_files.sh

EXIT
```

---

# ✔ **What this single SQL script does**

### **Step 1 — SPOOL**

Creates a file:

```
/tmp/create_trg_files.sh
```

with content like:

```
touch /your/unix/path/table1.trg
touch /your/unix/path/table2.trg
touch /your/unix/path/table3.trg
```

---

### **Step 2 — HOST chmod**

Makes the file executable:

```
chmod +x /tmp/create_trg_files.sh
```

---

### **Step 3 — HOST sh**

Runs the file:

```
sh /tmp/create_trg_files.sh
```

This **executes all touch commands** → creates all `.trg` files.

---

# ❗ IMPORTANT NOTES

* This works **only in SQL*Plus** (terminal or shell batch execution).
* This will **not** work inside PL/SQL procedures/jobs (they can't run OS commands).
* You must replace `/your/unix/path/` with your actual trigger directory path.

---

# ✔ Example of running it

```sh
sqlplus user/pass @create_trg_files.sql
```

---
