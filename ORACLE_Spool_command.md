`SPOOL` captures **exactly whatever SQL*Plus prints on the screen** — nothing more, nothing less.

THis is used for capturing the SQL ouputs to a text file. 

```
SPOOL /file/path/filename.txt

<sql commands here>;

SPOOL OFF

---

# ✔ **If you use these settings before SPOOL command in your sql script:**

```sql
SET HEADING OFF
SET FEEDBACK OFF
SET VERIFY OFF
SET ECHO OFF
SET PAGESIZE 0
```

Then:

### ✅ **SPOOL will capture only the output rows of the query**

➡ **No column names**
➡ **No query text**
➡ **No “X rows selected”**
➡ **No blank lines**

This is the correct setup when generating shell scripts or trigger files.

---

# ❌ **If HEADING is ON**

You will also get:

```
COLUMN_NAME
----------
value1
value2
```

Because SQL*Plus prints column headers → SPOOL captures them.

---

# ❌ **If FEEDBACK is ON**

You will also see:

```
3 rows selected.
```

This will also go into the spooled file.

---

# ✔ Summary Table

| SQL*Plus Setting | Effect on SPOOL                       |
| ---------------- | ------------------------------------- |
| `HEADING OFF`    | No column names                       |
| `FEEDBACK OFF`   | No “n rows selected”                  |
| `PAGESIZE 0`     | No page breaks / no extra blank lines |
| `ECHO OFF`       | Does not print SQL commands           |
| `VERIFY OFF`     | Avoids printing old/new values        |

---

# 🎯 **Recommended settings for clean SPOOL output (best practice)**

```sql
SET HEADING OFF
SET FEEDBACK OFF
SET VERIFY OFF
SET ECHO OFF
SET PAGESIZE 0
SET LINESIZE 32767
```

Now:

### 👉 SPOOL will contain *only* the text produced by your SELECT.

Nothing else.

---

If you want, show me the contents of your spooled `.sh` file and I’ll confirm it's clean.
