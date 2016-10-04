---
layout: post
title: Using Wildcards with Drake
excerpt:
         <p>Drake is cool little tool that is a bit like Make for data workflows. It was created by Factual for their own work and the released into the wild. It's very useful as it allows you to lay out your data workflow steps and include input and output dependencies, it allows you to call and run specific pieces and steps of your workflow from the command line, it allows you to call your existing scripts and code /tools (e.g., Shell, Python, and R, etc...). Unfortunately there is not yet a built way to list all of your input files using wildcards, which is something I do all the time. After some googling and stuffing about i've found a simple(ish) solution.</p>
---
[Drake](https://www.factual.com/blog/introducing-drake-a-kind-of-make-for-data) is cool little tool that is a bit like [Make](https://en.wikipedia.org/wiki/Make_(software)) for data workflows. It was created by [Factual](https://www.factual.com) for their own work and the released into the wild. It's very useful as it allows you to lay out your data workflow steps and include input and output dependencies, it allows you to call and run specific pieces and steps of your workflow from the command line, it allows you to call your existing scripts and code /tools (e.g., Shell, Python, and R, etc...). Unfortunately there is not yet a built way to list all of your input files using wildcards, which is something I do all the time. After some googling and stuffing about i've found a simple(ish) solution.

## How to use wildcard in Drake?
