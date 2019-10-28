---
layout: page_nohead
title: Commandline Workshop - Toolkit
permalink: /CLworkshop/Toolkit/
---

## __2. Gain a basic toolkit to start using the command line__

### _Navigating Files and Directories_

First, we are going to use the command line to download some files we will use in the rest of this workshop

```shell
# Download a zipped file named "data.zip" from the internet
$ cd Desktop/
$ wget kpmercier.github.io/workshop/data.zip

# Unzip the "data.zip" file
$ unzip data.zip
```

[Command Line Cheat Sheet](https://www.git-tower.com/blog/command-line-cheat-sheet/) PDF with listing common commands with short explanations

------

In the command line, lines beginning with # are comments and are not executed. The command line is used to run programs, which may have options and arguements

```shell
# This is the general format of unix command line tools
$ program -option1 -option2 argument
```

The part of the operating system responsible for managing files and directories is called the file system. It organizes our data into files, which hold information, and directories (also called ‘folders’), which hold files or other directories.

Several commands are frequently used to create, inspect, rename, and delete files and directories. To start exploring them, we’ll go to our open shell window.

First let’s find out where we are by running a command called pwd (which stands for ‘print working directory’). Directories are like places - at any time while we are using the shell we are in exactly one place, called our current working directory. Commands mostly read and write files in the current working directory, i.e. ‘here’, so knowing where you are before running a command is important. pwd shows you where you are:

```shell
$ pwd
/Users/Katie/Desktop
```

Now let’s learn the command that will let us see the contents of our own filesystem. We can see what’s in our home directory by running ls, which stands for ‘listing’:

```shell
$ ls
data-shell  data.zip
```
We can also use ls to see the contents of a different directory. 

```shell
$ ls data-shell
creatures          molecules          notes.txt           solar.pdf
data               north-pacific-gyre pizza.cfg           writing
```
Second, we can actually change our location to a different directory, so we are no longer located in our home directory.

```shell
$ cd data-shell
$ cd data
$ pwd
/Users/Katie/Desktop/data-shell/data
```
We now know how to go down the directory tree, but how do we go up? We might try the following:

```shell
$ cd data-shell
-bash: cd: data-shell: No such file or directory
```
But we get an error! Why is this?

With our methods so far, cd can only see sub-directories inside your current directory. There are different ways to see directories above your current location; we’ll start with the simplest.

There is a shortcut in the shell to move up one directory level that looks like this:

```shell
$ cd ..
$ pwd
/Users/Katie/Desktop/data-shell
```

------

__Task

Starting from _/Users/amanda/data_, what command could Amanda use to navigate to her home directory, which is _/Users/amanda?_ __

[Working with Files and Folders](/CLworkshop/Toolkit2/)
