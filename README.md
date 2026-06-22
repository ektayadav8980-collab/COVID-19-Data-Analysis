# COVID-19 Global Data Analytics Dashboard

## Comprehensive Data Analysis & Visualization of the Global Pandemic  

## 📌 Project Overview

This project is an in depth exploratory data analysis (EDA) of COVID-19 data across 180+ countries and regions worldwide. Using Python based data analytics tools, we uncover pandemic trends, mortality rates, recovery patterns, and regional disparities to provide actionable insights into the global health crisis.

## Why This Matters: 
The COVID-19 pandemic generated massive datasets. By systematically analyzing this data, we can understand disease progression, identify high risk regions, and track recovery patterns skills essential for real-world data analytics roles.

## 🎯 Problem Statement

## The Challenge:

Raw COVID-19 data exists in isolation thousands of data points across countries and time periods. To extract meaning, we need to ask critical questions:
<br>1. Which countries have the highest mortality rates?
<br>2. What is the correlation between confirmed cases and deaths?
<br>3. Which regions show the fastest recovery rates?
<br>4. How do active cases vary geographically?
<br>5. Are there regional patterns in case fatality rates?


## Our Approach:

Transform raw data into visual insights that tell the pandemic story through:


Statistical analysis
<br>
Comparative visualizations
<br>
Regional trend identification
<br>
Key performance indicator (KPI) calculation

## 📊 Dataset Description

Source: Public COVID-19 dataset (Kaggle / Johns Hopkins)
<br>Contains:
<br>Date-wise records
<br>Country/Region
<br>Confirmed, Deaths, Recovered

## 🔍 Key Business Insights
## Identify global hotspots:
Rank countries by confirmed cases, deaths, and active infections
## Quantify severity metrics:
Calculate and analyze mortality and recovery rates
## Regional benchmarking: 
Compare pandemic impact across WHO regions
## Growth trajectory analysis: 
Measure weekly case growth and acceleration rates
## Predictive insights:
Establish baseline metrics for epidemiological monitoring

# Setup
We will be using Numpy, Pandas, Matplotlib and Seaborn.Let’s begin:

```python
# Import Libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```
## Loading the data
COVID-19 data, including confirmed cases, deaths, and recoveries across different countries and time periods.

The data is loaded using the Pandas library for efficient data manipulation and analysis.
```python
# Load dataset
import pandas as pd
df = pd.read_csv(r"C:\Users\admin\Downloads\country_wise_latest.csv")
```
## 🔍 Dataset Overview
To understand the structure and quality of the dataset, we perform initial inspection:
```python
1  df.info()

<class 'pandas.core.frame.DataFrame'>
RangeIndex: 187 entries, 0 to 186
Data columns (total 15 columns):
 #   Column                  Non-Null Count  Dtype  
---  ------                  --------------  -----  
 0   Country/Region          187 non-null    object 
 1   Confirmed               187 non-null    int64  
 2   Deaths                  187 non-null    int64  
 3   Recovered               187 non-null    int64  
 4   Active                  187 non-null    int64  
 5   New cases               187 non-null    int64  
 6   New deaths              187 non-null    int64  
 7   New recovered           187 non-null    int64  
 8   Deaths / 100 Cases      187 non-null    float64
 9   Recovered / 100 Cases   187 non-null    float64
 10  Deaths / 100 Recovered  187 non-null    float64
 11  Confirmed last week     187 non-null    int64  
 12  1 week change           187 non-null    int64  
 13  1 week % increase       187 non-null    float64
 14  WHO Region              187 non-null    object 
dtypes: float64(4), int64(9), object(2)
memory usage: 22.0+ KB


2  df.describe()



	  Confirmed	Deaths   Recovered 	   Active   	 New cases   	New deaths	 New recovered	Deaths / 100 Cases	Recovered / 100 Cases	Deaths / 100 Recovered	Confirmed  last week	  1 week change	1 week % increase
count  	1.870000e+02	 187.000000	   1.870000e+02	 1.870000e+02	187.000000	 187.000000	    187.000000	        187.000000	            187.000000	             187.00	   1.870000e+02	  187.000000	187.000000
mean  	8.813094e+04	 3497.518717   5.063148e+04	 3.400194e+04	1222.957219	 28.957219	    933.812834	        3.019519	            64.820535	             inf	   7.868248e+04	  9448.459893	13.606203
std	    3.833187e+05	 14100.002482  1.901882e+05	 2.133262e+05	5710.374790	 120.037173	    4197.719635	        3.454302	            26.287694	             NaN	   3.382737e+05	  47491.127684	24.509838
min   	1.000000e+01	 0.000000	   0.000000e+00	 0.000000e+00	0.000000	 0.000000	    0.000000    	    0.000000	            0.000000	             0.00	   1.000000e+01	  -47.000000	-3.840000
25%   	1.114000e+03     18.500000     6.265000e+02	 1.415000e+02	4.000000	 0.000000	    0.000000    	    0.945000	            48.770000	             1.45	   1.051500e+03	  49.000000	    2.775000
50%	    5.059000e+03	 108.000000    2.815000e+03	 1.600000e+03	49.000000	 1.000000	    22.000000	        2.150000	            71.320000            	 3.62	   5.020000e+03	  432.000000	6.890000
75%	    4.046050e+04	 734.000000	   2.260600e+04	 9.149000e+03	419.500000	 6.000000	    221.000000      	3.875000	            86.885000	             6.44	   3.708050e+04	  3172.000000	16.855000
max   	4.290259e+06	 148011.000000 1.846641e+06	 2.816444e+06	56336.000000 1076.000000	33728.000000  	    28.560000	            100.000000       	     inf	   3.834677e+06	 455582.000000	226.320000

```

