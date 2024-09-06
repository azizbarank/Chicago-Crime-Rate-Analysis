# Chicago-Crime-Rate-Analysis

## Overview
This project aims to analyse and generate insight into the trends of crime rates in Chicago between the years 2001-2024. To achieve this, it uses the Python libraries of pandas, numpy, matplotlib and seaborn. Additionally, to have a clear object, three questions were defined beforehand:

### Project Questions:
* How much has crime fluctuated between 2001-2024?
* What type of crimes are the most common?
* What areas and locations of Chicago tend to have the highest rate of crime?

## Dataset & Methods
---
### Dataset
The dataset was taken from the official website of [Data.gov](https://catalog.data.gov/dataset/crimes-2001-to-present). It was extracted by the Chicago Police Department's CLEAR (Citizen Law Enforcement Analysis and Reporting) system. It consists of more than 8 million data entries and 22 columns in total.
---

### Methods & Steps
Below are the general steps taken for the data analysis. A few example codes are given to have an idea of what has been done. To look at the full codes, you can refer to the [notebook](https://github.com/azizbarank/California-Infectious-Diseases-Analysis/blob/main/california_disease_analysis.ipynb).
1. Importing the necessary packages:

```python
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline
```

2. First quick glance at the dataset:
```python
df.head()
df.columns
df.shape
df.info()
df.value_counts()
```

3. Data cleaning:
   * Dropping both unuseful columns and the ones with high NaN values
     ```python
      df.isna().sum()
      df = df.drop(axis=1, columns=['Ward',
                              'Community Area',
                              'Case Number',
                              'IUCR',
                              'Beat',
                              'District',
                              'FBI Code',
                              'Updated On'])
      ```
4. Gaining insights:
   ##### 1. The fluctuation of crime between 2001-2024 (*line plot + scatterplot + boxplot*)
   ##### 2. The most common crime types (*bar plot*)
   ##### 3. The locations and areas with the highest rate of crimes (*two bar plots*)
   ```python
   # Group the data by year and get monthly counts to observe fluctuations within each year
   df['Year'] = df.index.year  # Extract the year from the Date index
   # Create a boxplot showing the distribution of monthly crime counts for each year
   plt.figure(figsize=(18, 10))  # Adjust the figure size for better visualization
   plt.boxplot(
   .
   .
   .
   )
   df['Primary Type'].value_counts().iloc[:10]
   .
   .
   plt.figure(figsize=(15, 10))
   sns.countplot(
   y='Location Description',
   data=df,
   order=df['Location Description'].value_counts().iloc[:10].index,
   palette='viridis'  # Use a colorful palette like 'viridis', 'plasma', 'coolwarm', etc.
   )
   .
   .
   # Plotting categorical count plot for crime by area with a colorful palette
   sns.countplot(
   y='Block',
   data=df,
   orient='h',
   order=df['Block'].value_counts()[:10].index,
   palette='viridis'  # Use a vibrant palette like 'coolwarm', 'viridis', or 'Set2'
   )
   .
   .
   ```
   ---

## Results (Project Questions)
1. How much has crime fluctuated between 2001-2024?
   
![Line Plot](https://github.com/azizbarank/Chicago-Crime-Rate-Analysis/blob/main/images/crime_year.png)
![Scatter Plot](https://github.com/azizbarank/Chicago-Crime-Rate-Analysis/blob/main/images/scatter_year.png)
![Boxplot](https://github.com/azizbarank/Chicago-Crime-Rate-Analysis/blob/main/images/boxplot_year.png)

According to the boxplot, the average rate of crime ranges from 18000 to 42000 **per month**. It seems that there is a decline overall throughout the years as well. When we look at the both line and scatterplot, the number of crimes **per year** have been below the average level from 2012 onwards (i.e., below 339434). While 2002 was the year with the highest rate of crime, 2024 seems to be the lowest. However, that is probably we are still only at the half of it at the moment. Therefore, if we exclude 2024 from consideration, then 2021 seems to be the year with the lowest rate of crime.
   
2. What type of crimes are the most common (top 10)?
   
|       Crime Type   | Count |
| -----------------  |-------|
|Theft               |1723467|
|BATTERY             |1485544|
|CRIMINAL DAMAGE	   |927810|
|NARCOTICS	         |755508|
|ASSAULT	           |539209|
|OTHER OFFENSE	     |505999|
|BURGLARY	           |434820|
|MOTOR VEHICLE THEFT |410557|
|DECEPTIVE PRACTICE	 |369176|
|ROBBERY	           |306767|

Theft and battery seems to be much more common compared to the other crime types.

3. What areas and locations of Chicago tend to have the highest rate of crime?
![Block](https://github.com/azizbarank/Chicago-Crime-Rate-Analysis/blob/main/images/block.png)
![Location](https://github.com/azizbarank/Chicago-Crime-Rate-Analysis/blob/main/images/location.png)

The top three general locations of the crimes seem to be streets, residence and apartment. While the adresses with the most common crimes are also available, for privcy reasons, some of the sections were deliberately changed but the streets, boulevards and avenues are still visible.
