### Sales table analysis using SQL
```sql
USE harshdb;

drop table retail_sales;
CREATE TABLE retail_sales (
    product_id INT NOT NULL,
    product_name NVARCHAR(255) NOT NULL,
    sales_date DATE NOT NULL,
    sales_amount DECIMAL(18, 2) NOT NULL,
);

EXEC sp_rename 'retail_sales.product_name', 'product_category', 'COLUMN';


INSERT INTO retail_sales (product_id, product_category, sales_date, sales_amount) VALUES
(1, 'Product A', '2021-01-15', 100.00),
(1, 'Product A', '2021-02-14', 150.00),
(1, 'Product A', '2021-03-10', 200.00),
(1, 'Product A', '2021-04-25', 250.00),
(1, 'Product A', '2021-05-30', 300.00),
(1, 'Product A', '2021-06-05', 350.00),
(1, 'Product A', '2021-07-19', 400.00),
(1, 'Product A', '2021-08-23', 450.00),
(1, 'Product A', '2021-09-12', 500.00),
(1, 'Product A', '2021-10-18', 550.00),
(1, 'Product A', '2021-11-16', 600.00),
(1, 'Product A', '2021-12-31', 650.00),
(2, 'Product B', '2022-01-11', 80.00),
(2, 'Product B', '2022-02-22', 120.00),
(2, 'Product B', '2022-03-15', 180.00),
(2, 'Product B', '2022-04-10', 240.00),
(2, 'Product B', '2022-05-12', 300.00),
(2, 'Product B', '2022-06-20', 360.00),
(2, 'Product B', '2022-07-28', 420.00),
(2, 'Product B', '2022-08-19', 480.00),
(2, 'Product B', '2022-09-05', 540.00),
(2, 'Product B', '2022-10-14', 600.00),
(2, 'Product B', '2022-11-30', 660.00),
(2, 'Product B', '2022-12-01', 720.00),
(3, 'Product C', '2023-01-15', 90.00),
(3, 'Product C', '2023-02-14', 130.00),
(3, 'Product C', '2023-03-10', 190.00),
(3, 'Product C', '2023-04-25', 250.00),
(3, 'Product C', '2023-05-30', 310.00),
(3, 'Product C', '2023-06-05', 370.00),
(3, 'Product C', '2023-07-19', 430.00),
(3, 'Product C', '2023-08-23', 490.00),
(3, 'Product C', '2023-09-12', 550.00),
(3, 'Product C', '2023-10-18', 610.00),
(3, 'Product C', '2023-11-16', 670.00),
(3, 'Product C', '2023-12-31', 730.00),
(4, 'Product D', '2024-01-11', 75.00),
(4, 'Product D', '2024-02-22', 115.00),
(4, 'Product D', '2024-03-15', 175.00),
(4, 'Product D', '2024-04-10', 235.00),
(4, 'Product D', '2024-05-12', 295.00),
(4, 'Product D', '2024-06-20', 355.00),
(4, 'Product D', '2024-07-28', 415.00),
(4, 'Product D', '2024-08-19', 475.00),
(4, 'Product D', '2024-09-05', 535.00),
(4, 'Product D', '2024-10-14', 595.00),
(4, 'Product D', '2024-11-30', 655.00),
(4, 'Product D', '2024-12-01', 715.00),
(5, 'Product E', '2021-01-02', 200.00),
(5, 'Product E', '2021-02-02', 250.00),
(5, 'Product E', '2021-03-02', 300.00),
(5, 'Product E', '2021-04-02', 350.00),
(5, 'Product E', '2021-05-02', 400.00),
(5, 'Product E', '2021-06-02', 450.00),
(5, 'Product E', '2021-07-02', 500.00),
(5, 'Product E', '2021-08-02', 550.00),
(5, 'Product E', '2021-09-02', 600.00),
(5, 'Product E', '2021-10-02', 650.00),
(5, 'Product E', '2021-11-02', 700.00),
(5, 'Product E', '2021-12-02', 750.00),
(5, 'Product E', '2021-01-02', 200.00),
(5, 'Product E', '2021-02-02', 250.00),
(5, 'Product E', '2021-03-02', 300.00),
(5, 'Product E', '2021-04-02', 350.00),
(5, 'Product E', '2021-05-02', 400.00),
(5, 'Product E', '2021-06-02', 450.00),
(5, 'Product E', '2021-07-02', 500.00),
(5, 'Product E', '2021-08-02', 550.00),
(5, 'Product E', '2021-09-02', 600.00),
(5, 'Product E', '2021-10-02', 650.00),
(6, 'Product F', '2022-01-05', 110.00),
(6, 'Product F', '2022-02-12', 160.00),
(6, 'Product F', '2022-03-22', 210.00),
(6, 'Product F', '2022-04-15', 260.00),
(6, 'Product F', '2022-05-18', 310.00),
(6, 'Product F', '2022-06-11', 360.00),
(6, 'Product F', '2022-07-13', 410.00),
(6, 'Product F', '2022-08-25', 460.00),
(2, 'Product B', '2021-03-15', 180.00),
(2, 'Product B', '2021-04-10', 240.00),
(2, 'Product B', '2021-05-12', 300.00),
(2, 'Product B', '2021-06-20', 360.00),
(2, 'Product B', '2021-07-28', 420.00),
(3, 'Product C', '2024-06-05', 370.00),
(3, 'Product C', '2022-07-19', 430.00),
(3, 'Product C', '2024-08-23', 490.00),
(3, 'Product C', '2021-09-12', 550.00),
(3, 'Product C', '2024-10-18', 610.00);


select * from retail_sales;


--select FORMAT(sales_date, 'yyyy-MM') as sales_month from retail_sales;


--find 1. yearly sales for each year 
select 
	FORMAT(sales_date, 'yyyy') as sales_year,
	sum(sales_amount) as yearly_sales
from retail_sales
	group by FORMAT(sales_date, 'yyyy') 
	order by FORMAT(sales_date, 'yyyy');

--using CTE
WITH 
CTE AS (select FORMAT(sales_date, 'yyyy') as sales_year, sales_amount from retail_sales)

select 
	sales_year,
	sum(sales_amount) as yearly_sales
from CTE
	group by sales_year order by sales_year;


--2. monthly salses for each month. 
WITH 
CTE AS (select 
			FORMAT(sales_date, 'yyyy') as sales_year,
			FORMAT(sales_date, 'yyyy-MM') as sales_month,
			sales_amount 
		FROM retail_sales)
select 
	sales_year,
	sales_month,
	sum(sales_amount) as monthly_sales
from CTE
	group by sales_year,sales_month order by sales_year,sales_month;

--3. Most sold product category each year.
WITH 
CTE AS (
select product_category, FORMAT(sales_date, 'yyyy') as sales_year, sum(sales_amount) as total_sales from retail_sales
group by product_category, FORMAT(sales_date, 'yyyy')
)
select sales_year, product_category, total_sales,RANK() over(partition by sales_year order by total_sales) AS sales_rank from CTE
--WHERE sales_rank = 1;


--chat GPT response:-
WITH YearlySales AS (
    SELECT 
        YEAR(sales_date) AS sales_year,
        product_category,
        SUM(sales_amount) AS total_sales
    FROM 
        retail_sales
    GROUP BY 
        YEAR(sales_date), product_category
),
RankedSales AS (
    SELECT 
        sales_year,
        product_category,
        total_sales,
        RANK() OVER (PARTITION BY sales_year ORDER BY total_sales DESC) AS sales_rank
    FROM 
        YearlySales
)
SELECT 
    sales_year,
    product_category,
    total_sales,
    sales_rank
FROM 
    RankedSales
WHERE 
    sales_rank = 1;  -- To get only the top-ranked categories
```





