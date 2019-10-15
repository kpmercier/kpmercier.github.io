---
layout: page
title:  Welcome to the ITP Skills Labs for the Command Line!
permalink: /CLworkshop/
---

28 October 2019 \| Kathryn Mercier \| CUNY Graduate Center

## __Objectives__

1. Understand why the command line is useful
2. Gain a basic toolkit to start using the command line
3. Be able to find resources to build your personal toolkit

## __Understand why the command line is useful__

We have many ways of interacting with computers. We can use a mouse and keyboard, touch screens, and even voice commands. When we interact with our personal computers, we are usually using a graphic user interface, or GUI. GUIs are a visual representation of a program and allow us to use the mouse and keyboard to click options and input arguments to run the program. 

While this is intuitive and works well most of the time, imagine the following scenario. For a literature search you want to find how often 

Skills we will cover in this workshop include: navigating & creating folders; listing, searching & moving batches of files; editing & running shell scripts.

## __Gain a basic toolkit to start using the command line__

### Fundamentals

When you start up a terminal you will see a prompt

```bash
$ 
```

Lines beginning with # are comments and are not executed

```bash
# This is the general format of unix command line tools
$ program -option1 -option2 argument
```

```bash
# The 'pwd' program with no option or argument prints your current location
$ pwd

# The 'ls' program with no option or argument prints the files and folders in your current location
$ ls 
```

### The filesystem

![File System](Filesystem_tree.png)

We can use the command line to point to locations in the filesystem

```bash
# The root (top) of the entire filesystem (used for writing full paths).
$ /

# Here, in my current directory (used for writing relative paths).
$ ./

# Up one directory from my current directory (a relative path).
$ ../
```

We can use the 'ls' command we learned to see files and folders in different locations in the filesystem

```bash
# Show files and folders in your current directory
$ ls ./

# show files and folders in another location on the filesystem
$ ls -l /bin/
```

What do you think the default argument for 'ls' is?

Now, lets use a new command to move around the filesystem

```bash
# move to a new location. This becomes your new cur dir.
$ cd folder/
```
Additionally, we can make new folders in the filesystem

```bash
# make a new directory (mkdir is the program, genomics is the target)
$ mkdir genomics

# change directory (move) into the new directory and run pwd again
$ cd genomics
$ pwd
```

### Working with files

### Shell scripts

### The last one

[File system exercise](FSexercise/)

## __Find resources to build your personal toolkit__

[Command Line Cheat Sheet](https://www.git-tower.com/blog/command-line-cheat-sheet/) PDF with listing common commands with short explanations

### Inspiration for this workshop comes from 

http://swcarpentry.github.io/shell-novice/01-intro/index.html

RADcamp ipyrad command line introduction

Clemson Palmetto command line workshop
