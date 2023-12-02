---
layout: post
title: Unveiling Instagram Insights
image: "/posts/Instagram-Insights.png"
tags: [Data Cleaning, EDA, Python]
---

In this project we apply EDA to analyse the data and provide recommendations on what type of post are working for the page.

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

Data Analyst Duo is an instagram community (@𝒅𝒂𝒕𝒂𝒂𝒏𝒂𝒍𝒚𝒔𝒕𝒅𝒖𝒐) of ~𝟕𝟓𝐤 data enthusiasts founded by two individuals Aditi & Kalpesh. 
They share content around statistics, data science & analytics with budding data aspirants.

The goal is to analyse the data and provide recommendations on what type of post are working for the page.
<br>
<br>
### Actions <a name="overview-actions"></a>

I've collected the data from the instagram page "dataanalystduo".

I've performed data clearning i.e removing incorrect or irrelevant data on the dataset and analyzed unique counts of values present in each column or field of the dataset to get an understanding of how the data looks like.

Performed Exploratory Data Analysis on the dataset i.e using line charts to see the trends/patters in the columns like "Instagram Reach", "Instagram Profile Visits", "Instagram New Followers" and used pivot tables along with aggregate functions to see the average shares, reach, impressions, New followers, comments and saves followed by the counts of title for each of posts which includes IG Videos, Images and Carousel per day.

Finally we compared the averages and counts of each column with respect to the types of posts such as IG Videos, IG Images and IG Carousel to provide recommendation of what type of post should the duo opt for.
<br>
<br>

### Results <a name="overview-results"></a>

After analyzing the findings, it is found that **IG Videos** have worked well for the page "datanalystduo" in gaining New Followers and also **IG Carousel** for engaging the current audience of the page.
<br>
<br>
### Growth/Next Steps <a name="overview-growth"></a>

Social media feeds (specifically what people/posts you see when you log on) are driven by an algorithm but these can change from time to time.  For example, on LinkedIn, there was a time when polls got a huge amount of reach, then it became sharing PDF documents. The algorithm was being changed behind the scenes to up-weight or down-weight certain types of **post type**.

As of now IG videos/reels, act as better engagement widely in general.

In future, there might be possibilities that they may change the algorithm to favor image posts or some newly discovered **post type** which can act as better engagement for the users

So keeping this analysis up to date would help the user keep close to what was working **now** rather than what **worked several months ago**.

Also, diving deeper into **IG videos** to understand which **topics** got the most traction helps the duo in creating more content towards those topics.

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

<br>
**Line Chart**

* A line chart is a type of chart used to show information that changes over time. Line charts are created by plotting a series of several points and connecting them with a straight line. Line charts are used to track changes over short and long periods.
* A line chart is used to show the change in information over time. The horizontal axis is usually a time scale; for example, minutes, hours, days, months, or years. For example, you could create a line chart that shows the daily earnings of a store for five days. The horizontal axis would include the days of the week, while the vertical axis would have the daily earnings.


___

<br>
# Data Overview & Preparation  <a name="data-overview"></a>

In the code below, we:

* Load in the Python libraries we require for importing the data.
* Import the required data.

<br>

```python

# Import Libraries for data cleaning & data analysis & data visualisation

import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_excel(r'/Users/praju/Desktop/DADUO/did by me/dataanalystduo instagram analytics (1).xlsx')
df.head()

```
<br>
A sample of this data (the first 5 rows) can be seen below:
<br>
<br>

| **Date** |	**Instagram reach** | **Instagram Profile visits** | **New Instagram followers** | **Title** | **Post type** | **Impressions** | **Reach** | **Shares** | **Follows** | **Likes** | **Comments** | **Saves** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2022-01-01T00:00:00 | 348 | 70 | 0 | 0 | 0 | 0.0 | 0.0 | 0 | 0 | 0 | 0 | 0 |
| 2022-01-02T00:00:00 |	497 | 100 |	0 |	0 |	0 |	0.0 | 0.0 |	0 |	0 |	0 |	0 |	0 |
| 2022-01-03T00:00:00 |	2745 | 249 | 0 | 0 | 0 | 0.0 | 0.0 | 0 | 0 | 0 | 0 | 0 |
| 2022-01-04T00:00:00 |	1619 | 154 | 0 | 0 | 0 | 0.0 | 0.0 | 0 | 0 | 0 | 0 | 0 |
| 2022-01-05T00:00:00 |	2434 | 195 | 0 | 0 | 0 | 0.0 | 0.0 | 0 | 0 | 0 | 0 | 0 |

