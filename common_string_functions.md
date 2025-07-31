### ✅ **String Functions Used**

---

### 🔹 In **SQL**:

* `LOWER()` – converts to lowercase
* `UPPER()` – converts to uppercase
* `LTRIM()` / `RTRIM()` / `TRIM()` – remove spaces
* `SUBSTR()` / `SUBSTRING()` – extract substring
* `LENGTH()` – string length
* `INSTR()` – position of substring
* `REPLACE()` – replace substring
* `CONCAT()` / `||` – string concatenation
* `LIKE`, `ILIKE` – pattern matching
* `REGEXP_LIKE()` – regex match
* `CAST()` – convert datatype (e.g. string to int)

---

### 🔹 In **PySpark** (`pyspark.sql.functions`):

* `lower(col)` / `upper(col)`
* `ltrim(col)` / `rtrim(col)` / `trim(col)`
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

Let me know if you want syntax or examples for any.
