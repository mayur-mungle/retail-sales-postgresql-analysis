DROP TABLE IF EXISTS Retail_sales;

--SQL RETAIL SALES PROJECT----

CREATE TABLE Retail_sales(
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

--DATA CLEANING ---

SELECT * FROM Retail_sales;

SELECT COUNT(*)  FROM Retail_sales; /* count total number of rows */

SELECT COUNT(DISTINCT(gender))  FROM Retail_sales; /* count type of gender */

SELECT COUNT(DISTINCT(category)) FROM Retail_sales; /* count unique category */

SELECT * FROM Retail_sales
WHERE transactions_id  IS NULL;

---DELETE NULL VALUES ROWS ----

SELECT * FROM Retail_sales 
WHERE quantiy IS NULL
 OR 
  price_per_unit IS NULL
  OR 
  cogs IS NULL 
  OR 
  total_sale IS NULL;

DELETE  FROM Retail_sales 
WHERE quantiy IS NULL
 OR 
  price_per_unit IS NULL
  OR 
  cogs IS NULL 
  OR 
  total_sale IS NULL;

--DATA Exploration

--How many sales we have ?
SELECT COUNT(transactions_id) AS total_sales FROM Retail_sales;

--How many Unique customers we have?
SELECT COUNT(DISTINCT(customer_id)) AS total_customers FROM Retail_sales;

--How many categories we have ?
SELECT DISTINCT category FROM Retail_sales;

---DATA ANALYSIS OR BUSINESS KEY PROBLEMS 

-- My Analysis & Findings
-- Q.1 Write a SQL query to retrieve all columns for sales made on '2022-11-05
-- Q.2 Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4.
-- Q.3 Write a SQL query to calculate the total sales (total_sale) for each category.
-- Q.4 Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.
-- Q.5 Write a SQL query to find all transactions where the total_sale is greater than 1000.
-- Q.6 Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.
-- Q.7 Write a SQL query to find the top 5 customers based on the highest total sales 
-- Q.8 Write a SQL query to find the number of unique customers who purchased items from each category.
-- Q.9 Segment customers based on age group and spending value.

-- Q.1 Write a SQL query to retrieve all columns for sales made on '2022-11-05
SELECT * FROM Retail_sales 
WHERE sale_date = '2022-11-05'
ORDER BY transactions_id ;

/* Q.2 Write a SQL query to retrieve all transactions where 
the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov */
SELECT * FROM Retail_sales
WHERE category = 'Clothing'
      AND EXTRACT(MONTH FROM sale_date) = 11
	  AND quantiy >= 4;

-- Q.3 Write a SQL query to calculate the total sales (total_sale) for each category.
SELECT category , SUM(total_sale) AS net_sale
FROM Retail_sales 
GROUP BY category ;

-- Q.4 Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.
SELECT customer_id , category,Round(AVG(age),2) AS avg_age
FROM Retail_sales
GROUP BY customer_id ,category
HAVING category = 'Beauty'
ORDER BY customer_id;

-- Q.5 Write a SQL query to find all transactions where the total_sale is greater than 1000.
SELECT * FROM Retail_sales 
WHERE total_sale >= 1000;


-- Q.6 Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.
SELECT gender , category , COUNT(transactions_id) AS total_transactions
FROM Retail_sales
GROUP BY gender , category 
ORDER BY category;


	
-- Q.7 Write a SQL query to find the top 5 customers based on the highest total sales
SELECT * FROM 
(
SELECT DISTINCT(customer_id) , SUM(total_sale) AS total_sale,
RANK() OVER (ORDER BY SUM(total_sale) DESC) AS rank 
FROM Retail_sales
GROUP BY customer_id
ORDER BY 2 DESC  
 ) AS t2
 WHERE rank <=5;

-- Q.8 Write a SQL query to find the number of unique customers who purchased items from each category.
SELECT  category,COUNT(DISTINCT(customer_id)) AS total_unique_customers  
FROM Retail_sales 
GROUP BY category;


--Q.9 Segment customers based on age group and spending value --
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








