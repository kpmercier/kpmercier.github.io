---
layout: page_nohead
title: Commandline Workshop - Toolkit
permalink: /CLworkshop/Toolkit/
---

## __2. Gain a basic toolkit to start using the command line__
 
1. [Navigating Files and Folders]
2. [Working with Files and Folders]
3. [Finding Things]
4. [Pipes and Filters]
5. [Loops]
6. [Shell Scripts]

### __Navigating Files and Folders__

First, we are going to use the command line to download some files we will use in the rest of this workshop

```shell
# Download a zipped file named "data.zip" from the internet
$ cd Desktop/
$ wget kpmercier.github.io/workshop/data.zip

# Unzip the "data.zip" file
$ unzip data.zip
```

[Command Line Cheat Sheet](https://www.git-tower.com/blog/command-line-cheat-sheet/) PDF listing common commands with short explanations

------

In the command line, lines beginning with # are comments and are not executed. The command line is used to run programs, which may have options and arguments

```shell
# This is the general format of unix command line tools
$ program -option1 -option2 argument
```
```
output
```

The part of the operating system responsible for managing files and directories is called the file system. It organizes our data into files, which hold information, and directories (also called ‘folders’), which hold files or other directories.

Several commands are frequently used to create, inspect, rename, and delete files and directories. To start exploring them, we’ll go to our open shell window.

First let’s find out where we are by running a command called pwd (which stands for ‘print working directory’). Directories are like places - at any time while we are using the shell we are in exactly one place, called our current working directory. Commands mostly read and write files in the current working directory, i.e. ‘here’, so knowing where you are before running a command is important. pwd shows you where you are:

```shell
$ pwd
```
```
/Users/Katie/Desktop
```

Now let’s learn the command that will let us see the contents of our own filesystem. We can see what’s in our home directory by running ls, which stands for ‘listing’:

```shell
$ ls
```
```
data-shell  data.zip
```
We can also use ls to see the contents of a different directory. 

```shell
$ ls data-shell
```
```
creatures          molecules          notes.txt           solar.pdf
data               north-pacific-gyre pizza.cfg           writing
```

---

__Task__

You can also use two options at the same time. What does the command ls do when used with the -l option? What about if you use both the -l and the -h option?

Some of its output is about properties that we do not cover in this lesson (such as file permissions and ownership), but the rest should be useful nevertheless.

__Solution__

The -l option makes ls use a long listing format, showing not only the file/directory names but also additional information such as the file size and the time of its last modification. If you use both the -h option and the -l option, this makes the file size ‘human readable’, i.e. displaying something like 5.3K instead of 5369.

---

Second, we can actually change our location to a different directory, so we are no longer located in our home directory.

```shell
$ cd data-shell
$ cd data
$ pwd
```
```
/Users/Katie/Desktop/data-shell/data
```
We now know how to go down the directory tree, but how do we go up? We might try the following:

```shell
$ cd data-shell
```
```
-bash: cd: data-shell: No such file or directory
```
But we get an error! Why is this?

With our methods so far, cd can only see sub-directories inside your current directory. There are different ways to see directories above your current location; we’ll start with the simplest.

There is a shortcut in the shell to move up one directory level that looks like this:

```shell
$ cd ..
$ pwd
```
```
/Users/Katie/Desktop/data-shell
```
---
__Task__

Starting from _/Users/amanda/data_, what command could Amanda use to navigate to her home directory, which is _/Users/amanda?_

__Solution__

1. cd ~    stands for the user’s home directory, in this case /Users/amanda.
2. cd ..    Change directory to parent directory
3. cd       Shortcut for #1
4. cd ~/data/..    Extra complication, but okay!

---

__Nelle’s Pipeline: Organizing Files__

Knowing this much about files and directories, Nelle is ready to organize the files that the protein assay machine will create. First, she creates a directory called north-pacific-gyre (to remind herself where the data came from). Inside that, she creates a directory called 2012-07-03, which is the date she started processing the samples. She used to use names like conference-paper and revised-results, but she found them hard to understand after a couple of years. (The final straw was when she found herself creating a directory called revised-revised-results-3.)

_Sorting Output_

Nelle names her directories ‘year-month-day’, with leading zeroes for months and days, because the shell displays file and directory names in alphabetical order. If she used month names, December would come before July; if she didn’t use leading zeroes, November (‘11’) would come before July (‘7’). Similarly, putting the year first means that June 2012 will come before June 2013.

Each of her physical samples is labelled according to her lab’s convention with a unique ten-character ID, such as ‘NENE01729A’. This is what she used in her collection log to record the location, time, depth, and other characteristics of the sample, so she decides to use it as part of each data file’s name. Since the assay machine’s output is plain text, she will call her files NENE01729A.txt, NENE01812A.txt, and so on. All 1520 files will go into the same directory.

Now in her current directory data-shell, Nelle can see what files she has using the command:

```shell
$ ls north-pacific-gyre/2012-07-03/
```

This is a lot to type, but she can let the shell do most of the work through what is called tab completion. If she types:

```shell
$ ls nor
```

and then presses Tab (the tab key on her keyboard), the shell automatically completes the directory name for her:

```shell
$ ls north-pacific-gyre/
```

If she presses Tab again, Bash will add 2012-07-03/ to the command, since it’s the only possible completion. Pressing Tab again does nothing, since there are 19 possibilities; pressing Tab twice brings up a list of all the files, and so on. This is called tab completion, and we will see it in many other tools as we go on.

[Next Module: Working with Files and Folders](/CLworkshop/Toolkit2/)
