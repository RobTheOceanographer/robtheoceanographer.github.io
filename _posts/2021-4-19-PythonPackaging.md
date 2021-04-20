---
layout: post
title: Grow your own Python Package
excerpt:
         <p>I decided to write up this short post to help both me and some colleagues remember what the most basic way of constructing a python package is.</p>
         <img src="https://raw.githubusercontent.com/RobTheOceanographer/robtheoceanographer.github.io/master/images/python.png" alt="python_cartoon">
---
I decided to write up this short post to help both me and some colleagues remember what the most basic way of constructing a python package is.

This is a bare-bones build - *you should be doing more than this* - for example putting in `README` file and `LICENSE` file and good [docstrings](http://www.robtheoceanographer.com/HowToDocstring/).

The basic structure of a python package is quite straight forward:

```
basemypackage  --> Base
└── mypackage   --> Actual Module
    ├── extras
    │   ├── multiply.py
    │   ├── divide.py
    ├── add.py
    ├── subtract.py
```
Here we have a dir called `mypackage` which has two python files in it - `add.py` and `subtract.py` but it also has a sub dir called `extras` which contains two more python files. all of this will form up the basis of our imaginary python package. keep in mind that you will have different files and folders in your package and you can divide up the files/folders in as course or as fine a way as you like.

## The __init__.py
You will always find one or several `__init__.py` files in python packages. this is because the `__init__.py` files tell python to treat directories as modules (or sub-modules as we will see in a minute). this makes it an important part of our package and one we need to spend some time looking at.

The `__init__.py` file contains two important things:
- a doc string for the available subpackages/submodules/methods in this dir (see the one in `numpy` as an example: [`https://github.com/numpy/numpy/blob/main/numpy/__init__.py`](https://github.com/numpy/numpy/blob/main/numpy/__init__.py))
- the names of all the methods in all the Python files that are in this immediate directory.

A typical `__init__.py` looks like this:
```
"""
some helpful info of what each method is/does...
"""

from file import method  # 'method' is a function found in the python file called 'file.py'

```

You will need to put a `__init__.py` in each sub dir of your package and so each sub-dir will become sub-modules of your main package.

here is the specific `__init__.py` for our dummy example:
```
"""
Provides
1. ability to add two numbers
2. ability to subtract two number.

...

"""
from add import add
from subtract import subtract
```

as we have an `extras` sub dir we need one in there too:

```
"""
Provides
1. ability to add multiply numbers
2. ability to divide number.

...

"""

from multiply import multiply
from divide import divide
```

## The `setup.py`
Another attribute of a python package is the `setup.py` which is a python file that contains information about your package, it's version, its dependencies, and a whole whole lot more.

Within the `basemypackage` dir (and in the same directory as our module `mypackage` ) we will now add a `setup.py` file:

```
from setuptools import setup, find_packages

VERSION = '0.0.1' 
DESCRIPTION = 'My absolutely gorgeous Python package'
LONG_DESCRIPTION = 'My Python package, it is gorgeous, it makes you just want to import it.'

# Setting up
setup(
       # the name must match the folder name 'mypackage'
        name="mypackage", 
        version=VERSION,
        author="Marty McFly",
        author_email="Marty.McFly@deloreantimemachines.com>",
        description=DESCRIPTION,
        long_description=LONG_DESCRIPTION,
        packages=find_packages(),
        install_requires=[], # add any additional packages that 
        # needs to be installed along with this package. Eg: 'numpy'
        
        keywords=['python', 'gorgeous'],
        url='https://gitlab.com/mygroup/gorgeous/basemypackage',
        license='MIT',
        classifiers= [
            "Development Status :: 1 - Planning",
            "Intended Audience :: Religion",
            "Programming Language :: Python :: 3",
            "Operating System :: Unix",
        ]
)
```
The `setuptools.setup()` method accepts a variety of keyword arguments to specify additional metadata about your package. - info on this can be found here: [`https://github.com/pypa/sampleproject/blob/main/setup.py`](https://github.com/pypa/sampleproject/blob/main/setup.py).
This includs a classifiers section - a full list of classifiers can be found here: [`https://pypi.org/pypi?%3Aaction=list_classifiers`](https://pypi.org/pypi?%3Aaction=list_classifiers).

## Build/Install it
You can now build and install your package locally using the dir you have just set up. It is a better idea to store this package on-line somewhere where it can be version controlled and available whenever you need it. Many people build and distribute their package via PyPi - as it is the official Python repository where all Python packages are stored - but i find that a little scary and tend to just do my own private thing using gitlab so i'm not going to show you that. First we will cover just local build/install and then get to that other stuff later.

### Locally
It’s common to locally install your project in “editable” or “developer” mode while you’re still developing/working on it. This allows your project to be both installed and editable so that updates are available when they get made.

Within the `basemypackage` dir run:
```
python -m pip install -e .
```
Although somewhat cryptic, -e is short for --editable, and . refers to the current working directory, so it should install the current directory in editable mode. This will also install any dependencies declared in the `setup.py`.

You should now be able to `import mypackage` in your python environment.

### GitLab
It is more useful not to have a local copy of the package source-code but to use a version control system like gitlab to manage a lot of that for you.
This is my preferred method of working and allows you to control who installs your package.

If you don’t already have one, create a new gitlab project and clone it to your local machine. Put all of the code that you want to include in your package including all the stuff shown above into this folder.

`pip` can talk git directly so it's quite easy to build our python package from gitlab. Here is an example:
```
python3 -m pip install -e git+ssh://git@gitlab.com/mygroup/gorgeous/basemypackage.git
```
Or if you want to specify a non default branch:
```
python3 -m pip install git+ssh://git@gitlab.com/mygroup/gorgeous/basemypackage.git@dev
```
Or if you want to fetch a particular tag:
```
python3 -m pip install git+ssh://git@gitlab.com/mygroup/gorgeous/basemypackage.git@v0.01
```
*.N.B.* The `:` at the end of gitlab.com must be changed to a `/` and you must have an ssh key registered with gitlab.com for the machine you're working on.

There are a lot of other ways to install from version control that you can read about here: [`https://pip.pypa.io/en/stable/reference/pip_install/#vcs-support`](https://pip.pypa.io/en/stable/reference/pip_install/#vcs-support).

## Notes
What i haven't covered here is testing and adding test running to your package. This will come in the future i expect.