<br>

Data Dictionary:

The data set contains stats about the channel (@𝒅𝒂𝒕𝒂𝒂𝒏𝒂𝒍𝒚𝒔𝒕𝒅𝒖𝒐)

Domain: Social Media ( Instagram )

* Date: Date
* Instagram reach: The number of unique accounts that saw any of your posts or stories at least once. Impression is different from reach, which may include multiple views of your posts by the same accounts. This metric is estimated.
* Instagram profile visits: The number of times your profile was visited.
* New Instagram followers: The number of new accounts that started following your Instagram account.
* Title: Title of the post
* Post type: Type of post - IG video, IG carousel, IG Image
* Impressions: The number of times your post was viewed
* Reach: The number of accounts your post was reached
* Shares: The number of times you post was shared
* Follows: The number of new accounts that started following your Instagram account.
* Likes: The number of likes on the post
* Comments: The number of comments on the post
* Saves: The number of saves on the post

___

<br>
# Applying Data Cleaning & EDA <a name="DC-EDA-application"></a>

### Data Cleaning <a name="DC-context"></a>

```python

# View to Snapshot of data - Last 5 rows

df.tail()

```
<br>
Output:
<br>
<br>

| **Date** |	**Instagram reach** | **Instagram profile visits** | **New Instagram followers** | **Title** | **Post type** | **Impressions** | **Reach** | **Shares** | **Follows** | **Likes** | **Comments** | **Saves** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2023-04-11T00:00:00 |	9437 | 583 | 156 | 0 | 0 | 0.0 | 0.0 | 0 | 0 | 0 | 0 | 0 |
| 2023-04-12T00:00:00 |	16290 |	529 | 119 |	0 |	0 |	0.0 | 0.0 |	0 | 0 |	0 |	0 |	0 |
| 2023-04-13T00:00:00 |	13132 |	494 | 116 |	0 |	0 |	0.0 | 0.0 |	0 |	0 |	0 |	0 |	0 |
| 2023-04-14T00:00:00 |	7681 | 459 | 0 | 0 | 0 | 0.0 | 0.0 | 0 | 0 | 0 | 0 | 0 |
| 2023-04-15T00:00:00 |	942 | 76 | 0 | 0 | 0 | 0.0 | 0.0 | 0 | 0 | 0 | 0 | 0 |

<br>
* By looking at the data we can see the issue with the Date column. We will fix it.

<br>
#### Checking Info of the Dataset

```python

df.shape
>> (470,13)

df.info()

```
<br>
Output:
<br>
<br>

| **Column** | **Non-Null Count** | **Dtype** |  
|---|---|---|
| Date | 470 non-null | object | 
| Instagram reach | 470 non-null | int64 |  
| Instagram profile visits | 470 non-null | int64 |  
| New Instagram followers | 470 non-null | int64 |  
| Title | 470 non-null | object | 
| Post type | 470 non-null | object | 
| Impressions | 470 non-null | float64 |
| Reach | 470 non-null | float64 |
| Shares | 470 non-null | int64 |  
| Follows | 470 non-null | int64 |  
| Likes | 470 non-null | int64 |  
| Comments | 470 non-null | int64 |   
| Saves | 470 non-null | int64 |

<br>
#### Date Column Cleaning

```python

df['Date']= df['Date'].str.split('T').str[0]

#In the above example, str.split('T') splits the string in the "date_column" on the "T" character
#str[0] selects the first part of the resulting split, which is the date part before the "T".

df.head()

```
<br>
Output of first 5 rows:
<br>
<br>

| **Date** |	**Instagram reach** | **Instagram profile visits** | **New Instagram followers** | **Title** | **Post type** | **Impressions** | **Reach** | **Shares** | **Follows** | **Likes** | **Comments** | **Saves** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2022-01-01 | 348 | 70 | 0 | 0 | 0 | 0.0 | 0.0 | 0 | 0 | 0 | 0 | 0 |
| 2022-01-02 | 497 | 100 | 0 | 0 | 0 | 0.0 | 0.0 | 0 | 0 | 0 | 0 | 0 |
| 2022-01-03 | 2745 | 249 |	0 |	0 |	0 |	0.0 | 0.0 | 0 |	0 |	0 |	0 |	0 |
| 2022-01-04 | 1619 | 154 |	0 |	0 |	0 |	0.0 | 0.0 |	0 |	0 |	0 |	0 |	0 |
| 2022-01-05 | 2434 | 195 |	0 |	0 |	0 |	0.0 | 0.0 |	0 |	0 |	0 |	0 |	0 |

<br>
#### Convert "Date" Column 

```python

# Convert the 'date' column to datetime type
df['Date'] = pd.to_datetime(df['Date'])
df.info()

```
<br>
Output:
<br>
<br>

| **Column** | **Non-Null Count** | **Dtype** |  
|---|---|---|
| Date | 470 non-null | datetime64[ns] | 
| Instagram reach | 470 non-null | int64 |  
| Instagram profile visits | 470 non-null | int64 |  
| New Instagram followers | 470 non-null | int64 |  
| Title | 470 non-null | object | 
| Post type | 470 non-null | object | 
| Impressions | 470 non-null | float64 |
| Reach | 470 non-null | float64 |
| Shares | 470 non-null | int64 |  
| Follows | 470 non-null | int64 |  
| Likes | 470 non-null | int64 |  
| Comments | 470 non-null | int64 |   
| Saves | 470 non-null | int64 |

<br>
#### Check total number of rows in all the columns without zero values

```python

columns_to_check = ['Date', 'Instagram reach', 'Instagram profile visits', 'New Instagram followers', 'Title', 'Post type', 'Impressions', 'Reach', 'Shares', 'Follows', 'Likes', 'Comments', 'Saves']

for column in columns_to_check:
    non_zero_count = df[column].value_counts().drop(0, errors='ignore').sum()
    print("Number of rows without zero values in column '{}': {}".format(column, non_zero_count))

>> Number of rows without zero values in column 'Date': 470
>> Number of rows without zero values in column 'Instagram reach': 470
>> Number of rows without zero values in column 'Instagram profile visits': 470
>> Number of rows without zero values in column 'New Instagram followers': 270
>> Number of rows without zero values in column 'Title': 64
>> Number of rows without zero values in column 'Post type': 64
>> Number of rows without zero values in column 'Impressions': 64
>> Number of rows without zero values in column 'Reach': 64
>> Number of rows without zero values in column 'Shares': 63
>> Number of rows without zero values in column 'Follows': 62
>> Number of rows without zero values in column 'Likes': 63
>> Number of rows without zero values in column 'Comments': 62
>> Number of rows without zero values in column 'Saves': 63

```
<br>
We will loop through each column in the list and use the value_counts() method to get the count of each unique value, and the drop(0) method to remove the count of zero values. Finally, we use the sum() method to get the total count of non-zero values in each column, and print the results.

<br>
### Exploratory Data Analysis <a name="EDA-context"></a>

```python

# check the trend for the column 'Instagram reach'

# Set the figure size
plt.figure(figsize=(10, 6))

# Create the line chart
plt.plot(df['Date'], df['Instagram reach'], marker='o', markersize=6, linewidth=2)

# Set the x-axis label
plt.xlabel('Date')

# Set the y-axis label
plt.ylabel('Instagram reach')

# Set the title
plt.title('Instagram reach by day: Jan 2022- Apr 2023')

# Show the plot
plt.show()

```
<br>
Above code gives us the below plot - which visualises our results!

<br>
![alt text](/img/posts/UII_Reach.jpg "UII Reach")

<br>
The reach trend exhibits a highly volatile pattern, with three notable instances of significant increases in reach observed around March/April 2022, August/September 2022, and December/January 2023.

<br>
#### Checking Instagram Profile Visits

```python

# Set the figure size
plt.figure(figsize=(10, 6))

# Create the line chart
plt.plot(df['Date'], df['Instagram profile visits'], marker='o', markersize=6, linewidth=2)

# Set the x-axis label
plt.xlabel('Date')

# Set the y-axis label
plt.ylabel('Instagram profile visits')

# Set the title
plt.title('Instagram profile visits by day: Jan 2022- Apr 2023')

# Show the plot
plt.show()

```
<br>
Above code gives us the below plot - which visualises our results!

<br>
![alt text](/img/posts/UII_PV.jpg "UII PV")

