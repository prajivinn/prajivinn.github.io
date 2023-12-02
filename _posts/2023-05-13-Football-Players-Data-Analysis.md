---
layout: post
title: Analyzing Football Players using Central Tendency and Dispersion
image: "/posts/fa.png"
tags: [Measures of Central Tendency, Measures of Dispersion, Python]
---

In this project we apply measures of Central Tendency & Dispersion to suggest two players for the Striker position!

# Table of contents

- [00. Project Overview](#overview-main)
    - [Context](#overview-context)
    - [Actions](#overview-actions)
    - [Results](#overview-results)
- [01. Concept Overview](#concept-overview)
- [02. Data Overview & Preparation](#data-overview)
- [03. Applying Measures of Central Tendency & Dispersion](#Cent-Disp-application)
- [04. Analysing The Results](#player-results)

___

# Project Overview  <a name="overview-main"></a>

### Context <a name="overview-context"></a>

Manchester United football club wants to know which player they should sign for the Striker position from the list provided. We need to perform a comparative Analysis between players and suggest two players whom they should sign.

**Additional Note:** 

* One of the players should be **less than 25 years of age**.
* One of the players should have preferably played in the **English Premier League**.
<br>
<br>

### Actions <a name="overview-actions"></a>

We started inspecting the data to see any null values are present with help of .info() method. Based on the additional note, we created a column "Age Group" assigning a condition to players based on their age. We then found the value counts with respect to the "Age Group". We found there are 6 players who are below 25 years of Age. We also found value counts of players who played in English premier league. There are 3 players who played in EPL.

We then calculated the total contribution of each player based on **total number of goals** and **total number of assists** to get an understanding of player's contribution. While this can be a useful thing with respect to a player, it will not help in concluding that this is the best player. Further, we went in detail to understand their performances.

With respect to the measures of central tendency(Mean, Median, Mode), we calculated the mean(average) of columns such as  no.of shots, PS%, AerialsWon and Rating for each player but it turns out there are no clear differences between the players. Then we calculated the Mean, Median and Mode of "Ratings" column for each player but again most of the ratings are similar.

We finally used **Measures of Central tendency** in conjugation with **Measures of Dispersion** i.e using Variance and Standard Deviation to find the ratings of the players.
<br>
<br>

### Results <a name="overview-results"></a>

We found two players **Dusan Vlahovic** & **Harry Kane** who are selected for the striker position.

___

# Concept Overview  <a name="concept-overview"></a>

<br>
#### Measures of Central Tendency

* A measure of central tendency is a single value that attempts to describe a set of data by identifying the central position within that set of data.
* As such, measures of central tendency are sometimes called measures of central location.
* Example : Mean, Median & Mode.

<br>
**Mean**

Mean is a single number taken as representative of a list of numbers. It can be represented with symbol mu (µ)

<br>
**Median**

Median is the middle number of series when ordered.
Finding median in three steps:
* Arrange the numbers from largest to smallest.
* If you have an odd number of values, the median is the middle one.
* if you have an even number of values, the median is calculated by adding the two middle numbers together and divided by 2

<br>
**Mode**

The observation with highest frequency.

<br>

#### Measures of Dispersion

* Measures of Central Tendency yield information about center or middle part of a dataset.
* The measure of dispersion describes the spread of data.
* The measure of dispersion in conjuction with measures of central tendency makes possible a more complex numerical description of data
* For example : Range, Standard Deviation etc.

<br>
**Range**

Range is the difference between largest and smallest value.

<br>
**Quartiles**

The quartiles of a data set divide the data into four equal parts, with one-fourth of the data values in each part. The second quartile position is the median of the data set, which divides the data set in half.

To find the quartiles, you need to follow these steps:
* Sort the dataset in ascending order.
* Calculate the position of each quartile using the following formulas:
  a. Q1: (n + 1) / 4
  b. Q2 (Median): (n + 1) / 2
  c. Q3: 3 * (n + 1) / 4
  where n is the total number of data points in the dataset.
* If the position calculated in Step 2 is a whole number, the corresponding quartile is the value at that position in the sorted dataset. If the position is a decimal, take the average of the two values at the positions on either side of the decimal to find the quartile.

<br>
**Inter Quartile Range**

IQR is especially useful in a situation where data users are more interested in values toward the middle and less interested in
extremes. IQR is also used to identify outliers.

* To get around this, we divided the data into quarters, and we used the interquartile range to provide us with a cut-down range of the data.
* The range of the values in these two quartiles is called the interquartile range (IQR = Q3-Q1).

<br>
**Outliers**

Outliers are values which are extreme above or below a set of values. Outliers are occured in three Ways:

* Measurement Error

--> Human errors caused during data collection or recording

--> For example, while filling up a survey form, the respondent entered his age as 500 years instead of 50 years. The additional zero made him an outlier.

* Sampling Error

--> The error occurs when the sample does not represent the entire population.

--> We have to conduct a survey regarding the durability of iphones, our sample will consist of respondents who use iphones and not Android phones.

* Natural Error

--> When an outlier is not caused due to an error but occurs naturally.

--> In a Class of 50 Students, 2 Students passed the test and the rest 48 failed. Now the students who performed excellently and passed are outliers, but they are not caused due to an error.

<br>
**Skewness**

Skewness is a measure of the asymmetry or lack of symmetry in the data distribution. It tells us how the data is stretched out on one side compared to the other. Skewness can be positive, negative, or zero.

* Positive Skewness: In a positively skewed distribution, the tail on the righthand side is longer or stretched out, and most of the data is concentrated on the left. This is also known as a right-skewed distribution.
* Negative Skewness: In a negatively skewed distribution, the tail on the lefthand side is longer or stretched out, and most of the data is concentrated on the right. This is also known as a left-skewed distribution.
* Zero Skewness: If the data is symmetric and has a balanced distribution around the mean, it has zero skewness.

<br>
**Percentiles**

* Percentiles are measures of central tendency that divide a group of data into 100 parts.
* There are 99 percentiles because it takes 99 dividers to separate a group of data into 100 parts.
* Percentile is widely used in reporting test results.

<br>
**Variance**

* Variance is a way of measuring spread, and it's the average of the distance of values from the mean squared.
* The problem with variance is that it can be quite difficult to think about the spread in terms of distances squared.

<br>
**Standard Deviation**

* Standard Deviation is the square root of Variance.
* The Standard Deviation is expressed in the same units as the mean is , whereas the variance is expressed in squared units.

___

<br>
# Data Overview & Preparation  <a name="data-overview"></a>

This dataset contains stats for 10 football players from Europe's top leagues. I will use this data to solve the following problem statement.

In the code below, we:

* Load in the Python libraries we require for importing the data.
* Import the required data.

<br>
```python

# install the required python libraries
import pandas as pd
import numpy as np

# import Players data
df = pd.read_excel(r'/Users/praju/Desktop/DADUO/projects/Players data.xlsx')

df.head()

```
<br>
A sample of this data (the first 5 rows) can be seen below:
<br>
<br>

| **Player Name** |	**Age** | **Current Club** | **Opponent** | **competition** | **Date** | **Position** | **Mins** | **Goals** | **Assists** | **Yel** | **Red** | **Shots** | **PS%** | **AerialsWon** | **Rating** |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Aleksandar Mitrovic |	28 | Fulham | Brentford (A)3 - 2 | Premier League | 2023-06-03 00:00:00 | FW | 90 | 0 | 0 | 1 | 0 |	1 | 54.8 | 2 | 6 |
| Aleksandar Mitrovic |	28 | Fulham | Newcastle (A)1 - 0 | Premier League | 15-01-2023 | FW | 90 | 0 | 0 | 0 | 0 | 3 | 75.0 | 2 | 5 |
| Aleksandar Mitrovic |	28 | Fulham | Tottenham (A)2 - 1 | Premier League | 2022-03-09 00:00:00 | FW | 90 | 1 | 0 | 1 | 0 | 5 | 50.0 | 2 | 7 |
| Aleksandar Mitrovic |	28 | Fulham | Tottenham (H)0 - 1 | Premier League | 23-01-2023 | FW | 90 | 0 | 0 | 0 | 0 | 2 | 57.9 | 3 | 6 |
| Aleksandar Mitrovic | 28 | Fulham | Southampton (H)2 - 1 | Premier League | 31-12-2022 | FW | 90 | 0 | 0 | 0 | 0 | 2 | 68.0 | 3 | 6 |

<br>
Data Dictionary:

* Player Name: Name of the player
* Age: The age of the player
* Current Club: Name of the club that the player currently plays for
* Opponent: Name of the team that the player played against
* Competition: Name of the competition.
* Date: Date of the match played
* Position: Playing position of the player
* Mins: Minutes played
* Goals: Total goals
* Assists: Total assists
* Yel: Yellow card
* Red: Red card
* Shots: Total shots
* PS%: Pass success percentage
* AerialsWon: Aerial duels won
* Rating: Rating per match


___

<br>
# Applying Measures of Central Tendency & Dispersion <a name="Cent-Disp-application"></a>

<br>
#### Datatypes and Null values 

The very first thing we do is make sure the data types are correct and there are no null values present.

```python

# Get more information about datatypes and null values in the dataframe

df.info()

```

<br>
Output:
<br>
<br>

| **Column** | **Non-Null** | **Count** | **Dtype** |  
|---|---|---|---|
| Player Name | 289 | non-null | object | 
| Age | 289 | non-null | int64 |  
| Current Club | 289 | non-null | object | 
| Opponent | 289 | non-null | object | 
| competition | 289 | non-null | object | 
| Date | 289 | non-null | object | 
| Position | 289 | non-null | object | 
| Mins | 289 | non-null | int64 |  
| Goals | 289 | non-null | int64 |  
| Assists | 289 | non-null | int64 |  
| Yel | 289 | non-null | int64 |  
| Red | 289 | non-null | int64 |  
| Shots | 289 | non-null | int64 |  
| PS% | 289 | non-null | float64 |
| AerialsWon | 289 | non-null | int64 |  
| Rating | 289 | non-null | int64 |

<br>
We can see there are 289 non-null values in each column, indicating that there are no missing values.

<br>
#### Calculating Frequency

We will start with basic checks i.e count of values.

```python

df['Age_Group']=np.where(df['Age']>=25,'>= 25 years','< 25 years')
df.groupby('Age_Group')['Player Name'].nunique()

```

<br>
Output:
<br>
<br>

| **Age_Group** | **Count** |
|---|---|
| < 25 years | 6 |
| >= 25 years | 4 |

<br>
We can see:

* There are 6 players who are below 25 years.
* There are 4 players who are above or equal 25 years.

<br>
#### Number of Players played in EPL

Checking the number of players played in English Premier League.

```python

df.groupby('competition')['Player Name'].nunique()

```

<br>
Output:
<br>
<br>

| **competition** | **Count** |
|---|---|
| Bundesliga | 2 |
| Champions League | 5 |
| Europa League | 1 |
| Liga Portugal | 1 |
| Ligue 1 | 1 |
| Premier League | 3 |
| Seria A | 3 |

<br>
We can see :

* 3 Players played in English Premier League.

<br>
#### Number of goals & assists

Checking the number of goals & assists scored by each player.

```python

tc = df.groupby('Player Name')[['Goals','Assists']].agg('sum')
tc = pd.DataFrame(tc).reset_index()
tc

```

<br>
Output:
<br>
<br>

| **Player Name** | **Goals** | **Assists** |
|---|---|---|
| Aleksandar Mitrovic |	11 | 1 |
| Dusan Vlahovic | 11 |	4 |
| Gonçalo Ramos | 20 | 3 |
| Harry Kane | 24 | 4 |
| Ivan Toney | 18 | 4 |
| Jonathan David | 19 | 4 |
| Marcus Thuram | 13 | 4 |
| Randal Kolo Muani | 14 | 10 |
| Rasmus Højlund | 7 | 2 |
| Victor Osimhen | 25 | 4 |

<br>
#### Total Contribution ####

Calculating total contribution of each player.


```python

tc['Total Contribution'] = tc['Goals']+tc['Assists']
tc.sort_values(by='Total Contribution',ascending=False)

```

<br>
Output:
<br>
<br>

| **Player Name** | **Goals** |	**Assists** | **Total Contribution** |
|---|---|---|---|
| Victor Osimhen | 25 | 4 | 29 |
| Harry Kane | 24 | 4 | 28 |
| Randal Kolo Muani | 14 | 10 |	24 |
| Gonçalo Ramos | 20 | 3 | 23 |
| Jonathan David | 19 | 4 | 23 |
| Ivan Toney | 18 | 4 | 22 |
| Marcus Thuram | 13 | 4 | 17 |
| Dusan Vlahovic | 11 | 4 | 15 |
| Aleksandar Mitrovic | 11 | 1 | 12 |
| Rasmus Højlund | 7 | 2 | 9 |

<br>
We can find :

* Victor Osimhen & Harry Kane are top 2 in goals.
* Randal Kolo Muani is at top for assists.
* Six players with goal contribution more than 20.

So can we suggest the players to clients based on goals & Assists? 
No, We need to go in detail to understand their performance.

<br>
#### Apply Average

Check the average no.of shots, PS%, AerialsWon & Ratings per match by each player.

```python

others = df.groupby('Player Name')[['Shots','PS%','AerialsWon','Rating']].agg('mean').round(0).astype('int')
others = pd.DataFrame(others).reset_index()
others

```

<br>
Output:
<br>
<br>

| **Player Name** | **Shots** | **PS%** | **AerialsWon** | **Rating** |
|---|---|---|---|---|
| Aleksandar Mitrovic |	4 | 60 | 4 | 7 |
| Dusan Vlahovic | 3 | 71 | 1 | 6 |
| Gonçalo Ramos | 3 | 73 | 2 | 7 |
| Harry Kane | 3 | 71 | 2 | 7 |
| Ivan Toney | 3 | 62 | 4 | 7 |
| Jonathan David | 3 | 83 | 0 |	7 |
| Marcus Thuram | 3 | 73 | 1 | 7 |
| Randal Kolo Muani | 2 | 66 | 2 | 7 |
| Rasmus Højlund | 2 | 73 | 1 | 6 |
| Victor Osimhen | 4 | 72 | 2 | 7 |

<br>
We can see:

* Average shots per match : Mitrovic & Osimhen
* Average PS% per match : David, Ramos, Thuram, Hojlund
* Average AerialsWon per match : Mitrovic,Toney
* Average Rating : Multiple Players , there are no clear difference in rating if you see , most of them got either 7 or 6 rating. Out of 10 players, 2 of them with 6 rating.

***Average offers you only one-dimensional view of your data. They tell you what the center of your data is, but that's it. 
While this can be useful, its often not enough.***

<br>
#### Calculating Mean, Median & Mode of Rating

Checking mean, median & mode ratings by each player

```python

mmm = df.groupby(['Player Name'])['Rating'].agg(['mean','median']).round(0).astype('int')
mmm = pd.DataFrame(mmm).reset_index()
mmm1 = df.groupby('Player Name')['Rating'].apply(pd.Series.mode).to_frame()
mmm1 = mmm1.reset_index()
del mmm1['level_1']
mmm1.drop_duplicates(subset=['Player Name'],keep='first',inplace=True)
mmm1=mmm1.reset_index()
mmm['mode']=mmm1['Rating']
mmm

```

<br>
Output:
<br>
<br>

| **Player Name** | **mean** | **median** | **mode** |
|---|---|---|---|
| Aleksandar Mitrovic |	7 | 7 |	6 |
| Dusan Vlahovic | 6 | 6 | 6 |
| Gonçalo Ramos | 7 | 7 | 7 |
| Harry Kane | 7 | 7 | 7 |
| Ivan Toney | 7 | 6 | 6 |
| Jonathan David | 7 | 6 | 6 |
| Marcus Thuram | 7 | 7 | 6 |
| Randal Kolo Muani | 7 | 7 | 6 |
| Rasmus Højlund | 6 | 6 | 6 |
| Victor Osimhen | 7 | 7 | 7 |

<br>
We can see:

* Mean, Median, Mode are same for most of the players. so it is difficult for us to identify players with a difference.

**Note:**

* Mean, Median, Mode can provide information about the "Center" of data.
* Mean is most commonly used, however median can sometimes be a better measure.
* Mean can be easily influenced by extreme values, so be careful.
* Look for large difference between mean and median. Could be a warning sign.


<br>
#### Quartiles & Percentiles

Using Quartiles & percentiles on data to see if there is a difference in players.

```python

qp=df.groupby('Player Name')['Rating'].quantile([0.25,0.5,0.75,0.8,0.9])
qp=pd.DataFrame(qp).reset_index()
qp.head(20)

```

<br>
Output of first 20 rows:
<br>
<br>

| **Player Name** | **level_1** | **Rating** |
|---|---|---|
| Aleksandar Mitrovic |	0.25 | 6.0 |
| Aleksandar Mitrovic |	0.50 | 7.0 |
| Aleksandar Mitrovic |	0.75 | 7.0 |
| Aleksandar Mitrovic |	0.80 | 7.0 |
| Aleksandar Mitrovic |	0.90 | 8.0 |
| Dusan Vlahovic | 0.25 | 6.0 |
| Dusan Vlahovic | 0.50 | 6.0 |
| Dusan Vlahovic | 0.75 | 7.0 |
| Dusan Vlahovic | 0.80 | 7.0 |
| Dusan Vlahovic | 0.90 | 7.2 |
| Gonçalo Ramos | 0.25 | 6.0 |
| Gonçalo Ramos | 0.50 | 7.0 |
| Gonçalo Ramos | 0.75 | 7.0 |
| Gonçalo Ramos | 0.80 | 7.8 |
| Gonçalo Ramos | 0.90 | 8.0 |
| Harry Kane | 0.25 | 6.0 |
| Harry Kane | 0.50 | 7.0 |
| Harry Kane | 0.75 | 7.0 |
| Harry Kane | 0.80 | 7.0 |
| Harry Kane | 0.90 | 8.0 |

<br>
We can see:

* Nothing much can be inferred.
* We need some other way of summarizing the data in addition to the measures of central tendency.

<br>
#### Applying measures of Dispersion

Range - uses smallest & largest number in a set. The rest of the values are ignored.

```python

r1 = df.groupby('Player Name')['Rating'].agg(['max','min'])
r1 = pd.DataFrame(r1).reset_index()
r1['Range']=r1['max']-r1['min']
r1

```

<br>
Output:
<br>
<br>

| **Player Name** | **max** | **min** | **Range** |
|---|---|---|---|
| Aleksandar Mitrovic |	9 | 5 |	4 |
| Dusan Vlahovic | 8 | 5 | 3 |
| Gonçalo Ramos | 10 | 5 | 5 |
| Harry Kane | 9 | 6 | 3 |
| Ivan Toney | 10 | 5 | 5 |
| Jonathan David | 9 | 6 | 3 |
| Marcus Thuram | 8 | 5 | 3 |
| Randal Kolo Muani | 9 | 5 | 4 |
| Rasmus Højlund | 9 | 5 | 4 |
| Victor Osimhen | 9 | 5 | 4 |

<br>
We can see:

* Nothing can be inferred.

**Note**:

* Main problem with range is that it may include outliers
* If data has outliers, the range will include them, even though there may be only one or two extreme values, that could lead to a misleading result.
* The range can measure how far the values are spread out, but its difficult to get a real picture of how the data is distributed.

<br>
#### Calculating IQR

Checking IQR for each player

```python

iqr = df.groupby('Player Name')['Rating'].describe().drop(columns = ['min','max','mean','count','std','50%']).round(0).astype('int')
iqr = pd.DataFrame(iqr)
iqr['IQR'] = iqr['75%']-iqr['25%']
iqr

```

<br>
Output:
<br>
<br>

| **Player Name** | **25%** | **75%** | **IQR** |	
|---|---|---|---|
| Aleksandar Mitrovic |	6 | 7 |	1 |
| Dusan Vlahovic | 6 | 7 | 1 |
| Gonçalo Ramos | 6 | 7 | 1 |
| Harry Kane | 6 | 7 | 1 |
| Ivan Toney | 6 | 7 | 1 |
| Jonathan David | 6 | 7 | 1 |
| Marcus Thuram	| 6 | 7 | 1 |
| Randal Kolo Muani | 6 | 7 | 1 |
| Rasmus Højlund | 6 | 7 | 1 |
| Victor Osimhen | 7 | 8 | 1 |

<br>
We can see:

* Nothing can be inferred.

<br>
#### Calculating Variance & Dispersion

In this step we need to find the ratings which vary the least

```python

vsd = df.groupby('Player Name')['Rating'].agg(['var','std']).round(2)
vsd = pd.DataFrame(vsd)
vsd.sort_values(by='std')

```

<br>
Output:
<br>
<br>

| **Player Name** | **Var** | **Std** |
|---|---|---|
| Dusan Vlahovic | 0.64 | 0.80 |
| Harry Kane | 0.64 | 0.80 |
| Marcus Thuram | 0.70 | 0.84 |
| Rasmus Højlund | 0.79 | 0.89 |
| Randal Kolo Muani | 0.92 | 0.96 |
| Jonathan David | 0.98 | 0.99 |
| Gonçalo Ramos	| 1.02 | 1.01 |
| Aleksandar Mitrovic |	1.13 | 1.06 |
| Ivan Toney | 1.14 | 1.07 |
| Victor Osimhen | 1.24 | 1.11 |

<br>
We can see:

* As the standard deviation is high, the values tend to be away from the mean
* As the standard deviation is low, the values tend to be closer to the mean

###### As per the insights obtained from the above output, we can say the players 'Dusan Vlahovic' & 'Harry Kane' are closer to the Mean i.e their performance is consistent which indicates the ratings of these two players vary the least.

___

<br>

# Analysing The Results  <a name="player-results"></a>

#### Checking the players who played in different clubs

```python

df1=df[['Player Name','Age','competition']]
df1.groupby(['Player Name','Age'])['competition'].unique()

```

<br>
Output:
<br>
<br>

| **Player Name** | **Age** | **Clubs** |
|---|---|---|
| Aleksandar Mitrovic | 28 | [Premier League] |
| Dusan Vlahovic | 23 | [Seria A, Champions League, Europa League] |
| Gonçalo Ramos | 21 | [Liga Portugal, Champions League] |
| Harry Kane | 29 | [Premier League, Champions League] |
| Ivan Toney | 27 | [Premier League] |
| Jonathan David | 23 | [Ligue 1] |
| Marcus Thuram | 25 | [Bundesliga] |
| Randal Kolo Muani | 24 | [Bundesliga, Champions League] |
| Rasmus Højlund | 20 | [Seria A] |
| Victor Osimhen | 24 | [Seria A, Champions League] |

<br>
We can see:

* Players who played in different clubs

As per the Client Requirements: 

* One of the players should be less than 25 years of age - We can see '**Dusan Vlahovic**' whose age is less than 25.
* One of the players should have preferably played in the English Premier League - We can see '**Harry Kane**' who played in the English Premier League.

<br>

It is also important to note that we should also consider **total number of matches played by each player**, then only standard deviation will be more effective.


```python

df1['Player Name'].value_counts()

```

<br>
Output:
<br>
<br>

| **Player Name** | **Count** |
|---|---|
| Harry Kane | 38 |
| Randal Kolo Muani | 33 |
| Gonçalo Ramos | 32 |
| Jonathan David | 29 |
| Dusan Vlahovic | 29 |
| Victor Osimhen | 28 |
| Ivan Toney | 28 |
| Marcus Thuram | 26 |
| Rasmus Højlund | 25 |
| Aleksandar Mitrovic | 21 |

<br>
We can see:

* Harry Kane - played **38 matches**.
* Dusan Vlahovic - played **29 matches**.

##### Two players 'Dusan Vlahovic' & 'Harry Kane' are the finalists for the striker position!!!














































