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
- [03. Data Cleaning & Transformation](#data-DCT)

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
# Data Cleaning & Transformation <a name="data-DCT"></a>

Importing the *excel dataset* into the SQL database

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


