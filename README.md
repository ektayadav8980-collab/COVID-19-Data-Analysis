# COVID-19 Global Data Analytics Dashboard

## Comprehensive Data Analysis & Visualization of the Global Pandemic  

## 📌 Project Overview

This project is an in depth exploratory data analysis (EDA) of COVID-19 data across 180+ countries and regions worldwide. Using Python based data analytics tools, we uncover pandemic trends, mortality rates, recovery patterns, and regional disparities to provide actionable insights into the global health crisis.

## Why This Matters: 
The COVID-19 pandemic generated massive datasets. By systematically analyzing this data, we can understand disease progression, identify high risk regions, and track recovery patterns skills essential for real-world data analytics roles.

## 🎯 Problem Statement

## The Challenge:

Raw COVID-19 data exists in isolation—thousands of data points across countries and time periods. To extract meaning, we need to ask critical questions:
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
# Loading the data
COVID-19 data, including confirmed cases, deaths, and recoveries across different countries and time periods.

The data is loaded using the Pandas library for efficient data manipulation and analysis.
```python
# Load dataset
import pandas as pd
df = pd.read_csv(r"C:\Users\admin\Downloads\country_wise_latest.csv")
```
# Exploration
```python
1  df.shape


1  (187, 15)
```
187 columns, 15 of which are countries and regions. The rest are output from the PCA transformation. Let’s check for missing values:
