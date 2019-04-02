<!---
{"next": "Topics/pandas.md","title": "Loops"}
-->

# Iterating with Loops

In programming, we define iteration to be the act of running the same block of code over and over again a certain number of times. For example, say you want to print out every item within a list. You could certainly do it this way -

```python
visible_colors = ["red", "orange", "yellow", "green", "blue", "violet"]
print(visible_colors[0])
print(visible_colors[1])
print(visible_colors[2])
print(visible_colors[3])
print(visible_colors[4])
print(visible_colors[5])
```

Attempting to print each item in this list - while redundant - isn't so bad. But what if there were over 1000 items in that list? Or, worse still, what if that list changed based on user input (ie: *either* 10 items *or* 10000 items)?

To solve such problems, we can create a **loop** that will iterate through each item on our list and run the `print()` function. This way, we only have to write the print() one time to print out the whole list!

## the `while` loop

This is the simplest loop and is essentially a way to count:

```python
i = 0
while i < 100:
	print(i)
	i = i + 1
```

What is happening here is we are running the code block within the `while` 100 times. We know to stop because the `boolean comparison` will evaluate to `False` once i exceeds `100`, which is possible only because `i` is being incremented.

## the `for` loop

Now let's say we want to access some specific items from the lists and dicts we created in the last section and perform an operation on each of those items. We could get each item we're thinking of, but that could take a LONG time! 

In programming, we define iteration to be the act of running the same block of code over and over again a certain number of times. In simplest terms, this can be defined as:

```python
for i in range(11, 15):
    print(i, i ** 2)
    
# the above will print:
# 11 121
# 12 144
# 13 169
# 14 196
# 15 225
```

However, we can iterate over lists and dicts! Neato!

List iteration example:

```python
test_scores = [100, 68, 95, 84, 79, 99]
for score in test_scores:
  if score > 85:
    print(score, "passed!")
  else:
    print(score, "failed!")
    
# 100 passed!
# 68 failed!
# 95 passed!
# 84 failed!
# 79 failed!
# 99 passed!

```

Dict iteration example:

```python
students = {
  'taq': [86, 45, 98, 100],
  'sue': [100, 100, 100, 100],
  'jon': [38, 49, 90, 87],
}

def avg(list_of_grades):
  sum = 0
  for grade in list_of_grades:
    sum = sum + grade
  
  return sum / len(list_of_grades)
  
for student, grades in students.items():
  avg_student = avg(grades)
  if avg_student > 70:
    print(f"{student} passed with avg of {avg_student}")
  else:
    print(f"{student} failed with avg of {avg_student}")
```

Want index number in array loop?

```python
test_scores = [100, 68, 95, 84, 79, 99]
for idx, score in enumerate(test_scores):
  print(idx, score)
```



## 🚗 1. Shopping List Calculator w/User Input

Let's improve our calculator! Remember **[this](basic_data_types.md#-practice-shopping-list-calculator-i)** problem? Let's do it again, but this time - instead of hardcoding the variables, let's use a loop. Based on the inputs below, develop a problem where user can interactively add as many shopping list items as he wants and see the running total:

(The *>* is computer prompt, *<* is user response)

```text
> How many items?
< 2
> 1. Enter name of item:
< Eggs
> 1. Enter price of item:
< 2.00
> 1. Enter quantity of item:
> 6

> 2. Enter name of item:
< Steak
> 2. Enter price of item:
< 14.00
> 2. Enter quantity of item:
> 1

> Your total is: 26.00
> Tax is: 2.28
> Total total is: 28.28

```
