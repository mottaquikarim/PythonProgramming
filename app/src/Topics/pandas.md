<!---
{"next": "Topics/data_viz.md","title": "Data Manipulation"}
-->

# Data Manipulation with Pandas

In this section, our core focus will be using our wine review dataset to learn how to manipulate Pandas data structures objects. At a high-level, this lesson will cover:

* Wine Review Data Dictionary
* Importing Data
* Wrangling & Selecting Data
* Cleaning, & Organizing Data
* *coming soon...*

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

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

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

print(wine_reviews.shape) # (rows, columns) is (129971, 13)
print(len(wine_reviews)) # 129971
print(wine_reviews.size) # 1689623
```

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

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
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

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
* `df[df.Length > 7]` -- Extract rows that meet logical criteria.

>>ROWS
* `df[df.Length > 7]` -- Extract rows that meet logical criteria.
`df.nlargest(n, 'value')` -- Select and order top n entries.
`df.nsmallest(n, 'value')` -- Select and order bottom n entries

>>
where[blah blah]
df.sample(frac=0.5)
Randomly select fraction of rows.
df.sample(n=10)
Randomly select n rows.
filtering
* `df[df.Length > 7]` -- Extract rows that meet logical criteria.


```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

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
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

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
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

wine_ratings = wine_reviews[['title', 'country', 'rating', 'price']] # [129971 rows x 4 columns]
print(wine_ratings.head(3))
"""
                                           title   country  rating  price
0              Nicosia 2013 Vulkà Bianco  (Etna)     Italy      87    NaN
1  Quinta dos Avidagos 2011 Avidagos Red (Douro)  Portugal      87   15.0
2  Rainstorm 2013 Pinot Gris (Willamette Valley)        US      87   14.0
"""
```


## Cleaning & Organizing Data

#### Null & Duplicate Values

* `pd.isnull()` -- checks for null (NaN values in the data and returns an array of booleans, where "True" means missing and "False" means present
* `pd.notnull()` -- returns all values that are NOT null
* `pd.isnull().sum()` -- returns a count of null (NaN)
* `df.dropna()` -- Drops all rows that contain null values and returns a new df
* `df.dropna(axis=1)` -- Drops all columns that contain null values and returns a new df
* `df.dropna(subset=[col1)` -- Drops all rows that contain null values in one or more specific columns and returns a new df
* `df.fillna(x)` —- replace all missing values with some value `x`
* `s.fillna(s.mean())` -- Replaces all null values with the mean (mean can be replaced with almost any function from the statistics section)
* `df.drop_duplicates()` -- remove duplicate rows (only considers columns).

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

wine_ratings = wine_reviews[['title', 'country', 'rating', 'price']] # [129971 rows x 4 columns]

print(wine_ratings.isnull().sum())
"""
title         0
country      63
rating        0
price      8996
"""
print(len(wine_ratings)) # 129971

wine_ratings = wine_ratings.dropna(subset=['country', 'price'])

print(wine_ratings.isnull().sum())
"""
title       0
country     0
rating      0
price       0
"""
print(len(wine_ratings)) # 120916
```

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

wine_ratings = wine_reviews[['title', 'country', 'rating', 'price']] # [129971 rows x 4 columns]

m = prices.mean()
replace_value = {'price': prices.mean()}
wine_ratings = wine_ratings.fillna(value=replace_value)

print(wine_ratings.isnull().sum())
"""
title       0
country    63
rating      0
price       0
"""
print(len(wine_ratings)) # 129971

wine_ratings = wine_ratings.dropna(subset=['country'])
print(wine_ratings.isnull().sum())
"""
title       0
country     0
rating      0
price       0
"""
print(len(wine_ratings)) # 129908
```

#### Editing

* `s.replace(1,'one')` -- replace all values equal to 1 with 'one'
* `s.replace([1,3],['one','three'])` -- replace all values equal to 1 with 'one' and all values equal to 3 with 'three'
* `df.rename(columns={'old_name': 'new_ name'})` -- rename specific columns
* `df.set_index('column_one')` -- change the index of the data frame


```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

wine_reviews.rename(columns={'designation': 'vineyard'}, inplace=True)
wine_reviews.rename(columns={'points': 'rating'}, inplace=True)
```

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```


#### Sorting

* `df.sort_values(col1)` -- sort values in a certain column in *ascending* order
* `df.sort_index(axis=1)` -- sort axis values by index in *ascending* order
* `df.sort_values(col2,ascending=False)` -- sort values in a certain column in *descending* order
* `df.sort_index(axis=1, ascending=False)` -- sort axis values by index in *descending* order
* `df.sort_values([col1,col2],ascending=[True,False])` -- sort values in a col1 in *asscending* order, then sort values in col2 in *descending* order
* `df.rank()` -- rank every variable according to its value

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```

#### Reshaping

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```

#### Groupby

* `df.groupby(col)` -- returns groupby object for values from a single, specific column
* `df.groupby([col1,col2])` -- returns a groupby object for values from multiple columns, which you can specify

>>
filtering --- https://towardsdatascience.com/how-to-filter-rows-of-a-pandas-dataframe-by-column-value-51996ea621f8

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```


#### `Apply` Functions

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```

## Joining & Concatenating Data

>>https://www.datacamp.com/community/tutorials/joining-dataframes-pandas
https://pandas.pydata.org/pandas-docs/stable/user_guide/merging.html

* `df1.append(df2)` -- add the rows in df1 to the end of df2 (columns should be identical)
* `df.concat([df1, df2],axis=1)` —- add the columns in df1 to the end of df2 (rows should be identical)
* `df1.join(df2,on=col1,how='inner')` —- SQL-style join the columns in df1 with the columns on df2 where the rows for colhave identical values. how can be equal to one of: 'left', 'right', 'outer', 'inner'

>> https://www.tutorialspoint.com/python_pandas/python_pandas_merging_joining.htm
* `df.merge()` -- 
* `df.merge_ordered()` -- 

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


pd.merge(left, right, how='inner', on=None, left_on=None, right_on=None,left_index=False, right_index=False, sort=True)
```


```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```


```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')


```


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

```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

countries = wine_reviews['country']
unique_countries = countries.unique()
print(f'There are {countries.nunique()} unique countries: \n', unique_countries) 
"""
There are 43 unique countries:
['Italy' 'Portugal' 'US' 'Spain' 'France' 'Germany' 'Argentina' 'Chile' 'Australia' 'Austria' 'South Africa' 'New Zealand' 'Israel' 'Hungary' 'Greece' 'Romania' 'Mexico' 'Canada' nan 'Turkey' 'Czech Republic' 'Slovenia' 'Luxembourg' 'Croatia' 'Georgia' 'Uruguay' 'England' 'Lebanon' 'Serbia' 'Brazil' 'Moldova' 'Morocco' 'Peru' 'India' 'Bulgaria' 'Cyprus' 'Armenia' 'Switzerland' 'Bosnia and Herzegovina' 'Ukraine' 'Slovakia' 'Macedonia' 'China' 'Egypt']
"""

country_counts = countries.value_counts(dropna=False)
print(country_counts.head(3))
"""
US        54504
France    22093
Italy     19540
"""
```




```python
import numpy as np
import pandas as pd
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')

wine_ratings = wine_reviews[['title', 'country', 'rating', 'price']] # [129971 rows x 4 columns]
print(wine_ratings.describe())
"""
              rating          price
count  120916.000000  120916.000000
mean       88.421723      35.368644
std         3.044942      41.031052
min        80.000000       4.000000
25%        86.000000      17.000000
50%        88.000000      25.000000
75%        91.000000      42.000000
max       100.000000    3300.000000
"""
```

```python
import numpy as np
import pandas as pd

```


```python
import numpy as np
import pandas as pd

```


```python
import numpy as np
import pandas as pd


```


```python
import numpy as np
import pandas as pd

```




