# Retail Sales Analysis_EDA

A complete SQL Server project that demonstrates the ETL (Extract, Transform, Load) pipeline and Exploratory Data Analysis (EDA) on retail sales data. This repository shows how to ingest raw CSVs, clean and transform them into analytics-ready tables, and answer key business questions using SQL queries.

# Features
ETL Process
Create staging (mastertable) and gold (gold_mastertable) tables
Bulk load CSV data into SQL Server
Handle missing values (e.g., impute missing ages with average)
Correct raw data issues (typos, null cleanup)
Remove incomplete or invalid records

# Exploratory Data Analysis (EDA)
Sales by date and category
High-value transactions (>1000)
Top customers by total sales
Category-wise unique customer counts
Monthly average sales & best-selling months
Gender-wise transaction counts
Shift-wise sales trends (Morning, Afternoon, Evening)

# Tech Stack
Database: Microsoft SQL Server (2019 or later recommended)
Language: T-SQL
Data Source: CSV file (Retail Sales Transactions)


# Retail Sales Analysis_EDA/
├── sql/
│   ├── 01_create_db_and_tables.sql
│   ├── 02_bulk_insert_staging.sql
│   ├── 03_transform_to_gold.sql
│   └── 04_eda_queries.sql
├── data/
│   └── retail_sales.csv    # (example path; not included in repo)
├── README.md
└── LICENSE

# Sample EDA Queries

# Total sales by category
SELECT category, SUM(total_sale) AS TotalSales
FROM gold_mastertable
GROUP BY category
ORDER BY TotalSales DESC;

# Top 5 customers
SELECT TOP 5 customer_id, SUM(total_sale) AS TotalSales
FROM gold_mastertable
GROUP BY customer_id
ORDER BY TotalSales DESC;

# Shift-wise order counts
WITH shifts AS (
  SELECT *,
    CASE
      WHEN DATEPART(HOUR, sale_time) < 12 THEN 'Morning'
      WHEN DATEPART(HOUR, sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
      ELSE 'Evening' END AS shift_type
  FROM gold_mastertable
)
SELECT shift_type, COUNT(transactions_id) AS order_count
FROM shifts
GROUP BY shift_type;

# 🙌 Contribution

Pull requests are welcome! For major changes, please open an issue first to discuss what you’d like to change.







