---
layout: post
title: HR-Analytics
image: "/posts/emp_attrition.jpeg"
tags: [EDA, PowerBI]
---

In this project we perform exploratory data analaysis to identify factors influencing employee attrition and to analyze the effectiveness of training programs.


- [00. Project Overview](#overview-main)
- [01. Data Overview](#data-overview)
- [02. Dashboard](#data-dashboard)
- [03. Extracting Observations](#data-obs)
- [04. Recommendations Based On Analysis](#data-insights)

___

# Project Overview  <a name="overview-main"></a>

Problem Statement 1: "Identify Factors Influencing Employee Attrition"

Objective: Determine the factors that contribute to employee attrition within the company and provide insights to reduce attrition rates.

Problem Statement 2: "Optimize Employee Training Programs"

Objective: Analyze the effectiveness of training programs and recommend improvements to enhance employee skills and performance.

___

# Data Overview  <a name="data-overview"></a>

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

___
<br>
# Dashboard <a name="data-dashboard"></a>

**Attrition** - Yes

![HR_Analytics_Attrition_Yes](https://github.com/prajivinn/Employee_Attrition_PowerBi/assets/108303914/24dc6159-e9e8-46c6-ad44-24f45bdf55ab)

<br>

**Attrition** - No

![HR_Analytics_Attrition_No](https://github.com/prajivinn/Employee_Attrition_PowerBi/assets/108303914/04451d97-5926-4909-b363-8a1de006c5d1)

___
<br>
# Extracting Observations <a name="data-obs"></a>

*	There are total of 159 employees and attrition rate is about **34%**.
  
*	On an average, people spend around **5 years** in the company.
  
*	Average salary offered is around **68k** and Overall satisfaction score is **4**.
  
*	Average working and training hours are **41** and **20**.

**Age Distribution**:

* Of 159 employees, 86 employees are above 30 years, and 73 employees are below 30 years. So, the ratio is almost equal. There is not much difference.

**Gender Distribution**:

* Out of 159 employees, 54 employees left the company. Of the 54 employees who left most of them are male i.e., 52% but the male to female ratio is almost equal. There is a difference about 2-3%.

**Promotion vs Years of Experience**:

*	Among the 54 employees who left, 45 were not promoted and in 43 of them had spent more than 3 years in same position. Also, only 9 people received promotions. Additionally, out of the 159 employees who stayed, 33 were promoted. So promotion could be one of the factor which lead them to leave the company.

**Salary Buckets vs Satisfaction Score**:

*	Employees who left generally had salaries below the average salary of 68k. Out of 54 people, 41% (22 employees) had salaries lower than the company's average. Considering the range of salary group 50-60k, There are 8 people. Out of 8, 6 employees had an overall satisfaction score of 2-3. Considering the stats, we can assume salary could be one of the factor in employee attrition.

**Attrition by Department**:

*	Of 54 people who left, Majority of them are from IT and Finance Departments.
  
*	Of 28 people from Finance department, 54% of them i.e., 15 people have left the company followed by 36% i.e., 18 people from IT department which is second highest in attrition by department.

**Attrition By Position**:

*	Of 54 people who left, most of them are from positions such as Data Scientist, Financial Analyst & Software engineer followed by financial & marketing manager as the second highest.
  
*	Of 28 data scientist, 32% (9 people) and of 21 financial analyst, 43% (9 people) and of 22 software engineers, 41% (9 people) and of 7 financial manager, 86% (6 people) and of 11 marketing manager, 55% (6 people) have left the company.


**Work Hours Distribution**:

*	Out of the 54 employees who left, 33 of them (61%) were found to be working for more than average working hours i.e. 41 hours.
  
*	Employees working  for longer hours can lead to burnout, increased stress levels which affects physical and mental well-being. This makes them to leave the company.
  
*	So work hours could be one of the major contributor to the employee attrition.

**Training Hours Distribution**:

*	Of 54 employees who left, 44% (24 people) have undergone training less than the average training hours which is 20.
  
*	when training is inadequate, there are chances that employees may feel unprepared for challenges and less confident in their abilities. They may also feel disconnected from their workplace and are less likely to stay with the company.

**Training Hours vs Satisfaction Score**:

*	Of 54 employees who left, 44% (24 people) have undergone training less than the average training hours which is 20.
  
*	Within this group of 24 people, 11 people took 15 hours training. Out of 11, 6 employees had overall satisfaction score of 2-3.
  
*	Since it is an overall satisfaction score, we can assume the training is not good. 

**Department vs Training Hours**:

*	Within the group of 105 employees who have not left the company, people from Marketing (70%), HR (75%) and Sales (79%) department benefited more from training (based on department % distribution chart) and the average training hours for these departments(Marketing, Sales & HR) are greater ( Sales – 20, Finance - 22, HR - 22) than or equal to the average training hours which is 20.
  
*	Within the group of 54 people who had left the company, majority of them are from finance department. Of 28 people from Finance department, 15 (54%) people left the company. The average training hours for these 15 people is found to be 20, but this average is used to be 23 for the 105 people who have not left the company from finance department.
  
*	Within the group of 54 people who had left the company, second highest are from IT department. Of 50 people from IT department, 18 (36%) people left the company. The average training hours for these 18 people is found to be is 17, but the average is used to be 20 for the 105 people who have not left the company.

## Recommendations Based On Analysis <a name="data-insights"></a>

As per the observations of the dashboard, below are the factors leading to the attrition of the company:

*	Promotion
*	Working Hours
*	Training Hours

In order to **reduce the attrition rates**, I would recommend:

*	**Identify the employees who are performing well in their roles and reward them with promotions & awards** because among the 54 employees who left, 45 were not promoted and in 43 of them had spent more than 3 years in same position. Also, only 9 people received promotions. Additionally, out of the 159 employees who stayed, only 33 were promoted.

*	**Reduce the working hours to 8 hours per day** because out of the 54 employees who left the company, 33 of them (61%) were found to be working for more than average working hours aka 41 hours. It provides a better work life balance for the employees.

As per the analysis of training programs on each department, I would recommend:

*	**Implement more training hours for the people in IT and Finance departments** because the 54 employees who left the company, majority of them are from Finance and second highest is from IT department. Of 28 people from finance, 15 (54%) people left the company. The average training hours for these 15 people is found to be 20, but this average is used to be 23 for the 105 people who have not left the company from finance department. Of 50 people from IT department, 18 (36%) people left the company. The average training hours for these 18 people is found to be is 17, but the average is used to be 20 for the 105 people who have not left the company. This allows employees to build the required skills and helps them feel more confident in their abilities and helps them in performing well and are less likely to leave the company.
