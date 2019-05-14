<!---
{"next": "Topics/data_viz.md","title": "Pandas Analysis II"}
-->

# Pandas Analysis II

In this lesson, we'll continue exploring Pandas for EDA. Specifically: 

- Identify and handle missing values with Pandas.
- Implement groupby statements for specific segmented analysis.
- Use apply functions to clean data with Pandas.

## Data sets

* **[Adventureworks Cycles | Local](https://raw.githubusercontent.com/mottaquikarim/PythonProgramming/master/raw_data/production.product.tsv)**
	* *You can download a version of the Adventureworks Cycles dataset directly from this Github Repo* 


## Let's continue with the AdventureWorks Cycles Dataset

Here's the Production.Product table [data dictionary](https://www.sqldatadictionary.com/AdventureWorks2014/Production.Product.html), which is a description of the fields (columns) in the table (the .csv file we will import below):<br>

- **ProductID** - Primary key for Product records.
- **Name** - Name of the product.
- **ProductNumber** - Unique product identification number.
- **MakeFlag** - 0 = Product is purchased, 1 = Product is manufactured in-house.
- **FinishedGoodsFlag** - 0 = Product is not a salable item. 1 = Product is salable.
- **Color** - Product color.
- **SafetyStockLevel** - Minimum inventory quantity.
- **ReorderPoint** - Inventory level that triggers a purchase order or work order.
- **StandardCost** - Standard cost of the product.
- **ListPrice** - Selling price.
- **Size** - Product size.
- **SizeUnitMeasureCode** - Unit of measure for the Size column.
- **WeightUnitMeasureCode** - Unit of measure for the Weight column.
- **DaysToManufacture** - Number of days required to manufacture the product.
- **ProductLine** - R = Road, M = Mountain, T = Touring, S = Standard
- **Class** - H = High, M = Medium, L = Low
- **Style** - W = Womens, M = Mens, U = Universal
- **ProductSubcategoryID** - Product is a member of this product subcategory. Foreign key to ProductSubCategory.ProductSubCategoryID.
- **ProductModelID** - Product is a member of this product model. Foreign key to ProductModel.ProductModelID.
- **SellStartDate** - Date the product was available for sale.
- **SellEndDate** - Date the product was no longer available for sale.
- **DiscontinuedDate** - Date the product was discontinued.
- **rowguid** - ROWGUIDCOL number uniquely identifying the record. Used to support a merge replication sample.
- **ModifiedDate** - Date and time the record was last updated.

## Loading the Data

We can load our data as follows:

```python
import pandas as pd
import numpy as np

prod = pd.read_csv('/raw_data/production.product.tsv', sep='\t')

```

Note the `sep='\t'`; this is because we are pulling in a `tsv` file, which is basically a csv file but with `tabs` as delimiters vs commas.

**YOU DO**: Download the `tsv` file into your local machine, create a python virtualenv and run the code above, but on your machine.


## Handling missing data

Recall missing data is a systemic, challenging problem for data scientists. Imagine conducting a poll, but some of the data gets lost, or you run out of budget and can't complete it! 😮<br><br>

"Handling missing data" itself is a broad topic. We'll focus on two components:

- Using Pandas to identify we have missing data
- Strategies to fill in missing data (known in the business as `imputing`)
- Filling in missing data with Pandas

### Identifying missing data

Before *handling*, we must identify we're missing data at all!

We have a few ways to explore missing data, and they are reminiscient of our Boolean filters.

```python
# True when data isn't missing
prod.notnull().head(3)
# True when data is missing
prod.isnull().head(3)
```

**OUTPUT**: `notnull`

```text
   ProductID  Name  ProductNumber  MakeFlag  FinishedGoodsFlag  Color  ...  ProductModelID  SellStartDate  SellEndDate  DiscontinuedDate  rowguid  ModifiedDate
0       True  True           True      True               True  False  ...           False           True        False             False     True          True
1       True  True           True      True               True  False  ...           False           True        False             False     True          True
2       True  True           True      True               True  False  ...           False           True        False             False     True          True

[3 rows x 25 columns]
```

**OUTPUT**: `isnull`

```text
   ProductID   Name  ProductNumber  MakeFlag  FinishedGoodsFlag  Color  ...  ProductModelID  SellStartDate  SellEndDate  DiscontinuedDate  rowguid  ModifiedDate
0      False  False          False     False              False   True  ...            True          False         True              True    False         False
1      False  False          False     False              False   True  ...            True          False         True              True    False         False
2      False  False          False     False              False   True  ...            True          False         True              True    False         False

[3 rows x 25 columns]
```

* **YOU DO**: count the number of nulls in `Name` column
* **YOU DO**: count the number of notnulls in `Name` column

We can also access missing data in aggregate, as follows:

```python
# here is a quick and dirty way to do it
prod.isnull().sum()
```

```text
Name                       0
ProductNumber              0
MakeFlag                   0
FinishedGoodsFlag          0
Color                    248
SafetyStockLevel           0
ReorderPoint               0
StandardCost               0
ListPrice                  0
Size                     293
SizeUnitMeasureCode      328
WeightUnitMeasureCode    299
Weight                   299
DaysToManufacture          0
ProductLine              226
Class                    257
Style                    293
ProductSubcategoryID     209
ProductModelID           209
SellStartDate              0
SellEndDate              406
DiscontinuedDate         504
rowguid                    0
ModifiedDate               0
dtype: int64
```

## Pandas Reference


At a high-level, this section will will cover:

* [Joining & Concatenating](eda.md#joining--concatenating)
* [Grouping](eda.md#grouping)
* [Filtering](eda.md#filtering)
* [Descriptive Statistics](eda.md#descriptive-statistics)


## Joining & Concatenating

* `df1.append(df2)` -- add the rows in df1 to the end of df2 (columns should be identical)
* `df.concat([df1, df2],axis=1)` —- add the columns in df1 to the end of df2 (rows should be identical)
* `df1.join(df2,on=col1,how='inner')` —- SQL-style join the columns in df1 with the columns on df2 where the rows for col have identical values. how can be equal to one of: 'left', 'right', 'outer', 'inner'
* `df.merge()` -- merge two datasets together into one by aligning the rows from each based on common attributes or columns. how can be equal to one of: 'left', 'right', 'outer', 'inner'

## Reshaping

* `df.transform(func[, axis])` -- return DataFrame with transformed values
* `df.transpose(*args, **kwargs)` -- transpose rows and columns
* `df.rank()` -- rank every variable according to its value
* `pd.melt(df)` -- gathers columns into rows
* `df.pivot(columns='var', values='val')` -- spreads rows into columns

## Grouping w. GroupBy Objects

* `df.groupby(col)` -- returns groupby object for values from a single, specific column
* `df.groupby([col1,col2])` -- returns a groupby object for values from multiple columns, which you can specify

## Filtering


## Descriptive Statistics

* `df[col1].unique()` -- returns an ndarray of the distinct values within a given series
* `df[col1].nunique()` -- return # of unique values within a column
* `.value_counts()` -- returns count of each unique value
* `df.sample(frac = 0.5)` - randomly select a fraction of rows of a DataFrame
* `df.sample(n=10)` - randomly select n rows of a DataFrame
* `mean()` -- mean
* `median()` -- median
* `min()` -- minimum
* `max()` -- maximum
* `quantile(x)` -- quantile
* `var()` -- variance
* `std()` -- standard deviation
* `mad()` -- mean absolute variation
* `skew()` -- skewness of distribution
* `sem()` -- unbiased standard error of the mean
* `kurt()` -- kurtosis
* `cov()` -- covariance
* `corr()` -- Pearson Correlation coefficent
* `autocorr()` -- autocorelation
* `diff()` -- first discrete difference
* `cumsum()` -- cummulative sum
* `comprod()` -- cumulative product
* `cummin()` -- cumulative minimum
