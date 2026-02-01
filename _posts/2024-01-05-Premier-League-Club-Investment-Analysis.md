---
layout: post
title: Premier League Club Investment Analysis using EDA
image: "/posts/EPL.png"
tags: [Data Cleaning, EDA, Python]
---

In this project we apply EDA (Exploratory Data Analysis) to suggest a club for the management firm to invest!

# Table of contents

- [00. Project Overview](#overview-main)
    - [Context](#overview-context)
    - [Actions](#overview-actions)
    - [Results](#overview-results)
    - [Growth/Next Steps](#overview-growth)
- [01. Concept Overview](#concept-overview)
- [02. Data Overview & Preparation](#data-overview)
- [03. Applying Data Cleaning & EDA](#DC-EDA-application)
    - [Data Cleaning](#DC-context)
    - [Exploratory Data Analysis](#EDA-context)
- [04. Analysing The Results](#Club-results)
- [05. Growth & Next Steps](#growth-next-steps)

___

# Project Overview  <a name="overview-main"></a>

### Context <a name="overview-context"></a>

An investment company aims to invest in one of the top-performing club in the English Premier League. To aid in their decision-making process, the analytics department has been tasked with creating a comprehensive report on the performance of various clubs. However, some of the more established clubs have already been owned by the competitors. As a result, Company ABC wishes to identify the clubs they can approach and potentially invest to ensure a successful and profitable deal.
<br>
<br>
### Actions <a name="overview-actions"></a>

We collected the data of all the clubs from premierleague.com 

We undertook data cleaning on the dataset to replace null values as well as dealing with incorrect data on the columns.

We performed EDA on the data starting from identification of outliers using .describe method in each column with respect to the measures of dispersion i.e using Mean and Median. As per the project requirements, the more **established clubs** meaning clubs with high experience have already been owned by the competitors. Using Histogram, we identifed and removed those most established clubs( established clubs = higher experience/ high number of matches played) becasue it will skew our results in finding the potential club.

Since it is a cumulative data, It is essential to understand that the values in all the columns represent the cumulative scores over all the "matches played" . So we normalized the data by dividing the no. of wins, loss, drawn, clean sheet, goals by the number of matches played column.

With the help of box plot, we plotted the winning rate, loss rate, drawn rate, clean sheet rate. By visualizing it, we found **outliers** in Winning rate column. It is safe to say that these **outlier clubs** have exceptionally higher winning rate which can be a potential club to look on further. We also found the club with **least winning rate** so that we don't want to provide wrong suggestions to the client at the end of analysis.

A potential club can be a club with a **high winning rate** ( or ) a club with **high winning rate & high drawn rate** meaning the club/team is able to stand up strong & ensure not loosing. They are winning or they are making sure its a "Draw". Also a Club/team with **low Loss rate and high drawn rate** is a good combination. Following, we identified the clubs with high winning rate, low winning rate, high drawn rate and also the clubs who are currently playing in the premier league(2023).

Based on a recommendation framework, We created a **score** column which gives weightage/points to each club upto a total of 100 points per club. We gave more weightage/points to clubs who has/is:

* High Winning Rate
* Won the premier league
* Currently playing in the premier league 2023

Finally with the help of Bar Chart, we plotted the clubs with their respective "Scores".
<br>
<br>

### Results <a name="overview-results"></a>

The club which has highest score is **Leicester City**. Given this information, we recommend that stakeholders consider investing in Leicester City instead. We believe that Leicester City’s recent form and performance make them a better choice for investment.

**To support our claim, we conducted further secondary research to provide additional evidence of Leicester City’s current form and potential for success**
<br>
<br>
### Growth/Next Steps <a name="overview-growth"></a>

Since it is an investment decision, the **Price** would need to be in the equation too.  

We could discuss with client about their budget. Based on their budget, we could filter the teams. 

From the data point of view, we can try to collect each team's **price/value** to ensure that we have as much useful information available in making the final decision.

___

# Concept Overview  <a name="concept-overview"></a>

<br>
#### Data Cleaning 

Data cleaning is the process of identifying and correcting or removing errors, inconsistencies, and inaccuracies in a dataset.
There is a concept called GIGO(Garbage In Garbage Out) states that flawed or non-sense input data produces non-sense output.
So it is always important to make sure that the data is clean.

<br>
**Removal of Duplicate or Irrelevant Observations**

Remove unwanted observations from your dataset, including duplicate observations or irrelevant observations. Duplicate observations will happen most often during data collection. When you combine data sets from multiple places, scrape data, or receive data from clients or multiple departments, there are opportunities to create duplicate data. De-duplication is one of the largest areas to be considered in this process. Irrelevant observations are when you notice observations that do not fit into the specific problem you are trying to analyze.

For example, if you want to analyze data regarding millennial customers, but your dataset includes older generations, you might remove those irrelevant observations. This can make analysis more efficient, minimize distraction from your primary target, and create a more manageable and performable dataset.

<br>
**Fix structural errors**

Structural errors are when you measure or transfer data and notice strange naming conventions, typos, or incorrect capitalization. These inconsistencies can cause mislabeled categories or classes. For example, you may find "N/A" and "Not Applicable" in any sheet, but they should be analyzed in the same category.

<br>
**Filter unwanted outliers**

Often, there will be one-off observations where, at a glance, they do not appear to fit within the data you are analyzing. If you have a legitimate reason to remove an outlier, like improper data entry, doing so will help the performance of the data you are working with.

However, sometimes, the appearance of an outlier will prove a theory you are working on. And just because an outlier exists doesn't mean it is incorrect. This step is needed to determine the validity of that number. If an outlier proves to be irrelevant for analysis or is a mistake, consider removing it.

<br>
**Handling missing data**

You can't ignore missing data because many algorithms will not accept missing values. There are a couple of ways to deal with missing data. Neither is optimal, but both can be considered, such as:

* You can drop observations with missing values, but this will drop or lose information. If you can obtain more records then it's fine, if not be careful before removing it.
* You can input missing values based on other observations; again, there is an opportunity to lose the integrity of the data because you may be operating from assumptions and not actual observations.
* You might alter how the data is used to navigate null values effectively.

<br>

#### Exploratory Data Analysis

Exploratory Data Analysis (EDA) is the process of examining and visualizing a dataset to understand its main characteristics, such as the distribution of data, the relationships between variables, and any anomalies or patterns that may exist. The goal of EDA is to uncover insights and trends that can help inform further analysis or decision-making. It is often the first step in any data analysis project, as it provides a foundation for more advanced statistical methods and models.

<br>
**Why Plots/Charts?**

When you create a frequency(counts) table of data, it will be difficult sometimes to pick insights from the table. That's why we create plots or charts for better Understanding.

<br>
**Bar Chart**

* Bar Chart is one of the most commonly used charts to represent data in an effective and easy manner. 
* It is used when there are both categorical variables and numerical variables in the data. We use it when we want to see the aggregate measures of the numerical variable with respect to different categories.
* Bar Charts gives the visualized comparison between the discrete categories. It is a really effective chart where the categories in the data are less. Bar Chart can both be vertical and horizontal. In python, the matplotlib API provides the bar() function which helps in creating bar charts. It comes under univariate analysis.

<br>
**Histogram**

* Histogram is a chart we commonly use to see the distribution of data in specified ranges as bins. It is similar to a bar chart but condenses the data into logical ranges or bins thereby making it more interpretable. It is only really effective if the data points are not too many.
* In Python , the matplotlib library offers a hist() function using which we can make histograms. Thus, all in all we use histograms when data is big and we want to condense it into groups to see the data count of each group.

<br>
**Box Plot**

* A box plot or a whisker plot is a chart very commonly created in Data Analysis to display the summary of the data values. 
* Box plots divide the data into sections each containing approximately 25% of the data and give a five parameter summary like minimum, 1st quartile, median(2nd quartile), 3rd quartile, maximum.
* It is also used for detecting outliers in data points of numerical variables.

___

<br>
# Data Overview & Preparation  <a name="data-overview"></a>

The data set contains information on all the clubs so far participated in all the premier league tournaments starting from 1992-2022.

In the code below, we:

* Load in the Python libraries we require for importing the data
* Import the required data

<br>

```python

# Import Libraries for data cleaning & data analysis
import numpy as np 
import pandas as pd

# import dataset
df = pd.read_csv(r'/Users/Praju/Desktop/DADUO/did by me/Premier_League_Final_Data_batch2.csv')
df.head()

```

<br>
A sample of this data (the first 5 rows) can be seen below:
<br>
<br>

| **Club** | **Matches Played** |	**Win** |	**Loss** | **Drawn** | **Goals** | **Clean Sheets** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** |
|---|---|---|---|---|---|---|---|---|---|---|
| 1Arsenal | 1182 | 642 |	252 |	288 |	2089 |	448 |	1886 |	3.0 |	6 |	Apr-23 |
| 2Aston Villa | 1062 |	368 |	399 |	295 |	1306 | 311 |	1874 |	0.0 |	1 |	Apr-23 |
| 3Birmingham City |	266 |	73 |	111 |	82 |	273 |	66 |	1875 |	0.0 |	NaN |	May-11 |
| 4Blackburn Rovers |	696 |	262 |	250 |	184 |	927 |	210 |	1875 |	1.0 |	1 |	May-12 |
| 5Bolton Wanderers |	494 |	149 |	217 |	128 |	575 |	108 |	1874 |	0.0 |	0 |	May-12 |

<br>
Data Dictionary:

* Club: Name of the football club
* Matches: Number of matches the club has played in the Premier League
* Wins: Number of matches won by the club in the Premier League
* Loss: Number of matches lost by the club in the Premier League
* Draws: Number of matches drawn by the club in the Premier League
* Goals: Number of goals scored by each club in the Premier League
* Clean Sheets: Number of matches in which the club has prevented the opposing side from scoring
* Team Launch: Year in which the club was founded
* Winners: Number of times the club has won the Premier League
* Runners-up: Number of times the club has finished as runners-up in the Premier League
* lastplayed_pl: Year in which the team last played in the Premier League

___

<br>
# Applying Data Cleaning & EDA <a name="DC-EDA-application"></a>

### Data Cleaning <a name="DC-context"></a>

Checking the data if there are any null values/typos in it.

```python

# Analyzing first and last 5 rows of the data

df.head()
df.tail()

```
<br>
Output:
<br>
<br>

| **Club** | **Matches Played** |	**Win** |	**Loss** | **Drawn** | **Goals** | **Clean Sheets** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** |
|---|---|---|---|---|---|---|---|---|---|---|
| 1Arsenal | 1182 | 642 |	252 |	288 |	2089 |	448 |	1886 |	3.0 |	6 |	Apr-23 |
| 2Aston Villa | 1062 |	368 |	399 |	295 |	1306 | 311 |	1874 |	0.0 |	1 |	Apr-23 |
| 3Birmingham City |	266 |	73 |	111 |	82 |	273 |	66 |	1875 |	0.0 |	NaN |	May-11 |
| 4Blackburn Rovers |	696 |	262 |	250 |	184 |	927 |	210 |	1875 |	1.0 |	1 |	May-12 |
| 5Bolton Wanderers |	494 |	149 |	217 |	128 |	575 |	108 |	1874 |	0.0 |	0 |	May-12 |


| **Club** | **Matches Played** |	**Win** |	**Loss** | **Drawn** | **Goals** | **Clean Sheets** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** |
|---|---|---|---|---|---|---|---|---|---|---|
| 36West Bromwich Albion | 494 | 117 | 238 | 139 | 510 | 107 | 1878 | NaN |	0 |	Apr-18 |
| 37West Ham United | 1025 | 343 | 423 | 259 | 1262 | 266 | 1895 | NaN | 0 | Apr-23 |
| 38Wigan Athletic | 304 | 85 | 143 | 76 | 316 | 73 | 1932 | NaN | 0 | Apr-13 |
| 39Wolverhampton Wanderers | 334 |	98 | 151 | 85 |	353 | 75 | 1877 | 0.0 | 0 | Apr-23 |
| 40Portsmouth | 266 | 79 | 122 | 65 | 292 | 61 | April 1898 |	NaN | NaN |	Apr-10 |

<br>
* Upon examining the dataset, we note that it consists of 11 columns, with the first column containing the club name and the remaining 10 columns providing information on the club's performance in the Premier League. However, the data is not entirely clean. The club column has numerical values attached to it, likely indicating a serial number.
* We notice inconsistencies in the TeamLaunch column. While most clubs have a year mentioned, one club has a month & year mentioned instead. This inconsistency may cause problems in the analysis, and the column should be cleaned. Furthermore, we observe that there are null values in the Winners & Runners-up column.

<br>
#### Checking Info of the Dataset

```python

df.info()

```
<br>
Output:
<br>
<br>

| **Column** | **Non-Null Count** | **Dtype** |  
|---|---|---|
| Club | 40 non-null | object | 
| Matches Played | 40 non-null | int64 |  
| Win | 40 non-null | int64 |  
| Loss | 40 non-null | int64 |  
| Drawn | 40 non-null | int64 |  
| Goals | 40 non-null | int64 |  
| Clean Sheets | 40 non-null | int64 |  
| TeamLaunch | 40 non-null | object | 
| Winners | 25 non-null | float64 |
| Runners-up | 22 non-null | object | 
| lastplayed_pl | 40 non-null | object | 

<br>
* There are 40 non-null values in each column, indicating that there are no missing values. However, there are null values in the 'Winners' and 'Runners-up' columns as observed earlier. 
* We also notice that the data type for the "Runners-up" column is non-numeric (i.e., object type). To perform any numerical analysis on this column, we will need to convert it to a numeric data type.

<br>
#### Club Column Cleaning

```python

# Let us first start with Club column

df['Club']=df['Club'].str.replace('\d+','')

# In this code, '\d+' is a regular expression pattern that matches one or more digits at the start of the string. 
# The str.replace() method replaces this pattern with an empty string, 
# effectively removing the numbers from the front of each team name in the "Club" column. 

df.head()

```
<br>
Output of first 5 rows:
<br>
<br>

| **Club** | **Matches Played** |	**Win** |	**Loss** | **Drawn** | **Goals** | **Clean Sheets** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** |
|---|---|---|---|---|---|---|---|---|---|---|
| Arsenal | 1182 | 642 | 252 | 288 | 2089 | 448 | 1886 | 3.0 | 6 | Apr-23 |
| Aston Villa | 1062 | 368 | 399 | 295 | 1306 | 311 | 1874 | 0.0 | 1 | Apr-23 |
| Birmingham City |	266 | 73 | 111 | 82 | 273 |	66 | 1875 |	0.0 | NaN |	May-11 |
| Blackburn Rovers | 696 | 262 | 250 | 184 | 927 | 210 | 1875 |	1.0 | 1 | May-12 |
| Bolton Wanderers | 494 | 149 | 217 | 128 | 575 | 108 | 1874 |	0.0 | 0 | May-12 |

<br>
Removed the numbers from the 'Club' Column.

<br>
#### Winner Column Cleaning

```python

# Next, let us look at "Winners" column. Check if there is null value in a alternative way

df["Winners"].isnull().any()
>> True

# In this code, the isnull() method is called on the "Winners" column of the DataFrame.
# isnull() returns a boolean Series where each element indicates whether the corresponding value in the column is null (True) or not (False). 
# The any() method is then used to check if there is at least one True value in the Series, indicating the presence of null values in the "Winners" column.

```

<br>
#### Frequency of Winners

```python

df['Winners'].value_counts()
# The code returns the count of unique values in the "Winners" column and the number of times each value occurs.

```

<br>
Output:
<br>
<br>

| **Winner** | **Count** |
|---|---|
| 0.0 | 18 |
| 1.0 | 3 |
| 3.0 | 1 |
| 13.0 | 1 |
| 5.0 | 1 |
| 6.0 | 1 |

<br>
Upon inspecting the dataset, it can be observed that there are a total of **25 non-null values** in **Winner** column. Furthermore, it is noteworthy that out of the 18 football clubs listed, none of them have won the Premier League title, as the "Winners" column displays a count of 0 for each club. 

After looking at the counts, **it has been determined that there have been a total of 30 English Premier League tournaments held in the past (1992-2022 per year one tournament)**. Out of the 25 football clubs (Non zero non nulls in winner columns) listed in the dataset, 3 clubs have won the Premier League title once, 1 club has won it thrice, 1 club has won it 5 times, another club has won it 6 times, and 1 club has won it a remarkable 13 times, totaling to 30 victories. 

**This implies that all other clubs in the dataset have not won any Premier League matches. Therefore, it would be appropriate to update the "Winners" column by replacing the null values with 0, as these clubs have not won the Premier League title. This data cleaning step will ensure that the dataset accurately reflects the historical performance of each club in terms of Premier League wins**.

<br>
#### Replace null values of Winner Column

```python

# Replace null values with 0 in the "Winners" column

df["Winners"].fillna(0,inplace=True)

# .fillna(0, inplace=True) This is a method in pandas that is used to fill missing (null) values in a Series or DataFrame. 
# In this case, it is applied to the "Winners" column of the DataFrame df to fill any null values with the value 0.

df['Winners'].isnull().any()
>> False

df['Winners'].value_counts()

```

<br>
Output:
<br>
<br>

| **Winner** | **Count** |
|---|---|
| 0.0 | 33 |
| 1.0 | 3 |
| 3.0 | 1 |
| 13.0 | 1 |
| 5.0 | 1 |
| 6.0 | 1 |

<br>
#### Checking Counts/Null values in Runner Column

```python

# Next, let is look at Runners-up, As seen earlier even this column has Null value

df['Runners-up'].value_counts()

```

<br>
Output:
<br>
<br>

| **Runner** | **Count** |
|---|---|
| 0 | 10 |
| - | 3 |
| 1 | 3 |
| 4 | 1 |
| 7 | 1 |
| 6 | 1 |
| 5 | 1 |
| 2 | 1 |
| 3 | 1 |

<br>
* Teams have different numbers of runner-up finishes. One team has finished as runner-up 7 times, another 6 times, one team 5 times, another 4 times, another 3 times, one team 2 times and three teams have finished as runner-up once each.
* We also notice some inconsistency in data,this column particularly has null values, 0's and '-' We need to clean.

Since we know the **number of times English Premier League was conducted is 30** and we have data for all we will convert the null & '-' to 0 for all other clubs.

<br>

```python

# replace '-' and null values with zero

df['Runners-up'].fillna(0, inplace=True)
df['Runners-up'].replace('-', 0, inplace=True)

# replace() method is used to replace the "-" values with zero. The inplace=True argument is used to modify the original dataframe.

# Also we have seen it earlier that 'Runners-up' column is "Object" type let us convert it into int type

df['Runners-up'] = pd.to_numeric(df['Runners-up'], errors='coerce')
df['Runners-up'] = df['Runners-up'].astype('Int64')

```
<br>
This code is converting the "Runners-up" column in a pandas DataFrame, df, from an "Object" data type to an "Int64" data type.

The first line uses the pd.to_numeric() function to attempt to convert the "Runners-up" column to a numeric data type. The errors='coerce' argument tells the function to replace any values that cannot be converted to a number with NaN.

The second line uses the .astype() method to convert the "Runners-up" column to an "Int64" data type. The .astype() method is called on the "Runners-up" column of the DataFrame, and the argument "Int64" specifies the desired data type.

<br>
#### Checking Info of the DataFrame

```python

df.info()

```

<br>
Output:
<br>
<br>

| **Column** | **Non-Null Count** | **Dtype** |  
|---|---|---|
| Club | 40 non-null | object | 
| Matches Played | 40 non-null | int64 |  
| Win | 40 non-null | int64 |  
| Loss | 40 non-null | int64 |  
| Drawn | 40 non-null | int64 |  
| Goals | 40 non-null | int64 |  
| Clean Sheets | 40 non-null | int64 |  
| TeamLaunch | 40 non-null | object | 
| Winners | 40 non-null | float64 |
| Runners-up | 40 non-null | Int64 | 
| lastplayed_pl | 40 non-null | object | 

<br>
#### TeamLaunch Column

```python

df['TeamLaunch'].value_counts()

```

<br>
Output:
<br>
<br>

| **TeamLaunch** | **Count** |
|---|---|
| 1878 | 3 |
| 1905 | 2 |
| 1882 | 2 |
| 1884 | 2 |
| 1874 | 2 |
| 1886 | 2 |
| 1892 | 2 |
| 1875 | 2 |
| 1879 | 2 |
| 16 Oct 1878 | 1 |
| 1867 | 1 |
| 1904 | 1 |
| 1894 | 1 |
| 1865 | 1 |
| 1902 | 1 |
| 1881 | 1 |
| 1899 | 1 |
| 1876 | 1 |
| 1895 | 1 |
| 1863 | 1 |
| 1912 | 1 |
| April 1898 | 1 |
| 1861 | 1 |
| 1919 | 1 |
| 1932 | 1 |
| 1885 | 1 |
| Aug 1883 | 1 |
| 1901 | 1 |
| 1889 | 1 |
| 1877 | 1 |

<br>
We also observed TeamLaunch column has data inconsistency such as **Aug 1883**, **April 1898**.

<br>
#### Convert TeamLaunch Column

```python

# We need to convert the 'TeamLaunch' into 'YYYY'

# convert the column to datetime format

df['TeamLaunch'] = pd.to_datetime(df['TeamLaunch'], errors='coerce')

# convert the column to YYYY format

df['TeamLaunch'] = df['TeamLaunch'].dt.strftime('%Y')
df['TeamLaunch'].value_counts()

```

<br>
Output:
<br>
<br>

| **TeamLaunch** | **Count** |
|---|---|
| 1878 | 4 |
| 1875 | 2 |
| 1879 | 2 |
| 1882 | 2 |
| 1884 | 2 |
| 1905 | 2 |
| 1874 | 2 |
| 1892 | 2 |
| 1886 | 2 |
| 1865 | 1 |
| 1881 | 1 |
| 1899 | 1 |
| 1895 | 1 |
| 1904 | 1 |
| 1894 | 1 |
| 1902 | 1 |
| 1867 | 1 |
| 1898 | 1 |
| 1876 | 1 |
| 1863 | 1 |
| 1912 | 1 |
| 1861 | 1 |
| 1932 | 1 |
| 1885 | 1 |
| 1883 | 1 |
| 1919 | 1 |
| 1901 | 1 |
| 1889 | 1 |
| 1877 | 1 |

<br>
#### Lastplayed Column

```python

# Let us extract only the year in lastplayed_pl column

df['lastplayed_pl'] = (pd.to_datetime(df['lastplayed_pl'], format='%b-%y', errors='coerce')).dt.year
df['lastplayed_pl'].head()

#The "format" parameter specifies the expected format of the input string. 
#In this case '%b-%y' which indicates a three-letter month abbreviation followed by a two-digit year (e.g. "Mar-21"). 

```

<br>
Output of first 5 Rows:
<br>
<br>

| **lastplayed_pl** |
|---|
| 2023 |
| 2023 |
| 2011 |
| 2012 |
| 2012 |


___

<br>
### Exploratory Data Analysis <a name="EDA-context"></a>

```python

df.describe()

```
<br>
Describing the Summary of the Dataframe :
<br>
<br>

| **Summary** | **Matches Played** | **Win** | **Loss** | **Drawn** | **Goals** | **Clean Sheets** | **Winners** | **Runners-up** | **lastplayed_pl** |
|---|---|---|---|---|---|---|---|---|---|
| count | 40.000000 | 40.000000 | 40.000000 | 40.000000 | 40.000000 | 40.000000 | 40.000000 | 40.000000 | 40.000000 |
| mean | 573.750000 | 215.450000 | 210.425000 | 147.875000 | 769.000000 | 167.925000 | 0.750000 | 0.750000 | 2018.000000 |
| std | 358.986519 | 194.164608 | 102.132364 | 88.873632 | 627.746478 | 135.561584 | 2.372384 | 1.750458 | 6.876195 |
| min | 190.000000 | 41.000000 | 85.000000 | 48.000000 | 181.000000 | 45.000000 | 0.000000 | 0.000000 | 2000.000000 |
| 25% | 275.000000 | 80.500000 | 127.500000 | 71.500000 | 304.500000 | 66.000000 | 0.000000 | 0.000000 | 2014.500000 |
| 50% | 443.000000 | 116.500000 | 193.500000 | 120.000000 | 462.000000 | 104.000000 | 0.000000 | 0.000000 | 2022.000000 |
| 75% | 934.750000 | 295.750000 | 263.000000 | 222.000000 | 1142.750000 | 244.250000 | 0.000000 | 0.000000 | 2023.000000 |
| max | 1182.000000 | 720.000000 | 429.000000 | 329.000000 | 2229.000000 | 491.000000 | 13.000000 | 7.000000 | 2023.000000 |

<br>
* The average number of matches played by each team in the tournament is **573.75** 
* While the mean number of goals scored by all teams is **769**. However, the median number of goals scored is much lower at **462**, indicating that **some teams have scored significantly more goals than others**.
* Interestingly, the median number of **Winners** and **Runners-up** positions are both **0**, suggesting that most teams have not won or finished as runners-up in the tournament. 
* However, there is one team that has won the tournament a remarkable **13 times** and another team that has been the **runners-up 7 times**. It would be interesting to find out which teams these are.

<br>
#### Winner&Runner-up Teams

```python

# Team that has won Premier League 13 times

df[df['Winners']==13]['Club']
>> 20    Manchester United
>> Name: Club, dtype: object

# Team that has been runner-up 7 times

df[df['Runners-up']==7]['Club']
>> 20    Manchester United
>> Name: Club, dtype: object

```

<br>
We see that **Manchester United** has won Premier league **13 times** and have been runner-up **7 times**.

<br>
#### Plot Histogram


```python

import matplotlib.pyplot as plt
%matplotlib inline

# Let us visualize each column

# First let us start with Matches Played column
# plot histogram
plt.hist(df['Matches Played'])

# add labels and title
plt.xlabel('No. of Matches Played')
plt.ylabel('Frequency')
plt.title('Histogram of Matches Played')
plt.show()

```

<br>
That code gives us the below plot - which visualises our results!

<br>
![alt text](/img/posts/EDA_Hist.jpg "EDA Hist Plot")

<br>
We can see from the histogram that a majority of teams have played less than **400 matches**. However, there are a few teams that have played an exceptionally high number of matches, exceeding **900**. 

**As per the project requirements, it is worth noting that some of the more established clubs have already been owned by the competitors. Therefore, the client is interested in identifying potential clubs that may perform well in the future, even if they have less experience in the Premier League**.

<br>
#### Identify Teams >= 900


```python

# Identify teams who have played more than 900 matches
df[df['Matches Played']>=900]['Club']

```

<br>
Output:
<br>
<br>

| **Club** |
|---|
| Arsenal |
| Aston Villa |
| Chelsea |
| Everton |
| Liverpool |
| Manchester City |
| Manchester United |
| Newcastle United |
| Southampton |
| Tottenham Hotspur |
| West Ham United |

<br>
Upon analysis, we have observed that there are a total of 11 clubs who have significantly more experience in the Premier League as compared to the others. These clubs have played a higher number of matches and have established themselves as experienced players in the league.

As per the client's requirements, we are interested in identifying potential clubs that may perform well in the future, even if they have less experience in the Premier League. Therefore, we have decided to **drop these 11 clubs from our analysis, as their established presence in the league may skew our results and make it difficult to identify less experienced clubs with high potential**.

By removing these clubs, we can focus our analysis on the remaining clubs and potentially identify hidden gems that may have been overlooked due to their lack of experience in the league.

<br>
#### Identify Teams < 900

```python

df = df[df['Matches Played'] < 900].reset_index(drop=True)

df.shape
>> (29, 11)

df.head()

```

<br>
Output of first 5 rows:
<br>
<br>

| **Club** | **Matches Played** | **Win** | **Loss** | **Drawn** | **Goals** | **Clean Sheets** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** |
|---|---|---|---|---|---|---|---|---|---|---|
| Birmingham City | 266 | 73 | 111 | 82 | 273 | 66 | 1875 | 0.0 | 0 | 2011 |
| Blackburn Rovers | 696 | 262 | 250 | 184 | 927 | 210 | 1875 | 1.0 | 1 | 2012 |
| Bolton Wanderers | 494 | 149 | 217 | 128 | 575 | 108 | 1874 | 0.0 | 0 | 2012 |
| Bournemouth | 219 | 64 | 107 | 48 | 269 | 45 | 1899 | 0.0 | 0 | 2023 |
| Brighton & Hove Albion | 218 | 61 | 85 | 72 | 243 | 58 | 1901 | 0.0 | 0 | 2023 |

<br>
We removed the 11 clubs i.e clubs with more experience. We have only 29 Clubs.

<br>
#### Win, Loss, Drawn, and clean sheets Rate

```python

# Create new columns for Winning Rate, Loss Rate, Draw Rate, & Clean Sheet Rate

df['Winning Rate'] = (df['Win'] / df['Matches Played'])*100
df['Loss Rate'] = (df['Loss'] / df['Matches Played'])*100
df['Drawn Rate'] = (df['Drawn'] / df['Matches Played'])*100
df['Clean Sheet Rate'] = (df['Clean Sheets'] / df['Matches Played'])*100

# Create a column for average goals scored per match

df['Avg Goals Per Match']=df['Goals']/df['Matches Played']
df['Avg Goals Per Match']=df['Avg Goals Per Match'].round()

# View data

df[['Club','Matches Played','Win','Loss','Drawn','Goals','Clean Sheets','Winning Rate','Loss Rate','Drawn Rate','Clean Sheet Rate','Avg Goals Per Match']].head()

```

<br>
Output of first 5 rows:
<br>
<br>

| **Club** | **Matches Played** | **Win** | **Loss** | **Drawn** | **Goals** | **Clean Sheets** | **Winning Rate** | **Loss Rate** | **Drawn Rate** | **Clean Sheet Rate** | **Avg Goals Per Match** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Birmingham City | 266 | 73 | 111 | 82 | 273 | 66 | 27.443609 | 41.729323 | 30.827068 | 24.812030 | 1.0 |
| Blackburn Rovers | 696 | 262 | 250 | 184 | 927 | 210 | 37.643678 | 35.919540 | 26.436782 | 30.172414 | 1.0 |
| Bolton Wanderers | 494 | 149 | 217 | 128 | 575 | 108 | 30.161943 | 43.927126 | 25.910931 | 21.862348 | 1.0 |
| Bournemouth | 219 | 64 | 107 | 48 | 269 | 45 | 29.223744 | 48.858447 | 21.917808 | 20.547945 | 1.0 |
| Brighton & Hove Albion | 218 | 61 | 85 | 72 | 243 | 58 | 27.981651 | 38.990826 | 33.027523 | 26.605505 | 1.0 |

<br>
We can see 'Birmingham City' has won the matches **73** times out of **266 matches played**, While 'Blackburn Rovers' has won the matches **262** times out of **696 matches played**. 

My question is can we compare 73 Wins with 262 Wins? No, because obviously the teams who played lesser matches will have lesser wins **which does not mean they are a bad team just because they played lesser number of matches**. 

So there is a issue here. We easily analyzed 'Matches Played' Column but we can't do the same for **'Win', 'Loss', 'Drawn', 'Goals', 'Clean Sheets'**, can't compare these columns because everything depends on '**Matches Played**' 

It is essential to understand that the values in all the columns represent the cumulative scores over all the matches played. 

To accurately analyze the performance of the teams, we must normalize the data by dividing the no. of wins, loss, drawn, clean sheet, goals by the number of matches played. 

This normalization will provide us with a fair idea of the winning, losing, draw, and clean sheet percentages of each team along with goals per match.

<br>
#### Visualizing Winning, Loss, Drawn & Clean Sheet Rate


```python

# Now let us visualize Winning, Loss, Drawn rate, and Clean Sheet

# Set the figure size

plt.figure(figsize=(8, 6))

# Create the boxplot

boxplot = plt.boxplot([df['Winning Rate'], df['Drawn Rate'], df['Loss Rate'], df['Clean Sheet Rate']], 
                      patch_artist=True,
                      labels=['Winning Rate', 'Drawn Rate', 'Loss Rate', 'Clean Sheet Rate'])

# Set the title and axis labels

plt.title('Distribution of Winning Rate, Drawn Rate, Loss Rate and Clean Sheet Rate')
plt.xlabel('Winning, Drawn ,Lost Game & Clean Sheet')
plt.ylabel('Rate')

# Show the plot

plt.show()

```

<br>
That code gives us the below plot - which visualises our results!

<br>
![alt text](/img/posts/EDA_Box.jpg "EDA Box Plot")

<br>
###### Winning Rate

We observe that there are a few outliers in the Winning Rate boxplot, which are located above the upper whisker. It is safe to conclude that these outlier clubs have shown **exceptional winning rates compared to the other clubs**. Let us identify them ahead.

Also let us identify the club that has least "Winning Rate".

###### Drawn Rate

We observe an outlier in the drawn rate boxplot, indicating that there is one clubs has a much higher drawn rate compared to others. This may not necessarily be a positive indication, as it suggests that the club may struggle to secure wins in their matches. Going further let us identify which club is this.

###### Loss Rate

We can see very clearly that loss rates for these clubs are high compared to winning rate - **meaning tendency to lose the match is pretty high for these teams**.

###### Clean Sheet Rate

We see that data for Clean Sheet rate is pretty Symmetric. Nothing can be inferred.

<br>
#### Clubs with High Winning Rate

```python

# Calculate the interquartile range for the "Winning Rate" column

Q1 = df['Winning Rate'].quantile(0.25)
Q3 = df['Winning Rate'].quantile(0.75)
IQR = Q3 - Q1

# Calculate the upper boundaries for potential outliers <-- Expectional high winning rate compared to other teams

upper_bound = Q3 + 1.5 * IQR

# Identify the clubs with high winning rate 

highwinningrate = df[(df['Winning Rate'] > upper_bound)]
highwinningrate[['Club','Matches Played','Win','Loss','Drawn','Goals','Clean Sheets','TeamLaunch','Winners','Runners-up','lastplayed_pl','Winning Rate']]

```

<br>
Output:
<br>
<br>

| **Club** | **Matches Played** | **Win** | **Loss** | **Drawn** | **Goals** | **Clean Sheets** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** | **Winning Rate** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Blackburn Rovers | 696 | 262 | 250 | 184 | 927 | 210 | 1875 | 1.0 | 1 | 2012 | 37.643678 |
| Leeds United | 574 | 223 | 202 | 149 | 784 | 179 | 1919 | 0.0 | 0 | 2023 | 38.850174 |

<br>
Upon analyzing the data, we have found that two teams, **Leeds United and Blackburn Rovers, have exceptionally high winning rates of 39% and 38% respectively**.

<br>
#### Clubs with Low Winning Rate

```python

# Calculate the lower boundaries for potential outliers <-- Low winning rate compared to other teams

lower_bound = Q1 - 1.5 * IQR

# Identify the clubs with lowest winning rate 

lowwinningrate = df[(df['Winning Rate'] < lower_bound)]
lowwinningrate[['Club','Matches Played','Win','Loss','Drawn','Goals','Clean Sheets','TeamLaunch','Winners','Runners-up','lastplayed_pl','Winning Rate']]

```

<br>
Output:
<br>
<br>

| **Club** | **Matches Played** | **Win** | **Loss** | **Drawn** | **Goals** | **Clean Sheets** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** | **Winning Rate** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Hull City | 190 | 41 | 101 | 48 | 181 | 58 | 1904 | 0.0 | 0 | 2017 | 21.578947 |

<br>
Club with lowest winning rate of 22% is **Hull City**.

<br>
####  Clubs with High Drawn Rate

```python

# Calculate the interquartile range for the "Drawn Rate" column

Q1 = df['Drawn Rate'].quantile(0.25)
Q3 = df['Drawn Rate'].quantile(0.75)
IQR = Q3 - Q1

# Calculate the upper boundaries for potential outliers <-- Expectional high winning rate compared to other teams

upper_bound = Q3 + 1.5 * IQR

# Identify the clubs with high drawn rate 

highdrawnrate = df[(df['Drawn Rate'] > upper_bound)]
highdrawnrate[['Club','Matches Played','Win','Loss','Drawn','Goals','Clean Sheets','TeamLaunch','Winners','Runners-up','lastplayed_pl','Drawn Rate']]

```

<br>
Output:
<br>
<br>

| **Club** | **Matches Played** | **Win** | **Loss** | **Drawn** | **Goals** | **Clean Sheets** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** | **Drawn Rate** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Brighton & Hove Albion | 218 | 61 | 85 | 72 | 243 | 58 | 1901 | 0.0 | 0 | 2023 | 33.027523 |

<br>
**Brighton & Hove Albion** is expectionally high Drawn Rate of **33%**.

<br>
#### Average Goals Per Match

```python

# Now let us explore 'Avg Goals Per Match' column

df['Avg Goals Per Match'].describe()

```

<br>

| **Summary** | **Values** |
|---|---|
| count | 29.0 |
| mean | 1.0 |
| std | 0.0 |
| min | 1.0 |
| 25% | 1.0 |
| 50% | 1.0 |
| 75% | 1.0 |
| max | 1.0 |

<br>
As you can see we can't infer much from this metric. Therefore we will not use it for further analysis.

<br>
#### Exploring Winner & Runners-up Columns


```python

# Let us explore columns 'Winners' and 'Runners-up'

df['Winners'].value_counts()
>> 0.0 27
>> 1.0 2

df['Runners-up'].value_counts()
>> 0 28
>> 1 1

```

<br>
We observe that out of the 29 clubs, only 2 clubs have won the Premier League, and one club has been a runner-up. 
Let us identify these clubs.

<br>


```python

df[(df['Winners']>=1) | (df['Runners-up']>=1)][['Club','Matches Played','Win','Loss','Drawn','Goals','Clean Sheets','TeamLaunch','Winners','Runners-up','lastplayed_pl']]

```

<br>
Output:
<br>
<br>

| **Club** | **Matches Played** | **Win** | **Loss** | **Drawn** | **Goals** | **Clean Sheets** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** |
|---|---|---|---|---|---|---|---|---|---|---|
| Blackburn Rovers | 696 | 262 | 250 | 184 | 927 | 210 | 1875 | 1.0 | 1 | 2012 |
| Leicester City | 642 | 216 | 262 | 164 | 860 | 167 | 1884 | 1.0 | 0 | 2023 |

<br>
**Blackburn Rovers have won Premier League once and been an Runners-up once and Leicester City has won Premier League once**.

<br>
#### Analyzing Matches Played & Last Played Column


```python

# Lets us again analyse Matches Played Column for our reduced dataframe (29 clubs).

df['Matches Played'].describe()

```

<br>
Summary of the DataFrame:
<br>
<br>

| **Summary** | **Values** |
|---|---|
| count | 29.000000 |
| mean | 372.482759 |
| std | 153.533296 |
| min | 190.000000 |
| 25% | 266.000000 |
| 50% | 305.000000 |
| 75% | 494.000000 |
| max | 696.000000 |

<br>
Average matches played are 372.

<br>

```python

# Let us look at "lastplayed_pl" column

df['lastplayed_pl'].value_counts()

```

<br>
Output:
<br>
<br>

| **lastplayed_pl** | **Count** |
|---|---|
| 2023 | 8 |
| 2017 | 3 |
| 2018 | 3 |
| 2022 | 3 |
| 2012 | 2 |
| 2021 | 1 |
| 2000 | 1 |
| 2001 | 1 |
| 2002 | 1 |
| 2007 | 1 |
| 2008 | 1 |
| 2010 | 1 |
| 2011 | 1 |
| 2013 | 1 |
| 2015 | 1 |

<br>
Out of the total 29 teams, **eight are currently playing in the Premier League. Since these teams are currently active in the league, it makes sense to prioritize them in our analysis. However, there are also teams that date back as early as 2000. It may be appropriate to assign these teams less weight**.

<br>
#### Checking 8 Teams in Current League(2023)


```python

# Let us check the eight teams that are currently playing in the Premier League

df[df['lastplayed_pl']==2023]['Club']

```

<br>

| **lastplayed_pl** |
|---|
| Bournemouth |
| Brighton & Hove Albion |
| Crystal Palace |
| Fulham |
| Leeds United |
| Leicester City |
| Nottingham Forest |
| Wolverhampton Wanderers |

<br>
**Giving more priority to teams that have more recent experience playing in the Premier League is ideal. When making the final decision, we will assign higher weight to teams that have played more recently, and lesser weight to those that have not played recently**.

___
<br>
# Analysing The Results  <a name="Club-results"></a>

<br>
#### Final Recommendations Framework

Let's create a plan to Score each team on the pre defined metric.

* Give a score of 10 if club have a relatively high experience in the Premier League above average (372)
* Give a score of 15 if club has winning rate above Q3
* Give a score of 15 if club has lossing rate below Q1
* Give a score of 10 if club drawn rate below Q1 and losing rate is below Q1
* Give a score of 10 if club has clean sheet above Q3 and winning rate is above Q3
* Give a score of 15 if club has won premier league
* Give a score of 10 if club has been a runners-up in premier league
* Give a score of 15 if club has been currently playing in premier league


```python

# Calculate the upper bound for the "Winning Rate" column
upper_bound_WinningRate = df['Winning Rate'].quantile(0.75)

# Calculate the lower bound for the "Loss Rate" column
lower_bound_LosingRate = df['Loss Rate'].quantile(0.25)

# Calculate the lower bound for the "Drawn Rate" column
lower_bound_DrawnRate = df['Drawn Rate'].quantile(0.25)

# Calculate the upper bound for the "Drawn Rate" column
upper_bound_CleanSheetRate = df['Clean Sheet Rate'].quantile(0.75)

df['scores']=np.zeros(len(df))

```

<br>

```python

df.loc[df['Matches Played'] >= 372, 'scores'] += 10
df.loc[df['Winning Rate'] >= upper_bound_WinningRate, 'scores'] += 15
df.loc[df['Loss Rate'] <= lower_bound_LosingRate, 'scores'] += 15
df.loc[(df['Drawn Rate'] <= lower_bound_DrawnRate) & (df['Loss Rate'] <= lower_bound_LosingRate), 'scores'] += 10
df.loc[(df['Clean Sheet Rate'] >= upper_bound_CleanSheetRate) & (df['Winning Rate'] >= upper_bound_WinningRate), 'scores'] += 10
df.loc[df['Winners'] == 1, 'scores'] += 15
df.loc[df['Runners-up'] == 1, 'scores'] += 10
df.loc[df['lastplayed_pl'] == 2023, 'scores'] += 15

df[['Club','Matches Played','TeamLaunch','Winners','Runners-up','lastplayed_pl','Winning Rate','Loss Rate','Drawn Rate','Clean Sheet Rate','Avg Goals Per Match','scores']].head()

```

<br>
Output of first 5 rows:
<br>
<br>


| **Club** | **Matches Played** | **TeamLaunch** | **Winners** | **Runners-up** | **lastplayed_pl** | **Winning Rate** | **Loss Rate** | **Drawn Rate** | **Clean Sheet Rate** | **Avg Goals Per Match** | **scores** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| Birmingham City | 266 | 1875 | 0.0 | 0 | 2011 | 27.443609 | 41.729323 | 30.827068 | 24.812030 | 1.0 | 0.0 |
| Blackburn Rovers | 696 | 1875 | 1.0 | 1 | 2012 | 37.643678 | 35.919540 | 26.436782 | 30.172414 | 1.0 | 75.0 |
| Bolton Wanderers | 494 | 1874 | 0.0 | 0 | 2012 | 30.161943 | 43.927126 | 25.910931 | 21.862348 | 1.0 | 25.0 |
| Bournemouth | 219 | 1899 | 0.0 | 0 | 2023 | 29.223744 | 48.858447 | 21.917808 | 20.547945 | 1.0 | 15.0 |
| Brighton & Hove Albion | 218 | 1901 | 0.0 | 0 | 2023 | 27.981651 | 38.990826 | 33.027523 | 26.605505 | 1.0 | 30.0 |

<br>

```python

# sort the DataFrame by score in descending order
df_sort = df.sort_values(by='scores', ascending=False)

# create a bar chart of team scores
plt.figure(figsize=(25,10))
plt.bar(df_sort['Club'], df_sort['scores'], color='blue')

# add labels and title to the chart
plt.ylabel('Scores', fontsize=16)
plt.title('Football Club v/s performance score', fontsize=18)

# add legend to explain the blue bars
plt.legend(['Scores'], fontsize=14)

# rotate the team names on the x-axis for readability
plt.xticks(rotation=90, fontsize=14)
plt.yticks(fontsize=14)

# set the y-axis limit to start from 0 and end at 100
plt.ylim(0, 100)

# display the chart
plt.savefig('EDA_Bar.jpg',bbox_inches='tight',dpi=150)
plt.show()

```

<br>
That code gives us the below plot - which visualises our results!

<br>
![alt text](/img/posts/EDA_Bar.jpg "EDA Bar Plot")

<br>
**Based on the above chart, Blackburn Rovers has the highest score basis our analysis and next best Leicester City**

**To ensure a thorough evaluation of football club performance we must consider clubs current form**.

Let us check the score of those clubs that have played in the last three years. Specifically, suggest including clubs that have played in 2023, as well as those that last played in 2022 and 2021. 

This approach allows us to pinpoint those clubs that are currently in good form and have consistently performed well over the past few years.

<br>

```python

# sort the DataFrame by score in descending order
df_sort = df[(df['lastplayed_pl']==2023) | (df['lastplayed_pl']==2022) | (df['lastplayed_pl']==2021)].sort_values(by='scores', ascending=False)

# create a bar chart of team scores
plt.figure(figsize=(25,10))
plt.bar(df_sort['Club'], df_sort['scores'], color='blue')

# add labels and title to the chart
plt.ylabel('Scores', fontsize=16)
plt.title('Football Club v/s performance score', fontsize=18)

# add legend to explain the blue bars
plt.legend(['Scores'], fontsize=14)

# rotate the team names on the x-axis for readability
plt.xticks(rotation=90, fontsize=14)
plt.yticks(fontsize=14)

# set the y-axis limit to start from 0 and end at 100
plt.ylim(0, 100)

# display the chart

plt.savefig('EDA_Bar2.jpg',bbox_inches='tight',dpi=150)
plt.show()

```

<br>
That code gives us the below plot - which visualises our results!

<br>
![alt text](/img/posts/EDA_Bar2.jpg "EDA Bar2 Plot")

<br>
**Upon closer examination of the list, we can observe that our current leader, Blackburn Rovers, is not included. To gain a better understanding of their performance, it's necessary to investigate further and determine the last year in which Blackburn Rovers played. This information will provide crucial context to our analysis and enable us to assess their recent form accurately**. 

<br>

```python

df[df['Club']=='Blackburn Rovers']['lastplayed_pl']
>> 1    2012
>> Name: lastplayed_pl, dtype: int64

```

<br>
**Blackburn Rovers last played in the tournament in 2012**, which was quite some time ago. Given this information, we recommend that stakeholders consider investing in Leicester City instead. We believe that Leicester City's recent form and performance make them a better choice for investment.

To support our claim, we will conduct further secondary research to provide additional evidence of Leicester City's current form and potential for success

According to my research, Blackburn Rovers were relegated to the Championship league in 2012 i.e., league below Premier League and later to League One in 2017 i.e., league below Championship league. However, they were promoted back to the Championship in 2018 and have since finished in the middle of the table in recent years. Given their inconsistent performance and lack of presence in the Premier League since 2012, it would be inappropriate to recommend this club for investment.

On the other hand, Leicester City, the 2016 Premier League champions, have consistently finished in the top 10 in recent years. They placed 5th in both the 2019-2020 and 2020-2021 seasons and finished 8th in 2021-2022. With sufficient financial backing, Leicester City has the potential to achieve even greater success in the near future. Therefore, it would be reasonable to recommend Leicester City to our clients.

Source 1 : <a href="https://www.transfermarkt.co.in/blackburn-rovers/platzierungen/verein/164">transfermarkt/blackburn_rovers</a>

Source 2 : <a href="https://www.transfermarkt.co.in/leicester-city/platzierungen/verein/1003">transfermarkt/leicester_city</a>

### We recommend investing in "Leicester City" based on our analysis.

___
<br>
### Growth/Next Steps <a name="growth-next-steps"></a>

Since it is an investment decision, the **Price** would need to be in the equation too.  

We could discuss with client about their budget. Based on their budget, we could filter the teams. 

From the data point of view, we can try to collect each team's **price/value** to ensure that we have as much useful information available in making the final decision.

























