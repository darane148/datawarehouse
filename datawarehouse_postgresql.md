# DESIGNING DATA WAREHOUSE FOR REAL-TIME E-COMMERCE SALES ANALYTICS USING POSTGRESQL

---

# AIM

To design and implement a real-time E-Commerce Sales Analytics Data Warehouse using PostgreSQL for storing, processing, and analyzing transactional sales data efficiently.

---

# REQUIREMENTS

## Hardware Requirements

- Processor : Intel i3 / Ryzen 3 or above
- RAM : Minimum 4 GB
- Storage : 10 GB free space

## Software Requirements

- Operating System : Windows / Linux
- PostgreSQL
- pgAdmin 4
- SQL Shell (psql)

---

# REAL-TIME APPLICATION

This project is designed for a real-time E-Commerce Sales Analytics application where customer orders, product details, and transaction data are continuously collected and analyzed for business reporting and decision-making.

Examples:
- Amazon Sales Analysis
- Flipkart Product Analytics
- Online Order Monitoring
- Customer Purchase Tracking

---

# ALGORITHM

## Step 1
Install PostgreSQL and pgAdmin software on the system to create and manage the database environment required for the data warehouse application.

## Step 2
Open pgAdmin and create a new database named `realtime_dw` for storing the warehouse data and analytical information.

## Step 3
Design dimension tables such as customer, product, and time tables to store descriptive and categorized information separately.

## Step 4
Create the fact table named `fact_sales` to store transactional sales records along with foreign key relationships.

## Step 5
Define primary keys and foreign keys properly to maintain data integrity and establish relationships between tables.

## Step 6
Insert sample customer information into the customer dimension table for maintaining customer-related analytical data.

## Step 7
Insert product details such as product name, category, and price into the product dimension table for product analytics.

## Step 8
Store date and time information inside the time dimension table to perform monthly and yearly sales analysis efficiently.

## Step 9
Insert transactional sales data into the fact table by connecting customer, product, and time dimension references together.

## Step 10
Execute SQL analytical queries using JOIN operations to retrieve meaningful reports from the warehouse environment.

## Step 11
Analyze the generated output to understand customer purchases, product performance, and total sales generated in real time.

## Step 12
Verify the successful implementation of the real-time data warehouse system using PostgreSQL analytical queries and reporting.

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

-- Create Sales Fact Table
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

-- Analytical Query
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

| customer_name | product_name | order_date | quantity | total_amount |
|----------------|--------------|-------------|------------|---------------|
| Arun | Laptop | 2026-05-08 | 2 | 110000 |
| Kumar | Mobile | 2026-05-09 | 1 | 20000 |

---

# RESULT

Thus, the real-time E-Commerce Sales Analytics Data Warehouse was successfully designed and implemented using PostgreSQL. The warehouse system efficiently stored and analyzed customer, product, and transactional sales data for real-time business reporting and analytics.
