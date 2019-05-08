<!---
{"next": "Topics/data_viz.md","title": "Data Manipulation"}
-->

# Data Manipulation with Pandas

In this section, our core focus will be using our wine review dataset to learn how to manipulate Pandas data structures objects. At a high-level, this lesson will cover:

* Wine Review Data Dictionary
* Importing Data
* Wrangling, Cleaning, & Organizing Data
* Explorational Data Analysis
* *More coming soon*

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

print(wine_reviews.shape) # (rows, columns) is (129971, 13)
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


