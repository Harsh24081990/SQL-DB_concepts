MERGE INTO edw_prod.main_table t
USING stg.stage_table s
   ON (t.document_key = s.document_key)
WHEN MATCHED THEN
     UPDATE SET t.col1 = s.col1,
                t.col2 = s.col2,
                t.col3 = s.col3
WHEN NOT MATCHED THEN
     INSERT (document_key, col1, col2, col3)
     VALUES (s.document_key, s.col1, s.col2, s.col3);
