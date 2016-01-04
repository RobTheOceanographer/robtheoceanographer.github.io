---
layout: post
title: How to LaTeX - An Absolute Beginners Guide
excerpt:
         <p>I've been asked a few times recently about how to LaTeX so I thought I'd put a few notes up for everyone to refer back to later.</p>
         <p>![CTAN LION]({{ site.baseurl }}/images/CTAN_lion_drawing_by_Duane_Bibby.gif)</p>
---

## What is it?

There's no need to re-invent the wheel here so the best thing is to read the, actually pretty good, Wikipedia pages on [Tex](https://en.Wikipedia.org/wiki/TeX) and [LaTeX](https://en.Wikipedia.org/wiki/LaTeX).

Having said that I will highlight the purpose of LaTeX (TeX) for those of you, like me, who are too lazy to bother reading those pages - The original TeX was designed with two main goals in mind: to allow anybody to produce high-quality books using a reasonably minimal amount of effort, and to provide a system that would give exactly the same results on all computers, at any point in time. For me, LaTeX is all about the second of those two points - easy reproducibility.

## How to install LaTeX?

First of all, there are lots of different types of LaTeX distributions. To simplify your search here are a couple of simple suggests:

There are two parts to a LaTeX installation: a LaTeX distribution (the compiler) and an editor to write the document in (a text editor of your choice):

### Editors

You can use any text editor you like but there are a couple that were designed for LaTeX and have built in LaTeX typesetting functionality that is really useful - if you're just starting out I suggest: [TeXShop](uoregon.edu/~koch/texshop/) on a Mac and [TeXworks](https://www.tug.org/texworks/) or [Texmaker](http://www.xm1math.net/texmaker/) or [TeXStudio](http://texstudio.sourceforge.net/) on Linux, and [MiKTeX](http://miktex.org/) or [Texmaker](http://www.xm1math.net/texmaker/) on Windows.

### LaTeX

- Linux users: You may already have LaTeX installed on your system. Type `which latex` at a command prompt to find out - if you have it, it will respond with /usr/bin/latex or something like that. If you don't you'll need to install it. Using Fedora run the following as a superuser:
```bash
yum install texlive
```

If you are using another Linux distribution, you can download LaTeX and install it using your package manager (e.g. `apt-get install texlive` etc). I'm no linux guru and I was able to install it on my Linux machine without screwing too much up.

- Mac users: You can install everything you'll need from the MacTeX web page [http://www.tug.org/mactex/](http://www.tug.org/mactex/). MacTeX should take care of all of your latex compatibility stuff and should be pretty straight forward.

- Windows users: You can install MiKTeX [http://miktex.org/](http://miktex.org/), which is the latex distribution built for Windows. Some helpful notes are found here: [http://www.howtotex.com/howto/installing-latex-on-windows/](http://www.howtotex.com/howto/installing-latex-on-windows/).  It should take care of all of your LaTeX compatibility stuff and should be pretty straight forward  - your milage may vary, especially with the new Windows OS.

## The absolute basics

How to create a document with “hello world” as the content:

Go to this link and watch the video  [http://www.youtube.com/watch?v=kQl2XdBiWNE&feature=related](http://www.youtube.com/watch?v=kQl2XdBiWNE&feature=related). This video is designed for TexShop but most of this is applicable to TexWorks or MikTeX too. I suggest saving the first document you create into a folder on the desktop called "MyFirstTexDocument".

### Getting started

First of all, if you're not a coder, don't get scared by the code and funny symbols and stuff.

[Dr. Tom Remenyi](http://utas.academia.edu/TomasRemenyi) put together a very useful training document for LaTeX - mainly designed for marine scientists but it's forms a useful starting point for all disciplines. Keep this document handy when you're starting out. It makes a great cheat sheet. I have forked his githib repo and made it available here: [https://github.com/RobTheOceanographer/latex_training_document](https://github.com/RobTheOceanographer/latex_training_document).

The repo needs a little updating and I'll work on that in the future, but for now there are two core documents of interest to you:

- `Latex_training_document.pdf` (open as normal)
- `Latex_training_document.tex` (open with your latex editor).

The rest of the files are used by your machine to create the document and you can ignore them for now. Open both files and try to find the bits that are similar between the `.tex` and the `.pdf`. A lot of the comments on “how to do blah blah blah” are in the `.tex` document (comments are the bits that immediately follow a `%` sign).

I recommend that you start a new document for yourself and use Tom's Latex training document as a cheat sheet to copy an paste the commands you need to do the things you want. The beauty of it is you can see all the commands in the code, the code that YOU wrote, so it is easier to see why something isn't working and how to fix it. Also the online help is awesome - [Google](http://www.google.com) is your friend.

## Installing Packages

Installing new packages is usually a source of frustration for new LaTeX users. On Mac and Linux systems the easiest way to do it is to use your systems package management system (e.g `apt-get` or `yum`) to find and install packages. I've never really worked with LaTeX on windows you'll have to do some searching and work this bit out on your own.

To get [Tom's](http://utas.academia.edu/TomasRemenyi) [Latex training doc](https://github.com/RobTheOceanographer/latex_training_document) to typeset on [Fedora](https://getfedora.org) I had to install the following extra packages:
```bash
yum install texlive-preprint
yum install texlive-threeparttable
yum install texlive-multirow
```
If you can't find what you're looking for in your package manager you can search on the [Com­pre­hen­sive TeX Archive Net­work (CTAN)](https://www.ctan.org/) website. CTAN is the central place for all LaTeX packages and it currently abut 4952 packages, most of which are free. [https://www.ctan.org/](https://www.ctan.org/)

### How to [CTAN](https://www.ctan.org/)

If you download a package from CTAN you will need to build the `.sty` file, put it into a dir that LaTeX can see and then tell LaTeX about it. Below is a rough guide to do this:

- search for missing packages here: [https://www.ctan.org/search/](https://www.ctan.org/search/)

- Run LaTeX on the downloaded `<package>.ins` file. This should generate a `<package>.sty` file. If you want to have the documentation for this package then you need to run LaTeX on the `<package>.dtx` file too.

- Move the `<package>.sty` and `<package>.dvi` files to a directory where LaTeX looks for it's input files. On Linux this is usually somewhere like this: `~/texmf/tex/latex/<package>`.

- Update your LaTeX file name database using the `texhash` command (something like this: `texhash ~/texmf`) and you're done.


## Examples and Inspiration

If you need inspiration check out this [stackexchange](http://stackexchange.com) thread of beautifully typeset documents created in TeX/LaTeX: [http://tex.stackexchange.com/questions/1319/showcase-of-beautiful-typography-done-in-tex-friends](http://tex.stackexchange.com/questions/1319/showcase-of-beautiful-typography-done-in-tex-friends)
