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
- [04. Exploratory Data Analysis - Dashboard Creation](#data-DC)
- [05. Predictive Modelling](#data-PM)
    - [Modelling Overview](#PM-overview)
    - [Data Import & Analysis](#PM-DIA)
    - [Exploratory Data Analysis](#PM-EDA)
    - [Logistic Regression](#PM-LR)

___

# Project Overview  <a name="overview-main"></a>

### Context <a name="overview-context"></a>

A fintech company operating in India wants to optimize its loan approval process. They receive a large volume of loan applications daily and want to improve their approval process to reduce the risk of defaults while ensuring fair and timely approval decisions.

* **Data Collection and Preparation**: Start by collecting historical loan application data in an Excel spreadsheet. This data includes information such as applicant details, financial history, loan amounts, interest rates, and whether the loan was approved or not.

* **Data Import to SQL**: Import the Excel data into an SQL database for efficient management and analysis.
  
* **Data Cleaning and Transformation**: Perform data cleaning and transformation in SQL to handle missing values, outliers, and format discrepancies. Ensure that the dataset is well-prepared for analysis.

* **Dashboard Creation in Power BI**: Connect the SQL database to Power BI and create a dashboard that provides real-time insights into the loan application process. Key visualizations should include approval rates, average loan amounts, and applicant demographics.
  
* **Predictive Modeling in Python**: Use Python to build a linear regression model that predicts the likelihood of loan approval based on applicant attributes. This model should help in assessing the creditworthiness of future applicants.
  
* **Recommendations**: Based on the analysis, provide recommendations to the fintech company to improve their loan approval process, such as adjusting approval criteria or interest rates.
  
This project aims to create an end-to-end solution using Excel, SQL, Power BI, and Python, providing valuable insights to help the FinTech company make informed decisions and optimize their loan approval process.

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

<br>

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

We created an *empty_table* named **loan_applications** with specified columns and datatypes to match the columns of the excel dataset while importing it.

Import the *excel dataset* into the SQL database by

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
* We have put *cibil_score* under categories use **CASE** statements because there are different categories defined by government of India like for example cibil score above 690 or 700 is *Excellent* and there are also specified ranges for *Good*, *Fair* and *Low*.
* We created bins/categories for columns such as income_annum, loan_amount, residential_assests_value, commercial_assets_value, luxury_asset_value and bank_asset_value because it will be helpful to view the distributions by categories when creating a dashboard.

<br>

```sql

SELECT * FROM loan_application_details;

```
<br>
Output: A sample of first 5 rows of **21** columns is displayed below
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

| **comm_assets_value** | **comm_assets_group** | **luxury_assets_val** | **luxury_assets_group** | **bank_asset_val** | **bank_asset_group** | **loan_status** |
|---|---|---|---|---|---|---|
| 17600000 | 1.5-2 | 22700000 | 2-2.5 | 8000000 | 0.5-1 | Approved |
| 2200000 | 0-0.5 | 8800000 | 0.5-1 | 3300000 | 0-0.5 | Rejected |
| 4500000 | 0-0.5 | 33300000 | 3-3.5 | 12800000 | 1-1.5 | Rejected |
| 3300000 | 0-0.5 | 23300000 | 2-2.5 | 7900000 | 0.5-1 | Rejected |
| 8200000 | 0.5-1 | 29400000 | 2.5-3 | 5000000 | 0.5-1 | Rejected |

<br>

This cleaned dataset can be used for further analysis.

**Note**:

* For the column **residential_assets_value**, there are negative numbers and zero present in it. **Zero** means no residential assets available and **negative number** means there is already a **home loan** going on.

<br>

#### Finding Approval & Rejection applications and rates

```sql

SELECT *, ROUND((approved_applications/total_applications)*100,2) AS approval_rate
FROM
(SELECT 
	COUNT(*) AS total_applications,
    SUM(CASE WHEN loan_status = 'Approved' THEN 1 ELSE 0 END) AS approved_applications,
    SUM(CASE WHEN loan_status = 'Rejected' THEN 1 ELSE 0 END) AS rejected_applications
FROM loan_application_details) a;

```
<br>
Output:
<br>

| **total_applications** | **approved_applications** | **rejected_applications** | **approval_rate** | **rejection_rate** |
|---|---|---|---|---|
| 4269 | 2656 | 1613 | 62.22 | 37.78 |

<br>

* approval_rate is 62.22%
* rejection_rate is 37.78%

<br>

```sql

SELECT
    'Approved' AS "loan_status/gender",
    SUM(CASE WHEN gender = 'Female' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Female",
    SUM(CASE WHEN gender = 'Male' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Male"
FROM loan_application_details
UNION ALL
SELECT
    'Rejected' AS "loan_status/gender",
    SUM(CASE WHEN gender = 'Female' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Female",
    SUM(CASE WHEN gender = 'Male' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Male"
FROM loan_application_details;

```
<br>
Output:
<br>

| **loan_status/gender** | **Female** | **Male** |
|---|---|---|
| Approved | 1374 | 1282 |
| Rejected | 833 | 780 |

* Majority of the females got approved as well as rejected for loans compared to the males.

<br>

```sql

SELECT
    'Approved' AS "loan_status/education",
    SUM(CASE WHEN education = 'Graduate' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Graduate",
    SUM(CASE WHEN education = 'Not Graduate' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Not Graduate",
    SUM(CASE WHEN education = 'Post Graduate' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Post Graduate"
FROM loan_application_details
UNION ALL
SELECT
    'Rejected' AS "loan_status/education",
    SUM(CASE WHEN education = 'Graduate' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Graduate",
    SUM(CASE WHEN education = 'Not Graduate' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Not Graduate",
    SUM(CASE WHEN education = 'Post Graduate' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Post Graduate"
FROM loan_application_details;

```
<br>
Output:
<br>

| **loan_status/education** | **Graduate** | **Not Graduate** | **Post Graduate** |
|---|---|---|
| Approved | 1288 | 1251 | 117 |
| Rejected | 771 | 621 | 221 |

* Majority of the applicants who did *post graduate* got rejected.
* Majority of the applicants who did *not graduate* has got the loan approved.

<br>

```sql

SELECT
    'Approved' AS "loan_status/self-employed",
    SUM(CASE WHEN self_employed = 'No' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "No",
    SUM(CASE WHEN self_employed = 'Yes' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Yes"
FROM loan_application_details
UNION ALL
SELECT
    'Rejected' AS "loan_status/self-employed",
    SUM(CASE WHEN self_employed = 'No' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "No",
    SUM(CASE WHEN self_employed = 'Yes' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Yes"
FROM loan_application_details;

```
<br>
Output:
<br>

| **loan-status/self-employed** | **No** | **Yes** |
|---|---|---|
| Approved | 1318 | 1338 |
| Rejected | 801 | 812 |

<br>

* The proportion of getting approved or rejected is almost equal aka 50% for the people who are and not self-employed. 

<br>

```sql

SELECT
    'Approved' AS "loan_status/cibil_score",
    SUM(CASE WHEN cibil_score_category = 'Excellent' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Excellent",
    SUM(CASE WHEN cibil_score_category = 'Good' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Good",
    SUM(CASE WHEN cibil_score_category = 'Fair' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Fair",
	SUM(CASE WHEN cibil_score_category = 'Low' AND loan_status = 'Approved' THEN 1 ELSE 0 END) AS "Low"
FROM loan_application_details
UNION ALL
SELECT
    'Rejected' AS "loan_status/cibil_score",
    SUM(CASE WHEN cibil_score_category = 'Excellent' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Excellent",
    SUM(CASE WHEN cibil_score_category = 'Good' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Good",
    SUM(CASE WHEN cibil_score_category = 'Fair' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Fair",
	SUM(CASE WHEN cibil_score_category = 'Low' AND loan_status = 'Rejected' THEN 1 ELSE 0 END) AS "Low"
FROM loan_application_details;

```
<br>
Output:
<br>

| **loan_status/cibil_score** | **Excellent** | **Good** | **Fair** | **Low** |
|---|---|---|---|
| Approved | 1050 | 740 | 681 | 185 |
| Rejected | 6 | 5 | 2 | 1600 |

<br>

* There are 6 applications who have *excellent* cibil_score but still got rejected. 
* Majority of applicants who have *low* cibil_score got rejected but a group of people got approved.

So cibil_score is not the most contributing factor but one of the factor. So we are not still clear what is the driving factor that decides the loan **approval** or **rejection** rate.

___

# Dashboard Creation  <a name="data-DC"></a>

<img width="1459" alt="Screenshot 2024-01-12 183031" src="https://github.com/prajivinn/prajivinn.github.io/assets/108303914/c54c1e10-61fc-4ec2-be3b-374267bed956">

#### Extracting Observations

* Approximately 62.2% of the loans in the dataset are approved( 2656 out of 4,269 ), indicating a slight class imbalance that doesn't require rebalancing.
* Credit scores, particularly in the range of 540-550, serve as a distinct threshold for separating loan statuses.
* The loan_status is highly correlated with credit_scores, but some applicants with high credit scores ( above 740 ) were still rejected, suggesting additional factors influencing loan approval.
* No clear trends were observed between asset values and loan status, indicating that asset values alone might not be strong indicators of loan approval.

**From the above observations, we can infer that credit_score could be one of factor for loan approval or rejection.**

___

# Predictive Modelling  <a name="data-PM"></a>

<br>

### Modelling Overview  <a name="PM-overview"></a>

We will build a model that looks to accurately predict *loan_status*, based upon the customer metrics.

If that can be achieved,...

As we are predicting a binary output, we tested four classification modelling approaches, namely:

* Logistic Regression
* Decision Tree
* Random Forest
* K Nearest Neighbours (KNN)

### Data Import & Analysis <a name="PM-DIA"></a>

<br>

```python

from pymysql import connect
import pandas as pd

import pandas as pd
import numpy as np
from scipy import stats

from sklearn.model_selection import train_test_split
from sklearn.preprocessing import StandardScaler
from sklearn.preprocessing import MinMaxScaler

import matplotlib.pyplot as plt
import seaborn as sns

import scipy.stats as stats
from statsmodels.formula.api import ols
import statsmodels.api as sm

from sklearn.preprocessing import OneHotEncoder
from sklearn.feature_selection import RFECV

from sklearn.linear_model import LogisticRegression
from sklearn.metrics import recall_score, precision_score, f1_score, accuracy_score, confusion_matrix
import sklearn.metrics as metrics
from tabulate import tabulate

import warnings

warnings.filterwarnings("ignore")

database = connect(host = 'localhost', 
                  user = 'root',
                  password = '', 
                  database = 'capstone')

cur = database.cursor()

query = 'SELECT * FROM loan_application_details;'
cur.execute(query)
>> 4269

df = pd.read_sql(query, database)
df.head()

```
<br>
Output: A sample of first 5 rows of **21 columns** is displayed below
<br>
<br>

| **loan_id** | **no_of_dependents** | **gender** | **education** | **self_employed** | **income_annum** | **income_annum_group_lacs** |
|---|---|---|---|---|---|---|
| 1 | 2 | Male | Post Graduate | No | 9600000.0 | 90 Lacs+ |
| 2 | 0 | Male | Post Graduate | Yes | 4100000.0 | 40-50 Lacs |
| 3 | 3 | Male | Post Graduate | No | 9100000.0 | 90 Lacs+ |
| 4 | 3 | Female | Post Graduate | No | 8200000.0 | 80-90 Lacs |
| 5 | 5 | Male | Post Graduate | Yes | 9800000.0 | 90 Lacs+ |

<br>

| **loan_amount** | **loan_amount_group** | **loan_term** | **cibil_score** | **cibil_score_category** | **residential_assets_value** | **residential_assets_value_group** |
|---|---|---|---|---|---|---|
| 29900000.0 | 2.5-3 | 12 | 778 | Excellent | 2400000.0 | 0-0.5 |
| 12200000.0 | 1-1.5 | 8 | 417 | Low | 2700000.0 | 0-0.5 |
| 29700000.0 | 2.5-3 | 20 | 506 | Low | 7100000.0 | 0.5-1 |
| 30700000.0 | 3-3.5 | 8 | 467 | Low | 18200000.0 | 1.5-2 |
| 24200000.0 | 2-2.5 | 20 | 382 |	Low | 12400000.0 | 1-1.5 |

<br>

| **comm_assets_value** | **comm_assets_group** | **luxury_assets_val** | **luxury_assets_group** | **bank_asset_val** | **bank_asset_group** | **loan_status** |
|---|---|---|---|---|---|---|
| 17600000.0 | 1.5-2 | 22700000.0 | 2-2.5 | 8000000.0 | 0.5-1 | Approved |
| 2200000.0 | 0-0.5 | 8800000.0 | 0.5-1 | 3300000.0 | 0-0.5 | Rejected |
| 4500000.0 | 0-0.5 | 33300000.0 | 3-3.5 | 12800000.0 | 1-1.5 | Rejected |
| 3300000.0 | 0-0.5 | 23300000.0 | 2-2.5 | 7900000.0 | 0.5-1 | Rejected |
| 8200000.0 | 0.5-1 | 29400000.0 | 2.5-3 | 5000000.0 | 0.5-1 | Rejected |

<br>

```python

df.info()

```
<br>
Output:
<br>
<br>

| **Column** | **Non-Null Count** | **Dtype** |  
|---|---|---|
| loan_id | 4269 non-null | int64 |  
| no_of_dependents | 4269 non-null | int64 |  
| gender | 4269 non-null | object | 
| education | 4269 non-null | object | 
| self_employed | 4269 non-null | object | 
| income_annum | 4269 non-null | float64 |
| income_annum_group_lacs | 4269 non-null | object | 
| loan_amount | 4269 non-null | float64 |
| loan_amount_group | 4269 non-null | object | 
| loan_term | 4269 non-null | int64 |  
| cibil_score | 4269 non-null | int64 |  
| cibil_score_category | 4269 non-null | object | 
| residential_assets_value | 4269 non-null | float64 |
| residential_assets_value_group | 4269 non-null | object | 
| commercial_assets_value | 4269 non-null | float64 |
| commercial_assets_value_group | 4269 non-null | object | 
| luxury_assets_value | 4269 non-null | float64 |
| luxury_assets_value_group | 4269 non-null | object | 
| bank_asset_value | 4269 non-null | float64 |
| bank_asset_value_group | 4269 non-null | object | 
| loan_status | 4269 non-null | object |

<br>

#### Missing Values

```python

df.isna().sum()

```
<br>
Output:
<br>
<br>

| loan_id | 0 |
| no_of_dependents | 0 |
| gender | 0 |
| education | 0 |
| self_employed | 0 |
| income_annum | 0 |
| income_annum_group_lacs | 0 |
| loan_amount | 0 |
| loan_amount_group | 0 |
| loan_term | 0 |
| cibil_score | 0 |
| cibil_score_category | 0 |
| residential_assets_value | 0 | 
| residential_assets_value_group | 0 |
| commercial_assets_value | 0 |
| commercial_assets_value_group | 0 |
| luxury_assets_value | 0 |
| luxury_assets_value_group | 0 |
| bank_asset_value | 0 |
| bank_asset_value_group | 0 |
| loan_status | 0 |

<br>
There are no null values present in the dataset.

<br>

```python

# Checking shape of the dataset
df.shape
>> (4269,21)

df["loan_status"].value_counts(normalize = True)

```
<br>

| **loan_status** | **value** |
|---|---|
| Approved | 0.62216 |
| Rejected | 0.37784 |

<br>
We see that 62% of customers got their loan approved and 37% got rejected. This tells us that while the data isn’t perfectly balanced at 50:50, it isn’t too imbalanced either. Because of this, and as you will see, we make sure to not rely on classification accuracy alone when assessing results - also analysing Precision, Recall, and F1-Score.

<br>

___

### Exploratory Data Analysis <a name="PI-EDA"></a>

```python

sns.scatterplot(x=df['income_annum'], y= df['loan_amount'], hue=df['loan_status'])
plt.title("Loan Status, Loan Amount, Annual Income")
plt.xlabel("Annual Income")
plt.ylabel("Loan Amount")
plt.show()

```

<br>
![alt text](/img/posts/CP_1.jpg "LR_CP1")

<br>
As annual income rises, there is a tendency for the loan amount requested to increase. Notably, even among applicants with the highest annual incomes, some were approved for the highest loan amounts, while others faced rejections. This suggests that loan approval for a specific loan amount is not solely contingent on annual income.

Let's look at the asset value variables. we will create a subset and get to know the correlation scores between those 4 asset values and other variables.

<br>

```python

loan_asset_variables = df[['residential_assets_value', 'commercial_assets_value',
       'luxury_assets_value', 'bank_asset_value', 'no_of_dependents',
       'income_annum', 'loan_amount', 'loan_term', 'cibil_score']]

loan_asset_variables_corr = loan_asset_variables.corr()

sns.heatmap(loan_asset_variables_corr, annot=True, fmt=".2f", cmap="coolwarm")

```

<br>
![alt text](/img/posts/CP_2.jpg "LR_CP2")

<br>
The asset values exhibit moderate to strong positive linear associations with annual income. Applicants with higher annual incomes tend to have greater purchasing power, particularly when it comes to properties with higher asset values, including luxury assets.

<br>

```python

loan_term = pd.crosstab(index=df['loan_term'], columns=df['loan_status'])
loan_term['Total'] = loan_term['Approved'] + loan_term['Rejected'] 
loan_term['Approved_percentage'] = (loan_term['Approved']/loan_term['Total'])*100
loan_term['Rejected_percentage'] = (loan_term['Rejected']/loan_term['Total'])*100
loan_term

```
<br>
Output:
<br>
<br>

| **loan_term** | **Approved** | **Rejected** | **Total** | **Approved_percentage** | **Rejected_percentage** |
|---|---|---|---|---|---|				
| 2 | 315 | 89 | 404 | 77.970297 | 22.029703 |
| 4 | 366 | 81 | 447 | 81.879195 | 18.120805 |
| 6 | 282 | 208 | 490 | 57.551020 | 42.448980 |
| 8 | 220 | 166 | 386 | 56.994819 | 43.005181 |
| 10 | 229 | 207 | 436 | 52.522936 | 47.477064 |
| 12 | 276 | 180 | 456 | 60.526316 | 39.473684 |
| 14 | 239 | 166 | 405 | 59.012346 | 40.987654 |
| 16 | 236 | 176 | 412 | 57.281553 | 42.718447 |
| 18 | 257 | 165 | 422 | 60.900474 | 39.099526 |
| 20 | 236 | 175 | 411 | 57.420925 | 42.579075 |

<br>
* It's evident that shorter loan terms, such as 4, 6, and 8 years, have significantly higher approval percentages (above 56%) compared to longer terms.
* The 4-year term has the highest approval percentage, at 81.88%, suggesting that customers prefer shorter loan durations, possibly due to reduced interest costs.
* Conversely, longer loan terms like 10, 12, and 14 years have higher rejection percentages, with the 14-year term having the highest at 40.99%.
* This implies that customers are more likely to be rejected for loans with longer durations, possibly due to increased credit risk.
* Despite varying approval and rejection percentages, the total number of applications remains relatively consistent, hovering around 400 to 450 applications for most loan terms.

___

### Logistic Regression <a name="PI-LR"></a>

<br>

```python

df.columns
>> Index(['loan_id', 'no_of_dependents', 'gender', 'education', 'self_employed',
       'income_annum', 'income_annum_group_lacs', 'loan_amount',
       'loan_amount_group', 'loan_term', 'cibil_score', 'cibil_score_category',
       'residential_assets_value', 'residential_assets_value_group',
       'commercial_assets_value', 'commercial_assets_value_group',
       'luxury_assets_value', 'luxury_assets_value_group', 'bank_asset_value',
       'bank_asset_value_group', 'loan_status'],
      dtype='object')

# Removing loan_id 
df_model = df[['no_of_dependents', 'gender', 'education', 'self_employed','income_annum', 'loan_amount',     
               'loan_term', 'cibil_score','residential_assets_value','commercial_assets_value', 
               'luxury_assets_value',  'bank_asset_value', 'loan_status']]

# Label encoding
df_model["loan_status"]= df_model["loan_status"].map({"Approved":1,"Rejected":0})

df_model.info()

```
<br>
Output:
<br>
<br>

| **Column** | **Non-Null Count** | **Dtype** |  
|---|---|---|
| no_of_dependents | 4269 non-null | int64 |  
| gender | 4269 non-null | object | 
| education | 4269 non-null | object | 
| self_employed | 4269 non-null | object | 
| income_annum | 4269 non-null | float64 |
| income_annum_group_lacs | 4269 non-null | object | 
| loan_amount | 4269 non-null | float64 |
| loan_amount_group | 4269 non-null | object | 
| loan_term | 4269 non-null | int64 |  
| cibil_score | 4269 non-null | int64 |  
| cibil_score_category | 4269 non-null | object | 
| residential_assets_value | 4269 non-null | float64 |
| residential_assets_value_group | 4269 non-null | object | 
| commercial_assets_value | 4269 non-null | float64 |
| commercial_assets_value_group | 4269 non-null | object | 
| luxury_assets_value | 4269 non-null | float64 |
| luxury_assets_value_group | 4269 non-null | object | 
| bank_asset_value | 4269 non-null | float64 |
| bank_asset_value_group | 4269 non-null | object | 
| loan_status | 4269 non-null | int64 |

<br>

**Split Out Data For Modelling**

In the next code block we do two things, we firstly split our data into an X object which contains only the predictor variables, and a y object that contains only our dependent variable.

Once we have done this, we split our data into training and test sets to ensure we can fairly validate the accuracy of the predictions on data that was not used in training. In this case, we have allocated 80% of the data for training, and the remaining 20% for validation. We make sure to add in the stratify parameter to ensure that both our training and test sets have the same proportion of customers who got approved and rejected of the loan - meaning we can be more confident in our assessment of predictive performance.

```python

# split data into X and y objects for modelling
X = df_model.drop(["loan_status"], axis = 1)
y = df_model["loan_status"]

# split out training & test sets
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size = 0.2, random_state = 42, stratify = y)

print(X_train.shape)
>> (3415, 12)

print(X_test.shape)
>> (854, 12)

print(y_train.shape)
>> (3415,)

print(y_test.shape)
>> (854,)

```

<br>

**Categorical Predictor Variables**

In our dataset, we have one categorical variable gender which has values of “M” for Male, “F” for Female, and “U” for Unknown.

The Logistic Regression algorithm can’t deal with data in this format as it can’t assign any numerical meaning to it when looking to assess the relationship between the variable and the dependent variable.

As gender doesn’t have any explicit order to it, in other words, Male isn’t higher or lower than Female and vice versa - one appropriate approach is to apply One Hot Encoding to the categorical column.

One Hot Encoding can be thought of as a way to represent categorical variables as binary vectors, in other words, a set of new columns for each categorical value with either a 1 or a 0 saying whether that value is true or not for that observation. These new columns would go into our model as input variables, and the original column is discarded.

We also drop one of the new columns using the parameter drop = “first”. We do this to avoid the dummy variable trap where our newly created encoded columns perfectly predict each other - and we run the risk of breaking the assumption that there is no multicollinearity, a requirement or at least an important consideration for some models, Linear Regression being one of them! Multicollinearity occurs when two or more input variables are highly correlated with each other, it is a scenario we attempt to avoid as in short, while it won’t neccessarily affect the predictive accuracy of our model, it can make it difficult to trust the statistics around how well the model is performing, and how much each input variable is truly having.

In the code, we also make sure to apply fit_transform to the training set, but only transform to the test set. This means the One Hot Encoding logic will learn and apply the “rules” from the training data, but only apply them to the test data. This is important in order to avoid data leakage where the test set learns information about the training data, and means we can’t fully trust model performance metrics!

For ease, after we have applied One Hot Encoding, we turn our training and test objects back into Pandas Dataframes, with the column names applied.

```python

# list of categorical variables that need encoding
categorical_vars = ["gender","education", "self_employed"]

# instantiate OHE class
one_hot_encoder = OneHotEncoder(sparse=False, drop = "first")

# apply OHE
X_train_encoded = one_hot_encoder.fit_transform(X_train[categorical_vars])
X_test_encoded = one_hot_encoder.transform(X_test[categorical_vars])

# extract feature names for encoded columns
encoder_feature_names = one_hot_encoder.get_feature_names_out(categorical_vars)

# turn objects back to pandas dataframe
X_train_encoded = pd.DataFrame(X_train_encoded, columns = encoder_feature_names)
X_train = pd.concat([X_train.reset_index(drop=True), X_train_encoded.reset_index(drop=True)], axis = 1)
X_train.drop(categorical_vars, axis = 1, inplace = True)

X_test_encoded = pd.DataFrame(X_test_encoded, columns = encoder_feature_names)
X_test = pd.concat([X_test.reset_index(drop=True), X_test_encoded.reset_index(drop=True)], axis = 1)
X_test.drop(categorical_vars, axis = 1, inplace = True)

```

<br>

**Feature Scaling**

```python

# create our standardscaler object
scale_stand = StandardScaler()

# normalise the training set (using fit_transform)
X_train = pd.DataFrame(scale_stand.fit_transform(X_train), columns = X_train.columns)

# normalise the test set (using transform only)
X_test = pd.DataFrame(scale_stand.transform(X_test), columns = X_test.columns)

```

<br>

**Feature Selection** 

As we discussed when applying Logistic Regression above - Feature Selection is the process used to select the input variables that are most important to your Machine Learning task. For more information around this, please see that section above.

When applying KNN, Feature Selection is an interesting topic. The algorithm is measuring the distance between data-points across all dimensions, where each dimension is one of our input variables. The algorithm treats each input variable as equally important, there isn’t really a concept of “feature importance” so the spread of data within an unimportant variable could have an effect on judging other data points as either “close” or “far”. If we had a lot of “unimportant” variables in our data, this could create a lot of noise for the algorithm to deal with, and we’d just see poor classification accuracy without really knowing why.

Having a high number of input variables also means the algorithm has to process a lot more information when processing distances between all of the data-points, so any way to reduce dimensionality is important from a computational perspective as well.

For our task here we are again going to apply Recursive Feature Elimination With Cross Validation (RFECV) which is an approach that starts with all input variables, and then iteratively removes those with the weakest relationships with the output variable. RFECV does this using Cross Validation, so splits the data into many “chunks” and iteratively trains & validates models on each “chunk” seperately. This means that each time we assess different models with different variables included, or eliminated, the algorithm also knows how accurate each of those models was. From the suite of model scenarios that are created, the algorithm can determine which provided the best accuracy, and thus can infer the best set of input variables to use!

```python

# instantiate RFECV & the model type to be utilised
clf = LogisticRegression(random_state = 42, max_iter = 1000)
feature_selector = RFECV(clf)

# fit RFECV onto our training & test data
fit = feature_selector.fit(X_train,y_train)

# extract & print the optimal number of features
optimal_feature_count = feature_selector.n_features_
print(f"Optimal number of features: {optimal_feature_count}")
>> Optimal number of features: 3

X_train_features = X_train.loc[:, feature_selector.get_support()]
X_train_features.columns
>> Index(['income_annum', 'loan_amount', 'cibil_score'], dtype='object')

```
<br>
The below code then produces a plot that visualises the cross-validated classification accuracy with each potential number of features
<br>

```python

plt.style.use('seaborn-poster')
plt.plot(range(1, len(fit.cv_results_['mean_test_score']) + 1), fit.cv_results_['mean_test_score'], marker = "o")
plt.ylabel("Classification Accuracy")
plt.xlabel("Number of Features")
plt.title(f"Feature Selection using RFECV \n Optimal number of features is {optimal_feature_count} (at score of {round(max(fit.cv_results_['mean_test_score']),4)})")
plt.tight_layout()
plt.show()

```
<br>
![alt text](/img/posts/CP_3.jpg "LR_CP3")

<br>
This creates the above plot, which shows us that the highest cross-validated classification accuracy (0.9168) is when we include 3 of our  input variables such as *income_annum*, *loan_amount*, *cibil_score*. From the chart we can see that the **difference is not high when we include all the 13 variables** so it is negligible. We will continue on with all the 13 variables!

<br>

**Model Training**

Instantiating and training our Logistic Regression model is done using the below code. We use the random_state parameter to ensure reproducible results, meaning any refinements can be compared to past results. We also specify max_iter = 1000 to allow the solver more attempts at finding an optimal regression line, as the default value of 100 was not enough.

<br>

```python

lr = LogisticRegression(random_state = 42, max_iter = 1000)

# fit our model using our training & test sets
lr.fit(X_train, y_train)

```

<br>

**Model Performance Assessment**:

**Predict On The Test Set**
To assess how well our model is predicting on new data - we use the trained model object (here called clf) and ask it to predict the signup_flag variable for the test set.

In the code below we create one object to hold the binary 1/0 predictions, and another to hold the actual prediction probabilities for the positive class.

<br>

```python

# predict on the test set
y_pred_class = clf.predict(X_test)
y_pred_prob = clf.predict_proba(X_test)[:,1]

```
<br>

**Confusion Matrix**
A Confusion Matrix provides us a visual way to understand how our predictions match up against the actual values for those test set observations.

The below code creates the Confusion Matrix using the confusion_matrix functionality from within scikit-learn and then plots it using matplotlib.

<br>

```python

# create the confusion matrix
conf_matrix = confusion_matrix(y_test, y_pred_class)

# plot the confusion matrix
plt.style.use("seaborn-poster")
plt.matshow(conf_matrix, cmap = "coolwarm")
plt.gca().xaxis.tick_bottom()
plt.title("Confusion Matrix")
plt.ylabel("Actual Class")
plt.xlabel("Predicted Class")
for (i, j), corr_value in np.ndenumerate(conf_matrix):
    plt.text(j, i, corr_value, ha = "center", va = "center", fontsize = 20)

plt.show()

```
<br>
![alt text](/img/posts/CP_4.jpg "LR_CP4")

<br>
The aim is to have a high proportion of observations falling into the top left cell (predicted rejected and actual rejected) and the bottom right cell (predicted approved and actual approved).

Since the proportion of signups in our data was around 30:70 we will next analyse not only Classification Accuracy, but also Precision, Recall, and F1-Score which will help us assess how well our model has performed in reality.

<br>

**Classification Performance Metrics**

**Classification Accuracy**

Classification Accuracy is a metric that tells us of all predicted observations, what proportion did we correctly classify. This is very intuitive, but when dealing with imbalanced classes, can be misleading.

An example of this could be a rare disease. A model with a 98% Classification Accuracy on might appear like a fantastic result, but if our data contained 98% of patients without the disease, and 2% with the disease - then a 98% Classification Accuracy could be obtained simply by predicting that no one has the disease - which wouldn’t be a great model in the real world. Luckily, there are other metrics which can help us!

In this example of the rare disease, we could define Classification Accuracy as of all predicted patients, what proportion did we correctly classify as either having the disease, or not having the disease


**Precision & Recall**

Precision is a metric that tells us of all observations that were predicted as positive, how many actually were positive

Keeping with the rare disease example, Precision would tell us of all patients we predicted to have the disease, how many actually did

Recall is a metric that tells us of all positive observations, how many did we predict as positive

Again, referring to the rare disease example, Recall would tell us of all patients who actually had the disease, how many did we correctly predict

The tricky thing about Precision & Recall is that it is impossible to optimise both - it’s a zero-sum game. If you try to increase Precision, Recall decreases, and vice versa. Sometimes however it will make more sense to try and elevate one of them, in spite of the other. In the case of our rare-disease prediction like we’ve used in our example, perhaps it would be more important to optimise for Recall as we want to classify as many positive cases as possible. In saying this however, we don’t want to just classify every patient as having the disease, as that isn’t a great outcome either!

So - there is one more metric we will discuss & calculate, which is actually a combination of both…


**F1 Score**

F1-Score is a metric that essentially “combines” both Precision & Recall. Technically speaking, it is the harmonic mean of these two metrics. A good, or high, F1-Score comes when there is a balance between Precision & Recall, rather than a disparity between them.

Overall, optimising your model for F1-Score means that you’ll get a model that is working well for both positive & negative classifications rather than skewed towards one or the other. To return to the rare disease predictions, a high F1-Score would mean we’ve got a good balance between successfully predicting the disease when it’s present, and not predicting cases where it’s not present.

Using all of these metrics in combination gives a really good overview of the performance of a classification model, and gives us an understanding of the different scenarios & considerations!


In the code below, we utilise in-built functionality from scikit-learn to calculate these four metrics.

<br>

```python

print('Accuracy:', '%.3f' % accuracy_score(y_test, y_pred_class))
>> Accuracy: 0.917

print('Precision:', '%.3f' % precision_score(y_test, y_pred_class))
>> Precision: 0.921

print('Recall:', '%.3f' % recall_score(y_test, y_pred_class))
>> Recall: 0.947

print('F1 Score:', '%.3f' % f1_score(y_test, y_pred_class))
>> F1 Score: 0.934

```
<br>

The scores in the confusion matrix above mean:

* True negatives (upper left)  : The number of applications that were rejected that the model accurately predicted were rejected.
* False negatives (bottom left): The number of applications that were approved that the model inaccurately predicted were rejected.
* False positives (upper right): The number of applications that were rejected that the model inaccurately predicted were approved.
* True positives (bottom right): The number of applications that were approved that the model accurately predicted were approved.

Since our data is somewhat imbalanced, looking at these metrics rather than just Classification Accuracy on it’s own - is a good idea, and gives us a much better understanding of what our predictions mean! We will use these same metrics when applying other models for this task, and can compare how they stack up.

<br>

```python

# Get feature names (if using a DataFrame)
feature_names = X_train.columns if isinstance(X_train, pd.DataFrame) else np.arange(X_train.shape[1])

# Create a DataFrame to store feature names and their coefficients
feature_importance = pd.DataFrame({'Feature': feature_names, 'Coefficient': clf.coef_[0]})

# Sort by absolute coefficient values in descending order to find the most important features
feature_importance['Absolute_Coefficient'] = np.abs(feature_importance['Coefficient'])
feature_importance = feature_importance.sort_values(by='Absolute_Coefficient', ascending=False)

# Print or visualize the most important features
print(feature_importance)

```
<br>
Output:
<br>
<br>

| **Feature** | **Coefficient** | **Absolute_Coefficient** |
|---|---|---|
| cibil_score | 4.081895 | 4.081895
| income_annum | -1.626722 | 1.626722
| loan_amount | 1.368553 | 1.368553
| loan_term | -0.846972 | 0.846972
| education_Post Graduate | -0.385638 | 0.385638 |
| bank_asset_value | 0.172994 | 0.172994 |
| luxury_assets_value | 0.134816 | 0.134816 |
| commercial_assets_value | 0.068286 | 0.068286 |
| no_of_dependents | -0.064599 | 0.064599 |
| residential_assets_value | 0.035255 | 0.035255 |
| education_Not Graduate | 0.026293 | 0.026293 |
| gender_Male | 0.011976 | 0.011976 |
| self_employed_Yes | 0.006791 | 0.006791 |

<br>

**Finding The Optimal Classification Threshold**

By default, most pre-built classification models & algorithms will just use a 50% probability to discern between a positive class prediction (delivery club signup) and a negative class prediction (delivery club non-signup).

Just because 50% is the default threshold does not mean it is the best one for our task.

Here, we will test many potential classification thresholds, and plot the Precision, Recall & F1-Score, and find an optimal solution!

```python

# set up the list of thresholds to loop through
thresholds = np.arange(0, 1, 0.01)

# create empty lists to append the results to
precision_scores = []
recall_scores = []
f1_scores = []

# loop through each threshold - fit the model - append the results
for threshold in thresholds:
    
    pred_class = (y_pred_prob >= threshold) * 1
    
    precision = precision_score(y_test, pred_class, zero_division = 0)
    precision_scores.append(precision)
    
    recall = recall_score(y_test, pred_class)
    recall_scores.append(recall)
    
    f1 = f1_score(y_test, pred_class)
    f1_scores.append(f1)


# extract the optimal f1-score (and it's index)
max_f1 = max(f1_scores)
max_f1_idx = f1_scores.index(max_f1)


# plot the results
plt.style.use("seaborn-poster")
plt.plot(thresholds, precision_scores, label = "Precision", linestyle = "--")
plt.plot(thresholds, recall_scores, label = "Recall", linestyle = "--")
plt.plot(thresholds, f1_scores, label = "F1", linewidth = 5)
plt.title(f"Finding the Optimal Threshold for Classification Model \n Max F1: {round(max_f1,2)} (Threshold = {round(thresholds[max_f1_idx],2)})")
plt.xlabel("Threshold")
plt.ylabel("Assessment Score")
plt.legend(loc = "lower left")
plt.tight_layout()
plt.show()

```
<br>
![alt text](/img/posts/CP_5.jpg "LR_CP5")

<br>
Along the x-axis of the above plot we have the different classification thresholds that were testing. Along the y-axis we have the performance score for each of our three metrics. As per the legend, we have Precision as a blue dotted line, Recall as an orange dotted line, and F1-Score as a thick green line. You can see the interesting “zero-sum” relationship between Precision & Recall and you can see that the point where Precision & Recall meet is where F1-Score is maximised.

As you can see at the top of the plot, the optimal F1-Score for this model 0.94 and this is obtained at a classification threshold of 0.46. This is higher than the F1-Score of 0.934 that we achieved at the default classification threshold of 0.50!

___

