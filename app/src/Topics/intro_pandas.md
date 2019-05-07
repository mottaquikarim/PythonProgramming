<!---
{"next": "Topics/pandas.md","title": "Intro to Pandas"}
-->

# Intro to Pandas & NumPy

<img src="https://media.giphy.com/media/EatwJZRUIv41G/giphy.gif" style="margin: 0 auto; float: right;"/>

**Pandas** is an open-source Python library of data structures and tools for exploratory data analysis (EDA). Pandas primarily facilitates acquisition, cleaning, formatting, and manipulating. Used in tandem with NumPy, Matplotlib, SciPy, and other Python libraries, Pandas is an integral part of practicing data science.

To gain some baseline familiarity with Pandas features and pre-requisites, in this lesson, you'll learn about:

* Capabilities of Pandas
* NumPy `ndarray` Objects
* Setting Up Your First Data Science Project

## Capabilities of Pandas
* Robust IO tools to reading from flat files (CSV and TXT), JSON, XML, Excel files, SQL tables, and other databases.
* Inserting and deleting columns in DataFrame and higher dimensional objects
* Handling missing data in both floating point and non-floating point data sets
* Merging & joining datasets
* Reshaping and pivoting datasets
* Conditional data sorting and filtering
* Iterating through data sets
* Aggregating and transforming data sets with split-apply-combine operations from the group by engine
* Automatic and explicit aligning and manipulating of high-dimensional data structures via hierarchical labeling and axis indexing
* Subsetting, fancy indexing, and label-based slicing large data sets
* Time-series functionality such as date range generation, date shifting, lagging, frequency conversions, moving window statistics, and moving window linear regressions.

## Basic Data Structures: NumPy ndarrays

Because Pandas is built on top of NumPy, new users should first understand one NumPy data object that often appears within Pandas objects - the ndarray. An **ndarray, or N-dimensional array,** is a data type from the NumPy library. Ndarrays are deceptively similar to the more general Python `list` type we've been working with. An `ndarray` type is a group of elements, which can be accessed and updated using a zero-based index. Sounds exactly like a `list`, right? You can create and print an ndarray exactly like a list. You can even create an ndarray *from* a list like this:

```python
import numpy as np

listA = [1, 2, 3]
arrayA = np.array([1, 2, 3])
print(listA) # [1, 2, 3]
print(arrayA) # [1 2 3]

listB = ['a', 'b', 'c']
arrayB = np.array(listB)
print(listB) # ['a', 'b', 'c']
print(arrayB) # ['a' 'b' 'c']
```

However, there are several important differences to remember:

First, all ndarrays are homogenous.* All elements in an ndarray must be the same data type (e.g. integers, floats, strings, booleans, etc.). If you try to enter data that is not homogenous, the `.array()` function will force unity of data type. Side note - notice that ndarrays get printed out without commas.

```python
import numpy as np

arrayC = np.array([1, 'b', True])
print(arrayC) # ['1', 'b', 'True']

arrayD = np.array([1, False])
print(arrayD) # [1 0]
```

Second, ndarrays have a parameter called `ndmin`, which allows you to specify the number of dimensions you want for your array when you create it. Here are the three key takeaways from the examples of this below.
* Notice how each dimension prints on its own line, so the ndarray looks more like a *grid* than a single list.
* `arrayE1` and `arrayE2` above are identical. This illustrates that the `nddim` parameter is optional. In other words, you can directly pass in multi-dimensional data without having to enter an argument for it.
* `arrayF` throws an error because it's missing one vital piece of syntax that `arrayC1` has. Do you see it? The first parameter in the `.array()` method is the object (i.e. the values you want contained in the array). When you pass values for multiple dimensions of the array object into the `.array()` method, you separate them with commas. *You have to make sure you group the dimensions and their values into a single group by adding `()` around them.* If you don't, the `.array()` method might mistake the second dimension and its values for the second *parameter* of the `.array()` method.

```python
import numpy as np

arrayE1 = np.array(([1, 2, 3], [4, 5, 6]))
print(arrayC1)
"""
[[1 2 3]
 [4 5 6]]
"""

arrayE2 = np.array(([1, 2, 3], [4, 5, 6]), ndmin = 2)
print(arrayC2)
"""
[[1 2 3]
 [4 5 6]]
"""

arrayF = np.array([1, 2, 3], [4, 5, 6])
print(arrayF) # Error
```

The third, and most important, difference between an array and a list is, *ndarrays are designed to handle **vectorized** operations* while a python list is not. In other words, if you apply a function to an ndarray object, the program will perform said function on each item in the array individually. If you apply a function to a list, the function to be performed on the list object as a whole.As a bonus, these vectorization capabilities also allow ndarrays take up less memory space and run faster.

