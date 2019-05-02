<!---
{"next": "Topics/pandas.md","title": "Pandas Basics"}
-->

# Pandas Basics
<img src="https://media.giphy.com/media/EatwJZRUIv41G/giphy.gif" style="margin: 0 auto; float: right;"/>
**Pandas** is an open-source Python library of data structures and tools for exploratory data analysis (EDA). Pandas primarily facilitates acquisition, cleaning, formatting, and manipulating. Used in tandem with NumPy, Matplotlib, SciPy, and other Python libraries, Pandas is an integral part of practicing data science.

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

## Setting Up Our First Data Science Project

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