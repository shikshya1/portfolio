---
date: 2020-04-07T10:58:08-04:00
description: "Exploratory Data Analysis"
tags: ["Statistics"]
title: "Exploratory Data Analysis"
---

Statistics is the study of how to collect, organize, analyze and interpret numerical information and data. 

There are two major terms repeated frequently in the statistics domain: population and sample. 

- Population: It refers to the group of people or objects with common theme. Example: Technical team at Target.
- Sample: It refers to the small portion of population. Example: only UX designers at target.

## Exploratory data analysis (EDA): 
EDA is one of the most important step in any data science project. By summarizing and visualizing the data, we can gain valuable insights and understanding of the problem. 

Descriptive vs Inferential statistics:

### Descriptive statistics:
 It involves methods of organizing, visualizing and summarizing information from samples and population.

 ### Inferential statistics:
It involves methods of using information from a sample to draw a conclusion regarding a population. 

## Types of structured data:

Quantitative data: Data that are expressed on a numeric scale. It is further divided into interval and ratio. There is no true zero in interval. It means space between two things. Example of interval data is time as it cannot have 0. There can be true zero in ratio.

Qualitative data: Data that can take on specific set of values that represents categories. It can be further divided into nominal and ordinal data. Nominal data applies to categories that cannot be ordered from smallest to largest. Example of nominal includes country of origin. Ordinal data refers to data that can be arranged in order but the difference between the data values cannot be distinguished. Example of ordinal value includes level of emergency in trauma center.

## Estimates of location

Import libraries and read data
```
%matplotlib inline

from pathlib import Path

import pandas as pd
import numpy as np
from scipy.stats import trim_mean
from scipy import stats
from statsmodels import robust
import wquantiles

import seaborn as sns
import matplotlib.pylab as plt



state = pd.read_csv('state.csv')
```

1) Mean (average): sum of all values divided by number of values

```
state['Population'].mean()
```

2) Weighted mean (Weighted average) : Sum of all values times a weight divided by the sum of weights

```
np.average(state['Murder.Rate'], weights=state['Population'])
```

3) Trimmed mean (truncated mean) : The average of all values after dropping a fixed number of extreme values

```
trim_mean(state['Population'], 0.1)
```


4) Median (50th percentile): Number that is larger than half of the value and smaller than half of the value.
```
state['Population'].median()
```

5) Weighted median : Value such that one-half of the sum of weights lies above and below the sorted data

```
wquantiles.median(state['Murder.Rate'], weights=state['Population'])
```

6) Mode : Mode in french means popular. Value that occurs most frequently. There might be none, one or more than one values. 

```
stats.mode(state['Population'])
```

7) Percentile (Quantile) : The value such that P percent of value lies below it.
```
state['Murder.Rate'].quantile([0.05, 0.25, 0.5, 0.75, 0.95])
```

### Mean vs median:

Median is ressistant to outlier; thus is stable while mean is not ressistant to outliers. Trimmed mean can also be used to ensure outliers are removed from the data. If the histogram is symmetric, mean and median are the same. When the histogram is skewed to right, mean is greater than median.

## Estimates of Variability

Variability, also referred as dispersion, mesaures whether the data are tightly clustered or spread out.

1) Deviations: Difference between observed values and the estimate of location.
2) Variance: Sum of squared deviations from the mean divided by n-1.
3) Standard deviation: Standard deviation measures the dispersion of a dataset relative to its mean (square root of the variance). It is easier to interpret than variance as it is on same scale as the original data.

```
state['Population'].std()
```
4) Mean absolute deviation (l1 norm, Manhattan norm): Mean of the absolute values of the deviation from the mean.

```
robust.scale.mad(state['Population'])
```

5) Range: Difference between largest and smallest value in a dataset. 



## Understanding and Exporing data distributions

Distribution is the shape that is made if you draw a line along the edges of histogram's bars.

Types:

1) Normal distribution
2) Uniform distribution
3) Skewed left distribution
4) Skewed right distribution
5) Bimodal distribution

Exploring data distribution:

1) Boxplot : Boxplots are based on percentile and helps to see distribution of data. It depicts five key number of data (smallest value, Q1, Q2, Q3 and maximum value). Any data outside the whiskers plotted as single line or circles are often considered as outliers.

```
ax = (state['Population']/1000000).plot.box(figsize=(5, 5))
ax.set_ylabel('Population (millions)')
plt.show()
```

2) Frequency table: FT divides the variable range into equally spaced segments and tells how many values fall within each segment. 

```
binnedPopulation = pd.cut(state['Population'], 10)
print(binnedPopulation.value_counts())
```

3) Histogram: Histogram is a specific type of bar graph used to visualize frequency table, with bins on the x-axis and data count on y-axis.

```
ax = (state['Population'] / 1000000).plot.hist(figsize=(5, 5))
ax.set_xlabel('Population (millions)')
plt.show()
```

4) Density plot: Smoothed version of the histogram, computed directly from the data through a kernel density estimation.

```
ax = state['Murder.Rate'].plot.hist(density=True, xlim=[0, 12], 
                                    bins=range(1,12), figsize=(5, 5))
state['Murder.Rate'].plot.density(ax=ax)
ax.set_xlabel('Murder Rate (per 100,000)')
plt.show()
```

Some terms used in data distribution:

- Skewness: Refers to whether data is skewed to larger or smaller values
- Kutosis: Indicates the propensity of the data to have extreme values


### Link to github page: [Code](https://github.com/shikshya1/statistics/tree/main/exploratory_data_analysis)
