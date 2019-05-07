<!---
{"next": "Topics/data_viz.md","title": "Data Manipulation"}
-->

# Data Manipulation with Pandas

*More Coming Soon...*

<img src="https://media.giphy.com/media/EatwJZRUIv41G/giphy.gif" style="margin: 0 auto; display: block;"/><br>

In this section, our core focus will be using our wine review dataset to learn how to manipulate Pandas data structures objects. At a high-level, this lesson will cover:

>>* DataFrame Objects
* Viewing & Inspecting Data
	* summary func
	* describe/head etc.
	* selection
* Data Cleaning & Organization
	* !!!!! join, groupby, sort, map, apply, pivot
* Data Exploration
	* Statistics
	* Visualization (*maybe*)

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






