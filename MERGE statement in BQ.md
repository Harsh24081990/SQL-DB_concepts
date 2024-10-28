##### In BigQuery, the syntax for the MERGE statement does not require the use of INTO. You simply use MERGE followed by the target table alias. This is a bit different from SQL standards where MERGE INTO is more common.
### Merge into syntax
```sql
MERGE my_dataset.target_table AS t
USING my_dataset.temp_table AS s
ON t.id = s.id AND t.name = s.name AND t.value = s.value
WHEN NOT MATCHED THEN
  INSERT (id, name, value)
  VALUES (s.id, s.name, s.value)
```


##### If need to compare entire row between source and target (all columns) to check the records present or not in target , instead of comparing all column one by one we can use below:-
```SQL
MERGE my_dataset.target_table AS t
USING my_dataset.temp_table AS s
ON HASH(TO_JSON_STRING(t.*)) = HASH(TO_JSON_STRING(s.*))
WHEN NOT MATCHED THEN
  INSERT (column1, column2, ..., columnN)  -- List the columns you want to insert
  VALUES (s.column1, s.column2, ..., s.columnN)
```

- Make sure that your data types are compatible when using TO_JSON_STRING. Complex or nested data types might require additional handling.
- This method assumes that all columns are relevant for determining duplicates. If there are columns that shouldn't be considered (like timestamps), you may need to exclude them or adjust your approach accordingly.
