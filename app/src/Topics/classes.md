<!---
{"next":"Topics/pandas.md","title":"Classes"}
-->

# Classes & Inheritance

We already know that Python is based on the concept of **OOP, or Object-Oriented Programming**. Almost everything in Python is an object -- even functions are objects! **Classes**, and their facilitation of **inheritance**, are one of the most important and valuable Python objects. In this section, we'll cover:

* Class structure
* Class attributes
* Class methods
* The `__init__()` method
* The `self` keyword
* Class vs. instance variables
* Class instantiation
* Inheritance and child classes

## High-Level Overview

#### Creating & Structuring Classes
A **class** is essentially a data structure that serves as a blueprint for categorizing other objects and storing metadata about them. Once you have your "blueprint", you can create new **instances** of that class, which store unique metadata values. 

Creating a class is similar to defining a function. You start with the `class` keyword and then specify a name for the class. Note that class names are generally the only objects, which use a **CamelCase notation** naming convention. For example, if you were a zoologist, you might create a class called `Animal`. Each instance might represent a type of animal at your zoo.

```python
# Define a class called Animal
class Animal:
    # attributes
    # methods
    # etc ...

# Create the most basic instance
chameleons = Animal()
```

Before we go into the details of thoroughly defining a class, let's isolate some basic elements and concepts to get a general understanding of them.

#### Attributes & Methods
Each piece of a class's metadata is called an **attribute**. Once you have your "blueprint", you can create new **instances** of that class, which stores unique attribute values. As a zoologist, you would want define your `Animals` class so that it could store attributes of each type animal at your zoo such as species, natural habitat, etc..

```python
class Animal:
    kingdom = 'Animalia' # attribute
    
    # some other code...
```

In addition to attributes, classes also contain custom **methods**. Methods are essentially functions that belong to the class. You can call a function without referencing any other object, but to call a method, you need to reference its class. *Thus, all methods are functions, but not all functions are methods.* We've already used some `List` methods like `my_list.pop()`, `my_list.append()`, `my.list.insert(index)`, etc.. When you create a class, you can define methods to serve as shortcuts for actions you might want to call frequently on instances of your class. 

```python
class Animal:
    # some other code...

    def method1(self): # method
        # some action
```

Once you've defined attributes and methods, here's how you call them on your class instance:

```python
chameleons = Animal() # Create the instance.

print(chameleons.kingdom) # 'Animalia'

chameleons.method1() # This completes the defined method operations.
```

#### Inheritance Basics

Classes can inherit attributes and methods from other classes according to a parent-child class hierarchy. Naturally, a **child class** inherits from a **parent class**. When you define a brand new class, Python 3 implicitly uses the generic, built-in `object` as the parent class. That means, whether we explicitly see it or not, every parent class is also the child class of its own parent class!

In the context of our zoo example, the different instances of `Animal` each store general information about a certain type of animal. Imagine you want to expand on an instance of `Animal` called `elephants`. In order to document information about each elephant at the zoo, you might create an `Elephant` class that inherits from your `Animal` class. To do so, you use this general syntax:

```python
class Elephant(Animal):
    # attributes
    # methods
    # etc ...
```

Although the child class has access to everything defined for its parent class, the child class can also override or extend the parent class's traits and behavior. Note that this *does NOT redefine the parent class*. The new attributes and methods the child class declares apply only to instances of the child class. Parent class instances still adhere to the original parent class specs.

#### The __init__() Method & the self Keyword

When you create a new instance of your Class, you might want to it to exist in some default state. For example, you might want to initially assign default values for its attributes. In Python terms - *when you **instantiate** a new instance object, you **initialize** it with pre-defined default values*.

**The __init__() method** is where you give instructions for how you want each instance to exist in its initial state. Every time you instantiate a new instance object of your Class, you automatically invoke the `__init__()` method. That means when you create a new Class, the first thing you want to do is create its `__init__()` method. In general, the syntax looks like this:

```python
class Animal():
    def __init__(self):
        # ...
```

Notice we used the same notation as we did for defining functions. The `__init__()` method must have at least one argument, including the **self variable**. The `self` variable serves as a reference to the *current instance of the class*, and it must be the first parameter of *any* method in a class, including the `__init__()` method.

## Class vs. Instance Variables

Now we can get to the good stuff! As you define attributes and methods for your class, keep in mind their *scope*. If you want a certain attribute or method to be shared by ALL instances of a class, define it as a **class variable**. If you instead want it to be unique to each instance, define it as an **instance variable**. Before we see this in context, we first have to understand the two most basic elements of every Python class...

#### The __init__() Method & the self Keyword

When you create a new instance of your Class, you might want to it to exist in some default state. For example, you might want to initially assign default values for its attributes. In Python terms - *when you **instantiate** a new instance object, you **initialize** it with pre-defined default values*.

**The __init__() method** is where you give instructions for how you want each instance to exist in its initial state. Every time you instantiate a new instance object of your Class, you automatically invoke the `__init__()` method. That means when you create a new Class, the first thing you want to do is create its `__init__()` method. In general, the syntax looks like this:

```python
class Animal():
    def __init__(self):
        # ...
```

Notice we used the same notation as we did for defining functions. The `__init__()` method must have at least one argument, including the **self variable**. The `self` variable serves as a reference to the *current instance of the class*, and it must be the first parameter of *any* method in a class, including the `__init__()` method. 

## Class Definition Example
Now that we've isolated each key component of classes, let's put everything together by completing the code for our zoology scenario. At the highest level, we define a class called `Animal`. The annotated code below illustrates how each key structural element we covered above fits into this task.

