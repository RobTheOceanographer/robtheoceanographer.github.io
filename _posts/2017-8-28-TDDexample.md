---
layout: post
title: A Test Driven Dev Example
excerpt:
         <p>This blog is a small example of test-driven development in the interactive development environment.</p>
---

## How do you code?
Research [(see here)](https://software-carpentry.org/files/bib/secse-survey-2009.pdf) shows that:
 - 1) the knowledge required to develop and use scientific software is primarily acquired from peers and through self-study, rather than from formal education and training;
- 2) the number of scientists using supercomputers is small compared to the number using desktop or intermediate computers;
- 3) most scientists rely primarily on software with a large user base;
- 4) while many scientists believe that software testing is important, a smaller number believe they have sufficient understanding about testing concepts;

This blog is a small example of test-driven development and will hopefully help address point 4.

## Take away:
If you only take one thing from this post it's that everytime you do any coding ask yourself two questions:
- How do I (and you) trust this piece of code?
- How do I (and you) know it is doing what intended it to do?

## Why Test?
"We believe that software is just another kind of experimental apparatus and should be built, checked, and used as carefully as any physical apparatus. However, while most scientists are careful to validate their laboratory and field equipment, most do not know how reliable their software is." [source](http://journals.plos.org/plosbiology/article/file?id=10.1371/journal.pbio.1001745&type=printable)

You wouldn't use an instrument that hasn't been calibrated but we seem to have no problem using code without any check or balances at all.


## Test Driven Development

Test-driven Development (TDD) is a procedure that takes the process of writing code and the writing tests for it and flips it on it's head. It advocates that you write the tests first and the least amount of code possible to pass these tests second.

Before you write a single line of a function, you first write the test for that function.

After you've written the test you can then write the smallest amount of code needed to pass that test. If you want to do more or add more functionality you must first write another test and so on repeating the test-then-implement process until you have working code - often with as much testing code as actual code.

Most of the online info about TDD shows examples using testing harnesses and automated testing libraries. when i was starting out i found these very hard to follow and to use. Most scientist develop interactively in through an ide or terminal and so here i want to provide an example that can implement the principles of TDD in this framework.

# The example:
```python
import pandas
import numpy
```
# Non-test driven development

```python
# load my data.
some_data=pandas.read_csv('simple_data.csv', sep=',',header=None)
```

```python
# divide column two by 2.0.
some_data[1]/2.0
```

```
    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-3-15ba6180a4ae> in <module>()
          1 # divide column two by 2.0.
    ----> 2 some_data[1]/2.0

...

    TypeError: unsupported operand type(s) for /: 'str' and 'float'
```

####**_ We are already starting to run into errors that are making me go back and troubleshoot/debug._**

# Defensive dev version

### My Plan
1) Load data

Use my knowledge of the dataset to write a test upfront that will all me to be certain that the data has loaded properly.

2) Divide the second column of data by 2.

This will require a function that can do the math and then the application of that function to my data



### My Pre-defined Tests

```python
# 1) loading of data.
# I know that the data should have two columns and 39 rows when loaded so lets test that.
some_data.shape == (39,2)
```
```
$    False
```


```python
# 2) I know that when I divide the number 5 I should get 2.5 so lets test the divide function using that.
divide_by_two(5) == 2.5
```
```
    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-5-c169179b0f66> in <module>()
          1 # 2) I know that when I divide the number 5 I should get 2.5 so lets test the divide function using that.
    ----> 2 divide_by_two(5) == 2.5


    NameError: name 'divide_by_two' is not defined
```

### Redo the tests to be more useful and verbose

Nicer and more readble way to write tests like these is to use some inbuilt tools.

One of the easiest and most acessible is the *`assert`* statement. It is designed to catch conditions that should never occur in your code and to allow your code to stop at that point and return you a sensisble message.

- Python has `assert()`, http://swcarpentry.github.io/python-novice-inflammation/08-defensive/
- R has `assert()` but it's in a package called `testit` (https://cran.rstudio.com/web/packages/testit/index.html),
- Matlab has `assert()` but i don't know how to use it...

In python the basics of assert are:
```
assert x >= 0, 'x is less than zero'
```
when x is less than zero the logic of `x >= 0` will return false and an assert error will be raised printing the message that appears after the comma.


```python
# 1) loading of data.
assert some_data.shape == (39,2), "The data hasn't loaded properly. Size is not 39 x 2"

```
```
    ---------------------------------------------------------------------------

    AssertionError                            Traceback (most recent call last)

    <ipython-input-6-b2d7fe176e23> in <module>()
          1 # 1) loading of data.
    ----> 2 assert some_data.shape == (39,2), "The data hasn't loaded properly. Size is not 39 x 2"


    AssertionError: The data hasn't loaded properly. Size is not 39 x 2
```


```python
# 2) I know that when i divide the number 5 i should get 2.5 so lets test the divide function using that.
assert divide_by_two(5) == 2.5, "The divide_by_two function did not return 2.5 when given 5."

```
```

    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    <ipython-input-7-533c1c115487> in <module>()
          1 # 2) I know that when i divide the number 5 i should get 2.5 so lets test the divide function using that.
    ----> 2 assert divide_by_two(5) == 2.5, "The divide_by_two function did not return 2.5 when given 5."


    NameError: name 'divide_by_two' is not defined
```

### Now start coding to make the tests pass
- the idea is to write as little as possible to make the test pass.


```python
some_data = numpy.empty([39, 2])
```


```python
def divide_by_two(vals):
    return 2.5
```

#### start to refactor to actually work:


```python
some_data = pandas.read_csv('simple_data.csv', sep=',',header=0)
assert some_data.shape == (39,2), "The data hasn't loaded properly. Size is not 39 x 2"

```


```python
def divide_by_two(vals):
    return vals/2.0

assert divide_by_two(5) == 2.5, "The divide_by_two function did not return 2.5 when given 5."
```

#### Now put a piece of my data and my function together


```python
# 3) Now test the two things together.

# I know that the third number in my data is 4 and so the divide function should return 2.
assert some_data.sample_data[2] == 4, "The data in the third rows of col 2 is no longer 4..."

assert divide_by_two(some_data.sample_data[2]) == 2, "The divide_by_two function did not return 2 when given the 3rd element of some_data.sample_data"



```

### Now i can use this function in anger on the whole dataset


```python

divide_by_two(some_data.sample_data)
```
```

    0            0.5
    1            1.5
    2            2.0
    3            3.5
    4            5.5
    5            9.0
    6           14.5
    7           23.5
    8           38.0
    9           61.5
    10          99.5
    11         161.0
    12         260.5
    13         421.5
    14         682.0
    15        1103.5
    16        1785.5
    17        2889.0
    18        4674.5
    19        7563.5
    20       12238.0
    21       19801.5
    22       32039.5
    23       51841.0
    24       83880.5
    25      135721.5
    26      219602.0
    27      355323.5
    28      574925.5
    29      930249.0
    30     1505174.5
    31     2435423.5
    32     3940598.0
    33     6376021.5
    34    10316619.5
    35    16692641.0
    36    27009260.5
    37    43701901.5
    38    70711162.0
    Name: sample_data, dtype: float64
```
