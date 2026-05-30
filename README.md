# 🛒 Retail Sales Analysis SQL Project

## 📋 Project Overview

**Project Title**: Retail Sales Analysis  

This project analyzes retail sales data using SQL to generate actionable business insights. It focuses on sales trends, customer behavior, product performance, and revenue analysis to support data-driven decision-making

## 🛠️ Tools Used
- PostgreSQL (Database)
- pgAdmin (SQL Query Tool & Database Management)


## 🎯 Objectives

1. **Set up a retail sales database**: Create and populate a retail sales database with the provided sales data.
2. **Data Cleaning**: Identify and remove any records with missing or null values.
3. **Exploratory Data Analysis (EDA)**: Perform basic exploratory data analysis to understand the dataset.
4. **Business Analysis**: Use SQL to answer specific business questions and derive insights from the sales data.

## 📁 Project Structure

### 1. 🗄️ Database Setup

- **Database Creation**: The project begins by creating a database to store and manage retail sales data for analysis.

- **Table Creation**: A table named retail_sales is created to store transaction-level sales data. It includes details such as transaction ID, sale date and time, customer information, product category, quantity sold, pricing details, cost of goods sold (COGS), and total sale amount.

```sql

CREATE TABLE retail_sales
(
    transactions_id	 INT PRIMARY KEY,
	sale_date DATE,
	sale_time	TIME NOT NULL,
	customer_id	INT,
	gender VARCHAR(50),
	age	INT ,
	category VARCHAR(50),	
	quantiy INT ,
	price_per_unit FLOAT,
	cogs FLOAT,
	total_sale FLOAT
);
```

### 2. 🔍 Data Exploration & Cleaning

- **Record Count**: Determine the total number of records in the dataset.
- **Customer Count**: Find out how many unique customers are in the dataset.
- **Category Count**: Identify all unique product categories in the dataset.
- **Null Value Check**: Check for any null values in the dataset and delete records with missing data.

```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT * FROM retail_sales
WHERE 
    quantiy IS NULL OR  price_per_unit IS NULL
    OR cogs IS NULL OR total_sale IS NULL;

DELETE  FROM Retail_sales 
WHERE 
    quantiy IS NULL OR price_per_unit IS NULL OR 
    cogs IS NULL OR total_sale IS NULL;
```

### 3. 📊 Data Analysis & Findings

The following SQL queries were developed to answer specific business questions:

1. **Write a SQL query to retrieve all columns for sales made on '2022-11-05**:
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```

2. **Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov**:
```sql
SELECT *
FROM retail_sales
WHERE 
    category = 'Clothing'
    AND EXTRACT(MONTH FROM sale_date) = 11
	AND quantiy >= 4;
```

3. **Write a SQL query to calculate the total sales (total_sale) for each category.**:
```sql
SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1;
```

4. **Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**:
```sql
SELECT customer_id , 
    category,
    Round(AVG(age),2) AS avg_age
FROM Retail_sales
GROUP BY customer_id ,category
HAVING category = 'Beauty'
ORDER BY customer_id;
```

5. **Write a SQL query to find all transactions where the total_sale is greater than 1000.**:
```sql
SELECT * FROM retail_sales
WHERE total_sale > 1000
```

6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**:
```sql
SELECT gender, 
    category, 
    COUNT(transactions_id) AS total_transactions
FROM Retail_sales
GROUP BY gender,category 
ORDER BY category;
```

7. **Write a SQL query to find the top 5 customers based on the highest total sales**:
```sql
SELECT * FROM 
(
SELECT DISTINCT(customer_id) , SUM(total_sale) AS total_sale,
RANK() OVER (ORDER BY SUM(total_sale) DESC) AS rank 
FROM Retail_sales
GROUP BY customer_id
ORDER BY 2 DESC  
) AS t2
 WHERE rank <=5;

```

8. **Write a SQL query to find the number of unique customers who purchased items from each category**:
```sql
ELECT  category,COUNT(DISTINCT(customer_id)) AS total_unique_customers  
FROM Retail_sales 
GROUP BY category;
```

9. **Segment customers based on age group and spending value**:
```sql
 SELECT customer_id,age,total_sale,
CASE 
    WHEN age < 25 THEN 'Young'
	WHEN age BETWEEN 25 AND 45 THEN 'Middle Age'
	WHEN age > 45 THEN 'Senior'
	END AS customer_segment,
CASE
    WHEN total_sale > 1000 THEN 'High value'
	WHEN total_sale BETWEEN 500 AND 1000 THEN 'Medium Value'
	ELSE 'Low Value'
	END AS customer_value
FROM Retail_sales;
```


```

## 💡 Key Insights
-**Identified sales trends, customer behavior, and product performance using SQL analysis**.
-**Found top-performing categories and high-value customers contributing most to revenue**.
-**Observed sales patterns across time, regions, and customer segments for better decision-making**.

## 📑 Reports
-**Sales Summary**: Summary of total sales, customer details, and category-wise performance.
-**Trend Analysis**: Analysis of sales patterns across months and different time shifts.
-**Customer Insights**: Identification of top customers and unique customers per category.

## ✅ Conclusion

This project provides a comprehensive introduction to SQL for data analysis, covering database setup, data cleaning, and exploratory analysis using business-driven queries. The insights generated help in understanding sales trends, customer behavior, and product performance to support data-driven decision-making.
