<!---
{"next": "Topics/data_viz.md","title": "Data Manipulation"}
-->

# Data Manipulation with Pandas

In this section, our core focus will be using our wine review dataset to learn how to manipulate Pandas data structures objects. At a high-level, this lesson will cover:

* Basic Pandas Objects:
	* Index
	* Series
	* DataFrames
* Wine Review Data Dictionary
* Wrangling, Cleaning, & Organizing Data
* Explorational Data Analysis

## Basic Pandas Objects: Index

We know about the concept of an `index` from basic Python `lists`. Well, Pandas considers `Index` to be its own class of objects because you can customize an index in Pandas. As formally defined in the Pandas docs, an `index` object is an "immutable ndarray implementing an ordered, sliceable set" which is the default object for "storing axis labels for all pandas objects".

## Basic Pandas Objects: Series

<img src="../../../assets/pd_series.png" style="margin: 0 auto; display: block;"/>

A **Series** is a 1-D array of data just like the Python `list` datatype we've been working with, but it's a bit more flexible. Some notable characteristics include:

* A Series is like a dict in that you can get and set values by index label.
* A Pandas `Series` acts very similarly to a NumPy `ndarray`:
	* Just like ndarrays, looping through a Series value-by-value is usually not necessary because of its capability to handle vectorized operations.
* The Pandas Series does have some distinct differences from an ndarray:
	* A Series can only have one dimension.
	* Operations between Series automatically align the data based on index label.

Here's the general syntax for creating a Series:

```python
import numpy as np
import pandas as pd

s = pd.Series(data, index = index, dtype)
```

* The `data` parameter can intake a Python dict, an ndarray, or a scalar value (like 5, 7.5, True, or 'a').
* By default, the `index` parameter assigns an zero-based index to each element in data much like a regular Python `list`. Again though, you can pass custom index values to a `Series` to serve as axis labels for your data. Note that Pandas DOES support *non-unique* index values. 
* `dtype` specifies the type of data you're passing into your Series. If you leave this blank, the program will infer the `dtype` from the contents of the `data` parameter.

Using this syntax, you can instantiate a Series from a single scalar value, a list, an ndarray, or a dict. *Note:* If `data` is an `ndarray`, `index` must be the same length as `data`.

```python
import numpy as np
import pandas as pd
import random

# From a single scalar value
s_scalar = pd.Series(5., index=['a', 'b', 'c', 'd', 'e'])
"""
a    5.0
b    5.0
c    5.0
d    5.0
e    5.0
"""

# From a list
s_list = pd.Series(['red','orange','yellow','green','blue','purple'])
"""
0       red
1    orange
2    yellow
3     green
4      blue
5    purple
"""

# From an ndarray
s_ndarray = pd.Series(np.random.randn(5), index=['a', 'b', 'c', 'd', 'e'])
print(s_ndarray)
"""
a   -0.901847
b   10.503150
c    2.060891
d   -0.367695
e    1.040442
"""

# From a dict
d = {'b': 1, 'a': 0, 'c': 2} ### use wines from data set
s_dict = pd.Series(d)
"""
b    1
a    0
c    2
"""
```

## Basic Pandas Objects: DataFrames

<img src="../../../assets/pd_dataframe.png" style="margin: 0 auto; display: block;"/>


A **DataFrame** is a two-dimensional data matrix that stores data much like a spreadsheet does. It has labeled columns and rows with values for each column. Basically, it's virtual spreatsheet. It accepts many different data types as values, including strings, arrays (lists), dicts, Series, and even other DataFrames. The general syntax for creating a DataFrame is identical to that of a Series except it includes a second index parameter called `columns` parameter for adding the index values to the second dimension:

```python
import numpy as np
import pandas as pd

df = pd.DataFrame (data, index, columns)
```

Creating a DataFrame is a little more complex than creating a Series because you have to consider both `rows` and `columns`. Aside from creating a dataframe indirectly by importing an existing data structure, you can create a DataFrame by:

* Specifying column names (i.e. column index values) directly within the `data` parameter
* Specifying column names separately in the `columns` parameter

```python
import numpy as np
import pandas as pd

# Specify values for each column.
df = pd.DataFrame(
{"a" : [4 ,5, 6],
"b" : [7, 8, 9],
"c" : [10, 11, 12]},
index = [1, 2, 3])

# Specify values for each row.
df = pd.DataFrame(
[[4, 7, 10],
[5, 8, 11],
[6, 9, 12]],
index=[1, 2, 3],
columns=['a', 'b', 'c'])


# Both of these methods create a DataFrame with these values:
"""
   a   b   c
1  4   7   10
2  5   8   11
3  6   9   12
"""
```

Here are a few other examples:

