# DESIGNING DATA WAREHOUSE FOR REAL-TIME E-COMMERCE SALES ANALYTICS USING POSTGRESQL

---

# AIM

To design and implement a real-time E-Commerce Sales Analytics Data Warehouse using PostgreSQL command line tools for storing and analyzing sales transactions efficiently.

---

# REQUIREMENTS

## Hardware Requirements

- Processor : Intel i3 / Ryzen 3 or above
- RAM : Minimum 4 GB
- Storage : 10 GB free space

## Software Requirements

- Windows / Linux Operating System
- PostgreSQL
- Command Prompt (CMD)
- SQL Shell (psql)

---

# REAL-TIME APPLICATION

This project is developed for a real-time E-Commerce Sales Analytics system where customer purchases, product transactions, and sales reports are analyzed continuously using PostgreSQL Data Warehouse architecture.

---

# ALGORITHM

## Step 1
Install PostgreSQL software in the system and configure the PostgreSQL server with username, password, and default port settings properly.

## Step 2
Open Command Prompt and access PostgreSQL SQL Shell using the `psql` command to establish database connectivity.

## Step 3
Create a new database named `realtime_dw` for storing real-time warehouse data and analytical transaction records.

## Step 4
Connect to the created database using PostgreSQL command line interface to begin the warehouse implementation process.

## Step 5
Create dimension tables such as customer, product, and time tables to organize descriptive analytical data efficiently.

## Step 6
Create the sales fact table to store real-time transactional information with proper foreign key relationships.

## Step 7
Insert customer information into the customer dimension table for maintaining customer-based analytical records.

## Step 8
Insert product details and pricing information into the product dimension table for product sales analysis.

## Step 9
Insert time-based information into the time dimension table to support monthly and yearly business analytics.

## Step 10
Insert transactional sales records into the fact table by connecting all dimension references together properly.

## Step 11
Execute SQL JOIN queries from the command line interface to generate real-time analytical reports from the warehouse.

## Step 12
Verify the output and confirm the successful implementation of the PostgreSQL real-time data warehouse application.

---

# SETUP PROCEDURE USING CMD

## Step 1 : Open CMD

Press:

```text
Windows + R
```

Type:

```text
cmd
```

---

## Step 2 : Open PostgreSQL SQL Shell

Type:

```text
psql -U postgres
```

Enter password.

---

## Step 3 : Create Database

```sql
CREATE DATABASE realtime_dw;
```

---

## Step 4 : Connect Database

```sql
\c realtime_dw
```

---

# CODE

```sql
-- Create Customer Dimension Table
CREATE TABLE dim_customer (
    customer_id SERIAL PRIMARY KEY,
    customer_name VARCHAR(100),
    city VARCHAR(50),
    country VARCHAR(50)
);

-- Create Product Dimension Table
CREATE TABLE dim_product (
    product_id SERIAL PRIMARY KEY,
    product_name VARCHAR(100),
    category VARCHAR(50),
    price NUMERIC(10,2)
);

-- Create Time Dimension Table
CREATE TABLE dim_time (
    time_id SERIAL PRIMARY KEY,
    order_date DATE,
    month VARCHAR(20),
    year INT
);

-- Create Fact Table
CREATE TABLE fact_sales (
    sales_id SERIAL PRIMARY KEY,
    customer_id INT REFERENCES dim_customer(customer_id),
    product_id INT REFERENCES dim_product(product_id),
    time_id INT REFERENCES dim_time(time_id),
    quantity INT,
    total_amount NUMERIC(10,2)
);

-- Insert Customer Data
INSERT INTO dim_customer(customer_name, city, country)
VALUES
('Arun', 'Chennai', 'India'),
('Kumar', 'Bangalore', 'India');

-- Insert Product Data
INSERT INTO dim_product(product_name, category, price)
VALUES
('Laptop', 'Electronics', 55000),
('Mobile', 'Electronics', 20000);

-- Insert Time Data
INSERT INTO dim_time(order_date, month, year)
VALUES
('2026-05-08', 'May', 2026),
('2026-05-09', 'May', 2026);

-- Insert Sales Data
INSERT INTO fact_sales(customer_id, product_id, time_id, quantity, total_amount)
VALUES
(1, 1, 1, 2, 110000),
(2, 2, 2, 1, 20000);

-- Display Analytical Report
SELECT
    c.customer_name,
    p.product_name,
    t.order_date,
    f.quantity,
    f.total_amount
FROM fact_sales f
JOIN dim_customer c
ON f.customer_id = c.customer_id
JOIN dim_product p
ON f.product_id = p.product_id
JOIN dim_time t
ON f.time_id = t.time_id;
```

---

# OUTPUT

```text
 customer_name | product_name | order_date | quantity | total_amount
---------------+--------------+-------------+----------+--------------
 Arun          | Laptop       | 2026-05-08  |    2     |   110000
 Kumar         | Mobile       | 2026-05-09  |    1     |    20000
```

---

# RESULT

Thus, the real-time E-Commerce Sales Analytics Data Warehouse was successfully designed and implemented using PostgreSQL command line tools. The warehouse system efficiently stored and analyzed transactional sales data for real-time reporting and business analytics.
