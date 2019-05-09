<!---
{"next": "Topics/data_viz.md","title": "Data Manipulation"}
-->

# Data Manipulation with Pandas

In this section, our core focus will be using our wine review dataset to learn how to manipulate Pandas data structures objects. At a high-level, this lesson will cover:

* Wine Review Data Dictionary
* Importing Data
* Wrangling & Selecting Data
* Cleaning, & Organizing Data

## Wine Review Data Dictionary

To frame us for jumping into Pandas, let's review the details of our wine review dataset.

[Wine Reviews | Kaggle](https://www.kaggle.com/zynicide/wine-reviews/)
*130k wine reviews with variety, location, winery, price, and description* 

* `country`: The country that the wine is from
* `description`:
* `designation`: The vineyard within the winery where the grapes that made the wine are from
* `points`: The number of points WineEnthusiast rated the wine on a scale of 1-100 (though they say they only post reviews for wines that score >=80)
* `price`: The cost for a bottle of the wine
* `province`: The province or state that the wine is from
* `region_1`: The wine growing area in a province or state (ie Napa)
* `region_2`: Sometimes there are more specific regions specified within a wine growing area (ie Rutherford inside the Napa Valley), but this value can sometimes be blank
* `taster_name`: 
* `taster_twitter_handle`: 
* `title`: The title of the wine review, which often contains the vintage if you're interested in extracting that feature
* `variety`: The type of grapes used to make the wine (ie Pinot Noir)
* `winery`: The winery that made the wine

## Importing Data

In the last lesson, we imported the wine review data from a csv file like this:

```python
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')
```

After your initial import of some dataset, you'll want to do a gut check to make sure everything is in place. Here are the kind of very basic properties you might want to check:

* `df.info()` -- returns index, datatype and memory information
* `df.shape` -- returns the number of rows and columns in a data frame
* `len(df)` -- returns # of rows in the data
* `df.size` -- returns # of elements in the object (*S & df)
* `df.index` -- returns index of the rows specifically (*S & df)
* `df.columns` -- returns the column labels of the DataFrame.
* `df.head(n)` -- returns last n rows of a data frame
* `df.tail(n)` -- returns last n rows of a data frame

## Wrangling & Selecting Data

* `df[col]` -- select and name a column and return it as a Series
* `df.iloc[0,:]` -- First row
* `df.iloc[0,0]` -- First element of first column
* `s.iloc[0]` -- select an item by its position (*S)
* `s.loc[0]` -- select an item by its index position (*S)
* `df[[col1, col2]]` -- select and name multiple columns and return them as a new data frame
* `df.nlargest(n, 'value')` -- Select and order top n entries.
* `df.nsmallest(n, 'value')` -- Select and order bottom n entries

## Cleaning & Organizing Data

#### Null Values

* `pd.isnull()` -- checks for null (NaN values in the data and returns an array of booleans, where "True" means missing and "False" means present
* `pd.notnull()` -- returns all values that are NOT null
* `pd.isnull().sum()` -- returns a count of null (NaN)
* `df.dropna()` -- Drops all rows that contain null values and returns a new df
* `df.dropna(axis=1)` -- Drops all columns that contain null values and returns a new df
* `df.dropna(subset=[col1])` -- Drops all rows that contain null values in one or more specific columns and returns a new df
* `df.fillna(value=x)` —- replace all missing values with some value `x` (*S & df)
* `s.fillna(s.mean())` -- Replaces all null values with the mean (mean can be replaced with almost any function from the statistics section)

#### Editing Existing Data

* `df.drop(columns=[col1, col2, ...])` -- drops specified columns from the dataframe
* `s.replace(1,'one')` -- replace all values equal to 1 with 'one'
* `s.replace([1,3],['one','three'])` -- replace all values equal to 1 with 'one' and all values equal to 3 with 'three'
* `df.rename(columns={'old_name': 'new_ name'})` -- rename specific columns
* `df.set_index('column_one')` -- change the index of the data frame
* `df.reset_index()` -- Reset index of DataFrame to row numbers, moving
index to columns.

#### Sorting & Reshaping

* `df.sort_values(col1)` -- sort values in a certain column in *ascending* order
* `df.sort_index(axis=1)` -- sort axis values by index in *ascending* order
* `df.sort_values(col2,ascending=False)` -- sort values in a certain column in *descending* order
* `df.sort_index(axis=1, ascending=False)` -- sort axis values by index in *descending* order
* `df.sort_values([col1,col2],ascending=[True,False])` -- sort values in a col1 in *asscending* order, then sort values in col2 in *descending* order
* `df.rank()` -- rank every variable according to its value
* `pd.melt(df)` -- gathers columns into rows
* `df.pivot(columns='var', values='val')` -- spreads rows into columns

#### Grouping w. GroupBy Objects

* `df.groupby(col)` -- returns groupby object for values from a single, specific column
* `df.groupby([col1,col2])` -- returns a groupby object for values from multiple columns, which you can specify

## Joining & Concatenating Data

* `df1.append(df2)` -- add the rows in df1 to the end of df2 (columns should be identical)
* `df.concat([df1, df2],axis=1)` —- add the columns in df1 to the end of df2 (rows should be identical)
* `df1.join(df2,on=col1,how='inner')` —- SQL-style join the columns in df1 with the columns on df2 where the rows for col have identical values. how can be equal to one of: 'left', 'right', 'outer', 'inner'
* `df.merge()` -- merge two datasets together into one by aligning the rows from each based on common attributes or columns. how can be equal to one of: 'left', 'right', 'outer', 'inner'

## Exploring Data

* `df[col1].unique()` -- returns an ndarray of the distinct values within a given series
* `df[col1].nunique()` -- return # of unique values within a column
* `.value_counts()` -- returns count of each unique value
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