<br>
We can see similar trend in number of profile visits as well. The more "Reach" the more "profile visits".
In April we saw a peak and similarly in Auguest, September, December and January.

<br>
#### Checking New Instagram Followers

```python

# Set the figure size
plt.figure(figsize=(10, 6))

df_followers = df[df['New Instagram followers']!=0]

# Create the line chart
plt.plot(df_followers['Date'], df_followers['New Instagram followers'], marker='o', markersize=6, linewidth=2)

# Set the x-axis label
plt.xlabel('Date')

# Set the y-axis label
plt.ylabel('New followers')

# Set the title
plt.title('New Instagram followers gained by day: Jan 2022- Apr 2023')

# Show the plot
plt.show()

```
<br>
Above code gives us the below plot - which visualises our results!

<br>
![alt text](/img/posts/UII_IF.jpg "UII IF")

<br>

* On a daily basis, the number of new followers gained hovers around 200. 
* Significant increase in the followers in December 2022
* Number of followers decreasing post January 2023

**However, a remarkable surge in the count of new followers was witnessed during the period from December 2022 to January 2023**

Let's try to understand what exactly happenend during this period.

<br>
#### Finding Insights during the period Dec 2022 - Jan 2023

```python

#We will begin by determining the start date for which the posts' insights are available.
df_Title = df[df['Title']!=0]

# Check the minimum and maximum date in the filtered dataframe
min_date = df_Title['Date'].min()
max_date = df_Title['Date'].max()

print("Minimum Date: ", min_date)
print("Maximum Date: ", max_date)

>> Minimum Date:  2022-12-02 00:00:00
>> Maximum Date:  2023-03-28 00:00:00

df_dec_jan = df_Title[(df_Title['Date']>=pd.Timestamp('2022-12-01')) & (df_Title['Date']<=pd.Timestamp('2023-01-31'))]

df_dec_jan.head()

```
<br>
Output:
<br>
<br>

| **Date** |	**Instagram reach** | **Instagram profile visits** | **New Instagram followers** | **Title** | **Post type** | **Impressions** | **Reach** | **Shares** | **Follows** | **Likes** | **Comments** | **Saves** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2022-12-02 | 30583 | 1024 | 504 | How to find a good project idea? | IG video | 14050.0 | 14600.0 | 51 | 504 | 657 | 0 | 279 |
| 2022-12-03 | 32112 | 875 | 421 | What is Data Analytics? | IG video | 67050.0 | 67600.0 | 742 | 421 | 2800 | 38 | 335 |
| 2022-12-04 | 30851 | 829 | 475 | Why data is considered as valuable resource? | IG video | 10450.0 | 11000.0 | 26 | 475 | 454 | 3 | 388 |
| 2022-12-05 | 39611 | 1069 | 823 |	Coding Blocks | IG video | 20650.0 | 21200.0 | 271 | 823 | 720 | 7 | 334 |
| 2022-12-06 | 62370 | 1399 | 1418 | Is MEDIAN better than MEAN? | IG video | 16650.0 | 17200.0 | 50 | 1418 | 893 | 16 | 578 |

<br>
#### Define Aggregation Functions

```python

# Define aggregation functions
agg_funcs = {'Title': 'count', 'Impressions': 'mean', 'Reach': 'mean', 'Shares': 'mean', 'Likes': 'mean', 'Comments': 'mean', 'Saves': 'mean'}  # Example: 'sum', 'mean', 'median', 'min', 'max', etc.

df_dec_jan_pivot = round(pd.pivot_table(df_dec_jan, index = 'Post type', values = ['Title', 'Impressions', 'Reach', 'Shares', 'Likes', 'Comments', 'Saves'], aggfunc=agg_funcs))

df_dec_jan_pivot

```
<br>
Output:
<br>
<br>

| **Post type** | **Comments** | **Impressions** | **Likes** | **Reach** | **Saves** | **Shares** | **Title** |
|---|---|---|---|---|---|---|---|						
| IG video | 34.0 | 67288.0 | 2563.0 | 65636.0 | 697.0 | 1182.0 | 39 |

<br>

**Comments**: On average, the IG videos received 34 comments per video. This metric indicates the average level of engagement and interaction with the videos in terms of comments.

**Impressions**: On average, the IG videos garnered 67,288 impressions per video. Impressions refer to the average number of times the videos were viewed by users, whether or not they engaged with the content. This metric provides an indication of the average overall reach and visibility of the videos.

