<!---
{"next": "Topics/dicts.md","title": "Lists"}
-->

# Lists

In order to begin to truly write dynamic programs, we need to be able to work with *dynamic* data where we do not know how much of a certain type of variable we have.

The problem, essentially is, **variables hold only one item**.

```python
my_color = "red"
my_peer = "Brandi"
```
Lists hold multiple items - and lists can hold any datatype.

## Creating lists

Here are some different ways to declare a list variable:

```python
colors = ['red', 'yellow', 'green'] #strings
grades = [100, 99, 65, 54, 19] #numbers
bools = [True, False, True, True] #booleans
```

To create a new **blank** list, simply use ```python blank_list = list()```.

## Accessing Elements in the List

The **list index** means the location of something (an *element*) in the list.

List indexes start counting at 0!

|  List | "Brandi" | "Zoe" | "Steve" | "Aleksander" | "Dasha" |
|:-----:|:--------:|:-----:|:-------:|:------:|:------:|
| Index |     0    |   1   |    2    |    3   |    4   |

```python
my_class = ['Brandi', 'Zoe', 'Steve', 'Aleksander', 'Dasha']
print(my_class[0]) # Prints "Brandi"
print(my_class[1]) # Prints "Zoe"
print(my_class[4]) # Prints "Dasha"
```

## Built-in Operations for Analyzing Lists

Python has some built-in operations that allow you to analyze the content of a list. Some basic ones include:

* ```len()```: tells you how many items are in the list; can be used for lists composed of any data type (i.e. strings, numbers, booleans)
* ```sum()```: returns the sum of all items in *numerical lists*. 
* ```min()```: returns the smallest number *in a numerical list*.
* ```max()```: returns the largest number *in a numerical list*.
* ```any()```: returns a Boolean to indicates whether the list contains any values that evaluate to True
* ```all()```: returns a Boolean to indicates whether the list contains only values that evaluate to True

Here are some examples of each of these:

#### Length of a List
```python
# length_variable = len(your_list)

my_class = ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha"]
num_students = len(my_class)
print("There are", num_students, "students in the class")
# => 5
```

#### Sum of Items in a Numerical List
```python
# sum_variable = sum(your_numeric_list)

team_batting_avgs = [.328, .299, .208, .301, .275, .226, .253, .232, .287]
sum_avgs = sum(team_batting_avgs)
print(f"The total of all the batting averages is {sum_avgs}")
# => 2.409
```

#### Min and Max of a Numerical List
```python
# max(your_numeric_list)
# min(your_numeric_list)

team_batting_avgs = [.328, .299, .208, .301, .275, .226, .253, .232, .287]
print(f"The highest batting average is {max(team_batting_avgs}")
# => 0.328
print("The lowest batting average is", min(team_batting_avgs))
# => 0.208
```

#### Checking a List for Any Instances of an Element
Did anyone in the class get a perfect SAT score (i.e. 2400)?
```python
SAT_scores = [1890, 2010, 1740, 2400, 1970, 2400, 2150, 2280]
perfect_score = any(x = 2400 for x in SAT_scores)

if perfect_score is True:
	print("At least one person got a perfect SAT score!")
	# Based on the scores above, it will print this.
```

#### Checking for Consistency Between all Elements in a List
Consider this:
You just heard about a new Peruvian restaurant and want to try it. You take a poll asking whether your friends like Peruvian food or not to see if everyone would be okay with going to the new restaurant. If you get a unanimous yes, you can start dreaming about lomo saltado and ceviche - yum!

```python
poll_results = [True, False, True, False, True] # using booleans!
decision = all(poll_results)
print(decision)
```
Sadly, not all your friends like Peruvian food! Your all() function found 2 people who said "no" (i.e. False), so it returned ```False```. The decision is not unanimous, so you suggest a Korean restaurant you like and take another poll...

```python
poll_results = [True, True, True, True, True]
decision = all(poll_results)
print(decision)
```

## Built-In Operations for Manipulating Lists

#### Add Items to a List

If you want to extend the content of a single list, you can use `.append()` or `.insert()` to add elements of any data type.

`.append()`:
- Adds to the end of the list.

```python
# your_list.append(item)

my_class = ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha"]
my_class.append("Sonyl")
print(my_class)
# => ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha", "Sonyl"]
```

`.insert()`:
- Adds to any point in the list.
- Takes a index argument.

```python
# your_list.insert(index, item)

my_class = ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha", "Sonyl"]
my_class.insert(1, "Sanju")
print(my_class)
# => ["Brandi", "Sanju", "Zoe", "Steve", "Aleksander", "Dasha", "Sonyl"]
```

#### Delete Items from a List

Likewise, you can use `.pop()` or `.pop(index)` to remove any type of element from a list.

`.pop()`:
- Removes an item from the end of the list.

```python
# your_list.pop()

my_class = ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha", "Sonyl"]
student_that_left = my_class.pop()
print("The student", student_that_left, "has left the class.")
# => "Sonyl"
print(my_class)
# => ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha"]
```