## Exploration
```python
1   df.shape


1   (187, 15)
```
187 columns, 15 of which are countries and regions. The rest are output from the PCA transformation. Let’s check for missing values and data consistency::
```python
# Check Null Values
1   df.isnull().sum()


1   Country/Region            0
2   Confirmed                 0
3   Deaths                    0
4   Recovered                 0
5   Active                    0
6   New cases                 0
7   New deaths                0
8   New recovered             0
9   Deaths / 100 Cases        0
10  Recovered / 100 Cases     0
11  Deaths / 100 Recovered    0
12  Confirmed last week       0
13  1 week change             0
14  1 week % increase         0
15  WHO Region                0
16  dtype: int64
```
## Handling Duplicate Records
Ensuring data quality is a critical step in any data analysis project. Duplicate records can lead to biased results, incorrect aggregations, and misleading insights.To identify duplicate entries in the dataset df.duplicated() is used.
df.duplicated() scans the dataset row by row and flags duplicate records as True.
sum() aggregates these values to return the total number of duplicate rows.

In Python, True = 1 and False = 0, so summing gives the total duplicate count.
```python
# Check Duplicate Records
1  df.duplicated().sum()

1  np.int64(0)
```
## Data Preprocessing(Renaming Columns)
To improve readability and ensure consistency in column naming, spaces in column names were replaced with underscores.
```python
# Rename Columns
df.columns = df.columns.str.replace(" ","_")
```
## Top 10 Countries by Confirmed COVID-19 Cases
To identify the most affected regions, the dataset was sorted based on the total number of confirmed COVID-19 cases in descending order. The top 10 countries were then extracted for focused analysis.
```python
# Top 10 Countries by Confirmed Cases
top_cases = df.sort_values(
    by='Confirmed',
    ascending=False
).head()
```
To identify the most impacted regions, the top 10 countries were extracted based on the highest number of confirmed COVID-19 cases.A horizontal bar chart is used to clearly compare countries by confirmed cases.
```python
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Top 10 Countries by Confirmed Cases

top10 = df.nlargest(10, 'Confirmed')

plt.figure(figsize=(10,6))

sns.barplot(
    data=top10,
    x='Confirmed',
    y='Country/Region',
    hue='Country/Region',
    palette='viridis',
    legend=False
)

plt.title('Top 10 Countries by Confirmed Cases')
plt.xlabel('Confirmed Cases')
plt.ylabel('Country')
plt.show()
```
<img width="1362" height="669" alt="top10_Confirmed_cases" src="https://github.com/user-attachments/assets/8598d84d-a575-467d-96b0-f935b5435aab" />

The goal of this analysis is to identify and visualize the top 10 countries with the highest number of COVID-19 deaths, helping understand the global impact of the pandemic.
```python
# Top 10 Countries by Deaths
top10_deaths = df.nlargest(10,'Deaths')

plt.figure(figsize=(10,6))
sns.barplot(data=top10_deaths,
            x='Deaths',
            y='Country/Region',
            hue='Country/Region',
            palette='viridis',
    legend=False
)

plt.title('Top 10 Countries by Deaths')
plt.xlabel('Deaths')
plt.ylabel('Country')
plt.show()
```
<img width="1449" height="753" alt="Top 10 Countries by Deaths" src="https://github.com/user-attachments/assets/d209d5e4-3971-4285-af2d-4d3eb6e4b1cd" />