**Likes**: On average, the IG videos received 2,563 likes per video. Likes are a common engagement metric on Instagram, reflecting the average number of users who showed appreciation for the videos by liking them.

**Reach**: On average, the IG videos reached 65,636 users per video. Reach represents the average unique number of users who viewed the videos. It provides insights into the average audience reached by the videos, indicating the potential impact and exposure of the content.

**Saves**: On average, the IG videos were saved by 697 users per video. Saves represent the average number of times users saved the videos to their collections for later viewing. This metric reflects the average level of interest and value users found in the videos.

**Shares**: On average, the IG videos were shared by 1,182 users per video. Shares represent the average number of times users shared the videos with their own followers, extending the reach and potential exposure of the content.

During the period of Dec 2022 - Jan 2023, the duo have posted 39 IG videos. So the duo should post consistently the IG videos or reels

**Consistent upload of IG videos or reels have performed good for Data Analyst Duo**

<br>

# Analysing The Results  <a name="Club-results"></a>

```python
# Checking different types of posts released

# Define aggregation functions
agg_funcs = {'Title': 'count', 'Impressions': 'mean', 'Reach': 'mean', 'Shares': 'mean', 'Likes': 'mean', 'Comments': 'mean', 'Saves': 'mean'}  # Example: 'sum', 'mean', 'median', 'min', 'max', etc.

# Create pivot table
df_Title_pivot = round(pd.pivot_table(df_Title, index = 'Post type', values = ['Title', 'Impressions', 'Reach', 'Shares', 'Likes', 'Comments', 'Saves'], aggfunc=agg_funcs))

df_Title_pivot

```
<br>
Output:
<br>
<br>

| **Post type** | **Comments** | **Impressions** | **Likes** | **Reach** | **Saves** | **Shares** | **Title** |
|---|---|---|---|---|---|---|---|
| IG carousel |	40.0 | 41353.0 | 1574.0 | 30840.0 | 1879.0 | 235.0 | 9 |
| IG image | 44.0 |	61590.0 | 1356.0 | 58822.0 | 864.0 | 124.0 | 4 |
| IG video | 30.0 |	57058.0 | 2188.0 | 54507.0 | 636.0 | 924.0 | 51 |

<br>

Based on the given pivot table, the following observations and insights can be inferred:

Now "Reach" of IG image is higher than "IG video". So now should we start posting images instead of videos?

No. One thing we should understand here :

The 'IG image' post type has the highest average values for most of the metrics including 'Comments', 'Impressions', 'Likes', 'Reach', 'Saves', and 'Shares', compared to 'IG carousel' and 'IG video' post types. This suggests that 'IG image' posts may be performing better in terms of engagement on average compared to the other two types of posts. But the sample of 'IG image' is 4 compared to 'IG carousel' 9 and 'IG video' 51.

Let us look at the 'IG image' data once before we make any conclusion.

<br>
#### Inspect "IG image"


```python

df_Title[(df_Title['Post type']=='IG image')]

```
<br>
Output:
<br>
<br>

| **Date** |	**Instagram reach** | **Instagram profile visits** | **New Instagram followers** | **Title** | **Post type** | **Impressions** | **Reach** | **Shares** | **Follows** | **Likes** | **Comments** | **Saves** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2022-09-15 | 36445 | 832 | 153 | time allocation to study | IG image | 169062.0 | 164673.0 | 438 | 481 | 2450 | 46 | 3181 |
| 2022-10-02 | 29154 | 914 | 347 | your favourite data couple | IG image | 20346.0 | 19026.0 | 6 | 24 | 817 | 8 | 12 |
| 2023-03-27 | 19409 | 637 | 117 | Introduction post | IG image | 22446.0 | 20500.0 | 12 | 4 | 1566 | 34 | 47 |
| 2023-04-09 | 20627 | 695 | 160 | Statistics for data analysis workshop | IG image | 34504.0 | 31088.0 | 41 | 7 | 592 | 88 | 216 |

<br>

If you see the title **time allocation to study** has more reach compared to other posts. So if you see this post it reached almost 160K people whereas others have reached around 20-30k. So this is one of the post which got **viral**. What will we term this "time allocation to study" as?

It's called an **Outlier**. By the way its not an harmful outlier it is naturally occuring. 

Now let's remove this title and compare the results again

