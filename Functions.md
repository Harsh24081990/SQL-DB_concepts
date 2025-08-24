### ✅ **Functions Used (Spark SQL compatible) **

### 🔹 String Functions:

* `lower(col)` / `upper(col)`
* `ltrim(col)` / `rtrim(col)` / `trim(col)`
* `LIKE`, `ILIKE` – pattern matching (LIKE for case sensitive match and ILIKE for case **Insensitive** match)
* `length(col)`
* `substring(col, pos, len)`
* `instr(col, substr)`
* `regexp_replace(col, pattern, replacement)`
* `regexp_extract(col, pattern, idx)`
* `concat(col1, col2, ...)`
* `concat_ws(separator, col1, col2, ...)`
* `translate(col, from_str, to_str)`
* `initcap(col)` – capitalize first letter of each word
* `reverse(col)` – reverse the string
* `split(col, pattern)` – split string to array
* `locate(substr, str)` – position of substring
* `CAST(expression AS data_type)` – convert datatype (e.g. string to int) (Throws error if conversion fails)
* `TRY_CAST()` – (Spark 3.0+) which returns NULL instead of throwing an error if conversion fails.

----------------

👍 Here’s a **Spark SQL Functions Cheat Sheet** — categorized with **syntax + example** for quick reference:

---

# 🚀 Spark SQL Functions Cheat Sheet

---

## 🔹 1. String Functions

```sql
LOWER('Harsh') → 'harsh'
UPPER('Harsh') → 'HARSH'
INITCAP('harsh data') → 'Harsh Data'
LTRIM('   hi') → 'hi'
RTRIM('hi   ') → 'hi'
TRIM('   hi   ') → 'hi'
LENGTH('Spark') → 5
SUBSTRING('SparkSQL', 1, 5) → 'Spark'
INSTR('dataengineer', 'engine') → 5
REGEXP_REPLACE('2025-08-22','-','/') → '2025/08/22'
REGEXP_EXTRACT('abc-123','(\\d+)',1) → '123'
CONCAT('Harsh','Data') → 'HarshData'
CONCAT_WS('-', '2025','08','22') → '2025-08-22'
TRANSLATE('abc','abc','xyz') → 'xyz'
REVERSE('abc') → 'cba'
SPLIT('a,b,c',',') → ['a','b','c']
LOCATE('ar','Spark') → 2
```

---

## 🔹 2. Aggregate Functions

```sql
SUM(salary) → total salary
AVG(salary) → avg salary
MIN(age) → minimum age
MAX(age) → maximum age
COUNT(*) → row count
COLLECT_LIST(city) → ['Pune','Indore','Pune']
COLLECT_SET(city) → ['Pune','Indore']
```

---

## 🔹 3. Analytic (Window) Functions

```sql
ROW_NUMBER() OVER(PARTITION BY dept ORDER BY salary) → 1,2,3...
RANK() OVER(ORDER BY score DESC) → 1,2,2,4
DENSE_RANK() OVER(ORDER BY score DESC) → 1,2,2,3
LAG(salary,1) OVER(ORDER BY hire_date) → prev salary
LEAD(salary,1) OVER(ORDER BY hire_date) → next salary
SUM(sales) OVER(PARTITION BY product ORDER BY date) → running total
```

---

## 🔹 4. Date & Time Functions

```sql
CURRENT_DATE() → 2025-08-22
CURRENT_TIMESTAMP() → 2025-08-22 13:45:00
DATE_ADD('2025-08-22', 5) → 2025-08-27
DATE_SUB('2025-08-22', 5) → 2025-08-17
DATEDIFF('2025-08-22','2025-08-01') → 21
MONTHS_BETWEEN('2025-08-22','2025-06-22') → 2.0
TRUNC('2025-08-22','MM') → 2025-08-01
LAST_DAY('2025-08-22') → 2025-08-31
DATE_FORMAT('2025-08-22','yyyy/MM/dd') → '2025/08/22'
```

---

## 🔹 5. Math Functions

```sql
ABS(-10) → 10
ROUND(45.678,2) → 45.68
CEIL(4.2) → 5
FLOOR(4.8) → 4
SQRT(16) → 4
POW(2,3) → 8
EXP(1) → 2.718...
LOG(10) → 2.302...
RAND() → random [0,1)
RANDN() → normal distribution
```

---

## 🔹 6. Conditional Functions

```sql
CASE WHEN score > 50 THEN 'Pass' ELSE 'Fail' END
IF(age > 18, 'Adult', 'Minor')
NULLIF(col1, col2) → NULL if equal
COALESCE(NULL,'x','y') → 'x'
NVL(NULL,'default') → 'default'
```

---

## 🔹 7. Collection (Array/Map) Functions

```sql
SIZE(array(1,2,3)) → 3
ARRAY_CONTAINS(array('a','b'),'a') → true
SORT_ARRAY(array(3,1,2)) → [1,2,3]
EXPLODE(array(10,20)) → multiple rows: 10, 20
MAP_KEYS(map('a',1,'b',2)) → ['a','b']
MAP_VALUES(map('a',1,'b',2)) → [1,2]
```

---

## 🔹 8. JSON Functions

```sql
GET_JSON_OBJECT('{"id":1,"name":"Harsh"}','$.name') → 'Harsh'
FROM_JSON('{"id":1}', 'id INT') → {id:1}
TO_JSON(named_struct('id',1,'name','Harsh')) → {"id":1,"name":"Harsh"}
JSON_TUPLE('{"a":1,"b":2}','a','b') → 1,2
```

---

## 🔹 9. Higher-Order Functions (arrays/maps, Spark ≥ 2.4)

```sql
TRANSFORM(array(1,2,3), x -> x+1) → [2,3,4]
FILTER(array(1,2,3,4), x -> x%2=0) → [2,4]
EXISTS(array(1,2,3), x -> x=2) → true
AGGREGATE(array(1,2,3), 0, (acc,x) -> acc+x) → 6
```

---

## 🔹 10. Miscellaneous Functions

```sql
SHA2('abc',256) → hash value
BASE64('spark') → 'c3Bhcms='
UNBASE64('c3Bhcms=') → 'spark'
INPUT_FILE_NAME() → full path of source file
UUID() → random UUID
MONOTONICALLY_INCREASING_ID() → unique increasing id
```
```
MD5('spark') → '8cde774d6f7333752ed72cacddb05126'
SHA1('spark') → 'b37f7e36d4e59e79eea36b43fe0ad192b9cd99ef'
SHA2('spark', 256) → '401b85e...f5b8'   -- SHA-256
SHA2('spark', 512) → 'd88249d...c293'   -- SHA-512
```

---


