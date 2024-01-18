![image](https://github.com/prajivinn/prajivinn.github.io/assets/108303914/fc4674e9-ea82-4af8-8489-b81a8afa04b8)---
layout: post
title: Dominos Pizza Sales Using SQL
image: "/posts/OLAP.jpeg"
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
| butterscotch_mousse_cake_cke | Butterscotch mousse cake |	Cake
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