## WHO Region Analysis (COVID-19)
This analysis focuses on understanding how COVID-19 cases are distributed across different WHO regions, helping identify the most affected global regions.
```python
# WHO Region Analysis
region = df.groupby(
'WHO_Region'
)['Confirmed'].sum()
```
To visualizes the distribution of confirmed COVID-19 cases across WHO regions using a pie chart, making it easy to understand each region's contribution to global cases.Regions like Americas / Europe (depending on dataset) usually contribute the largest share
```python
# WHO Region Distribution 
region_cases = df.groupby('WHO_Region')['Confirmed'].sum()

plt.figure(figsize=(8,8))
plt.pie(region_cases,
        labels=region_cases.index,
        autopct='%1.1f%%')

plt.title('Confirmed Cases by WHO_Region')
plt.show()
```
<img width="983" height="752" alt="Distribution of COVID-19 Cases" src="https://github.com/user-attachments/assets/00a9329e-f19d-4d8d-b04f-f247379e91b0" />

## Mortality Rate Analysis (COVID-19)
TO calculates the mortality rate (%) for each country to understand the severity of COVID-19 by comparing deaths to confirmed cases.

Formula Used:
<br>Mortality Rate = Death/Confirmed×100
```python
# Mortality Rate
df['Mortality Rate']=(df['Deaths']/df['Confirmed'])*100
```
​
To calculates the Recovery Rate (%) for COVID-19 cases.
```python
# Recovery Rate
df['Recovery_Rate'] = (
df['Recovered']/df['Confirmed']
)*100
```
​
To calculates the Active cases for COVID-19 cases.
```python
df['Active_Rate'] = (
df['Active']/df['Confirmed']
)*100
```
## 📊 Recovery vs Death Comparison
To compares the total number of recovered cases and total deaths globally using a simple bar chart.
<br> What the Code Does:
<br>1. Calculates the total recovered cases and total deaths from the dataset.
<br>2. Stores them in a list for visualization.
<br>3. Uses a bar chart to compare both values side-by-side.

Recovered cases are significantly higher than deaths, which reflects:
<br>1. Improvements in healthcare response
<br>2. Effectiveness of treatments over time
<br>3. Global recovery trends​
```python
# Recovery vs Death Comparison
totals = [
    df['Recovered'].sum(),
    df['Deaths'].sum()
]

labels = ['Recovered', 'Deaths']

plt.figure(figsize=(7,5))

plt.bar(
    labels,
    totals,
    color=['green', 'red']  # Recovered = Green, Deaths = Red
)

plt.title('Recovered vs Deaths')
plt.ylabel('Count')
plt.show()
```
<img width="831" height="544" alt="Recovery vs Death" src="https://github.com/user-attachments/assets/65c308b2-681a-4778-b6cd-905f65edf8eb" />

## Countries by Active COVID-19 Cases
To identifies the top countries with the highest active COVID-19 cases, helping highlight regions under the most pressure during the pandemic.

🚨 High active cases indicate:
<br>1. Ongoing spread
<br>2. Healthcare system pressure
<br>3. Need for policy intervention

This helps governments prioritize:
<br>1. Medical resources
<br>2. Lockdown strategies
<br>3. Vaccination campaigns
```python
# Top 10 Active Case Countries
active = df.nlargest(10,'Active')

plt.figure(figsize=(10,6))
sns.barplot(data=active,
            x='Active',
            y='Country/Region')

plt.title('Top 10 Active Cases')
plt.show()
```
<img width="1211" height="659" alt="Active COVID-19 Cases" src="https://github.com/user-attachments/assets/f45a9940-bd05-40fa-854c-580e86f3edcd" />

## 📈 Weekly Growth Analysis
To analyzes the top countries with the highest weekly increase in COVID-19 cases. The goal is to identify regions experiencing rapid spikes and highlight short-term trends.

Objective:
<br>1. Detect countries with the fastest growth rate in the past week
<br>2. Compare growth across regions
<br>3.Support data-driven insights for trend monitoring
```python
# Weekly Growth Analysis
growth = df.nlargest(10,'1_week_change')

plt.figure(figsize=(10,6))
sns.barplot(data=growth,
            x='1_week_change',
            y='Country/Region')

plt.title('Highest Weekly Growth')
plt.show()
```
<img width="1128" height="656" alt="Weekly Growth Analysis" src="https://github.com/user-attachments/assets/49b2f444-3c37-4ae8-845c-b145b52a62aa" />

## Death Rate Distribution Analysis
To visualizes the distribution of COVID-19 death rates across countries using a histogram with a Kernel Density Estimation (KDE) curve.

