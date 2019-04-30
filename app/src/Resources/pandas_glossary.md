<!---
{"next":"About/README.md","title":"Pandas Glossary"}
-->

# Pandas Glossary

<img src="https://news.nationalgeographic.com/content/dam/news/2015/12/15/pandas/01pandainsemination.ngsversion.1450209600474.adapt.1900.1.jpg" style="margin: 0 auto; width: 50%; display: block;"/>

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

## Reading & Writing Data

* `pd.read_csv(filename)` -- From a CSV file
* `pd.read_table(filename)` -- From a delimited text file (like TSV)
* `pd.read_excel(filename)` # From an Excel file
* `pd.read_sql(query, connection_object)` # Reads from a SQL table/database
* `pd.read_json(json_string)` # Reads from a JSON formatted string, URL or file.
* `pd.read_html(url) # Parses an html URL, string or file and extracts tables to a list of dataframes
* `pd.read_clipboard()` # Takes the contents of your clipboard and passes it to read_table()
* `pd.DataFrame(dict)` # From a dict, keys for columns names, values for data as lists
* df.to_csv(filename) # Writes to a CSV file
* `df.to_excel(filename)` # Writes to an Excel file
* `df.to_sql(table_name, connection_object)` # Writes to a SQL table
* `df.to_json(filename)` # Writes to a file in JSON format
* `df.to_html(filename)` # Saves as an HTML table
* `df.to_clipboard()` # Writes to the clipboard

## Data Wrangling & Cleaning

* `df[col]` -- select and name a column and return it as a Series
* `df[[col1, col2]]` -- select and name multiple columns and return them as a new data frame
* `s.iloc[0]` -- select an item by its position
* `s.loc['index_one']` -- select an item by its index position
* df.iloc[0,:] # First row
* df.iloc[0,0] # First element of first column
* `pd.isnull()` -- checks for null values in the data and returns an array of booleans, where "True" means missing and "False" means present
* `pd.notnull()` -- returns all values that are NOT null
* `df.dropna()` -- remove all missing values
* `df.fillna(x)` —- replace all missing values with some value "x"
* `s.replace(1,'one')` -- replace all values equal to 1 with 'one'
* `s.replace([1,3],['one','three'])` -- replace all values equal to 1 with 'one' and all values equal to 3 with 'three'
* `df.rename(columns={'old_name': 'new_ name'})` -- rename specific columns
* `df.set_index('column_one')` -- change the index of the data frame
df.columns = ['a','b','c'] # Renames columns
pd.isnull() # Checks for null Values, Returns Boolean Array
pd.notnull() # Opposite of s.isnull()
df.dropna() # Drops all rows that contain null values
df.dropna(axis=1) # Drops all columns that contain null values
df.dropna(axis=1,thresh=n) # Drops all rows have have less than n non null values
df.fillna(x) # Replaces all null values with x
s.fillna(s.mean()) # Replaces all null values with the mean (mean can be replaced with almost any function from the statistics section)
s.astype(float) # Converts the datatype of the series to float
s.replace(1,'one') # Replaces all values equal to 1 with 'one'
s.replace([1,3],['one','three']) # Replaces all 1 with 'one' and 3 with 'three'
df.rename(columns=lambda x: x + 1) # Mass renaming of columns
df.rename(columns={'old_name': 'new_ name'}) # Selective renaming
df.set_index('column_one') # Changes the index
df.rename(index=lambda x: x + 1) # Mass renaming of index

## Exploring Data

* `df.info()` -- returns index, datatype and memory information
* `df.shape()` -- returns the number of rows and columns in a data frame
* `df.head(n)` -- returns last n rows of a data frame
* `df.tail(n)` -- returns last n rows of a data frame
* `df.count()` -- returns number of non-null values in each data frame column
* `value_counts()` -- returns count of each category in a categorical attributed series of values
* `describe()` -- returns basic summary statistics (e.g. count, mean, std, min, quartiles, & max)
* `df.mean()` -- returns mean of all columns
* `df.median()` -- returns median of each column
* `df.min()` -- returns lowest value in each column
* `df.max()` -- returns highest value in each column
* `quantile(x)` -- quantile
* `cumsum()` -- cummulative sum
* `comprod()` -- cumulative product
* `cummin()` -- cumulative minimum
* `var()` -- returns the variance among values in **each** column
* `df.std()` -- returns standard deviation of each column
* `cov()` -- covariance
* `mad()` -- mean absolute variation
* `skew()` -- skewness of distribution
* `kurt()` -- kurtosis
* `corr()` -- returns the Pearson correlation coefficent between columns in a data frame
* `autocorr()` -- auto-correlation
* `diff()` -- first discrete difference

## Organizating Data

* `df1.append(df2)` -- add the rows in df1 to the end of df2 (columns should be identical)
* `df.concat([df1, df2],axis=1)` —- add the columns in df1 to the end of df2 (rows should be identical)
* `df1.join(df2,on=col1,how='inner')` —- SQL-style join the columns in df1 with the columns on df2 where the rows for colhave identical values. how can be equal to one of: 'left', 'right', 'outer', 'inner'
* `df.sort_values(col1)` -- sort values in a certain column in *ascending* order
* `df.sort_values(col2,ascending=False)` -- sort values in a certain column in *descending* order
* `df.sort_values([col1,col2],ascending=[True,False])` -- sort values in a col1 in *asscending* order, then sort values in col2 in *descending* order

* `df[df[col] > 0.5]` # Rows where the col column is greater than 0.5
* `df[(df[col] > 0.5) & (df[col] < 0.7)]` # Rows where 0.5 < col < 0.7

* `df.groupby(col)` -- returns groupby object for values from a single, specific column
* `df.groupby([col1,col2])` -- returns a `groupby` object for values from multiple columns, which you can specify
* `df.groupby(col1)[col2].mean()` # Returns the mean of the values in col2, grouped by the values in col1 (mean can be replaced with almost any function from the statistics section)

* `df.pivot_table(index=col1, values= col2,col3], aggfunc=mean)` # Creates a pivot table that groups by col1 and calculates the mean of col2 and col3
* `df.groupby(col1).agg(np.mean)` # Finds the average across all columns for every unique column 1 group
* `df.apply(np.<function>)` # Applies a function across each column
* `df.apply(np.<function>, axis=1)` # Applies a function across each row



#### Sources
* [Pandas Docs](http://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html)
