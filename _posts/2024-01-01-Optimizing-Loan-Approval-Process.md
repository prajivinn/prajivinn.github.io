---
layout: post
title: Optimizing Loan Approval Process For Fintech Company
image: "/posts/startup-title.jpeg"
tags: [Excel, SQL, PowerBI, Python, Machine Learning]
---

In this project we aim to create an end-to-end solution using Excel, SQL, Power BI, and Python, providing valuable insights to help the FinTech company make informed decisions and optimize their loan approval process.

# Table of contents

- [00. Project Overview](#overview-main)
    - [Context](#overview-context)
    - [Actions](#overview-actions)
    - [Results](#overview-results)
    - [Growth/Next Steps](#overview-growth)
- [01. Concept Overview](#concept-overview)
- [02. Data Overview & Preparation](#data-overview)
- [03. Data Cleaning & Transformation - SQL](#data-DCT)

___

# Project Overview  <a name="overview-main"></a>

### Context <a name="overview-context"></a>

A fintech company operating in India wants to optimize its loan approval process. They receive a large volume of loan applications daily and want to improve their approval process to reduce the risk of defaults while ensuring fair and timely approval decisions.

___

# Concept Overview  <a name="concept-overview"></a>

___

<br>
# Data Overview & Preparation  <a name="data-overview"></a>

This data includes information such as applicant details, financial history, loan amounts, interest rates, and whether the loan was approved or not.

In the code below, we:

* Import the required data in excel

```python

click the column header or use "CTRL+A". The status bar, in the lower-right corner of your Excel window, will tell you the below row count

>> 4269

```
<br>
A sample of this data (the first 5 rows) can be seen below:
<br>
<br>

<iframe width="1090" height="230" frameborder="0" scrolling="no" src="https://1drv.ms/x/c/a8cc30b6e6df073d/IQN599eh_Qx3RrSNkkxYeoTMAcN5fv3dIPMjnlBgXcH7r_U?wdAllowInteractivity=False&Item='Sheet1'!A1%3AN7&wdInConfigurator=True&wdInConfigurator=True"></iframe>


**Data Dictionary**

* loan_id - Loan ID of the applicant.
* no_of_dependents - Number of Dependents for the person.
* gender - Refers to the gender of the person i.e 'male' or 'female'
* education - Refers to the education.
* self_employed - whether the person is self-employed or not.
* income_annum - Refers to the yearly income of the person.
* loan_amount - Refers to the loan amount disbursed.
* loan_term_yrs - Refers to the loan term in years.
* cibil_score - This is a cibil score of the person.
* residential_assets_value - Refers to the price of residential assets such as apartment, villa etc
* commercial_assets_value - Refers to the price of commerical assets such as offices, medical centres, hotels, malls etc
* luxury_assets_value - Refers to the price of luxury assets such as luxury cars or items
* bank_asset_value - Refers how much money is in the bank including bank shares, Fixed deposits etc
* loan_status - Refers to the status of the loan whether it is approved or not.

___

<br>
# Data Cleaning & Transformation - SQL <a name="data-DCT"></a>

We created an *empty_table* named **loan_applications** with specified columns and datatypes to match the columns of the excel dataset.

Importing the *excel dataset* into the SQL database by

* Right click on Tables and select *Table Data Import Wizard*.
* Select the file path and click on "Next".
* Select *Use existing table* because you already created a skeleton of it and click on "Next".
* You can see the column names and values. Just click "Next" again. Data will be imported successfully.

```sql

CREATE TABLE loan_applications (
    loan_id INT PRIMARY KEY,
    no_of_dependents INT,
    education VARCHAR(50),
    gender VARCHAR(10),
    self_employed VARCHAR(10),
    income_annum DECIMAL(10, 2),
    loan_amount DECIMAL(10, 2),
    loan_term INT,
    cibil_score INT,
    residential_assets_value DECIMAL(10, 2),
    commercial_assets_value DECIMAL(10, 2),
    luxury_assets_value DECIMAL(10, 2),
    bank_asset_value DECIMAL(10, 2),
    loan_status VARCHAR(20)
);

# Checking for blank spaces in loan_status column

select loan_status from loan_applications 
where substring(loan_status,1,1)=' ';

```
<br>
Output: A sample of first 5 rows is displayed below
<br>
<br>

| **loan_status** |
|---|
|  Approved |
|  Rejected |
|  Rejected |
|  Rejected |
|  Rejected |

<br>
It seems the column *loan_status* has **leading blank spaces**.

<br>

```sql

select education from loan_applications 
where substring(education,1,1)=' ';

```
<br>
Output: A sample of first 5 rows is displayed below
<br>
<br>

| **education** |
|---|
| Not Graduate |
| Not Graduate |
| Not Graduate |
| Not Graduate |
| Not Graduate |

<br>
The *education* column has **leading blank spaces**.

<br>

```sql

select gender from loan_applications 
where substring(gender,1,1)=' ';

```
<br>
Output: A sample of first 5 rows is displayed below
<br>
<br>

| **gender** |
|---|
| Male |
| Male |
| Male |
| Female |
| Male |

<br>
The column *gender* has **leading blank spaces**.

<br>

```sql

select self_employed from loan_applications 
where substring(self_employed,1,1)=' ';

```
<br>
Output: A sample of first 5 rows is displayed below
<br>
<br>

| **gender** |
|---|
| No |
| Yes |
| No |
| No |
| Yes |

<br>
The column *gender* has **leading blank spaces**.

<br>

```sql

CREATE TABLE loan_application_details 
AS
SELECT 
	loan_id,	 
    no_of_dependents,	
    TRIM(gender) AS gender,	 
    TRIM(education) AS education,	 
    TRIM(self_employed) AS self_employed,	 
    ROUND(income_annum,2) AS income_annum,
	CASE
        WHEN income_annum >= 0 AND income_annum <= 999999 THEN '0-10 Lacs'
        WHEN income_annum >= 1000000 AND income_annum <= 1999999 THEN '10-20 Lacs'
        WHEN income_annum >= 2000000 AND income_annum <= 2999999 THEN '20-30 Lacs'
        WHEN income_annum >= 3000000 AND income_annum <= 3999999 THEN '30-40 Lacs'
        WHEN income_annum >= 4000000 AND income_annum <= 4999999 THEN '40-50 Lacs'
        WHEN income_annum >= 5000000 AND income_annum <= 5999999 THEN '50-60 Lacs'
        WHEN income_annum >= 6000000 AND income_annum <= 6999999 THEN '60-70 Lacs'
        WHEN income_annum >= 7000000 AND income_annum <= 7999999 THEN '70-80 Lacs'
        WHEN income_annum >= 8000000 AND income_annum <= 8999999 THEN '80-90 Lacs'
        WHEN income_annum >= 9000000 AND income_annum <= 9999999 THEN '90 Lacs+'
        ELSE 'Unknown' -- Handle any other cases if necessary
    END AS income_annum_group_lacs,
    ROUND(loan_amount,2) AS loan_amount,
	CASE
        WHEN loan_amount >= 0 AND loan_amount <= 4999999 THEN '0-0.5'
        WHEN loan_amount >= 5000000 AND loan_amount <= 9999999 THEN '0.5-1'
        WHEN loan_amount >= 10000000 AND loan_amount <= 14999999 THEN '1-1.5'
        WHEN loan_amount >= 15000000 AND loan_amount <= 19999999 THEN '1.5-2'
        WHEN loan_amount >= 20000000 AND loan_amount <= 24999999 THEN '2-2.5'
        WHEN loan_amount >= 25000000 AND loan_amount <= 29999999 THEN '2.5-3'
        WHEN loan_amount >= 30000000 AND loan_amount <= 34999999 THEN '3-3.5'
        WHEN loan_amount >= 35000000 AND loan_amount <= 39999999 THEN '3.5+'
        ELSE 'Unknown' -- Handle any other cases if necessary
    END AS loan_amount_group,
    loan_term,	 
    cibil_score,
    CASE
        WHEN cibil_score BETWEEN 300 AND 549 THEN 'Low'
        WHEN cibil_score BETWEEN 550 AND 649 THEN 'Fair'
        WHEN cibil_score BETWEEN 650 AND 749 THEN 'Good'
        WHEN cibil_score BETWEEN 750 AND 900 THEN 'Excellent'
        ELSE 'Unknown' -- Handle any other cases if necessary
    END AS cibil_score_category,
    ROUND(residential_assets_value,2) AS residential_assets_value,
	CASE
		WHEN residential_assets_value < 0 THEN 'negative_value'
        WHEN residential_assets_value = 0 THEN 'zero_value'
        WHEN residential_assets_value >= 1 AND residential_assets_value <= 4999999 THEN '0-0.5'
        WHEN residential_assets_value >= 5000000 AND residential_assets_value <= 9999999 THEN '0.5-1'
        WHEN residential_assets_value >= 10000000 AND residential_assets_value <= 14999999 THEN '1-1.5'
        WHEN residential_assets_value >= 15000000 AND residential_assets_value <= 19999999 THEN '1.5-2'
        WHEN residential_assets_value >= 20000000 AND residential_assets_value <= 24999999 THEN '2-2.5'
        WHEN residential_assets_value >= 25000000 AND residential_assets_value <= 29999999 THEN '2.5-3'
        WHEN residential_assets_value >= 30000000 AND residential_assets_value <= 34999999 THEN '3-3.5'
        WHEN residential_assets_value >= 35000000 AND residential_assets_value <= 39999999 THEN '3.5+'
        ELSE 'Unknown' -- Handle any other cases if necessary
    END AS residential_assets_value_group,
    ROUND(commercial_assets_value,2) AS commercial_assets_value,
	CASE
		WHEN commercial_assets_value < 0 THEN 'negative_Value'
        WHEN commercial_assets_value = 0 THEN 'zero_value'
        WHEN commercial_assets_value >= 1 AND commercial_assets_value <= 4999999 THEN '0-0.5'
        WHEN commercial_assets_value >= 5000000 AND commercial_assets_value <= 9999999 THEN '0.5-1'
        WHEN commercial_assets_value >= 10000000 AND commercial_assets_value <= 14999999 THEN '1-1.5'
        WHEN commercial_assets_value >= 15000000 AND commercial_assets_value <= 19999999 THEN '1.5-2'
        WHEN commercial_assets_value >= 20000000 AND commercial_assets_value <= 24999999 THEN '2-2.5'
        WHEN commercial_assets_value >= 25000000 AND commercial_assets_value <= 29999999 THEN '2.5-3'
        WHEN commercial_assets_value >= 30000000 AND commercial_assets_value <= 34999999 THEN '3-3.5'
        WHEN commercial_assets_value >= 35000000 AND commercial_assets_value <= 39999999 THEN '3.5+'
        ELSE 'Unknown' -- Handle any other cases if necessary
    END AS commercial_assets_value_group,
	ROUND(luxury_assets_value,2) AS luxury_assets_value,
	CASE
		WHEN luxury_assets_value < 0 THEN 'negative_Value'
        WHEN luxury_assets_value = 0 THEN 'zero_value'
        WHEN luxury_assets_value >= 1 AND luxury_assets_value <= 4999999 THEN '0-0.5'
        WHEN luxury_assets_value >= 5000000 AND luxury_assets_value <= 9999999 THEN '0.5-1'
        WHEN luxury_assets_value >= 10000000 AND luxury_assets_value <= 14999999 THEN '1-1.5'
        WHEN luxury_assets_value >= 15000000 AND luxury_assets_value <= 19999999 THEN '1.5-2'
        WHEN luxury_assets_value >= 20000000 AND luxury_assets_value <= 24999999 THEN '2-2.5'
        WHEN luxury_assets_value >= 25000000 AND luxury_assets_value <= 29999999 THEN '2.5-3'
        WHEN luxury_assets_value >= 30000000 AND luxury_assets_value <= 34999999 THEN '3-3.5'
        WHEN luxury_assets_value >= 35000000 AND luxury_assets_value <= 39999999 THEN '3.5+'
        ELSE 'Unknown' -- Handle any other cases if necessary
    END AS luxury_assets_value_group,
	ROUND(bank_asset_value,2) AS bank_asset_value,
	CASE
		WHEN bank_asset_value < 0 THEN 'negative_value'
        WHEN bank_asset_value = 0 THEN 'zero_value'
        WHEN bank_asset_value >= 1 AND bank_asset_value <= 4999999 THEN '0-0.5'
        WHEN bank_asset_value >= 5000000 AND bank_asset_value <= 9999999 THEN '0.5-1'
        WHEN bank_asset_value >= 10000000 AND bank_asset_value <= 14999999 THEN '1-1.5'
        WHEN bank_asset_value >= 15000000 AND bank_asset_value <= 19999999 THEN '1.5-2'
        WHEN bank_asset_value >= 20000000 AND bank_asset_value <= 24999999 THEN '2-2.5'
        WHEN bank_asset_value >= 25000000 AND bank_asset_value <= 29999999 THEN '2.5-3'
        WHEN bank_asset_value >= 30000000 AND bank_asset_value <= 34999999 THEN '3-3.5'
        WHEN bank_asset_value >= 35000000 AND bank_asset_value <= 39999999 THEN '3.5+'
        ELSE 'Unknown' -- Handle any other cases if necessary
    END AS bank_asset_value_group,
    TRIM(loan_status) AS loan_status
FROM loan_applications;

```
<br>

We have created a *new table* called **loan_application_details** which contains no blank values in columns and performed feature engineering on some columns.

* We removed the *leading blank spaces* using **TRIM** command of all the categorical variables such as *gender*, *education*, *self_employed* and *loan_status*.
* We have put *cibil_score* under categories because there are different categories defined by government of India like for example cibil score above 690 or 700 is *Excellent* and there are also specified ranges for *Good*, *Fair* and *Low*.
* We created bins/categories for columns such as *income_annum**, *loan_amount*, *residential_assests_value*, *commercial_assets_value*, *luxury_asset_value* and *bank_asset_value* because it will be helpful to view the distributions by categories when creating a dashboard.

<br>

```sql

SELECT * FROM loan_application_details;

```
<br>
output: A sample of first 5 rows of **21** columns is displayed below
<br>
<br>

| **loan_id** | **no_of_dependents** | **gender** | **education** | **self_employed** | **income_annum** | **income_annum_group_lacs** |
|---|---|---|---|---|---|---|
| 1 | 2 | Male | Post Graduate | No | 9600000 |	90 Lacs+ |
| 2 | 0 | Male | Post Graduate | Yes | 4100000 | 40-50 Lacs |
| 3 | 3 | Male | Post Graduate | No | 9100000 |	90 Lacs+ |
| 4 | 3 | Female | Post Graduate | No | 8200000 | 80-90 Lacs |
| 5 | 5 | Male | Post Graduate | Yes | 9800000 | 90 Lacs+ |
<br>
| **loan_amount** | **loan_amount_group** | **loan_term** | **cibil_score** | **cibil_score_category** | **residential_assets_value** | **residential_assets_value_group** |
|---|---|---|---|---|---|---|
| 29900000 | 2.5-3 | 12 | 778 | Excellent | 2400000 | 0-0.5 |
| 12200000 | 1-1.5 | 8 | 417 | Low | 2700000 | 0-0.5 |
| 29700000 | 2.5-3 | 20 | 506 | Low | 7100000 |	0.5-1 |
| 30700000 | 3-3.5 | 8 | 467 | Low | 18200000 |	1.5-2 |
| 24200000 | 2-2.5 | 20 | 382 |	Low | 12400000 | 1-1.5 |
<br>
| **commercial_assets_value** | **commercial_assets_value_group** | **luxury_assets_value** | **luxury_assets_value_group** | **bank_asset_value** | **bank_asset_value_group** | **loan_status** |
|---|---|---|---|---|---|---|
| 17600000 | 1.5-2 | 22700000 | 2-2.5 | 8000000 | 0.5-1 | Approved |
| 2200000 | 0-0.5 | 8800000 | 0.5-1 | 3300000 | 0-0.5 | Rejected |
| 4500000 | 0-0.5 | 33300000 | 3-3.5 | 12800000 | 1-1.5 | Rejected |
| 3300000 | 0-0.5 | 23300000 | 2-2.5 | 7900000 | 0.5-1 | Rejected |
| 8200000 | 0.5-1 | 29400000 | 2.5-3 | 5000000 | 0.5-1 | Rejected |







