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

* Import the required data in exce.

```sql

-- CHECK THE TABLE
SELECT * FROM loan_applications;

```
<br>
Output:
<br>

| **loan_id** | **no_of_dependents** | **gender** | **education** | **self_employed** | **income_annum** | **loan_amount** | **loan_term_yrs** | **cibil_score** |	 **residential_assets_value** | **commercial_assets_value** | **luxury_assets_value** | **bank_asset_value** | **loan_status** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 1 | 2 | Male | Post Graduate | No | 9600000 | 29900000 | 12 | 778 | 2400000 | 17600000 | 22700000 | 8000000 | Approved |
| 2 |	0 |	Male | Post Graduate | Yes | 4100000 | 12200000 |	8 |	417 |	2700000 |	2200000 |	8800000 | 3300000 | Rejected |
| 3 |	3 |	Male | Post Graduate | No |	9100000 |	29700000 | 20 |	506 |	7100000 |	4500000 | 33300000 | 12800000 | Rejected |
| 4 |	3 |	Female | Post Graduate | No |	8200000 |	30700000 | 8 | 467 | 18200000 |	3300000 | 23300000 | 7900000 | Rejected |
| 5 |	5 |	Male | Post Graduate | Yes |	9800000 |	24200000 | 20 |	382 | 12400000 | 8200000 | 29400000 | 5000000 | Rejected |

