# Film Finance - Exploring Influence on Revenue

## Overview
this project, done using a dataset of different movies with their information such as release, date, year, budget and gross earnings. By analyzing the correlation between budget and gross earnings,I aim to reveal whether higher production costs translate into greater financial success. Additionally, I investigate the average gross earnings by genre, shedding light on which types of films perform best at the box office.

### Tools I Used
Python - Pandas library: to analyse the data. 
         Matplotlib library: to visualize the data.
         Numpy library: to process and calculate data.
Jupyter Notebook - The tool i used to run my Python scripts which let me easily include my notes and analysis.
Git & GitHub - Essentials for version conrol and sharing my Python code and analysis.

## Data Preparation and Cleanup
This section outlines the steps taken to prepare the data for analysis, ensuring accuray and usabilty.

### Import & Clean Up Data
I start by importing necessary libraries, loading and copying the dataset, followed by the initial data cleaning tasks to ensure data quality.

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
sns.set()

df = pd.read_csv("movies.csv")
df_copy = df.copy()
df_copy.head()

# Dropping missing and nan values from the dataset
df_copy.dropna(subset = ["released"], inplace = True)
df_copy.dropna(subset = ["rating"], inplace = True)
df_copy.dropna(subset = ["writer"], inplace = True)
df_copy.dropna(subset = ["star"], inplace = True)
df_copy.dropna(subset = ["country"], inplace = True)
df_copy.dropna(subset = ["company"], inplace = True)
df_copy["rating"].isna().sum()

df_copy["score"] = df_copy["score"].fillna(df_copy["score"].mean())
df_copy["votes"] = df_copy["votes"].fillna(df_copy["votes"].mean())
df_copy["budget"] = df_copy["budget"].fillna(df_copy["budget"].mean())
df_copy["gross"] = df_copy["gross"].fillna(df_copy["gross"].mean())
df_copy["runtime"] = df_copy["runtime"].fillna(df_copy["runtime"].mean())

# Updating the year column
df_copy['year_correct'] = df_copy['released'].astype(str).str.split().str[2]
df_copy['year_correct']
```
## The Analysis
This project aims at investigating specifics aspects features that may enable a movie to perform well at the box office, taking the correlation of certain features to the gross earned.

### Visualize Data
```python
# Budget vs Gross regression plot
plt.figure(figsize = (10, 8))
sns.regplot(df_copy, 
            x = "budget", 
            y = "gross", 
            scatter_kws = {'color': 'b'}, 
            line_kws = {'color': 'red'})
plt.title("Budget vs Gross Earnings")
plt.savefig('budget-vs-gross-earnings.png')
```
#### Results
![budget vs Gross Earnings](budget-vs-gross-earnings.png)