```python
class Animal: # A.
    def __init__(self, species = '', diet= ''): # B. 
        self.species = species # C.
        self.diet = diet # C.

    kingdom = 'Animalia' # D.

    def my_kingdom(self):
        print(self.kingdom)

    def feed_me(self): # E.
        if self.diet == 'omnivore':
            food = 'plants and meat'
        elif self.diet == 'carnivore':
            food = 'meat'
        elif self.diet == 'herbivore':
            food = 'plants'
        print(f'{self.species} eat {food}!')
        return None
```

A. `Animal` is a *child class* of `object` as well as a potential *parent class*.
B. Every time we instantiate a new class object, the `__init__()` method will automatically be called to initialize the instance's values.
C. Each instance of the `Animal` class will store unique values for the **instance attributes** `species` and `diet`. By default these will be blank or Nonetypes, but each instance can have its own unique values for them.
D. ALL instances of the Animal class will have the `kingdom` **class attribute** with the value `Animalia`.
E. We can call **instance methods** `my_kingdom` and `feed_me` on ANY instance of the `Animal` class. **Note!** In `my_kingdom`, we access the class variable `kingdom`, but still reference it using `self`.

#### Class Instantiation

To instantiate a member of our `Animal` class, you would pass arguments for `species` and `diet`. This automatically invokes the `__init__()` method and assigns the values of the arguments you passed to your new instance attributes.

```python
# Instantiate a new member of the Animal class. Notice we left the diet arg blank, so it will default to a blank string.
chameleons = Animal('Chameleon')

# Access this instance's species attribute
print(chameleons.species) # Chameleon

# Call the feed_me method on this instance
chameleons.feed_me() # A chameleon eats meat!
```

#### Modifying Class Instances

Since each instance is meant to be unique, you of course need a way to modify its values or create new ones after its initial instantiation. 

```python
# Update the values of an instance attribute for chameleons.
print(chameleons.diet) # (empty string)
chameleons.diet = 'Carnivore'

# Define a new instance attribute, which will apply only to chameleons.
chameleons.avg_weight_pounds = 31
```

#### Defining a Child Class (Inheritance)

Let's go into some more detail

```python
class Elephant(Animal): # A.
    def __init__(self, name = '', genus = '', species = '', habitat = '', age = None): # B.
        self.name = name # C. 
        self.genus = genus # C.
        self.species = species # C.
        self.habitat = habitat # C.
        self.age = age # C.
        self.taxonomy = {} # C.

    diet = 'Herbivore' # D.

    common_taxonomy = { # D.
    'Class': 'Mammalia',
    'Family': 'Elephantidae',
    }

    def complete_taxonomy(self): # E.
      x = self.common_taxonomy
      y = self.taxonomy
      y.update({'Kingdom': Animal.kingdom})
      for k, v in x.items():
        y.update({k: v})
      y.update({'Genus': self.genus, 'Species': self.species})
      self.taxonomy = y
      return self.taxonomy

    def summary(self): # E.
      print(f'{self.name} \nElephant, age {self.age}\n{self.diet}')
      for k,v in self.taxonomy.items():
        print(f'{k}: {v}')
```

A. Declares `Elephant` as a *child class* of `Animal`.
B. The `__init__()` method
C. These are *instance attributes*. Notice that even though `taxonomy` is not a parameter for the `__init__()` method, we can still define it upon every instantiation.
D. *Class attributes*
LL instances of the Animal class will have the `kingdom` **class attribute** with the value `Animalia`.
E. We will be able to call the **instance method** `identify` on ALL instances of the Animal class.

#### Checking Class Values

In case someone who is not an expert zoologist like you needs to access the zoo's database of animals, that person could use the `isinstance()` function is used to determine if an instance is also an instance of a certain parent class. For this example, imagine you have already also defined another class called `Toucan` with the same input variables as our `Elephant` class.

```python
# Is elephant1 an instance of Animal()?
print(isinstance(elephant1, Animal)) # True

# Is toucan1 an instance of Elephant()?
print(isinstance(toucan1, Elephant)) # False
```

#### Overriding the Functionality of a Parent Class

Remember that child classes can also override parent attributes and behaviors without redefining the parent class. For example:

```python
class Animal:
    category = 'Animals'
    # etc ...

class Toucan(Animal):
    category = 'Birds'
    # etc ...

harvey = Animal() # plus any required input
harvey.category # Animals

talulah = Toucan() # plus any required input
talulah.category # Birds
```

If you wanted, the `Toucan` class could simply inherit the `category` class attribute from its parent class `Animal`. In this case, every instance of `Toucan` would  would have the same value -- `Animals`. However, it makes sense that you'd want to differentiate further for the child class `Toucan`. To do that, you'd simply override `category` when you define `Toucan` by setting its value to `Birds`.

## Review of Classes & Inheritance
* A **class** outlines a set of **attributes** and **methods**, which will help categorize other objects.
* To add objects to the class, you declare them as an **instance** of that class.
* **Class variables** store values belonging to ALL instances of a class, whereas **instance variables** store values unique to each instance. 
* **The __init__() method** is where you give instructions for how you want each instance to exist in its initial state. Every time you instantiate a new instance object of your Class, you automatically invoke the `__init__()` method.
* The **self variable** serves as a reference to the current instance of the class, and it must be the first parameter of *any* method in a class, including the `__init__()` method.
* **Child classes** can inherit attributes and methods from **parent classes**. 
* **Child classes** can also override parent attributes and behaviors without redefining the parent class.

## Practice Problems

