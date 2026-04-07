---
layout: post
title: HR-Analytics
image: "/posts/emp_attrition.jpeg"
tags: [EDA, PowerBI]
---

In this project we perform exploratory data analaysis to identify factors influencing employee attrition and to analyze the effectiveness of training programs.

# Table of contents

- [00. Project Overview](#overview-main)
    - [Context](#overview-context)
    - [Results](#overview-results)
    - [Expected Impact](#overview-ei)
- [01. Concept Overview](#concept-overview)
- [02. Data Overview](#data-overview)
- [03. Dashboard](#data-dashboard)
- [04. Extracting Observations](#data-obs)
- [05. Recommendations Based On Analysis](#data-insights)

___

# Project Overview  <a name="overview-main"></a>

Adviti Pvt.Ltd is experiencing very high employee attrition (~34%), which increases hiring costs, disrupts teams and impacts productivity

### Context <a name="overview-context"></a>

Problem Statement 1: "**Identify Factors Influencing Employee Attrition**"

**Objective**: Determine the factors that contribute to employee attrition within the company and provide insights to reduce attrition rates.

Problem Statement 2: "**Optimize Employee Training Programs**"

**Objective**: Analyze the effectiveness of training programs and recommend improvements to enhance employee skills and performance.


These objectives guide the analysis structure and ensure that insights are aligned with practical business decisions.
<br>
<br>

### Results <a name="overview-results"></a>

As per the observations of the dashboard, below are the factors leading to the attrition of the company:

**Promotion** - Employees who receive promotions are far more likely to stay
**Working Hours** - Dissatisfaction is highest around work-life balance
**Training Hours** - Employees with sufficient training show significantly lower attrition

In order to reduce the attrition rates, I would recommend:

* Identify the employees who are performing well in their roles and reward them with promotions & awards because among the 54 employees who left, 45 were not promoted and in 43 of them had spent more than 3 years in same position. Also, only 9 people received promotions. Additionally, out of the 159 employees who stayed, only 33 were promoted.

* Reduce the working hours to 8 hours per day because out of the 54 employees who left the company, 33 of them (61%) were found to be working for more than average working hours aka 41 hours. It provides a better work life balance for the employees.

As per the analysis of training programs on each department, I would recommend:

* Implement more training hours for the people in IT and Finance departments because the 54 employees who left the company, majority of them are from Finance and second highest is from IT department. Of 28 people from finance, 15 (54%) people left the company. The average training hours for these 15 people is found to be 20, but this average is used to be 23 for the 105 people who have not left the company from finance department. Of 50 people from IT department, 18 (36%) people left the company. The average training hours for these 18 people is found to be is 17, but the average is used to be 20 for the 105 people who have not left the company. This allows employees to build the required skills and helps them feel more confident in their abilities and helps them in performing well and are less likely to leave the company.
<br>
<br>

### Expected Impact <a name="overview-ei"></a>

* Higher engagement and productivity
* Lower rehiring and onboarding costs
* Stronger long-term workforce stability
  
___

# Concept Overview  <a name="concept-overview"></a>


**Early-Tenure Attrition KPIs**


KPI 1: Early-Tenure Attrition Rate (0–2 Years)

Definition: Percentage of employees with ≤2 years of service who exit the organization.

Formula: Leavers with Years_of_Service ≤ 2 ÷ Total employees with Years_of_Service ≤ 2

Why track this: Early tenure is the single largest attrition risk period. A reduction here has the highest impact on overall attrition.

Target direction: Decrease over time



KPI 2: 12-Month Retention Rate

Definition: Percentage of employees who remain employed 12 months after joining.

Why track this: Measures onboarding effectiveness and early employee experience.

Target direction: Increase over time


**Engagement-Related KPIs**


KPI 3: Average Employee Engagement Score

Definition: Average engagement score across all employees.

Why track this: Engagement is the strongest leading indicator of attrition risk.

Target direction: Increase and remain stable


KPI 4: Percentage of Low-Engagement Employees

Definition: Employees with engagement score in the lowest category ÷ total employees.

Why track this: A growing low-engagement population signals future attrition risk.

Target direction: Decrease over time


**Job Satisfaction KPIs**


KPI 5: Overall Job Satisfaction Index

Definition: Average job satisfaction rate across employees.

Why track this: Provides a high-level view of employee experience quality.

Target direction: Increase over time


KPI 6: Management Satisfaction Rate

Definition: Percentage of employees satisfied with management support.

Why track this: Management dissatisfaction shows one of the strongest links to attrition.

Target direction: Increase consistently


KPI 7: Work-Life Balance Satisfaction Rate

Definition: Percentage of employees satisfied with work-life balance.

Why track this: Directly linked to workload stress and burnout.

Target direction: Increase or remain stable


**Training Effectiveness KPIs**

KPI 8: Average Training Hours per Employee

Definition: Total training hours ÷ total employees.

Why track this: Training exposure acts as a retention and engagement lever.

Target direction: Meet or exceed minimum threshold (e.g., 20 hours/year)


KPI 9: Training Coverage Rate

Definition: Percentage of employees receiving ≥20 training hours annually.

Why track this: Ensures training is not limited to a small subset of employees.

Target direction: Increase toward full coverage


**Career Growth & Promotion KPIs**

KPI 10: Promotion Rate

Definition: Employees promoted in a year ÷ total employees.

Why track this: Promotion significantly improves retention and engagement.

Target direction: Increase gradually and consistently


KPI 11: Promotion Rate for Early-Tenure Employees

Definition: Employees with ≤3 years of service who were promoted ÷ total early-tenure employees.

Why track this: Directly addresses early attrition risk.

Target direction: Increase cautiously (quality over quantity)


6. Work Condition & Operational KPIs

KPI 12: Average Commute Distance

Definition: Average distance from work across employees.

Why track this: Long commute distances are strongly associated with attrition.

Target direction: Reduce via remote/hybrid options or location-based hiring


KPI 13: Percentage of Long-Commute Employees

Definition: Employees with commute distance >20 km ÷ total employees.

Why track this: Identifies employees at higher operational attrition risk.

Target direction: Decrease or manage via flexibility policies


**Absenteeism & Performance Context KPIs**


KPI 14: Average Absenteeism Days per Employee

Definition: Total absenteeism days ÷ total employees.

Why track this: Provides context on workload stress and employee well-being.

Target direction: Stable or slightly decreasing (not zero)


KPI 15: Low Performance Employee Ratio

Definition: Employees with lowest performance ratings ÷ total employees.

Why track this: Helps identify skill gaps and training needs early.

Target direction: Decrease through development programs

___

# Data Overview  <a name="data-overview"></a>

A sample of first **5 rows** is shown below

<br>

<iframe width="1090" height="230" frameborder="0" scrolling="no" src="https://1drv.ms/x/c/a8cc30b6e6df073d/IQOrPuKUu3eaR5oN5mS21z96ARzQlbvwZI80feRVs1JGlTs?wdAllowInteractivity=False&Item='Sheet1'!A1%3AN7&wdInConfigurator=True&wdInConfigurator=True"></iframe>

<br>

**Data Dictionary**:

* Employee_ID: Unique identifier for each employee.
* Employee_Name: Name of the employee.
* Age: Age of the employee.
* Gender: Gender of the employee.
* Department: The department in which the employee works (e.g., Sales, Marketing, IT).
* Position: Employee's job position or title.
* Years_of_Service: The number of years the employee has been with the company.
* Salary: Employee's annual salary.
* Performance_Rating: A rating indicating the employee's performance (e.g., on a scale of 1 to 5).
* Work_Hours: The average number of hours worked per week.
* Attrition: Whether the employee has left the company (Yes/No).
* Promotion: Whether the employee has been promoted in the las year (Yes/No).
* Training_Hours: The number of training hours the employee has completed.
* Satisfaction_Score: Employee's satisfaction score (e.g., on a scale of 1 to 5).
* Last_Promotion_Date: Date of the employee's last promotion.


Each row in the dataset represents a unique employee record. Key attributes in the dataset include age, department, position, salary, years of experience, performance rating, training hours, engagment scores, job satisfaction indicators and attrition status

The dataset provides a comprehensive view of the workforce, enabling analysis across multiple dimensions relevant to HR decision-making.

___
<br>
# Dashboard <a name="data-dashboard"></a>

<br>

**Attrition** - Yes

<br>

<img width="1554" alt="yes-blank" src="https://github.com/prajivinn/prajivinn.github.io/assets/108303914/81407959-b152-4628-a8b2-7858bf7813e7">

<br>

**Attrition** - No

<br>

<img width="1553" alt="no-blank" src="https://github.com/prajivinn/prajivinn.github.io/assets/108303914/58bec6e5-78b2-45ff-9200-0a0bee00cd58">

___
<br>

# Extracting Observations <a name="data-obs"></a>

*	There are total of 159 employees and attrition rate is about **34%**.
  
*	On an average, people spend around **5 years** in the company.
  
*	Average salary offered is around **68k** and Overall satisfaction score is **4**.
  
*	Average working and training hours are **41** and **20**.

<br>

**Age Distribution**:

* Of 159 employees, 86 employees are above 30 years, and 73 employees are below 30 years. So, the ratio is almost equal. There is not much difference.

<br>

**Gender Distribution**:

* Out of 159 employees, 54 employees left the company. Of the 54 employees who left most of them are male i.e., 52% but the male to female ratio is almost equal. There is a difference about 2-3%.

<br>

**Promotion vs Years of Experience**:

*	Among the 54 employees who left, 45 were not promoted and in 43 of them had spent more than 3 years in same position. Also, only 9 people received promotions. Additionally, out of the 159 employees who stayed, 33 were promoted. So promotion could be one of the factor which lead them to leave the company.

<br>

**Salary Buckets vs Satisfaction Score**:

*	Employees who left generally had salaries below the average salary of 68k. Out of 54 people, 41% (22 employees) had salaries lower than the company's average. Considering the range of salary group 50-60k, There are 8 people. Out of 8, 6 employees had an overall satisfaction score of 2-3. Considering the stats, we can assume salary could be one of the factor in employee attrition.

<br>

**Attrition by Department**:

*	Of 54 people who left, Majority of them are from IT and Finance Departments.
  
*	Of 28 people from Finance department, 54% of them i.e., 15 people have left the company followed by 36% i.e., 18 people from IT department which is second highest in attrition by department.

<br>

**Attrition By Position**:

*	Of 54 people who left, most of them are from positions such as Data Scientist, Financial Analyst & Software engineer followed by financial & marketing manager as the second highest.
  
*	Of 28 data scientist, 32% (9 people) and of 21 financial analyst, 43% (9 people) and of 22 software engineers, 41% (9 people) and of 7 financial manager, 86% (6 people) and of 11 marketing manager, 55% (6 people) have left the company.

<br>

**Work Hours Distribution**:

*	Out of the 54 employees who left, 33 of them (61%) were found to be working for more than average working hours i.e. 41 hours.
  
*	Employees working  for longer hours can lead to burnout, increased stress levels which affects physical and mental well-being. This makes them to leave the company.
  
*	So work hours could be one of the major contributor to the employee attrition.

<br>

**Training Hours Distribution**:

*	Of 54 employees who left, 44% (24 people) have undergone training less than the average training hours which is 20.
  
*	when training is inadequate, there are chances that employees may feel unprepared for challenges and less confident in their abilities. They may also feel disconnected from their workplace and are less likely to stay with the company.

<br>

**Training Hours vs Satisfaction Score**:

*	Of 54 employees who left, 44% (24 people) have undergone training less than the average training hours which is 20.
  
*	Within this group of 24 people, 11 people took 15 hours training. Out of 11, 6 employees had overall satisfaction score of 2-3.
  
*	Since it is an overall satisfaction score, we can assume the training is not good.

<br>

**Department vs Training Hours**:

*	Within the group of 105 employees who have not left the company, people from Marketing (70%), HR (75%) and Sales (79%) department benefited more from training (based on department % distribution chart) and the average training hours for these departments(Marketing, Sales & HR) are greater ( Sales – 20, Finance - 22, HR - 22) than or equal to the average training hours which is 20.
  
*	Within the group of 54 people who had left the company, majority of them are from finance department. Of 28 people from Finance department, 15 (54%) people left the company. The average training hours for these 15 people is found to be 20, but this average is used to be 23 for the 105 people who have not left the company from finance department.
  
*	Within the group of 54 people who had left the company, second highest are from IT department. Of 50 people from IT department, 18 (36%) people left the company. The average training hours for these 18 people is found to be is 17, but the average is used to be 20 for the 105 people who have not left the company.

<br>

___

## Recommendations Based On Analysis <a name="data-insights"></a>

<br>

As per the observations of the dashboard, below are the factors leading to the attrition of the company:

*	Promotion - Employees who receive promotions are far more likely to stay
*	Working Hours - Dissatisfaction is highest around work-life balance
*	Training Hours - Employees with sufficient training show significantly lower attrition

In order to **reduce the attrition rates**, I would recommend:

*	**Identify the employees who are performing well in their roles and reward them with promotions & awards** because among the 54 employees who left, 45 were not promoted and in 43 of them had spent more than 3 years in same position. Also, only 9 people received promotions. Additionally, out of the 159 employees who stayed, only 33 were promoted.

*	**Reduce the working hours to 8 hours per day** because out of the 54 employees who left the company, 33 of them (61%) were found to be working for more than average working hours aka 41 hours. It provides a better work life balance for the employees.

As per the analysis of training programs on each department, I would recommend:

*	**Implement more training hours for the people in IT and Finance departments** because the 54 employees who left the company, majority of them are from Finance and second highest is from IT department. Of 28 people from finance, 15 (54%) people left the company. The average training hours for these 15 people is found to be 20, but this average is used to be 23 for the 105 people who have not left the company from finance department. Of 50 people from IT department, 18 (36%) people left the company. The average training hours for these 18 people is found to be is 17, but the average is used to be 20 for the 105 people who have not left the company. This allows employees to build the required skills and helps them feel more confident in their abilities and helps them in performing well and are less likely to leave the company.
