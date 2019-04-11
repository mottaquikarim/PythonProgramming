<!---
{"next":"Topics/classes.md","title":"Functions"}
-->

# Functions

In Python, `functions` are your best friends! Let's say you need to perform some action or calculation multiple times for multiple values. For example, you might want to convert temperatures in Celsius to Fahrenheit like you did in the last chapter's exercises. It would be inefficient and messy to copy that code every time you need it. Instead, you can define a `function` to contain that code. Every time you call that function, it runs the whole block of code inside and saves you lots of time. Sweet!

Python includes lots of built-in functions in its main library. We've seen lots of these already like `len()`, `sum()`, `.append()`, `.popitem`, etc. You can extend the range of built-in functions available to you by importing `modules`. We'll talk about those next!

## Elements of a Function

For now, let's start with the basics. Here's the skeleton of a function and a breakdown of each part.

```python
def function_name(parameters):
	"""docstring"""
	# statement(s)
```

* `def` shows you are "defining" a new function
* A unique function name; same naming rules as  variables)
* *Optional* parameters, or arguments, to be passed into the function when it is called.
* `:` ends the function header
* An *optional* `docstring`, i.e. a comment with documentation describing the function.
* At least one statement make up the "function body"; this code achieves the purpose for calling the function.
* An *optional* return statement, which exits the function and passes out some value from the body code.

**NOTE!** *It is a best practice to always create notes and documentation. Other potential users of your functions - and maybe future YOU - will thank you for the extra info.*

## Input/Output: Function Arguments & The `return` Statement

When you create a function, you might need to feed it some input and have it give back some output. We call function input `arguments` and function output `return` values. Remember - both `arguments` and `return` values are *optional* depending on the purpose of your function.

Let's say we want to create a function to get the square of a number. At the most basic level, there are three parts:
1. Input the number we want to square
2. Calculate the square of that number
3. Output the square of that number

Let's implement this in a function called `NumSquared()`.

```python
def NumSquared(num):
	"""Find the square of some number passed in"""
	square = num*num # code to find the square
	return square
```

1. Input the number we want to square 
	We create an argument called `num` to represent the number we will past into our function as an argument. Remember that arguments should always be passed in the correct format and positional order, or the function will not be able to recognize them.
2. Calculate the square of that number
	Using the value of `num`, we write the formula for calculating a square and assign it to the variable `square`.
3. Output the square of that number
	We return `square` to pass out the numeric value we calculated. The return statement exits the function so the program can move on to the next block of code you've written. If you don't need to specify a value to return, the function will default to `return None` in order to exit the function.

Once we've written this logic, we can call `NumSquared()` every time we want to use it. Let's say we want to find the value of 12 squared...

```python
sq12 = NumSquared(12)
print(sq12)
```

**NOTE!** You should store the function call within a var so that the return value gets stored in the var. If you don't, how will you access the output you wanted??

## Anonymous Functions

#### The `lambda` Keyword



## Variable Scope

```python
x = "global"

def foo():
    print("x inside :", x)

foo()
print("x outside:", x)
```


```python
def foo():
    y = "local"

foo()
print(y)
```

The above code will output `NameError: name 'y' is not defined` because `y` only exists within the function.