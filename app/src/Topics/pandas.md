<!---
{"next": "Topics/data_viz.md","title": "Data Manipulation"}
-->

# Data Manipulation with Pandas

In this section, our core focus will be using our wine review dataset to learn how to manipulate Pandas data structures objects. At a high-level, this lesson will cover:

* Basic Pandas Objects:
	* Index
	* Series
	* DataFrames
* Viewing & Inspecting Data
* Data Cleaning & Organization
* Data Exploration

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

## Basic Pandas Objects: Index

We know about the concept of an `index` from basic Python `lists`. Well, Pandas considers `Index` to be its own class of objects because you can customize an index in Pandas. As formally defined in the Pandas docs, an `index` object is an "immutable ndarray implementing an ordered, sliceable set" which is the default object for "storing axis labels for all pandas objects".

## Basic Pandas Objects: Series

A **Series** is a 1-D array of data just like the Python `list` datatype we've been working with, but it's a bit more flexible. Some notable characteristics include:

* A Series is like a dict in that you can get and set values by index label.
* A Pandas `Series` acts very similarly to a NumPy `ndarray`:
	* Just like ndarrays, looping through a Series value-by-value is usually not necessary because of its capability to handle vectorized operations.
* The Pandas Series does have some distinct differences from an ndarray:
	* A Series can only have one dimension.
	* Operations between Series automatically align the data based on index label.

#### Creating a Series

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

A **DataFrame** is a two-dimensional data matrix that stores data much like a spreadsheet does. It has labeled columns and rows with values for each column. Basically, it's virtual spreatsheet. It accepts many different data types as values, including strings, arrays (lists), dicts, Series, and even other DataFrames.

```python
import numpy as np
import pandas as pd

df = pd.DataFrame (data, index, columns, dtype)
```

*More Coming Soon...*