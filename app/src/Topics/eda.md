<!---
{"next": "Topics/data_viz.md","title": "Exploratory Data Analysis"}
-->

# Exploratory Data Analysis with Pandas

In this section, our core focus will be using our wine review dataset to learn how to manipulate and analyze data with Pandas. (Look back at the 
[Wine Review Data Dictionary](pandas.md#wine-review-data-dictionary) for reference if needed.) 

At a high-level, this lesson will cover:

* [Categorical Data](eda.md#categorical-data)
* [Joining & Concatenating](eda.md#joining--concatenating)
* [Grouping](eda.md#grouping)
* [Filtering](eda.md#filtering)
* [Descriptive Statistics](eda.md#descriptive-statistics)

## Joining & Concatenating

* `df1.append(df2)` -- add the rows in df1 to the end of df2 (columns should be identical)
* `df.concat([df1, df2],axis=1)` —- add the columns in df1 to the end of df2 (rows should be identical)
* `df1.join(df2,on=col1,how='inner')` —- SQL-style join the columns in df1 with the columns on df2 where the rows for col have identical values. how can be equal to one of: 'left', 'right', 'outer', 'inner'
* `df.merge()` -- merge two datasets together into one by aligning the rows from each based on common attributes or columns. how can be equal to one of: 'left', 'right', 'outer', 'inner'

## Reshaping

* `df.transform(func[, axis])` -- return DataFrame with transformed values
* `df.transpose(*args, **kwargs)` -- transpose rows and columns
* `df.rank()` -- rank every variable according to its value
* `pd.melt(df)` -- gathers columns into rows
* `df.pivot(columns='var', values='val')` -- spreads rows into columns

## Grouping w. GroupBy Objects

* `df.groupby(col)` -- returns groupby object for values from a single, specific column
* `df.groupby([col1,col2])` -- returns a groupby object for values from multiple columns, which you can specify

## Filtering


## Descriptive Statistics

* `df[col1].unique()` -- returns an ndarray of the distinct values within a given series
* `df[col1].nunique()` -- return # of unique values within a column
* `.value_counts()` -- returns count of each unique value
* `df.sample(frac = 0.5)` - randomly select a fraction of rows of a DataFrame
* `df.sample(n=10)` - randomly select n rows of a DataFrame
* `mean()` -- mean
* `median()` -- median
* `min()` -- minimum
* `max()` -- maximum
* `quantile(x)` -- quantile
* `var()` -- variance
* `std()` -- standard deviation
* `mad()` -- mean absolute variation
* `skew()` -- skewness of distribution
* `sem()` -- unbiased standard error of the mean
* `kurt()` -- kurtosis
* `cov()` -- covariance
* `corr()` -- Pearson Correlation coefficent
* `autocorr()` -- autocorelation
* `diff()` -- first discrete difference
* `cumsum()` -- cummulative sum
* `comprod()` -- cumulative product
* `cummin()` -- cumulative minimum
