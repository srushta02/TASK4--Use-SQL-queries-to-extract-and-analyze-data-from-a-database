-- Task 4: SQL for Data Analysis on sales_data_sample

-- a) SELECT, WHERE, ORDER BY, GROUP BY
SELECT ORDERNUMBER, CUSTOMERNAME, COUNTRY, SALES
FROM sales_data_sample
WHERE COUNTRY = 'USA';

SELECT ORDERNUMBER, CUSTOMERNAME, SALES
FROM sales_data_sample
ORDER BY SALES DESC
LIMIT 10;

SELECT COUNTRY, SUM(SALES) AS total_sales
FROM sales_data_sample
GROUP BY COUNTRY
ORDER BY total_sales DESC;

-- b) JOINS (Self Joins)
SELECT o1.ORDERNUMBER, o1.CUSTOMERNAME, o2.PRODUCTLINE, o1.SALES
FROM sales_data_sample o1
INNER JOIN sales_data_sample o2 ON o1.ORDERNUMBER = o2.ORDERNUMBER;

SELECT o1.ORDERNUMBER, o1.CUSTOMERNAME, o2.PRODUCTLINE, o1.SALES
FROM sales_data_sample o1
LEFT JOIN sales_data_sample o2 ON o1.ORDERNUMBER = o2.ORDERNUMBER;

SELECT o1.ORDERNUMBER, o1.CUSTOMERNAME, o2.PRODUCTLINE, o1.SALES
FROM sales_data_sample o1
RIGHT JOIN sales_data_sample o2 ON o1.ORDERNUMBER = o2.ORDERNUMBER;

-- c) Subquery
SELECT DISTINCT CUSTOMERNAME
FROM sales_data_sample
WHERE CUSTOMERNAME IN (
    SELECT CUSTOMERNAME
    FROM sales_data_sample
    GROUP BY CUSTOMERNAME
    HAVING SUM(SALES) > (SELECT AVG(SALES) FROM sales_data_sample)
);

-- d) Aggregate Functions
SELECT SUM(SALES) AS total_revenue FROM sales_data_sample;
SELECT AVG(SALES) AS avg_sales FROM sales_data_sample;
SELECT PRODUCTLINE, SUM(SALES) AS total_sales
FROM sales_data_sample
GROUP BY PRODUCTLINE
ORDER BY total_sales DESC;

-- e) Views
CREATE VIEW Top_Customers AS
SELECT CUSTOMERNAME, COUNTRY, SUM(SALES) AS total_sales
FROM sales_data_sample
GROUP BY CUSTOMERNAME, COUNTRY
ORDER BY total_sales DESC;

SELECT * FROM Top_Customers LIMIT 10;

-- f) Indexes
CREATE INDEX idx_ordernumber ON sales_data_sample(ORDERNUMBER);
CREATE INDEX idx_customername ON sales_data_sample(CUSTOMERNAME);
CREATE INDEX idx_productline ON sales_data_sample(PRODUCTLINE);


# Task 4: SQL for Data Analysis

**Objective:** Analyze the `sales_data_sample` table using SQL queries.
**Tools:** MySQL (Workbench)
**Dataset:** `sales.sales_data_sample`

---

 a) SELECT, WHERE, ORDER BY, GROUP BY

Queries used to filter, sort, and group sales data. Helpful for region-wise and order-level insights.

 b) JOINS

Self-joins demonstrate combining rows with the same order number. Useful for linking orders and product details.

 c) Subqueries

Finds customers whose total sales exceed average sales. Helps identify high-value customers.

 d) Aggregate Functions

Calculates total revenue, average sales, and category-wise performance. Provides key business metrics.

 e) Views

Created a reusable view (`Top_Customers`) to analyze customer contribution easily. Simplifies reporting.

f) Indexes

Indexes on `ORDERNUMBER`, `CUSTOMERNAME`, and `PRODUCTLINE` improve query performance. Optimizes searches.








