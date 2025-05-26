#### Problem : 	compare each date price with previous date price and create the price_change column accordingly. 

![image](https://github.com/user-attachments/assets/fae6d47d-2aa8-4abe-8ec5-1ee268c07053)

#### create table
```sql
create table stocks
(
  stock_id STRING,
  date DATE,
  price DOUBLE
);
INSERT INTO stocks
(stock_id, date, price) VALUES
('A', '2024-01-01', 150.0),
('A', '2024-01-02', 153.0),
('A', '2024-01-03', 153.0),
('A', '2024-01-04', 155.0),
('A', '2024-01-05', 145.0),
('B', '2024-01-01', 2800.0),
('B', '2024-01-02', 2825.0),
('B', '2024-01-03', 2825.0),
('B', '2024-01-04', 2790.0),
('C', '2024-01-01', 3800.0),
('C', '2024-01-02', 2825.0),
('C', '2024-01-02', 2825.0),
('C', '2024-01-03', 3790.0);
```

#### slotion using conventional way - using self join and 'DATEADD' function to compare previous row of same table. 
```sql
SELECT 
  A.stock_id, 
  A.date AS date, 
  A.price,
  CASE 
    WHEN B.price IS NULL THEN NULL
    WHEN A.price = B.price THEN 'SAME'
    WHEN A.price > B.price THEN 'UP'
    WHEN A.price < B.price THEN 'DOWN'
  END AS price_change
FROM stocks A
LEFT JOIN stocks B 
  ON A.stock_id = B.stock_id 
  AND A.date = DATEADD(DAY, 1, B.date)
ORDER BY A.stock_id, A.date;
```

#### using LAG windows function and subquery. (LAG for comparing previous row of same table without using self join)
```sql
select stock_id,
        date,
        price,
        CASE WHEN price_change is null then NULL
              WHEN price_change > 0 then 'UP'
              WHEN price_change < 0 then 'DOWN'
              WHEN price_change = 0 then 'SAME'
        END AS PRICE_CHANGE
FROM
(SELECT
  stock_id,
  date,
  price,
  price - LAG(price) OVER (PARTITION BY stock_id ORDER BY date) AS price_change
FROM stocks)
```


#### using LAG windows function and Common Table Expression.
```sql
SELECT
  stock_id,
  date,
  price,
  price - LAG(price) OVER (PARTITION BY stock_id ORDER BY date) AS price_change
FROM stocks)
select stock_id,
        date,
        price,
        CASE WHEN price_change is null then NULL
              WHEN price_change > 0 then 'UP'
              WHEN price_change < 0 then 'DOWN'
              WHEN price_change = 0 then 'SAME'
        END AS PRICE_CHANGE
from CTE
```
