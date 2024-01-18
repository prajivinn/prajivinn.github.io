---
layout: post
title: Ecommerce Sales Analysis Using SQL
image: "/posts/OLAP.jpeg"
tags: [EDA, SQL]
---

In this project we perform data analysis using SQL to gain insights into sales patterns and customer behavior.

# Table of contents

- [00. Project Overview](#overview-main)
- [01. Data Overview & Preparation](#data-overview)
- [02. Exploratory Data Analysis](#data-DC)

___

# Project Overview  <a name="overview-main"></a>

This project involves the creation of a sales analysis database, including customer information, product details, employee data, orders, and order details. 

The aim is to gain insights into sales patterns and customer behavior.

___

<br>
# Data Overview & Preparation <a name="data-overview"></a>

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
| 101 |	John | Doe | john.doe@example.com |	USA |
| 102 |	Jane | Smith | jane.smith@example.com |	Canada |
| 103 |	Michael |	Johnson |	michael.johnson@example.com |	USA |
| 104 |	Emily |	Williams | emily.williams@example.com |	UK |
| 105 |	Daniel | Brown | daniel.brown@example.com |	Australia |

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
| 1 |	David | Johnson | Manager | Sales | 2020-01-15 |
| 2 |	Emily |	Williams | Analyst | Marketing | 2021-03-10 |
| 3 |	Daniel | Smith | Developer | IT |	2019-06-20 |
| 4 |	Sarah |	Jones | Analyst |	Marketing |	2022-02-01 |
| 5	| James |	Miller | Developer | IT | 2020-08-12 |

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
| 1 |	Laptop | Electronics | 1000 |
| 2 |	Smartphone | Electronics | 800 |
| 3 |	Chair |	Furniture |	150 |
| 4 |	Tablet | Electronics | 400 |
| 5 |	Desk | Furniture | 250 |

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
| 1 |	101 |	2023-01-15 | 1800.00 | 2 |
| 2 |	102 |	2023-02-10 | 950.00 | 3 |
| 3 |	101 |	2023-03-20 | 450.00 | 1 |
| 4 |	103 |	2023-04-05 | 1200.00 | 4 |
| 5 |	102 |	2023-05-18 | 900.00 | 2 |

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
| 1 |	1 |	1 |	2 |	2000.00 | 2 |
| 2 |	1 |	3 |	1 |	150.00 | 3 |
| 3 |	2 |	2 |	1 |	800.00 | 1 |
| 4 |	3 |	5 |	3 | 600.00 | 4 |
| 5 |	4 |	1 |	1 |	1000.00 | 2 |

<br>

**Data Dictionary**:

* OrderDetailID – order detail ID.
* OrderID – ID of the order.
* ProductID – ID of the product.
* Quantity – Total quantity ordered by the customer.
* Subtotal – represents subtotal for each product.
* EmployeeID – ID of the employee who handled the order of the customer.
