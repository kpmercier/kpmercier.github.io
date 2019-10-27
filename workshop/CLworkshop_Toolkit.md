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
$ wget kpmercier.github.io/workshop/data.zip

# Unzip the "data.zip" file
$ unzip data.zip
```

[Command Line Cheat Sheet](https://www.git-tower.com/blog/command-line-cheat-sheet/) PDF with listing common commands with short explanations

------

The part of the operating system responsible for managing files and directories is called the file system. It organizes our data into files, which hold information, and directories (also called ‘folders’), which hold files or other directories.

Several commands are frequently used to create, inspect, rename, and delete files and directories. To start exploring them, we’ll go to our open shell window.

First let’s find out where we are by running a command called pwd (which stands for ‘print working directory’). Directories are like places - at any time while we are using the shell we are in exactly one place, called our current working directory. Commands mostly read and write files in the current working directory, i.e. ‘here’, so knowing where you are before running a command is important. pwd shows you where you are:

$ pwd

Now let’s learn the command that will let us see the contents of our own filesystem. We can see what’s in our home directory by running ls, which stands for ‘listing’:

$ ls

------

#### Nelle’s Pipeline: Organizing Files
Knowing this much about files and directories, Nelle is ready to organize the files that the protein assay machine will create. First, she creates a directory called north-pacific-gyre (to remind herself where the data came from). Inside that, she creates a directory called 2012-07-03, which is the date she started processing the samples. She used to use names like conference-paper and revised-results, but she found them hard to understand after a couple of years. (The final straw was when she found herself creating a directory called revised-revised-results-3.)

Sorting Output
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

[Next: Working with Files](Toolkit2/)
