---
layout: post
title: Impact of Funding and Funding Rounds on Startups Growth
image: "/posts/ab-testing-title-img.png"
tags: [Hypothesis Testing, EDA, Chi-Square, Independent Two Sample T-test, Python]
---

In this project we apply Independent Two Sample T-Test and Chi-Square Test to assess the impact of funding and funding rounds on startups in India.

# Table of contents

- [00. Project Overview](#overview-main)
    - [Context](#overview-context)
    - [Actions](#overview-actions)
    - [Results & Discussion](#overview-results)
- [01. Concept Overview](#concept-overview)
- [02. Data Overview & Preparation](#data-overview)
- [03. Applying Data Clearning & EDA](#data-EDA)
- [04. Applying Two Sample Independent T-Test](#Independent-2Sample-application)
- [05. Applying Chi-Square Test For Independence](#chi-square-application)
- [05. Analysing The Results](#chi-square-results)
- [06. Discussion](#discussion)

___

# Project Overview  <a name="overview-main"></a>

### Context <a name="overview-context"></a>

Company X, a leading Indian online publisher dedicated to startup industry insights, is driven by a mission to empower its audience with actionable knowledge. In the dynamic world of startups, the company recognizes the crucial need to answer a pivotal question: What financial factors differentiate thriving, currently operating startups from those that ultimately cease operations?

This project seeks to address the critical questions of whether there is a statistically significant difference in the mean funds raised by startups that are currently operating compared to those that have ceased operations. Additionally, we aim to investigate whether there exists a significant disparity in the number of funding rounds between currently operating startups and startups that have closed.

<br>
<br>

___

# Concept Overview  <a name="concept-overview"></a>

<br>
#### Hypothesis Testing

Hypothesis refers to a statement or assumption about a population parameter, which is a characteristic of a larger group or population. A Hypothesis Test is used to assess the plausibility, or likelihood of an assumed viewpoint based on sample data - in other words, a it helps us assess whether a certain view we have about some data is likely to be true or not.

The objective of the Hypothesis Testing is to ESTABLISH a specific value for the parameter(s) and perform a statistical TEST to see whether that value is tenable(meaning - defensible or justifiable) in the light of the evidence gathered from the sample.

<br>
**The Null Hypothesis**

Null hypothesis(Ho) - the presumed current status of the matter or status quo. It is a statement assumed to be true if proven otherwise.

In any Hypothesis Test, we start with the Null Hypothesis. The Null Hypothesis is where we state our initial viewpoint, and in statistics, and specifically Hypothesis Testing, our initial viewpoint is always that the result is purely by chance or that there is no relationship or association between two outcomes or groups.

<br>
**The Alternate Hypothesis**

Alternative hypothesis(Ha) - It represents the opposing viewpoint, a specific research hypothesis or a targeted improvement basically something that challenges null hypothesis.

The aim of the Hypothesis Test is to look for evidence to support or reject the Null Hypothesis.  If we reject the Null Hypothesis, that would mean we’d be supporting the Alternate Hypothesis.  The Alternate Hypothesis is essentially the opposite viewpoint to the Null Hypothesis - that the result is *not* by chance, or that there *is* a relationship between two outcomes or groups.

<br>
**What is one tailed test?**

One-Tailed test talks about only one direction. Direction can be "Increase" or "Decrease" but not *both*.

For example, The Research question: Does a new exercise regimen lead to an increase in average running speed?

* Null Hypothesis(H0): The new exercise regimen does not result in an increase in average running speed.
* Alternative hypothesis(Ha): The new exercise regimen leads to a significant increase in average running speed.

<br>
**What is two tailed test?**

Two-Tailed test talks about both directions. This is why it is called Two-tailed t-test

For example, The Research question: Is the average IQ score of a sample *significantly different* from the national average of 100 ?

* Null Hypothesis(H0): The average IQ score of the sample is not significantly different from the national average of 100.
* Alternative Hypothesis(Ha): The average IQ score of the sample is significantly different from the national average of 100.

<br>
**What is Test Statistic**

* A test statisitc is a numerical value calculated from sample data during hypothesis testing
* It serves as a way to quantify the difference between the sample data and the expected values under the null hypothesis
* In Simpler terms, a test statistic helps us decide whether the observed data supports or contradicts the null hypothesis.
* If the test statistic is far from what would be expected under the null hypothesis, it suggests favor towards alternative hypothesis.
* Different types of tests and statistical methods have their own specific test statistics
* For example, in a t-test, the test statistic is the t-value, while in a chi-square test, it’s the chi-square statistic
* The choice of test statistic depends on the nature of the data and the specific hypothesis being tested

<br>
**probabilistic nature of hypothesis testing**

* The very nature of hypothesis testing is that it is probabilistic in nature. We say this because hypothesis testing relies on using a sample of data to make conclusions about an entire population.
* Imagine you’re trying to figure out the average height of all students in a huge school, but its impossible to measure everyone. So you measure a smaller group. your “sample”.
* Now, because you’re working with a sample, your conclusions aren’t 100% certain.
* They’re educated guesses based on probability. Just like you can’t be sure that a coin will land heads up every time you flip it. you can’t be certain about your conclusions in hypothesis testing.
* It’s about making the best guess, knowing that there’s a chance you might not be completely right due to the limited sample you’re using.
* As our conclusions in hypothesis testing are not 100% certain and because of this only there is an element of chance or probability that is involved and we must be extremely careful.
* Sometimes our result may not be right thing and that’s the reason there are errors associated with hypothesis testing.

<br>
**Type I and Type II Error**

As the results/conlusions in hypothesis testing are not 100% certain, there are errors associated with hypothesis testing.

* As previously demonstrated, the process of testing hypothesis is inherently susceptible to errors
* Null Hypothesis: The new drug has no effect on blood pressure.
* Alternate Hypothesis: The new drug lowers blood pressure.
* Type I Error ( false positive ): “ The new drug has no effect on blood pressure, but the study incorrectly concludes that it does”.
* Type II Error ( false negative ): “ The new drug lowers blood pressure, but the study fails to detect this effect “

<br>
**Level of Significance, p-value, critical region**

* **Level of Significance**: Probability of rejecting the null hypothesis when it is true. Let us set it at 5%
* **Acceptance or Rejection Region**: The total area under the distribution curve of the test statistic is partitioned into acceptance and rejection region. Reject the null hypothesis when the test statistic lies in the rejection region, Else we fail to reject it.
* **P-value**: Probability of observing test statistic or more extreme results than the computed test statistic, under the null hypothesis. p-value depends on the value of test statistic.

There are two ways to compare the final answer of hypothesis testing, one way to get the answer is looking at the p-value and the level of significance and other way is to look at the test statistic and the critical value. 

<br>
**Types Of Hypothesis Test**

There are many different types of Hypothesis Tests, each of which is appropriate for use in differing scenarios - depending on a) the type of data that you’re looking to test and b) the question that you’re asking of that data.

In the case of our task here, where we are looking to understand the impact of funding and funding rounds on startups in India - We will utilise the Independence Two sample T-Test and Chi-Square Test For Independence.

<br>
#### Independent Two Sample T-Test

When we want to compare means from 2 samples that are independent, we then use Independent two sample t-test. The assumption of two sample t-test is that the variance of the samples should be same. We need to make sure that this assumption is satisfied and to test this assumption there is a test called levene's test.

<br>
#### Chi-Square Test For Independence

The Chi-Square Test For Independence is a type of Hypothesis Test that assumes observed frequencies for categorical variables will match the expected frequencies.

The *assumption* is the Null Hypothesis, which as discussed above is always the viewpoint that the two groups will be equal.  With the Chi-Square Test For Independence we look to calculate a statistic which, based on the specified Acceptance Criteria will mean we either reject or support this initial assumption.

The *observed frequencies* are the true values that we’ve seen.

The *expected frequencies* are essentially what we would *expect* to see based on all of the data.

___

<br>
# Data Overview & Preparation  <a name="data-overview"></a>

The data set contains information on all the startups in India

In the code below, we:

* Load in the Python libraries we require for importing the data
* Import the required data

<br>

```python

# import library
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns 

%matplotlib inline

# import dataset
startup_df = pd.read_excel(r"/Users/praju/Desktop/Intensive_bootcamp/Statistics_for_Data_Analysis_level_2/Startup_Project/Funding_dataset.xlsx")

startup_df.head()

```

<br>
A sample of this data (the first 5 rows) can be seen below:
<br>
<br>

| **permalink** | **name** |	**homepage_url** |	**category_list** | **funding_total_usd** | **Status** | **Country_Code** | **State_Code** | **Region** | **City** | **Funding_Rounds** | **Founded_At** | **First_Funding_At** | **Last_Funding_At** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| /organization/-fame |	#fame |	http://livfame.com | Media | 10000000.0 | operating | IND | 16.0 | Mumbai | Mumbai | 1 | NaT | 2015-01-05 | 2015-01-05 |
| /organization/21diamonds-india | 21Diamonds | http://www.21diamonds.de | E-Commerce | 6369507.0 | operating | IND | 10.0 | New Delhi | Gurgaon | 1 | 2012-06-01 | 2012-11-15 | 2012-11-15 |
| /organization/247-learning-private | 24x7 Learning | http://www.24x7learning.com | EdTech | Education | Systems | 4000000.0 | operating | IND | 19.0 | Bangalore | Bangalore | 1 | 2001-01-01 | 2007-11-06 | 2007-11-06 |
| /organization/33coupons | 33Coupons | http://33coupons.in | Internet | 20000.0 | operating | IND | 36.0 | Kanpur | Kanpur | 1 | 2015-05-01 |	2015-07-06 | 2015-07-06 |
| /organization/3dsoc | 3DSoC | http://www.3dsoc.com | 3D | Mobile | 2065000.0 | operating | IND | 19.0 | Bangalore |	Bangalore | 2 | 2006-06-01 | 2007-12-01 | 2010-08-01 |

<br>
Data Dictionary:

* Permalink - Refers to the link to the organisation.
* name - Company Name.
* homepage_url - Startup site.
* Category_list - Field of the company.
* Funding_Total_USD - Total fundings in USD.
* Status - Company's status whether it is *operating* or *closed*.
* Country_Code - Refers the code for each country.
* State_Code - State code of the company location.
* Region - Region of the company location.
* City - City of company location.
* Funding_Rounds - Number of funding rounds for each company.
* Founded_At - Refers to the origin of the company.
* First_Funding_At - Refers to the date where first funding took place.
* Last_Funding_At - Refers to the date where last funding took place.

___

<br>
# Applying Data Cleaning & EDA <a name="data-EDA"></a>
