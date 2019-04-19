<!---
{"next":"Topics/pandas.md","title":"Classes"}
-->

# Classes & Inheritance

We already know that Python is based on the concept of **OOP, or Object-Oriented Programming**. Almost everything in Python is an object -- even functions are objects! **Classes**, and their facilitation of **inheritance**, are one of the most important and valuable Python objects.
## Creating & Structuring Classes
A **class** is essentially a data structure that serves as a blueprint for categorizing other objects and storing metadata about them. Once you have your "blueprint", you can create new **instances** of that class, which store unique metadata values. 

Creating a class is similar to defining a function. You start with the `class` keyword and then specify a name for the class. Note that class names are generally the only objects, which use a **CamelCase notation** naming convention. Here's the general structure:

```python
# Define a class called Animal
class Animal:
	# attributes
	# methods
	# etc ...
```

#### Attributes & Methods
Each piece of metadata is called an **attribute**. Once you have your "blueprint", you can create new **instances** of that class, which stores unique attribute values. For example, if you were a zookeeper, you might create a class called `Animal`. You would define your Animals class so that it could store attributes of each animal at your zoo such as species, natural habitat, age, gender, etc..

In addition to attributes, classes also contain custom **methods**. Methods are essentially functions that belong to the class. You can call a function without referencing any other object, but to call a method, you need to reference its class. *Thus, all methods are functions, but not all functions are methods.* We've already used some `List` methods like `my_list.pop()`, `my_list.append()`, `my.list.insert(index)`, etc.. When you create a class, you can define methods to serve as shortcuts for actions you might want to call frequently on instances of your class. 

## Class vs. Instance Variables

As you define attributes and methods for your class, keep in mind their *scope*. If you want a certain attribute or method to be shared by ALL instances of a class, define it as a **class variable**. If you instead want it to be unique to each instance, define it as an **instance variable**. Before we see this in context, we first have to understand the two most basic elements of every Python class...

#### The __init__() Method & the self Keyword

When you create a new instance of your Class, you might want to it to exist in some default state. For example, you might want to initially assign default values for its attributes. In Python terms - *when you **instantiate** a new instance object, you **initialize** it with pre-defined default values*.

**The __init__() method** is where you give instructions for how you want each instance to exist in its initial state. Every time you instantiate a new instance object of your Class, you automatically invoke the `__init__()` method. That means when you create a new Class, the first thing you want to do is create its `__init__()` method. In general, the syntax looks like this:

```python
class ClassName():
	def __init__(self):
		# ...
```

Notice we used the same notation as we did for defining functions. The `__init__()` method must have at least one argument, including the **self variable**. The `self` variable serves as a reference to the *current instance of the class*, and it must be the first parameter of *any* method in a class, including the `__init__()` method. 

## Class Definition Example
Let's take a look at how we might define an `Animal` class for the animals in our zoo example.

```python
class Animal(): # Parent class name

	kingdom = 'Animalia' # Class attribute shared by all instances

	def __init__(self, name = '', species = ''):
		self.name = name # Instance attribute unique to each instance
		self.species = species

	def identify(self): # Instance method
		print(f'Hi, I\m {self.name} the {self.species}!')
```

In the example above, we have many of the key structural elements of classes, which we discussed above.

* Every instance will have the `class attribute` with the value `Animalia`.
* Each instance will have `instance attributes` called `name` and `species`. By default these will be blank, but each instance can have its own unique values for them.
* We can call the `instance method` called `identify()` on all instances of the Animal class.

#### Class Instantiation

To instantiate a member of our `Animal` class, you would pass arguments for `name` and `species`. This automatically invokes the `__init__()` method and assigns the values of the arguments you passed to your new instance variable.

```python
# Instantiate a new member of the Animal class
harvey = Animal('Harvey','iguana')

# Access this instance's name attribute
print(harvey.name) # Harvey

# Call the identify method on this instance
s = harvey.identify()
print(s) # Hi, I'm Harvey the iguana!
```


## Inheritance

*More coming soon...*