`.pop(index)`:
- Removes an item from the list.
- Can take an index.

```python
# your_list.pop(index)

my_class = ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha", "Sonyl"]
student_that_left = my_class.pop(2) # Remember to count from 0!
print("The student", student_that_left, "has left the class.")
# => "Steve"
print(my_class)
# => ["Brandi", "Zoe", "Aleksander", "Dasha", "Sonyl"]
```

#### Sorting Lists

If you want to organize your lists better, you can sort them with the `sorted()` method. At the some basic level, you can sort both numerically and alphabetically.

**Numbers - Ascending & Descending

```python
numbers = [1, 3, 7, 5, 6, 4, 2]

ascending = sorted(numbers)
print(ascending) # [1, 2, 3, 4, 5, 6, 7]
```
To do this in descending order, simply add `reverse=True` as an argument in `sorted()` like this:
```python
descending = sorted(numbers, reverse=True)
print(descending) # [7, 6, 5, 4, 3, 2, 1]
```
Letters - Alphabetically & Reverse

```python
letters = ['b', 'e', 'c', 'a', 'd']

ascending = sorted(letters)
print(ascending) # ['a', 'b', 'c', 'd', 'e']

descending = sorted(letters, reverse=True)
print(descending) # ['e', 'd', 'c', 'b', 'a']
```

### Review of Basic List Operations

```python
# List Creation
my_list = ["red", 7, "yellow", 1]

# List Length
list_length = len(my_list) # 4

# List Index
print(my_list[0]) # red

# List Append
my_list.append("Yi") # ["red", 7, "yellow", 1, "Yi"]

# List Insert at Index
my_list.insert(1, "Sanju") # ["red", "Sanju", 7, "yellow", 1, "Yi"]

# List Delete
student_that_left = my_list.pop() # "Yi"; ["red", "Sanju", 7, "yellow", 1]

# List Delete at Index
student_that_left = my_list.pop(2) # 7; ["red", "Sanju", "yellow", 1]

# List Sorting
numbers = [1, 5, 7, 3, 6, 4, 2]
ascending = sorted(numbers) # [1, 2, 3, 4, 5, 6, 7]
descending = sorted(numbers, reverse=True) # [7, 6, 5, 4, 3, 2, 1]
```

## Tuples

Tuples are a special subset of lists - they are *immutable* - in that they cannot be changed after creation.

We write tuples as:

```python
score_1 = ('Taq', 100)

# OR

score_2 = 'Sue', 101
```

Tuples are denoted with the `()`.

We read tuples just like we would read a list:

```python
print(score_1[0]) # 'Taq'
```

## Sets

Sets are special lists in that they can only have **unique** elements

```python
set_1 = {1,2,3,4,5} # this is a set, notice the {}
set_2 = {1,1,1,2,2,3,4,5,5,5} # this is still a set
print(set_2) # {1,2,3,4,5}

print(set_1 == set_2) # True
```

Sets are not indexed, so you cannot access say the 3rd element in a set. Instead, you can:

```python
print(2 in set_1) # True
print(9 in set_1) # False
```
Here's a **[helpful list](https://snakify.org/en/lessons/sets/#section_4)** of set operations.


## 🚗 1. Simple List operations

1. Create a **list** with the names `"Holly"`, `"Juan"`, and `"Ming"`.
2. Print the third name.
3. Create a **list** with the numbers `2`,`4`, `6`, and `8`.
4. Print the first number.

## 🚗 2. Editing & Manipulating Lists

1. Declare a list with the names of your classmates
2. Print out the length of that list
3. Print the 3rd name on the list
4. Delete the first name on the list
5. Re-add the name you deleted to the end of the list
6. You work for Spotify and are creating a feature for users to alphabetize their playlists by song title. Below are is a list of titles from one user's playlist. Alphabetize these songs.
`playlist_titles = ["Rollin' Stone", "At Last", "Tiny Dancer", "Hey Jude", "Movin' Out"]`
7. Create a list with 6 numbers and sort it in descending order.

## 🚗 3. Math Operations

On your local computer, create a `.py` file named `list_practice.py`. In it:

1. Save a list with the numbers `2`, `4`, `6`, and `8` into a variable called `numbers`.
2. Print the max of `numbers`.
3. Pop the last element in `numbers` off; re-insert it at index `2`.
4. Pop the second number in `numbers` off.
5. Append `3` to `numbers`.
6. Print out the average number.
7. Print `numbers`.



## Additional Resources

- [Python Lists - Khan Academy Video](https://www.youtube.com/watch?v=zEyEC34MY1A)
- [Google For Education: Python Lists](https://developers.google.com/edu/python/lists)
- [Python-Lists](https://www.tutorialspoint.com/python/python_lists.htm)
- [Python List Methods](https://www.programiz.com/python-programming/methods/list/)
