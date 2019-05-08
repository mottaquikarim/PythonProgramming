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
* Viewing & Inspecting Data
* Data Cleaning & Organization
* Data Exploration

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

*More Coming Soon...*


