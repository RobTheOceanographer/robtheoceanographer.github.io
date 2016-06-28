---
layout: post
title: In search of a better Tilde.
excerpt:
         <p>My good friend Dr. Tom Remenyi just sent me a little LaTeX hack that I thought would be worth sharing. He recently found himself in need of a Tilde, that is a '~' and quickly became frustrated with the standard/default LaTeX rendering and as such decided to define his own. Here's how you can too...</p>
---
My good friend [Dr. Tom Remenyi](http://utas.academia.edu/TomasRemenyi) just sent me a little [LaTeX](https://en.Wikipedia.org/wiki/LaTeX) hack that I thought would be worth sharing. He recently found himself in need of a [tilde](http://whatis.techtarget.com/definition/tilde), that is a '~' and quickly became frustrated with the standard/default LaTeX rendering and as such decided to define his own. Here's how you can to...

## What is a tilde?
[tilde](https://en.wikipedia.org/wiki/Tilde) (~ , pronounced TILL-duh or TILL-dee and sometimes called a "twiddle" or a "squiggle") is a foundational mathematical symbol meaning "approximately" and in much of computer science logic means "not."

## Dr.Tom's instructions:
What follows is a direct quote of his email to me:

For years it has bugged me that using the tilde symbol in latex is a real pain, solutions have been never quite right.  I have needed to use it quite a bit in a recent document, so I have found a solution.  I thought I would share it, since I like it so much.  I hope one of you find this useful.

Below is a line of code you can add to the preamble of any document and it will define a command that will place a sensibly sized and positioned tilde where you want it.  (I have quite figured out where I can put it so it always works and doesn’t get overwritten by new packages).  Why this isn’t the default (or close to the default), I don’t know, but here it is.

```

\newcommand{\goodtilde}{{\raise0.17ex\hbox{$\scriptstyle\sim$}}}  %create a command that uses a decent ~ (tilde) in-text.

```

It is used like this throughout the latex of the document:

```There are \goodtilde50 excellent reasons why this should be the default symbol in latex.```

OR

```This is the way to put a \goodtilde symbol in your text.```
