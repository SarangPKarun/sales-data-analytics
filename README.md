# Data Analysis Using MySQL and Power BI
=====================================

## Installation Steps
---------------

### 1. Install MySQL

* Download and install MySQL Server and MySQL Workbench from the official website.
* Follow the installation wizard and set up a root user and password.

### 2. Install Power BI Desktop

* Download Power BI Desktop from the Microsoft Power BI website.
* Follow the installation instructions to complete the setup.

---

## Import Database into MySQL
-------------------------

### Steps

1. Open MySQL Workbench.
2. Navigate to `File > Open SQL Script`.
3. Select the `db_dump.sql` file to open it in MySQL Workbench.
4. Execute the script to import the database into MySQL by clicking the lightning bolt (`Execute`) button.
5. The database will be imported, and you can view its tables in the left-hand sidebar.

---

## SQL Queries for Data Analysis
-----------------------------

### 1. Show all customer records

```sql
SELECT * 
FROM customers;
```

### 2. Count the total number of customers

```sql
SELECT COUNT(*) AS total_customers 
FROM customers;
```

### 3. Show transactions for the Chennai market

```sql
SELECT *  
FROM transactions  
WHERE market_code = 'Mark001';  
```

### 4. Show distinct product codes sold in Chennai

```sql
SELECT DISTINCT product_code  
FROM transactions  
WHERE market_code = 'Mark001';  
```

### 5. Show transactions where currency is USD

```sql
SELECT *  
FROM transactions  
WHERE currency = 'USD';  
```

### 6. Show transactions for the year 2020

```sql
SELECT t.*, d.*  
FROM transactions AS t  
INNER JOIN date AS d  
ON t.order_date = d.date  
WHERE d.year = 2020;  
```

### 7. Show total revenue for the year 2020

```sql
SELECT SUM(t.sales_amount) AS total_revenue  
FROM transactions AS t  
INNER JOIN date AS d  
ON t.order_date = d.date  
WHERE d.year = 2020  
AND (t.currency = 'INR' OR t.currency = 'USD');  
```

### 8. Show total revenue for January 2020

```sql
SELECT SUM(t.sales_amount) AS january_revenue  
FROM transactions AS t  
INNER JOIN date AS d  
ON t.order_date = d.date  
WHERE d.year = 2020  
AND d.month_name = 'January'  
AND (t.currency = 'INR' OR t.currency = 'USD');  
```

### 9. Show total revenue for the year 2020 in Chennai

```sql
SELECT SUM(t.sales_amount) AS chennai_revenue  
FROM transactions AS t  
INNER JOIN date AS d  
ON t.order_date = d.date  
WHERE d.year = 2020  
AND t.market_code = 'Mark001';  
```


### Connect Power BI to MySQL

1. Open Power BI Desktop.  
2. Go to **Home > Get Data > More**.  
3. Select **MySQL database** from the list of data sources.  
4. Enter `localhost` as the server and provide your MySQL credentials.  
5. Select the database you imported and load the data into Power BI.  

---

### Power BI: Create `norm_amount` Column

1. Navigate to the **Transform Data** section in Power BI.  
2. Use the following formula to create a new column:  

```
= Table.AddColumn(#"Filtered Rows", "norm_amount", if [currency] = "USD" or [currency] = "USD#(cr)" then [sales_amount] * 75 else [sales_amount], type number)
```

- This formula converts all USD sales amounts to INR (multiplying by 75) and keeps INR values unchanged.  

---

### Create Power BI Report

#### Option 1: Use Pre-existing Report

- Import a `.pbitx` file if available by navigating to **File > Import > Power BI Template**.  

#### Option 2: Create Report from Scratch

1. Load the transformed data into Power BI.  
2. Build visualizations such as bar charts, line graphs, and tables to analyze revenue trends, market performance, and more.  

---

### Summary

This guide walks you through:  

- Setting up MySQL and Power BI.  
- Importing a database into MySQL.  
- Running SQL queries for data analysis.  
- Connecting Power BI to MySQL and creating visualizations.  