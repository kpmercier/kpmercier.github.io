---
layout: page
permalink: /CLworkshop/
---

# Welcome to the ITP Skills Labs for the Command Line!

28 October 2019 \| Kathryn Mercier

CUNY Graduate Center

------ Objectives

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

```
# This is the general format of unix command line tools
program -option1 -option2 target
```

```
# The 'pwd' program with no option or target prints your current directory
pwd
```

### File System

```
# The root (top) of the entire filesystem (used for writing full paths).
/

# Here, in my current directory (used for writing relative paths).
./

# Up one directory from my current directory (a relative path).
../
```

```
# show the files and folders in a location (default target is cur dir)
$ ls 

# show result as a list for cur dir.
$ ls -l ./

# show another location on the filesystem
$ ls -l /bin/

  # move to a new location. This becomes your new cur dir.
  $ cd folder/
```

## How to find resources to enhace your personal toolkit

[Command Line Cheat Sheet](https://www.git-tower.com/blog/command-line-cheat-sheet/) PDF with listing common commands with short explanations