```python
import numpy as np

listG = [1, 2, 3]
arrayG = np.array(listA)

print(arrayG + 2) # [3 4 5]
print(listG + 2) # Error
```

#### Creating Random & Range ndarrays

There are a handful of other ways to create ndarrays, including random generation...

```python
import numpy as np
import random

# Create an array of 5 random integers between 50 and 100. They will form a uniform distribution.
rand_array1 = np.random.randint(50,  100,  5)
print(rand_array1) # [54 86 91 61 90]

# Create a matrix of 2 rows and 3 columns, with all values between -1 and 1.
rand_array2 = np.random.rand(2, 3)
print(rand_array2)
"""
[[0.11298458 0.49065597 0.14219546]
 [0.27545168 0.87526704 0.93213146]]
"""

# Create a matrix of 2 rows and 3 columns, with all values between 0 and 1. They will form a normal distribution.
rand_array3 = np.random.randn(2, 3)
print(rand_array3)
"""
[[-0.24525306  1.9082735   0.55667231]
 [-1.17418436  0.12749887 -1.47157527]]
"""
```

...and via the `.arange()` method. This method takes the start point of the array, the end point, and (optionally) the step size. Remember that the final value will actually be one less than the specified end point.

```python
range_array = np.arange(2, 8, 2)
print(range_array) # [2, 4, 6]
```

## Setting Up Your First Data Science Project

Before we dive into analysis, we have to make sure we set up a stable, organized environment. For our lesson on Pandas we'll be using this dataset:

[Wine Reviews | Kaggle](https://www.kaggle.com/zynicide/wine-reviews/) -- 
*130k wine reviews with variety, location, winery, price, & description*

Instead of convoluting things with a specialized Data Science IDE, we're going to start simple -- working locally, straight in the terminal. We'll walk through how to spin this up together step by step:

**1)** On your Desktop, create a new folder called "WineReviews". In here, we want to split up our code files from our raw data files to keep things organized.

**2)** Within this parent directory, create an empty "main.py" file.

**3)** Now, create another folder called "raw_data". Drag the `wine_reviews.csv` file into it.

**4)** Go back to the main.py file. In practice, when we go to run the main.py file in terminal, the code we'll write here will open the csv file and give the program access to its full contents.

```python
import numpy as np 
import pandas as pd

# B) Read csv file
wine_reviews = pd.read_csv('raw_data/winemag-data-130k.csv')
```

First, notice that the standard is to import numpy and pandas into your python program as `np` and `pd`. Second, when you write the command to open the file, make sure you put the file name in quotes and reference the path to its location in the project directory.

**5)** Open up your terminal and `cd` into our project's parent directory.

```terminal
cd ~/Desktop/WineReviews
```

**6)** Create your virtual environment

```terminal
python3 -m venv .env
```

**7)** Activate the virtual environment.

```terminal
source .env/bin/activate
```

**8)** Install Pandas.

```terminal
pip install pandas
```

There are a couple salient points to mention here:

>> * **Remember** that we installed Python3 in our high-level system environment, but you don't want to do that with more specific libraries. It could cause you to run into issues if a certain version references older iterations of that library. 
>> * For the `WineReviews` project, you will only have to install Pandas once. Every time you reactivate this project's virtual environment, it will have it there.
>> * Having NumPy installed is a pre-requisite for using Pandas. However, installing Pandas automatically installs NumPy. That's why we don't have to call `pip install numpy` explicitly.

**9)** Run the main.py file to make sure the code works!

```terminal
python3 main.py
```

## Reading Files Summary

We've just finished preparing our first dataset for analysis. This one was in .CSV format, but we also learned above that Pandas can handle many different file types. To open each of these in pandas we use a slightly customized version of the general method `pd.read_<filetype>(<file_name>)`.

For your future reference, here's a quick summary of commands for handling different file types in Pandas. You can also find this [here](../Resources/pandas_glossary.html#reading--writing-data) as part of our larger Pandas Glossary.

* `pd.read_csv(filename)` -- From a CSV file
* `pd.read_table(filename)` -- From a delimited text file (like TSV)
* `pd.read_excel(filename)` # From an Excel file
* `pd.read_sql(query, connection_object)` # Reads from a SQL table/database
* `pd.read_json(json_string)` # Reads from a JSON formatted string, URL or file.
* `pd.read_html(url)` # Parses an html URL, string or file and extracts tables to a list of dataframes
* `pd.read_clipboard()` # Takes the contents of your clipboard and passes it to read_table()