Objective:
<br>1. Understand how death rates are spread globally
<br>2. Identify whether most countries have low, moderate, or high fatality rates
<br>3. Detect outliers with unusually high death rates
```python
# Death Rate Distribution
plt.figure(figsize=(10,5))
sns.histplot(df['Deaths_/_100_Cases'],
             bins=20,
             kde=True)

plt.title('Death Rate Distribution')
plt.show()
```
<img width="1117" height="558" alt="Death Rate Distribution" src="https://github.com/user-attachments/assets/232c0ccc-b10d-4511-8c98-783e3b947e46" />

## Recovery Rate Distribution Analysis
To visualizes the distribution of COVID-19 recovery rates across countries using a histogram combined with a KDE (Kernel Density Estimation) curve.

Objective:
<br>1. Analyze how recovery rates vary globally
<br>2. Identify whether most countries have high or low recovery performance
<br>3. Detect outliers with unusually low or high recovery rates
```python
# Recovery Rate Distribution
plt.figure(figsize=(10,5))
sns.histplot(df['Recovered_/_100_Cases'],
             bins=20,
             kde=True)

plt.title('Recovery Rate Distribution')
plt.show()
```
<img width="1124" height="566" alt="Recovery Rate" src="https://github.com/user-attachments/assets/2c7d101d-c8d7-49cc-a61b-33fd2a45c2d5" />

## Correlation Heatmap Analysis
To visualizes the relationship between numerical variables in the dataset using a correlation heatmap. It helps identify how strongly different features are related to each other.

Objective:
<br>1. Understand relationships between key numerical metrics
<br>2. Identify strong positive or negative correlations
<br>3. Detect features that influence each other (e.g., cases, deaths, recovery)
```python
# Correlation Heatmap
plt.figure(figsize=(10,8))

sns.heatmap(
    df.select_dtypes(include='number').corr(),
    annot=True,
    cmap='coolwarm'
)

plt.title('Correlation Heatmap')
plt.show()
```
<img width="743" height="638" alt="Correlation Heatmap" src="https://github.com/user-attachments/assets/6fd60d06-642d-47eb-bef4-35685d05b336" />

## Confirmed Cases vs Deaths (Scatter Plot)
To explores the relationship between confirmed COVID-19 cases and total deaths using a scatter plot. It helps in understanding whether higher case counts are associated with higher fatalities.

Objective:
<br>1. Analyze the relationship between confirmed cases and deaths
<br>2. Identify patterns, trends, and clusters
<br>3. Detect outliers (countries with unusual death rates)
```python
# Scatter Plot (Confirmed vs Deaths)
plt.figure(figsize=(10,6))

sns.scatterplot(
    data=df,
    x='Confirmed',
    y='Deaths'
)

plt.title('Confirmed Cases vs Deaths')
plt.show()
```
<img width="937" height="546" alt="Scatter Plot" src="https://github.com/user-attachments/assets/1570127b-b3a8-41d2-8de1-b458c4e9a86c" />

## Outlier Detection in Confirmed Cases (Box Plot)
A box plot to identify outliers in confirmed COVID-19 cases across countries. It provides a quick summary of data distribution and highlights extreme values.

Objective:
<br>1. Detect outliers in confirmed cases
<br>2. Understand the spread and variability of data
<br>3. Identify countries with exceptionally high case counts
```python
# Box Plot for Outlier Detection
plt.figure(figsize=(10,5))

sns.boxplot(
    x=df['Confirmed']
)

plt.title('Outliers in Confirmed Cases')
plt.show()
```
<img width="827" height="470" alt="Box Plot" src="https://github.com/user-attachments/assets/3e82052f-9fe5-409e-8bd6-716e64556cc2" />

## Global COVID-19 Confirmed Cases (Choropleth Map)
To presents an interactive world map visualizing the distribution of COVID-19 confirmed cases across countries. It helps in understanding the geographical spread and intensity of the pandemic.

Objective:
<br>1. Visualize global distribution of confirmed cases
<br>2. Identify high-impact regions and hotspots
<br>3. Enable interactive exploration of country-wise data
```python
import pandas as pd
import plotly.express as px
import warnings

# Hide the deprecation warning
warnings.filterwarnings("ignore", category=DeprecationWarning)

# Create Choropleth Map
fig = px.choropleth(
    df,
    locations='Country/Region',
    locationmode='country names',
    color='Confirmed',
    hover_name='Country/Region',
    color_continuous_scale='Blues',
    title='🌍 Global COVID-19 Confirmed Cases'
)

# Customize layout
fig.update_layout(
    width=1200,
    height=700,
    title_x=0.5
)

fig.show()
```
<img width="1100" height="658" alt="Global COVID-19" src="https://github.com/user-attachments/assets/346931c3-4d56-4509-b1d5-c84588f57dd0" />
