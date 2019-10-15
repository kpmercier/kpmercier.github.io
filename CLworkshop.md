---
layout: page
title:  Welcome to the ITP Skills Labs for the Command Line!
permalink: /CLworkshop/
---

28 October 2019 \| Kathryn Mercier \| CUNY Graduate Center

## __Objectives__

1. Understand why the command line is useful
2. Gain a basic toolkit to start using the command line
3. How to find resources to enhace your personal toolkit

## Understand why the command line is useful

The command line is a tool to control your computer using a text interface. It will be 
very useful if you are working with very large text data sets, or want to run the same
process over and over again. 

## Gain a basic toolkit to start using the command line

Skills we will cover in this workshop include: navigating & creating folders; 
listing, searching & moving batches of files; editing & running shell scripts. 

Lines beginning with # are comments and are not executed

```bash
# This is the general format of unix command line tools
program -option1 -option2 target
```

```bash
# The 'pwd' program with no option or target prints your current directory
pwd
```

### File System

```bash
# The root (top) of the entire filesystem (used for writing full paths).
/

# Here, in my current directory (used for writing relative paths).
./

# Up one directory from my current directory (a relative path).
../
```

```bash
# show the files and folders in a location (default target is cur dir)
$ ls 

# show result as a list for cur dir.
$ ls -l ./

# show another location on the filesystem
$ ls -l /bin/

# move to a new location. This becomes your new cur dir.
$ cd folder/
```
```bash
# make a new directory (mkdir is the program, genomics is the target)
$ mkdir genomics

# change directory (move) into the new directory and run pwd again
$ cd genomics
$ pwd
```

## How to find resources to enhace your personal toolkit

[Command Line Cheat Sheet](https://www.git-tower.com/blog/command-line-cheat-sheet/) PDF with listing common commands with short explanations


