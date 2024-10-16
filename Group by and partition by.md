## Group by Vs Partition by
- **`GROUP BY`**: Reduces the number of rows in the result set to one per group (one row per category). You cannot see individual sales amounts or any other details.
- **`PARTITION BY`**: Retains all individual rows while adding aggregated values, allowing you to analyze the data in more detail alongside the calculated aggregates.
Use `GROUP BY` when you need summarized results, such as finding maximum values per category, and use `PARTITION BY` when you want to maintain the detail of individual records while performing calculations on those records.

--------------------------------------------------
One key use case for the `PARTITION BY` clause that cannot be achieved with `GROUP BY` is the calculation of **running totals** or **cumulative sums**. 

### Example of Running Total

Suppose you have a `sales` table like this:

| product_id | sales_date  | sales_amount |
|------------|-------------|--------------|
| 1          | 2024-01-01  | 100          |
| 1          | 2024-01-02  | 150          |
| 1          | 2024-01-03  | 200          |
| 2          | 2024-01-01  | 250          |
| 2          | 2024-01-02  | 300          |

### Using `PARTITION BY` for Running Total

You can calculate a running total for each product using the following query:

```sql
SELECT product_id,
       sales_date,
       sales_amount,
       SUM(sales_amount) OVER (PARTITION BY product_id ORDER BY sales_date) AS running_total
FROM sales;
```

### Result

The result would look like this:

| product_id | sales_date  | sales_amount | running_total |
|------------|-------------|--------------|---------------|
| 1          | 2024-01-01  | 100          | 100           |
| 1          | 2024-01-02  | 150          | 250           |
| 1          | 2024-01-03  | 200          | 450           |
| 2          | 2024-01-01  | 250          | 250           |
| 2          | 2024-01-02  | 300          | 550           |

### Why This Cannot Be Done with `GROUP BY`

- **Row-Level Context**: The `PARTITION BY` clause allows you to retain the detail of individual rows while performing calculations across them. You can see how the total accumulates over time for each product.
- **No Aggregation Loss**: Using `GROUP BY` would reduce the dataset to one row per product, losing all row-level detail, including the date and individual sales amounts. You would not be able to show how the total changes over time.

### Conclusion

The ability to compute running totals or cumulative aggregates while keeping individual record details is a key feature of window functions with `PARTITION BY`, making it a scenario that cannot be accomplished using `GROUP BY`.

-----------------------------------------------------------------
Another use case for `PARTITION BY` that cannot be accomplished with `GROUP BY` is the calculation of **rankings or row numbering** within partitions of your data.

### Example of Ranking with `RANK()`

Consider a `sales` table structured like this:

| product_id | category_id | sales_amount |
|------------|-------------|--------------|
| 1          | A           | 100          |
| 2          | A           | 150          |
| 3          | A           | 200          |
| 4          | B           | 250          |
| 5          | B           | 300          |

### Using `PARTITION BY` for Ranking

You can calculate the rank of sales amounts within each category using:

```sql
SELECT product_id,
       category_id,
       sales_amount,
       RANK() OVER (PARTITION BY category_id ORDER BY sales_amount DESC) AS sales_rank
FROM sales;
```

### Result

The result would look like this:

| product_id | category_id | sales_amount | sales_rank |
|------------|-------------|--------------|------------|
| 3          | A           | 200          | 1          |
| 2          | A           | 150          | 2          |
| 1          | A           | 100          | 3          |
| 5          | B           | 300          | 1          |
| 4          | B           | 250          | 2          |

### Why This Cannot Be Done with `GROUP BY`

- **Row-Level Context**: The `RANK()` function with `PARTITION BY` retains the details of each individual row while assigning ranks based on their values within the partition.
- **No Aggregation Loss**: Using `GROUP BY` would not allow you to assign ranks since it collapses multiple rows into a single row per group. You cannot see how individual items compare against each other within their categories.
- **Multiple Ranks**: Additionally, if there are ties in sales amounts, `RANK()` provides the same rank to tied values and skips the next rank(s), which cannot be replicated with `GROUP BY`.

### Conclusion

Calculating rankings or row numbers based on specific criteria within partitions of data is a strong use case for `PARTITION BY`. It provides insights into the relative standing of each record within its group, something that cannot be done with `GROUP BY` alone.
---------------------------------------------------------------------
