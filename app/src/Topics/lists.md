<!---
{"next": "Topics/loops.md","title": "Lists"}
-->

# Lists

In order to begin to truly write dynamic programs, we need to be able to work with *dynamic* data where we do not know how much of a certain type of variable we have.

The problem, essentially is, **variables hold one item**.

```python
my_color = "red"
my_peer = "Brandi"
```

Lists hold multiple items - and lists can hold anything.

## Working with lists

Here's how we may declare a list variable.

```python
colors = ["red", "yellow", "green"]
grades = [100, 99, 65, 54, 19]
```

### Strings
```python
colors = ["red", "yellow", "green"]
```

### Numbers
```python
my_nums = [4, 7, 9, 1, 4]
```

### Booleans
```python
bools = [True, False, True, True]
```

### Other lists
```python
taq = [100, 100, 100]
john = [85, 98, 54]

students = [taq, john]
```

## Accessing Elements


**List Index** means the location of something (an *element*) in the list.

List indexes start counting at 0!

|  List | "Brandi" | "Zoe" | "Steve" | "Aleksander" | "Dasha" |
|:-----:|:--------:|:-----:|:-------:|:------:|:------:|
| Index |     0    |   1   |    2    |    3   |    4   |

```python
my_class = ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha"]
print(my_class[0]) # Prints "Brandi"
print(my_class[1]) # Prints "Zoe"
print(my_class[4]) # Prints "Dasha"
```

## List Operations - Length


`len()`:

- A built in `list` operation.
- How long is the list?

```python
# length_variable = len(your_list)

my_class = ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha"]
num_students = len(my_class)
print("There are", num_students, "students in the class")
# => 5
```

## Adding Elements: Append

`.append()`:

- A built in `list` operation.
- Adds to the end of the list.
- Takes any element.

```python
# your_list.append(item)

my_class = ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha"]
my_class.append("Sonyl")
print(my_class)
# => ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha", "Sonyl"]
```

## Adding Elements: Insert

`.insert()`:

- A built in `list` operation.
- Adds to any point in the list
- Takes any element and an index.

```python
# your_list.insert(index, item)

my_class = ["Brandi", "Zoe", "Steve", "Aleksander", "Dasha", "Sonyl"]
my_class.insert(1, "Sanju")
print(my_class)
# => ["Brandi", "Sanju", "Zoe", "Steve", "Aleksander", "Dasha", "Sonyl"]
```

## Removing elements - Pop


`.pop()`:

- A built in `list` operation.
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

## Removing elements - Pop(index)

`.pop(index)`:

- A built in `list` operation.
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

## Quick Review: Basic List Operations

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
```

## Numerical List Operations - Sum

Some actions can only be performed on lists with numbers.

`sum()`:

- A built in `list` operation.
- Adds the list together.
- Only works on lists with numbers!

```python
# sum(your_numeric_list)

team_batting_avgs = [.328, .299, .208, .301, .275, .226, .253, .232, .287]
sum_avgs = sum(team_batting_avgs)
print("The total of all the batting averages is", sum_avgs)
# => 2.409
```

## List Operations - Max/Min


`max()` or `min()`:

- Built in `list` operations.
- Finds highest, or lowest, in the list.

```python
# max(your_numeric_list)
# min(your_numeric_list)

team_batting_avgs = [.328, .299, .208, .301, .275, .226, .253, .232, .287]
print("The highest batting average is", max(team_batting_avgs))
# => 0.328
print("The lowest batting average is", min(team_batting_avgs))
# => 0.208
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


## 🚗 2. Pop, Insert, and Append

1. Declare a list with the names of your classmates
2. Print out the length of that list
3. Print the 3rd name on the list
4. Delete the first name on the list
5. Re-add the name you deleted to the end of the list

## 🚗 3. Math Operations

On your local computer, create a `.py` file named `list_practice.py`. In it:

1. Save a list with the numbers `2`, `4`, `6`, and `8` into a variable called `numbers`.
2. Print the max of `numbers`.
3. Pop the last element in `numbers` off; re-insert it at index `2`.
4. Pop the second number in `numbers` off.
5. Append `3` to `numbers`.
6. Print out the average number (divide the sum of `numbers` by the length).
7. Print `numbers`.
