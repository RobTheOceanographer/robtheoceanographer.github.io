---
layout: post
title: Python docstrings - An Absolute Beginners Guide
excerpt:
         <p>I've been asked a few times recently about how to write good docstrings in Python so I thought I'd put a few notes up for everyone to refer back to later.</p>
         <img src="https://raw.githubusercontent.com/RobTheOceanographer/robtheoceanographer.github.io/master/images/docstring.png" alt="docstring_cartoon">
---
I've been asked a few times recently about how to write good docstrings in Python so I thought I'd put a few notes up for everyone to refer back to later.

## What is it?

There's no need to re-invent the wheel here so the best thing is to read the python definition on [what-is-a-docstring](https://www.python.org/dev/peps/pep-0257/#what-is-a-docstring).

But, having said that I will highlight the purpose of a docstring for those of you, like me, who are too lazy to bother reading those pages - a docstring is a piece of text that occurs as the first line(s) in a python function, class, or module. This text becomes the `__doc__` special attribute of that object and is used to help users know what the thing you wrote is, does, and needs. Without a docstring your work is pretty useless and almost completely un-reusable and un-sharable. For me, docstrings are all about the re-usability and sharability.

## Functions
Every function you write needs a docstring - in fact I'd say this is the most important thing you can do when writing a function (aside from testing, but you're already doing that...right?).

A good docstring contains three elements:

1. a one line description of the purpose.
2. a clear description of the inputs and outputs to the function.
3. the `type` each input and output will be.

Here is how to write a good docstring for a function:

```
def add_binary(a, b):
    '''
    Returns the sum of two decimal numbers in binary digits.

            Parameters:
                    a (int): A decimal integer
                    b (int): Another decimal integer

            Returns:
                    binary_sum (str): Binary string of the sum of a and b
    '''
    binary_sum = bin(a+b)[2:]
    return binary_sum
```

The docstring has now become the objects `__doc__` attribute and can now be used by users to get help on the use of the function:
```
print(add_binary.__doc__)
```
output:
```
Returns the sum of two decimal numbers in binary digits.

    Parameters:
        a (int): A decimal integer
        b (int): Another decimal integer

    Returns:
        binary_sum (str): Binary string of the sum of a and b
```


## Classes
Most people are good at putting docstrings in their function but people often forget to put them in the classes they write. The docstring for a class is very similar to the function docstring but it has two extra elements:

 1. a description of the basic behavior of the class.
 2. a list of the public methods available to the user.

Here is an example of a class docstring:

```
class Person:
    """
    A class to represent a person.

    some blah about why/what it does.

    Attributes
    ----------
    name : str
        first name of the person
    surname : str
        family name of the person
    age : int
        age of the person

    Methods
    -------
    info(additional=""):
        Prints the person's name and age.
    """

    def __init__(self, name, surname, age):
        """
        Constructs all the necessary attributes for the person object.

        Parameters
        ----------
            name : str
                first name of the person
            surname : str
                family name of the person
            age : int
                age of the person
        """

        self.name = name
        self.surname = surname
        self.age = age

    ...
```

As per the function dcostring this text is also assigned to the `__docstring__` attribute for the class.
we can see that by:

```
print(Person.__doc__)
```
Output
```
    A class to represent a person.

    some blah about why/what it does.

    Attributes
    ----------
    name : str
        first name of the person
    surname : str
        family name of the person
    age : int
        age of the person

    Methods
    -------
    info(additional=""):
        Prints the person's name and age.
```


## Modules
If people are slack with class docstring then they are completely hopeless when it comes to docstrings in Modules. Module docstrings are much like a Class docstring except that it also includes descriptions of the classes available in the module. This is best way to understand this is with an example. Here we will look at the `pickle`  module:

```
import pickle
print(pickle.__doc__)
```
output
```
Create portable serialized representations of Python objects.

See module cPickle for a (much) faster implementation.
See module copy_reg for a mechanism for registering custom picklers.
See module pickletools source for extensive comments.

Classes:

    Pickler
    Unpickler

Functions:

    dump(object, file)
    dumps(object) -> string
    load(file) -> object
    loads(string) -> object

Misc variables:

    __version__
    format_version
    compatible_formats
```
Here, we can see the docstring that is written at the beginning of the `pickle.py` module file which has been assigned to the `__doc__` attribute for the module and can be be accessed as its docstring.

## Help()
There is a help() function in python that leverages all of these docstrings and aggregates them into a nice little manual for the user to explore your code. Again, Pickle is a good example:

```
import pickle
help(pickle)
```
I won't paste the output here as it's too long... go run it yourself and see what happens...


## More Info

If you need inspiration check out [pep 257 -- Docstring Conventions](https://www.python.org/dev/peps/pep-0257/) or go hunting around in your favorite python module.