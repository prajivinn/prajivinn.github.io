---
layout: post
title: Dominos Pizza Sales Using SQL
image: "/posts/dominos.jpeg"
tags: [EDA, SQL]
---

In this project we use SQL manage pizza orders, including selecting pizza types, placing orders, and analyzing order data.

# Table of contents

- [00. Project Overview](#overview-main)
- [01. Data Overview & Preparation](#data-overview)
- [02. Exploratory Data Analysis](#data-EDA)

___

# Project Overview  <a name="overview-main"></a>

The project aimed to enhance Domino's India operations and menu selection. Implement SQL queries to manage pizza orders, including selecting pizza types, placing orders, and analyzing order data.

___

<br>
# Data Overview & Preparation <a name="data-overview"></a>

<br>

## Pizzas Table

```sql

select * from pizzas;

```
<br>
Output: A sample of first 5 rows are displayed
<br>
<br>

| **pizza_id** | **pizza_type_id** | **Size** | **Price** |
|---|---|---|
| achari_do_pyaza_vz_L | achari_do_pyaza_vz |	L |	579 |
| achari_do_pyaza_vz_M | achari_do_pyaza_vz |	M |	349 |
| achari_do_pyaza_vz_R | achari_do_pyaza_vz | R | 189 |
| brownie_fantasy_cke_R |	brownie_fantasy_cke |	R | 125 |
| butterscotch_mousse_cake_cke_R | butterscotch_mousse_cake_cke |	R |	103 |

<br>

**Data Dictionary**:

* Pizza_id – name of the pizza(including size)
* Pizza_type_id – refers to the type of the pizza i.e. veg or non-veg.
* Size – refers to the size of the pizza.
* Price – refers to the price of the pizza.

<br>

## Pizza Types Table

```sql

select * from pizza_types;

```
<br>
Output: A sample of first 5 rows are displayed
<br>
<br>

| **pizza_type_id** |	**Name** | **Category** |
|---|---|---|
| achari_do_pyaza_vz | Achari do pyaza | Veg pizza |
| brownie_fantasy_cke |	Brownie fantasy | Cake |
| butterscotch_mousse_cake_cke | Butterscotch mousse cake |	Cake |
| capsicum_vpm | Capsicum |	Veg pizza mania |
| cheese_dip_dip | Cheese dip | Dip |

<br>

**Data Dictionary**:

* Pizza_type_id – refers to the type of the pizza i.e veg or non-veg
* Name – name of the pizza.
* Category – refers to the category of the pizza.

<br>

## Orders Table

```sql

select * from pizzas;

```
<br>
Output: A sample of first 5 rows are displayed
<br>
<br>

| **order_id** | **date** | **time** |
|---|---|---|
| 1 |	2022-01-01 | 11:38:36 |
| 2 |	2022-01-01 | 11:57:40 |
| 3 |	2022-01-01 | 12:12:28 |
| 4 |	2022-01-01 | 12:16:31 |
| 5 |	2022-01-01 | 12:21:30 |

<br>

**Data Dictionary**:

* order_id – refers to the order ID.
* date – refers to the date of the order placed.
* time – refers to the time of the order placed.

<br>

## Orders Details Table

```sql

select * from order_details;

```
<br>
Output: A sample of first 5 rows are displayed
<br>
<br>

| **order_details_id** | **order_id** | **pizza_id** | **quantity** |
|---|---|---|
| 1 |	1 |	achari_do_pyaza_vz_L | 1 |
| 2 | 2 |	cheese_n_corn_vz_L | 1 |
| 3 |	2 |	deluxe_veggie_vz_L | 1 |
| 4 |	2 |	double_cheese_margherita_vz_L |	1 |
| 5 |	2 |	farm_house_vz_L |	1 |

<br>

**Data Dictionary**:

* order_detail_id – refers to the ID of the order_detail.
* order_id – refers to the ID of the order.
* Pizza_id – name of the pizza(including size)
* Quantity – refers to the quantity of items.

___

<br>
# Explorating Data Analysis  <a name="data-EDA"></a>

<br>

This section represents each of the analysis conducted for answering the business questions, along with the key findings and insights.

<br>

## Daily Customer Count and Peak Hours

<br>

```sql

SELECT
    DATE(date) AS order_date,
    COUNT(DISTINCT order_id) AS total_customers,
    EXTRACT(HOUR FROM time) AS hour_of_day
FROM Orders
GROUP BY order_date, hour_of_day
ORDER BY total_customers DESC;

```
<br>
Output: A sample of **first 10 rows** are displayed
<br>
<br>

| **order_date** | **total_customers** | **hour_of_day** |
|---|---|---|
| 2022-10-15 | 19 | 13 |
| 2022-11-26 | 19 | 19 |
| 2022-10-15 | 18 |	17 |
| 2022-07-24 | 18 |	18 |
| 2022-08-14 | 16 |	13 |
| 2022-06-27 | 16 |	18 |
| 2022-11-26 | 16 |	12 |
| 2022-09-11 | 15	| 17 |
| 2022-04-20 | 15	| 12 |
| 2022-03-05 | 15	| 13 |

<br>

#### Observations

* This query calculates the number of customers each day and identifies peak hours.
* Between 12 to 1 PM ( hour_of_day = 13 ) & 4 to 8 PM ( hour_of_day = 19 ) is the peak where we are getting maximum orders.

<br>

#### Insights

* It can help in understanding daily demand patterns and planning staff schedules accordingly.

<br>

## Average Pizzas per Order and Bestsellers

<br>

```sql

/* Average Pizzas per order */
SELECT AVG(quantity) AS avg_pizzas_per_order
FROM Order_Details;


/* Bestselling pizzas */
SELECT pizza_id, SUM(quantity) AS total_sold
FROM Order_Details
GROUP BY pizza_id
ORDER BY total_sold DESC
LIMIT 5;

```
<br>
Output:
<br>
<br>

| **avg_pizzas_per_order** |
|---|
| 1.0196 |

<br>

| **pizza_id** | **total_sold** |
|---|---|
| double_cheese_margherita_vz_M |	1914 |
| fresh_veggie_vz_L | 1410 |
| deluxe_veggie_vz_L | 1409 |
| fresh_veggie_vz_M	| 1316 |
| cheese_n_corn_vz_L | 1181 | 

<br>

#### Observations

* Average number of pizzas per order is 1 which is essential for inventory management.
* There are 5 best selling pizzas i.e. these pizzas are ordered maximum number of times.

<br>

#### Insights

* Identifying bestselling pizzas allows you to focus on popular items and potentially optimize menu offerings.

<br>

## Monthly Revenue and Seasonality

<br>

```sql

SELECT
    MONTHNAME(date) AS month,
    SUM(Price * quantity) AS revenue
FROM Orders
JOIN Order_Details ON Orders.order_id = Order_Details.order_id
JOIN Pizzas ON Order_Details.pizza_id = Pizzas.pizza_id
GROUP BY month
ORDER BY revenue DESC;

```
<br>
Output:
<br>
<br>

| **month** | **revenue** |
|---|---|
| July | 2084396 |
| May | 2051116 |
| November | 2018098 |
| March | 2012405 |
| January |	1998982 |
| August | 1974430 |
| June | 1947815 |
| April |	1937541 |
| February | 1860372 |
| September | 1828926 |
| December | 1827360 |
| October |	1798995 |

<br>

#### Observations

* It calculates the revenue for each month of the year.
* July month is the highest revenue followed by others. From July-October, The revenue went down.

<br>

#### Insights

* By analyzing monthly revenue, you can identify seasonality in sales and plan promotions or menu changes accordingly.

<br>

## Pizza Sales Analysis

<br>

```sql

SELECT od.pizza_id, SUM(od.quantity) AS totalunitssold, (p.Price * SUM(od.quantity)) AS totalrevenue
FROM order_details od 
INNER JOIN pizzas p 
        ON od.pizza_id = p.pizza_id
GROUP BY od.pizza_id
ORDER BY totalunitssold
;

```
<br>
Output: A sample of **first 5 rows** are displayed
<br>
<br>

| **pizza_id** | **totalunitssold** |	**totalrevenue** |
|---|---|---|
| garlic_breadsticks_brd_R | 28 | 3052 |
| non_veg_supreme_nvz_M |	95 | 58805 |
| keema_do_pyaza_nvz_M | 96 |	43104 |
| non_veg_loaded_nvpm_R |	99 | 13761 |
| chicken_fiesta_nvz_L | 162 | 139158 |

<br>

#### Observations

* This query provides information on the sales of each pizza.
  
<br>

#### Insights

* It can help in identifying underperforming pizzas that may need to be removed from the menu or promoting top sellers.

<br>

##  Average Order Value by Pizza Category

<br>

```sql

WITH table1 AS (
SELECT o.order_id, o.date, od.pizza_id, od.quantity, CASE
  WHEN od.quantity = 4 THEN 4*p.price
  WHEN od.quantity = 3 THEN 3*p.price
  WHEN od.quantity = 2 THEN 2*p.price
ELSE p.price
END AS tprice, p.pizza_type_id, pt.Category
FROM orders o 
INNER JOIN order_details od
        ON o.order_id = od.order_id
INNER JOIN pizzas p
        ON od.pizza_id = p.pizza_id
INNER JOIN pizza_types pt
        ON p.pizza_type_id = pt.pizza_type_id
)

SELECT Category, AVG(tprice) AS Average_Order_Value
FROM table1
GROUP BY Category
ORDER BY Average_Order_Value desc;


```
<br>
Output:
<br>
<br>

| **Category** | **Avg(tprice)** |
|---|---|
| Veg Pizza | 498.8602 |
| Non-Veg pizza | 625.2764 |
| Taco | 131.8228 |
| Cake | 114.9944 |
| Non-Veg pizza mania | 119.7657 |
| More | 99.7226 |
| Bread |	109.0000 |

<br>

#### Observations

* Average amount spent by customers is highest for Non-veg pizzas around 600 followed by 500 for Veg Pizzas.
* Lowest amount is spent for the category “more” items i.e. water, pepsi, ice tea etc.

<br>

#### Insights

* This information can be used for pricing strategies and understanding customer preferences.

<br>

## Sales Trends by Day of the Week

<br>

```sql

SELECT
    DAYNAME(date) AS day_of_week,
    SUM(Price * quantity) AS total_sales
FROM Orders
JOIN Order_Details ON Orders.order_id = Order_Details.order_id
JOIN Pizzas ON Order_Details.pizza_id = Pizzas.pizza_id
GROUP BY day_of_week
ORDER BY total_sales DESC;

```
<br>
Output:
<br>
<br>

| **day_of_week** | **total_sales** |
|---|---|
| Sunday | 3901616 |
| Saturday | 3542902 |
| Monday | 3497633 |
| Thursday | 3273906 |
| Friday | 3236273 |
| Wednesday | 3055545 |
| Tuesday | 2832561 |

<br>

#### Observations

* Maximum revenue is generated on Sunday followed by Saturday and Monday.
* This makes sense that on weekends there will be more people visiting the restaurants and also there might be special discounts/offers on items which can lead to maximum sales.

<br>

#### Insights

* It can help in optimizing marketing efforts and staffing levels on specific days.


















