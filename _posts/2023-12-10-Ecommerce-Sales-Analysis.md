---
layout: post
title: Ecommerce Sales Analysis Using SQL
image: "/posts/OLAP.jpeg"
tags: [EDA, SQL]
---

In this project we Perform SQL queries to analyze sales data and answer various business questions.

# Table of contents

- [00. Project Overview](#overview-main)
- [01. Data Overview & Preparation](#data-overview)
- [02. Exploratory Data Analysis](#data-EDA)

___

# Project Overview  <a name="overview-main"></a>

This project involves the creation of a sales analysis database, including customer information, product details, employee data, orders, and order details. 

The aim is to gain insights into sales patterns and customer behavior.

___

<br>
# Data Overview & Preparation <a name="data-overview"></a>

<br>

## Customers Table

<br>

```sql

select * from customers;

```
<br>
Output:
<br>
<br>

| CustomerID | FirstName | LastName | Email | Country |
|---|---|---|---|---|
| 101 |	John | Doe | john.doe@example.com | USA |
| 102 |	Jane | Smith | jane.smith@example.com |	Canada |
| 103 |	Michael | Johnson | michael.johnson@example.com | USA |
| 104 |	Emily |	Williams | emily.williams@example.com |	UK |
| 105 |	Daniel | Brown | daniel.brown@example.com | Australia |

<br>

**Data Dictionary**:

* CustomerID – ID of the customer.
* FirstName - Customer’s first name.
* LastName - Customer’s last name.
* Email – Email ID of the customer.
* Country – Customer’s country of origin.

<br>

## Employees Table

<br>

```sql

select * from employees;

```
<br>
Output:
<br>
<br>

| **EmployeeID** | **FirstName** | **LastName** | **Position** | **Department** | **JoinDate** |
|---|---|---|---|---|---|
| 1 | David | Johnson | Manager | Sales | 2020-01-15 |
| 2 | Emily | Williams | Analyst | Marketing | 2021-03-10 |
| 3 | Daniel | Smith | Developer | IT |	2019-06-20 |
| 4 | Sarah | Jones | Analyst |	Marketing | 2022-02-01 |
| 5 | James | Miller | Developer | IT | 2020-08-12 |

<br>

**Data Dictionary**:

* EmployeeID – ID of the employee.
* FirstName – employee’s first name.
* LastName – employee’s last name.
* Position – employee’s role.
* Department – employee’s department.
* JoinDate – Join date of the employee.

<br>

## Products Table

<br>

```sql

select * from products;

```
<br>
Output:
<br>
<br>

| **ProductID** | **ProductName** | **Category** | **Price** |
|---|---|---|---|
| 1 | Laptop | Electronics | 1000 |
| 2 | Smartphone | Electronics | 800 |
| 3 | Chair | Furniture | 150 |
| 4 | Tablet | Electronics | 400 |
| 5 | Desk | Furniture | 250 |

<br>

**Data Dictionary**:

* ProductID – ID of the product.
* ProductName – product’s name.
* Category – category of the product.
* Price – price of the product.

<br>

## Orders Table

<br>

```sql

select * from orders;

```
<br>
Output: A sample of first 5 rows is displayed below:
<br>
<br>

| **OrderID** |	**CustomerID** | **OrderDate** | **TotalAmount** | **EmployeeID** |
|---|---|---|---|---|
| 1 | 101 | 2023-01-15 | 1800.00 | 2 |
| 2 | 102 | 2023-02-10 | 950.00 | 3 |
| 3 | 101 | 2023-03-20 | 450.00 | 1 |
| 4 | 103 | 2023-04-05 | 1200.00 | 4 |
| 5 | 102 | 2023-05-18 | 900.00 | 2 |

<br>

**Data Dictionary**:

* OrderID – ID of the order.
* CustomerID – ID of the Customer who placed the order.
* OrderDate – the date when the order is placed.
* TotalAmount – total price of the products.
* EmployeeID – ID of the employee who handled the customer’s order.

<br>

## OrderDetails Table

<br>

```sql

select * from orderdetails;

```
<br>
Output: A sample of first 5 rows is displayed below:
<br>
<br>

| **OrderDetailID** | **OrderID** | **ProductID** | **Quantity** | **Subtotal** | **EmployeeID** |
|---|---|---|---|---|---|
| 1 | 1 | 1 | 2 | 2000.00 | 2 |
| 2 | 1 | 3 | 1 | 150.00 | 3 |
| 3 | 2 | 2 | 1 | 800.00 | 1 |
| 4 | 3 | 5 | 3 | 600.00 | 4 |
| 5 | 4 | 1 | 1 | 1000.00 | 2 |

<br>

**Data Dictionary**:

* OrderDetailID – order detail ID.
* OrderID – ID of the order.
* ProductID – ID of the product.
* Quantity – Total quantity ordered by the customer.
* Subtotal – represents subtotal for each product.
* EmployeeID – ID of the employee who handled the order of the customer.

___

<br>
# Explorating Data Analysis  <a name="data-EDA"></a>

<br>

This section represents each of the analysis conducted for answering the business questions, along with the key findings and insights.

<br>

## Total Sales Amount by Customer

<br>

```sql

select c.FirstName, c.LastName, SUM(O.TotalAmount) as Total_Sales
from Orders O 
INNER JOIN customers c
        ON O.CustomerID=c.CustomerID
GROUP BY O.CustomerID;

```
<br>
Output:
<br>
<br>

| **FirstName** | **LastName** | **total_sales** |
|---|---|---|
| John | Doe | 6030.00 |
| Jane | Smith | 4900.00 |
| Michael | Johnson | 3540.00 |
| Emily | Williams | 4350.00 |
| Daniel | Brown | 2820.00 |

<br>

#### Observations

* Highest Purchase is done by John Doe followed by Jane Smith who is the second highest. The increase in the purchase of the products can be due to the ratings and reviews of the products.
* Lowest purchase is done by Daniel brown.

<br>

#### Insights

* Identifying top-performing customers can help tailor marketing and loyalty programs.

<br>

## Orders with Above-Average Total Amount

<br>

```sql

SELECT OrderID, OrderDate, TotalAmount
FROM orders
WHERE TotalAmount > (SELECT avg(TotalAmount) FROM orders)
;

```
<br>
Output:
<br>
<br>

| **OrderID** | **OrderDate** | **TotalAmount** |
|---|---|---|
| 1 | 2023-01-15 | 1800.00 |
| 4 | 2023-04-05 | 1200.00 |
| 8 | 2023-08-05 | 1600.00 |
| 9 | 2023-08-15 | 1100.00 |
| 10 | 2023-08-25 | 1650.00 |
| 14 | 2023-10-15 | 2000.00 |
| 16 | 2023-11-18 | 1200.00 |
| 19 | 2024-01-05 | 1100.00 |
| 20 | 2024-01-18 | 1400.00 |

<br>

#### Observations

* The customers with order ID's such as  1, 4, 5, 8, 9, 10, 14, and 16 have above-average total amounts.
* This can be because of any unexpected needs to purchase extra products during those days rather than their usual pattern or can be due to seasonality trends, where customers purchase more products based on offers provided.

<br>

#### Insights

* Focusing on high-value orders can inform targeted marketing or upselling strategies.

<br>

## Total Quantity and Subtotal by Product 

<br>

```sql

SELECT o.ProductID, p.ProductName, sum(o.Quantity) as Total_Quantity, sum(o.Subtotal) as SubTotal
FROM orderdetails o
INNER JOIN products p 
	ON o.ProductID = p.ProductID
GROUP BY o.ProductID, p.ProductName;

```
<br>
Output:
<br>
<br>

| **ProductID** | **ProductName** | **total_quantity** | **subtotal** |
| 1 | Laptop | 9 | 9000.00 |
| 2 | Smartphone | 6 | 4800.00 |
| 3 | Chair | 6 | 900.00 |
| 4 | Tablet | 7 | 4200.00 |
| 5 | Desk | 6 | 1200.00 |

<br>

#### Observations

* Laptop is the one which has been ordered more compared to the other products while the smartphone, chair and desk are equal in terms of quantity ordered by the customers.
* Laptop (ProductID 1) has the highest total quantity sold (9) and subtotal ($9,000).
* Chair (ProductID 3) has the lowest total quantity sold (6) and subtotal ($900).

<br>

#### Insights

* Understanding product performance is essential for inventory management and marketing decisions.

<br>

## Categorizing Orders by Total Amount 

<br>

```sql

SELECT OrderID, TotalAmount,
CASE 
	WHEN TotalAmount >= 1500 THEN 'High'
    WHEN TotalAmount >= 1000 AND TotalAmount < 1500 THEN 'Medium'
    ELSE 'Low'
END AS Category
FROM orders;

```
<br>
Output:
<br>
<br>

| **OrderID** |	**TotalAmount** | **Category** |
|---|---|---|
| 1 | 1800.00 | High |
| 2 | 950.00 | Low |
| 3 | 450.00 | Low |
| 4 | 1200.00 |	Medium |
| 5 | 900.00 | Low |
| 6 | 700.00 | Low |
| 7 | 850.00 | Low |
| 8 | 1600.00 |	High |
| 9 | 1100.00 |	Medium |
| 10 | 1650.00 | High |
| 11 | 720.00 |	Low | 
| 12 | 980.00 |	Low |
| 13 | 570.00 |	Low |
| 14 | 2000.00 | High |
| 15 | 850.00 |	Low |
| 16 | 1200.00 | Medium |
| 17 | 920.00 |	Low |
| 18 | 700.00 |	Low |
| 19 | 1100.00 | Medium |
| 20 | 1400.00 | Medium |

<br>

#### Observations

* Most of the customer’s total order amount falls under “Low” category. Maybe the price of the products is too high or maybe the customer can’t find the exact product which they are looking for. In this case, we can study the customer’s needs to understand their preferences. As per their preferences, we can arrange the products in different categories so that the customers can easily locate the desired ones.

* There are only 4 orders where the total amount is high. In this case we can keep track of these customers and provide additional discount/offers to these customers.

<br>

#### Insights

* Categorizing orders can help identify trends and segment customers for targeted promotions.

<br>

## Employee Order Ranking

<br>

```sql

SELECT EmployeeID, COUNT(OrderID) as Total_Orders,
  RANK() OVER (ORDER BY COUNT(OrderID) DESC) AS OrderRank
FROM orders
GROUP BY EmployeeID;

```
<br>
Output:
<br>
<br>

| **EmployeeID** | **Total_orders** | **rankemp** |
|---|---|---|
| 2 | 6 | 1 |
| 1 | 5 | 2 |
| 3 | 5 | 2 | 
| 4 | 4 | 4 |

<br>

#### Observations

* Maximum orders are handled by the employee Emily Williams (EmployeeID – 2) followed by David Johnson(EmployeeID - 1)
* Based on the ranking, we can understand which employees are performing well and which are not. We can give them awards for achieving high number of orders.

<br>

#### Insights

* Recognizing high-performing employees can inform recognition and incentive programs.

<br>

## Products Ordered Above Average Quantity

<br>

```sql

WITH avgquant AS (
SELECT ProductID, sum(Quantity) AS total_quantity
FROM OrderDetails
GROUP BY ProductID
)
SELECT o.ProductID, p.ProductName, sum(o.Quantity) AS Total_Quantity
FROM OrderDetails o 
INNER JOIN Products p
        ON o.ProductID=p.ProductID
GROUP BY o.ProductID
HAVING total_quantity > ( SELECT avg(total_quantity) FROM avgquant);

```
<br>
Output:
<br>
<br>

| **ProductName** | **ProductID** | **Total_quantity** |
|---|---|---|
| Laptop | 1 | 9 |
| Tablet | 4 | 7 |

<br>

#### Observations

* Products such as Laptop (ProductID 1) and Tablet (ProductID 4) have above-average sales quantities. This can be due to the reviews and ratings of the products or based on seasonality trends i.e., offers offered on these products.
  
<br>

#### Insights

* Identifying top-selling products can guide inventory and marketing efforts.

<br>

## Customer and Employee Details 

<br>

```sql

SELECT c.FirstName AS CustomerFirstName, c.LastName AS CustomerLastName, e.FirstName AS EmployeeFirstName, e.LastName AS EmployeeLastName
FROM customers c 
INNER JOIN orders o
        ON c.CustomerID = o.CustomerID
INNER JOIN employees e
        ON o.EmployeeID = e.EmployeeID;

```
<br>
Output:
<br>
<br>

| **CustFirstName** | **CustLastName** | **EmpFirstName** | **EmpLastName** | **EmployeeID** |
|---|---|---|---|---|
| John | Doe | Emily | Williams | 2 |
| John | Doe | David | Johnson | 1 |
| John | Doe | Emily | Williams | 2 |
| John | Doe | Daniel |	Smith | 3 |
| John | Doe | Daniel |	Smith | 3 |
| Jane | Smith | Daniel | Smith | 3 |
| Jane | Smith | Emily | Williams | 2 |
| Jane | Smith | Sarah | Jones | 4 |
| Jane | Smith | Emily | Williams | 2 |
| Jane | Smith | Emily | Williams | 2 |
| Michael | Johnson | Sarah | Jones | 4 |
| Michael | Johnson | Daniel | Smith | 3 |
| Michael | Johnson | Sarah | Jones | 4 |
| Michale | Johnson | Sarah | Jones | 4 |
| Emily | Williams | David | Johnson | 1 |
| Emily | Williams | David | Johnson | 1 |
| Emily | Williams | David | Johnson | 1 |
| Daniel | Brown | David | Johnson | 1 |
| Daniel | Brown | Emily | Williams | 2 |
| Daniel | Brown | Daniel | Smith | 3 |

<br>

#### Observations

* Maximum orders are handled by the employee Emily Williams (EmployeeID – 2).
* Provides a linkage between customers, orders, and employees, enabling customer service tracking.

<br>

#### Insights

* Understanding the customer-employee interaction can be valuable for customer satisfaction.

<br>

## Total Quantity Sold and Average Price by Category

<br>

```sql

SELECT p.Category, SUM(o.Quantity) as Total_Quantity, AVG(p.Price) as Average_Price_Per_Category
FROM products p
INNER JOIN orderdetails o
	ON p.ProductID = o.ProductID
GROUP BY p.Category;

```
<br>
Output:
<br>
<br>

| **Category** | **Total_quantity** | **Avg_category** |
|---|---|---|
| Electronics | 22 | 783.333333 |
| Furniture | 12 | 200.000000 |

<br>

#### Observations

* Electronics has the highest quantity sold, followed by Furniture.
* Electronics category also has the highest average price.

#### Insights

* Knowing category performance can inform pricing and marketing strategies.

<br>

## Customers with Above-Average Orders

<br>

```sql

WITH Customer_Orders as (
SELECT CustomerID, COUNT(CustomerID) AS orders
FROM orders
GROUP BY CustomerID)

SELECT o.CustomerID,c.FirstName, c.LastName, COUNT(o.CustomerID) AS orders
FROM orders o 
INNER JOIN customers c
        ON o.CustomerID = c.CustomerID
GROUP BY o.CustomerID
HAVING orders > ( SELECT avg(orders) FROM Customer_Orders);

```
<br>
Output:
<br>
<br>

| **CustomerID** | **FirstName** | **LastName** | **Orders** |
|---|---|---|
| 101 | John | Doe | 5 |
| 102 | Jane | Smith | 5 |

<br>

#### Observations

* John Doe and Jane Smith have placed orders more than the average number of orders which indeed says they are more active in placing orders.

<br>

#### Insights

* Targeting active customers with special offers or loyalty programs can boost sales.




