<br>
#### Removing Title of a post

```python

df_IG_image = df_Title[(df_Title['Post type']=='IG image') & (df_Title['Title']!= 'time allocation to study')]
df_IG_image

```
<br>
Output:
<br>
<br>

| **Date** |	**Instagram reach** | **Instagram profile visits** | **New Instagram followers** | **Title** | **Post type** | **Impressions** | **Reach** | **Shares** | **Follows** | **Likes** | **Comments** | **Saves** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 2022-10-02 | 29154 | 914 | 347 | your favourite data couple | IG image | 20346.0 | 19026.0 | 6 | 24 | 817 | 8 | 12 |
| 2023-03-27 | 19409 | 637 | 117 | Introduction post | IG image | 22446.0 | 20500.0 | 12 | 4 | 1566 | 34 | 47 |
| 2023-04-09 | 20627 | 695 | 160 | Statistics for data analysis workshop | IG image | 34504.0 | 31088.0 | 41 | 7 | 592 | 88 | 216 |

<br>
#### Pivot Table of IG_Image

```python

df_IG_image = round(pd.pivot_table(df_IG_image, index = 'Post type', values = ['Impressions', 'Reach', 'Shares', 'Likes', 'Comments', 'Saves'], aggfunc=np.mean))
df_IG_image

```
<br>
Output:
<br>
<br>

| **Post type** | **Comments** | **Impressions** | **Likes** | **Reach** | **Saves** | **Shares** | **Title** |
|---|---|---|---|---|---|---|---|
| IG image | 43.0 | 25765.0 | 992.0 | 23538 | 92.0 | 20.0 |

<br>
Now we can see the impressions and reach are reduced to around 25k and 23k. Before it was 61k and 58k around.
Now we can understand how an **Outlier** data point affect an entire data.

<br>
#### Exclude post with title 'time allocation to study'

```python

df_Title = df_Title[(df_Title['Title']!= 'time allocation to study')]

# Create pivot table
df_Title_pivot = round(pd.pivot_table(df_Title, index = 'Post type', values = ['Title', 'Impressions', 'Reach', 'Shares', 'Likes', 'Comments', 'Saves'], aggfunc=agg_funcs))
df_Title_pivot

```
<br>
Output:
<br>
<br>

| **Post type** | **Comments** | **Impressions** | **Likes** | **Reach** | **Saves** | **Shares** | **Title** |
|---|---|---|---|---|---|---|---|
| IG carousel |	40.0 | 41353.0 | 1574.0 | 30840.0 | 1879.0 | 235.0 | 9 |
| IG image | 43.0 | 25765.0 | 992.0 | 23538.0 | 92.0 | 20.0 | 3 |
| IG video | 30.0 | 57058.0 | 2188.0 | 54507.0 | 636.0 | 924.0 | 51 |

<br>
Based on the given pivot table, the following observations and insights can be inferred:

* The 'IG video' post type has the highest average values for most of the metrics including 'Impressions', 'Likes', 'Reach' and 'Shares' compared to 'IG carousel' and 'IG image' post types. 
* It appears that 'IG video' posts are performing better in terms of engagement compared to 'IG image' and 'IG carousel' posts for Data Analyst Duo.
* If they consistently post IG videos, the duo would get good results.

**Shares--->Reach-->Impressions-->New followers**

With respect to Reach and Impressions, New followers can be gained if they put IG Videos but inorder to **engage the existing audience of the page, data analyst duo should post IG carousel because of high number of Comments and Saves**

### I would suggest the Duo to go with IG Videos followed by IG Carousel by posting consistently

___
<br>
# Growth & Next Steps <a name="growth-next-steps"></a>

Social media feeds (specifically what people/posts you see when you log on) are driven by an algorithm but these can change from time to time.  For example, on LinkedIn, there was a time when polls got a huge amount of reach, then it became sharing PDF documents. The algorithm was being changed behind the scenes to up-weight or down-weight certain types of **post type**.

As of now IG videos/reels, act as better engagement widely in general.

In future, there might be possibilities that they may change the algorithm to favor image posts or some newly discovered **post type** which can act as better engagement for the users

So keeping this analysis up to date would help the user keep close to what was working **now** rather than what **worked several months ago**.

Also, diving deeper into **IG videos** to understand which **topics** got the most traction helps the duo in creating more content towards those topics.
