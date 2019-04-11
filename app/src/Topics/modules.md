<!---
{"next":"Topics/functions.md","title":"Modules & Packages"}
-->

# Modules & Packages

In Python, a `module` is Python source file that contains pre-defined objects like variables, functions, classes, and other items we'll talk about soon. A Python `package`, sometimes used synonymously with the term `library`, is simply a collection of Python modules. The diagram below can show you this hierarchy visually.

![package_def](https://365datascience.com/wp-content/uploads/2018/07/image2-min-6-768x419.png)

Essentially, packages and modules are a means of `modularizing` code by grouping functions and objects into specific areas of focus. For instance, the `statsmodels` module ([here](https://www.statsmodels.org/)) contains code useful to a data scientist. The `Pyglet` library ([here](http://www.pyglet.org/)) contains code useful to game developers needing shortcuts for 3D game animation. But vice versa?

`Modular programming` allows us to break out modules and packages dealing with specific topics in order make the standard library more efficient for the general public. It's sort of like "a la carte" code. This becomes especially valuable once you scale your programs. Who needs that extra baggage?

## Global vs. Local Scope

One of the reasons Python leverages modular programming is because it helps avoid conflicts between `local` and `global` variables by creating separate `namespaces`. `Namespaces` are the place where variables are stored, and they exist on several independent levels, including **local, global, built-in, and nested namespaces**. For instance, the functions `builtin.open()` and `os.open()` are distinguished by their namespaces. Namespaces also aid readability and maintainability by making it clear which module implements a function. 

At a high level, a variable declared outside a function has `global scope`, meaning you can access a it inside or outside functions. A variable declared within a function has `local scope`, which means you can only access it within the object you created it. If you try to oaccess it outside that, you will get a `NameError` telling you that variable is not defined.

We'll get more into how to use and interpret local and global scope as we dive into modules and functions...

## Importing

Importing modules and packages is very easy and saves you a lot of time you'd otherwise spend reinventing the wheel. Modules can even import other modules! The best practice is to place all import statements at the of your script file so you can easily see everything you've imported right at the top. 

#### Importing Modules 
Let's look at a few different way to import modules and their contents. The simplest way to import a module is to simply write `import module_name`. This will allow you to access all the contents within that module. 

If you want to easily find out exactly what is in your newly imported module, you can call the built-in function `dir()` on it. This will list all types of names: variables, modules, functions, etc. 

```python
import math
dir(math)
# prints ['__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'acos', 'acosh', 'asin', ... etc.]
```

You can also import one specific object from a module like this:

```python
from math import sqrt()
math.sqrt(25) # 5
```

Notice how we included `math.` when we called the `sqrt()` function. Because of *variable scope*, you need to reference the `namespace` where `sqrt()` is defined. Simply importing `sqrt()` does not give it `global scope`. It still has `local scope` within the math module.

However, you can help avoid verbose code by importing modules and their items like this:

```python
from math import sqrt() as s
s(25) # 5
```

By importing the `sqrt() as s`, you can call the function as `s()` instead of `math.sqrt()`. The same works for modules. Note the difference in how we reference the square root function though... 

```python
from math as m
m.sqrt(25) # 5
```

...we only renamed the module in this import and not the function. So we have to go back to the `module_name.function()` syntax. *However*, because we renamed the module on import, we can reference it in function calls by its shortened name, i.e. `m.sqrt()`.

#### Importing Packages (aka Libraries)
Importing packages works similarly to importing modules. 

```python
import unittest.mock # a packages
# OR
from unittest.mock import patch # patch is a module in this package
```

## Package Initialization
If a file named __init__.py is present in a package directory, it is invoked when the package or a module in the package is imported. This can be used for execution of package initialization code, such as initialization of package-level data.

For example, consider the following __init__.py file:

__init__.py

print(f'Invoking __init__.py for {__name__}')
A = ['quux', 'corge', 'grault']

if the __init__.py file in the package directory contains a list named __all__, it is taken to be a list of modules that should be imported when the statement from <package_name> import * is encountered.


## Common & Featured Modules

[](https://pythontips.com/2013/07/30/20-python-libraries-you-cant-live-without/)