---
layout: page
title:  Welcome to the ITP Skills Labs for the Command Line!
permalink: /CLworkshop/
---

28 October 2019 \| Kathryn Mercier \| CUNY Graduate Center

This lab has been modified from the [Software Carpentry](https://software-carpentry.org/) lesson [The Unix Shell](http://swcarpentry.github.io/shell-novice/)

## __Objectives__

1. Understand why the command line is useful
2. Gain a basic toolkit to start using the command line
3. Be able to find resources to build your personal toolkit

## __1. Understand why the command line is useful__

We have many ways of interacting with computers. We can use a mouse and keyboard, touch screens, and even voice commands. When we interact with our personal computers, we are usually using a graphical user interface, or GUI. GUIs are a visual representation of a program and allow us to use the mouse and keyboard to click options and input arguments to run the program. 

While GUIs are intuitive and work well most of the time, imagine the following scenario. For a literature search, you have to copy the third line of one thousand text files in one thousand different directories and paste it into a single file. Using a GUI, you would not only be clicking at your desk for several hours, but you could potentially also commit an error in the process of completing this repetitive task. This is where we take advantage of the command line, allowing such repetitive tasks to be done automatically and fast. With the proper commands, the command line can repeat tasks as many times as we want.

Today, we will be using a Unix-based command line, used on Mac and Linux computers. Windows computers use a slightly different language for their command line, but the skills we learn should be transferable. Skills we will cover in this workshop include: navigating & creating folders; listing, searching & moving batches of files; editing & running shell scripts.

------

Nelle’s Pipeline: A Typical Problem
Nelle Nemo, a marine biologist, has just returned from a six-month survey of the North Pacific Gyre, where she has been sampling gelatinous marine life in the Great Pacific Garbage Patch. She has 1520 samples that she’s run through an assay machine to measure the relative abundance of 300 proteins. She needs to run these 1520 files through an imaginary program called goostats she inherited. On top of this huge task, she has to write up results by the end of the month so her paper can appear in a special issue of Aquatic Goo Letters.

The bad news is that if she has to run goostats by hand using a GUI, she’ll have to select and open a file 1520 times. If goostats takes 30 seconds to run each file, the whole process will take more than 12 hours of Nelle’s attention. With the shell, Nelle can instead assign her computer this mundane task while she focuses her attention on writing her paper.

The next few lessons will explore the ways Nelle can achieve this. More specifically, they explain how she can use a command shell to run the goostats program, using loops to automate the repetitive steps of entering file names, so that her computer can work while she writes her paper.

As a bonus, once she has put a processing pipeline together, she will be able to use it again whenever she collects more data.

[Onto the toolkit!](Toolkit/)
