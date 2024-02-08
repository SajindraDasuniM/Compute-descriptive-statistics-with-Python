# Compute descriptive statistics with Python


## Introduction

Throughout this notebook, I will practice computing descriptive statistics to explore and summarize a dataset. 

## Overview

Computing descriptive stats is a common step to take after data cleaning. 

In this notebook, I will use descriptive stats to get a basic understanding of the literacy rate data for each district in the education dataset. 


## Import packages and libraries


```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```


```python
# import csv file
education_districtwise = pd.read_csv('C:/2_PERSONAL/Data Science/Google Advanced Data Analytics/Course4_The Power of Statistics/New folder/Files (1)/education_districtwise.csv')
```

## Explore the data


```python
# check first 5 rows
education_districtwise.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>DISTNAME</th>
      <th>STATNAME</th>
      <th>BLOCKS</th>
      <th>VILLAGES</th>
      <th>CLUSTERS</th>
      <th>TOTPOPULAT</th>
      <th>OVERALL_LI</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>DISTRICT32</td>
      <td>STATE1</td>
      <td>13</td>
      <td>391</td>
      <td>104</td>
      <td>875564.0</td>
      <td>66.92</td>
    </tr>
    <tr>
      <th>1</th>
      <td>DISTRICT649</td>
      <td>STATE1</td>
      <td>18</td>
      <td>678</td>
      <td>144</td>
      <td>1015503.0</td>
      <td>66.93</td>
    </tr>
    <tr>
      <th>2</th>
      <td>DISTRICT229</td>
      <td>STATE1</td>
      <td>8</td>
      <td>94</td>
      <td>65</td>
      <td>1269751.0</td>
      <td>71.21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>DISTRICT259</td>
      <td>STATE1</td>
      <td>13</td>
      <td>523</td>
      <td>104</td>
      <td>735753.0</td>
      <td>57.98</td>
    </tr>
    <tr>
      <th>4</th>
      <td>DISTRICT486</td>
      <td>STATE1</td>
      <td>8</td>
      <td>359</td>
      <td>64</td>
      <td>570060.0</td>
      <td>65.00</td>
    </tr>
  </tbody>
</table>
</div>



**Note**: To interpret this data correctly, it’s important to understand that each row, or observation, refers to a different *district* (and not, for example, to a state or a village). So, the `VILLAGES` column indicates how many villages are in each district, the `TOTPOPULAT` column indicates the population for each district, and the `OVERALL_LI` column indicates the literacy rate for each district. 


```python
# check the shape
education_districtwise.shape
```




    (680, 7)



### Compute descriptive stats

 `describe()` gives you the following output: 

*   `count`: Number of non-NA/null observations
*   `mean`: The arithmetic average
*   `std`: The standard deviation
*   `min`: The smallest (minimum) value
*   `25%`: The first quartile (25th percentile)
*   `50%`: The median (50th percentile) 
*   `75%`: The third quartile (75th percentile)
*   `max`: The largest (maximum) value

Our main interest is the literacy rate. This data is contained in the `OVERALL_LI` column, which shows the literacy rate for each district in the nation. 


```python
# Use the `describe()` function to reveal key stats about literacy rate. 
education_districtwise['OVERALL_LI'].describe()
```




    count    634.000000
    mean      73.395189
    std       10.098460
    min       37.220000
    25%       66.437500
    50%       73.490000
    75%       80.815000
    max       98.760000
    Name: OVERALL_LI, dtype: float64



The average literacy rate is about 73% for all districts. This information is useful in itself and also as a basis for comparison. Knowing the mean literacy rate for all districts helps us understand which individual districts are significantly above or below the mean. 

**Note**: `describe()` excludes missing values (`NaN`) in the dataset from consideration. You may notice that the count, or the number of observations for `OVERALL_LI` (634), is fewer than the number of rows in the dataset (680).

You can also use mean() and median() functions 


```python
# compute mean using mean()
education_districtwise['OVERALL_LI'].mean()

# compute median using median()
education_districtwise['OVERALL_LI'].median()
```




    73.49000000000001



You can also use the `describe()` function for a column with categorical data, like the `STATNAME` column. 

 `describe()` gives you the following output: 

*   `count`: Number of non-NA/null observations
*  `unique`: Number of unique values
*   `top`: The most common value (the mode)
*   `freq`: The frequency of the most common value



```python
# use describe() on a categorical data
education_districtwise['STATNAME'].describe()
```




    count         680
    unique         36
    top       STATE21
    freq           75
    Name: STATNAME, dtype: object



The `unique` category indicates that there are 36 states in our dataset. The `top` category indicates that `STATE21` is the most commonly occurring value, or mode. The `frequency` category tells you that `STATE21` appears in 75 rows, which means it includes 75 different districts. 

###  Calculate range using min(), max() 

These individual functions are also useful if you want to do further computations based on descriptive stats. For example, you can use the `min()` and `max()` functions together to compute the range of your data.



```python
# compute range
range_overall_li = education_districtwise['OVERALL_LI'].max() - education_districtwise['OVERALL_LI'].min()
range_overall_li
```




    61.540000000000006



The range in literacy rates for all districts is about 61.5 percentage points. 

This large difference tells you that some districts have much higher literacy rates than others. This will help the government better understand literacy rates nationally and build on their successful educational programs. 
