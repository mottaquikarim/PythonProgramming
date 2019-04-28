<!---
{"next":"About/README.md","title":"Pandas Glossary"}
-->

# Pandas Glossary

*More coming soon...*

## Attributes

* `T` -- Transpose index and columns.
* `at` -- Access a single value for a row/column label pair
* `axes` -- Return a list representing the axes of the DataFrame.
* `blocks` -- (DEPRECATED) Internal property, property synonym for as_blocks().
* `columns` -- The column labels of the DataFrame.
* `dtypes` -- Return the dtypes in the DataFrame.
* `empty` -- Indicator whether DataFrame is empty.
* `ftypes` -- Return the ftypes (indication of sparse/dense and dtype) in DataFrame.
* `iat` -- Access a single value for a row/column pair by integer position.
* `iloc` -- Purely integer-location based indexing for selection by position.
* `index` -- The index (row labels) of the DataFrame.
* `is_copy` -- Return the copy.
* `ix` -- A primarily label-location based indexer, with integer position fallback.
`loc` -- Access a group of rows and columns by label(s) or a boolean array.
* `ndim` -- Return an int representing the number of axes / array dimensions.
* `shape` -- Return a tuple representing the dimensionality of the DataFrame.
* `size` -- Return an int representing the number of elements in this object.
* `style` -- Property returning a Styler object containing methods for building a styled HTML representation fo the DataFrame.
* `values` -- Return a Numpy representation of the DataFrame.

## Data Wrangling & Cleaning

* `pd.isnull()` -- checks for null values in the data and returns an array of booleans, where "True" means missing and "False" means present
* `pd.notnull()` -- returns all values that are NOT null
* `df.dropna()` -- remove all missing values
* `df.fillna(x)` —- replace all missing values with some value "x"
* `s.replace(1,'one')` -- replace all values equal to 1 with 'one'
* `s.replace([1,3],['one','three'])` -- replace all values equal to 1 with 'one' and all values equal to 3 with 'three'
* `df.rename(columns={'old_name': 'new_ name'})` -- rename specific columns
* `df.set_index('column_one')` -- change the index of the data frame

## Viewing & Inspecting Data

* `df.info()` -- returns index, datatype and memory information
* `df.shape()` -- returns the number of rows and columns in a data frame
* `df.head(n)` -- returns last n rows of a data frame
* `df.tail(n)` -- returns last n rows of a data frame
* `df.describe()` -- returns summary statistics
* `df.mean()` -- returns the mean of all columns
* `df.corr()` -- returns the correlation between columns in a data frame
* `df.count()` -- returns the number of non-null values in each data frame column
* `df.max()` -- returns the highest value in each column
* `df.min()` -- returns the lowest value in each column
* `df.median()` -- returns the median of each column
* `df.std()` -- returns the standard deviation of each column

## Selecting & Organizating Data

* `df[col]` -- select and name a column and return it as a Series
* `df[[col1, col2]]` -- select and name multiple columns and return them as a new data frame
* `s.iloc[0]` -- select an item by its position
* `s.loc['index_one']` -- select an item by its index position
* `df1.append(df2)` -- add the rows in df1 to the end of df2 (columns should be identical)
* `df.concat([df1, df2],axis=1)` —- add the columns in df1 to the end of df2 (rows should be identical)
* `df1.join(df2,on=col1,how='inner')` —- SQL-style join the columns in df1 with the columns on df2 where the rows for colhave identical values. how can be equal to one of: 'left', 'right', 'outer', 'inner'
* `df.sort_values(col1)` -- sort values in a certain column in *ascending* order
* `df.sort_values(col2,ascending=False)` -- sort values in a certain column in *descending* order
* `df.sort_values([col1,col2],ascending=[True,False])` -- sort values in a col1 in *asscending* order, then sort values in col2 in *descending* order
* `df.groupby(col)` -- returns groupby object for values from a single, specific column
* `df.groupby([col1,col2])` -- returns a groupby object for values from multiple columns, which you can specify

## Statistical Analysis

* `describe()` -- returns basic summary statistics (e.g. count, mean, std, min, quartiles, & max)
* `value_counts()` -- returns count of each category in a categorical attributed series of values
* `mean()` -- mean
* `median()` -- median
* `min()` -- minimum
* `max()` -- maximum
* `quantile(x)` -- quantile
* `var()` -- variance
* `std()` -- standard deviation
* `mad()` -- mean absolute variation
* `skew()` -- skewness of distribution
* `kurt()` -- kurtosis
* `cov()` -- covariance
* `corr()` -- Pearson Correlation coefficent
* `autocorr()` -- autocorelation
* `diff()` -- first discrete difference
* `cumsum()` -- cummulative sum
* `comprod()` -- cumulative product
* `cummin()` -- cumulative minimum


#### Sources
* [Pandas Docs](http://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)
