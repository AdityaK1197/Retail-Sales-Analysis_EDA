#  Retail Sales Analysis_EDA

A complete SQL Server project that demonstrates the ETL (Extract, Transform, Load) pipeline and Exploratory Data Analysis (EDA) on retail sales data. This repository shows how to ingest raw CSVs, clean and transform them into analytics-ready tables, and answer key business questions using SQL queries.

# 📌 Features
A) ETL Process

1) Create staging (mastertable) and gold (gold_mastertable) tables
2) Bulk load CSV data into SQL Server
3) Handle missing values (e.g., impute missing ages with average)
4) Correct raw data issues (typos, null cleanup)
5) Remove incomplete or invalid records

B) Exploratory Data Analysis (EDA)

1) Sales by date and category
2) High-value transactions (>1000)
3) Top customers by total sales
4) Category-wise unique customer counts
5) Monthly average sales & best-selling months
6) Gender-wise transaction counts
7) Shift-wise sales trends (Morning, Afternoon, Evening)

# 🛠️ Tech Stack
Database: Microsoft SQL Server (2019 or later recommended)
Language: T-SQL
Data Source: CSV file (Retail Sales Transactions)

# 📂 Repository Structure

![my image](https://github.com/AdityaK1197/Retail-Sales-Analysis_EDA/blob/b0896dc071d28ee3e44e3114f77819bc75345143/Repostructure.png)

# 📊 Sample EDA Queries

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

# 📄License
This project is licensed under the MIT License

# 🙌 Contribution

Pull requests are welcome! For major changes, please open an issue first to discuss what you’d like to change.







