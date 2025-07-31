### QUE: What are materialized view, when it is needed and must to use, give any practical example where you have used in your career ?

### ANS:

**Materialized View (MV):**
A materialized view is a precomputed, stored result of a query. Unlike normal views (which are virtual and recomputed on access), MVs store data physically and must be refreshed manually or on schedule.

---

**When to Use (Must Use Scenarios):**

* Complex joins/aggregations on large datasets.
* Frequent querying of the same aggregated data.
* Performance boost is needed for BI tools (e.g., Power BI/Tableau).
* Data doesn't need to be real-time.

---

**Example Use Case from Career:**
In a sales reporting dashboard (Power BI), daily sales by region/product required heavy joins across `sales`, `customer`, and `product` tables. Query took 40+ seconds.
**Solution:** Created a materialized view that pre-aggregated daily sales.

```sql
CREATE MATERIALIZED VIEW daily_sales_mv
AS
SELECT region, product_id, SUM(sale_amount) AS total_sales, sale_date
FROM sales
JOIN customer ON sales.cust_id = customer.id
GROUP BY region, product_id, sale_date;
```

**Benefit:** Dashboard load time reduced to under 5 seconds.