```python
import numpy as np
import pandas as pd

# From dict of Series or dicts
data1 = {'one': pd.Series([1., 2., 3.], index=['a', 'b', 'c']), 'two': pd.Series([1., 2., 3., 4.], index=['a', 'b', 'c', 'd'])}
df1 = pd.DataFrame(data1, index=['d', 'b', 'a'], columns=['two', 'three'])
"""
   two three
d  4.0   NaN
b  2.0   NaN
a  1.0   NaN
"""

# From dict of ndarrays / lists
data2 = {'one': [1., 2., 3., 4.],'two': [4., 3., 2., 1.]}
df2 = pd.DataFrame(data2, index=['a', 'b', 'c', 'd'])
"""
   one  two
a  1.0  4.0
b  2.0  3.0
c  3.0  2.0
d  4.0  1.0
"""

# From a list of dicts
data3 = [{'a': 1, 'b': 2}, {'a': 5, 'b': 10, 'c': 20}]
df3 = pd.DataFrame(data3, index=['first', 'second'], columns=['a', 'b', 'c'])
"""
        a   b     c
first   1   2   NaN
second  5  10  20.0
"""
```

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

## First Steps with Wine Review Data

```python
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')
```

* `df.info()` -- returns index, datatype and memory information
* `df.shape` -- returns the number of rows and columns in a data frame
* `len(df)` -- returns # of rows in the data
* `.size` -- returns # of elements in the object (*S & df)
* `.index` -- returns index of the rows specifically (*S & df)
* `df.columns` -- returns the column labels of the DataFrame.
* `df.head(n)` -- returns last n rows of a data frame
* `df.tail(n)` -- returns last n rows of a data frame

```python
import numpy as np
import pandas as pd

print(wine_reviews.info())
"""
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 129971 entries, 0 to 129970
Data columns (total 13 columns):
country                  129908 non-null object
description              129971 non-null object
designation              92506 non-null object
points                   129971 non-null int64
price                    120975 non-null float64
province                 129908 non-null object
region_1                 108724 non-null object
region_2                 50511 non-null object
taster_name              103727 non-null object
taster_twitter_handle    98758 non-null object
title                    129971 non-null object
variety                  129970 non-null object
winery                   129971 non-null object
dtypes: float64(1), int64(1), object(11)
"""

print(wine_reviews.shape) # (rows, columns) --> (129971, 13)
print(len(wine_reviews)) # 129971
print(wine_reviews.size) # 1689623
```

```python
import numpy as np
import pandas as pd

# Row labels
print(wine_reviews.index) # RangeIndex(start=0, stop=129971, step=1)

# Column labels
print(wine_reviews.columns) # Index(['country', 'description', 'designation', 'points', 'price', 'province', 'region_1', 'region_2', 'taster_name', 'taster_twitter_handle', 'title', 'variety', 'winery'], dtype='object')

# Row & Column labels
print(wine_reviews.axes)
"""
[RangeIndex(start=0, stop=129971, step=1), Index(['country', 'description', 'designation', 'points', 'price', 'province', 'region_1', 'region_2', 'taster_name', 'taster_twitter_handle', 'title', 'variety', 'winery'], dtype='object')
"""
```

```python
import numpy as np
import pandas as pd

print(wine_reviews.head())
"""
    country  ...               winery
0     Italy  ...              Nicosia
1  Portugal  ...  Quinta dos Avidagos
2        US  ...            Rainstorm
3        US  ...           St. Julian
4        US  ...         Sweet Cheeks
"""
print(wine_reviews.tail(3))
"""
        country  ...                winery
129968   France  ...       Domaine Gresser
129969   France  ...  Domaine Marcel Deiss
129970   France  ...      Domaine Schoffit

[3 rows x 13 columns]
"""
```

## Wrangling & Selecting Data

* `df[col]` -- select and name a column and return it as a Series
 `df.iloc[0,:]` -- First row
* `df.iloc[0,0]` -- First element of first column
* `s.iloc[0]` -- select an item by its position (*S)
* `s.loc[0]` -- select an item by its index position (*S)
* `df[[col1, col2]]` -- select and name multiple columns and return them as a new data frame


```python
import numpy as np
import pandas as pd

# Print values in first row
print(wine_reviews.iloc[0,:])
"""
country                                                              Italy
description              Aromas include tropical fruit, broom, brimston...
designation                                                   Vulkà Bianco
points                                                                  87
price                                                                  NaN
province                                                 Sicily & Sardinia
region_1                                                              Etna
region_2                                                               NaN
taster_name                                                  Kerin O’Keefe
taster_twitter_handle                                         @kerinokeefe
title                                    Nicosia 2013 Vulkà Bianco  (Etna)
variety                                                        White Blend
winery                                                             Nicosia
"""

# Print values in row at index 5 in first col
print(wine_reviews.iloc[0,5]) # Sicily & Sardinia
```


```python
import numpy as np
import pandas as pd

# A) Print first 3 values in 'country' col
print(wine_reviews['country'][:3])

# B) Print first 3 values in 'countries' Series
countries = wine_reviews['country']
print(countries.iloc[:3])

"""
A & B both output:

0       Italy
1    Portugal
2          US
"""

# Print item at index 5 in 'countries' Series
print(countries.iloc[5]) # Spain

# Print item at index 6 in 'countries' Series
print(countries.loc[6]) # Italy
```


```python
import numpy as np
import pandas as pd

points_per_title = wine_reviews[['title', 'points']] # [129971 rows x 2 columns]
print(points_per_title.head(3))
"""
                                           title  points
0              Nicosia 2013 Vulkà Bianco  (Etna)      87
1  Quinta dos Avidagos 2011 Avidagos Red (Douro)      87
2  Rainstorm 2013 Pinot Gris (Willamette Valley)      87
"""
```

*More Coming Soon...*


