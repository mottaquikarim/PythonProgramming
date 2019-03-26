<!---
{"next": "Homework/README.md","title": "Loops"}
-->

# Loops

Consider this problem - 

```python
visible_colors = ["red", "orange", "yellow", "green", "blue", "violet"]
print(visible_colors[0])
print(visible_colors[1])
print(visible_colors[2])
print(visible_colors[3])
print(visible_colors[4])
print(visible_colors[5])
```

Attempting to print each item in this list - while redundant - isn't so bad. But what if there were over 1000 items in that list? Or, worse still, what if that list changed based on user input (ie: *either* 10 items *or* 10000 items). 

To solve such problems, we must implement a **loop**.

## the `while` loop

The simplest loop is the `while` loop, which is essentially a way to count:

```python
i = 0
while i < 100:
	print(i)
	i = i + 1
```

What is happening here is we are running the code block within the `while` 100 times. We know to stop because the `boolean comparison` will evaluate to `False` once i exceeds `100`, which is possible only because `i` is being incremented.

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
