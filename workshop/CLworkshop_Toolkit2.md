---
layout: page_nohead
title: Commandline Workshop - Toolkit2
permalink: /CLworkshop/Toolkit2
---

### _Working with files_

First, we are going to use the command line to download some files we will use in the rest of this workshop

```shell
# Download a zipped file named "data.zip" from the internet
$ wget kpmercier.github.io/workshop/data.zip

# Unzip the "data.zip" file
$ unzip data.zip
```

We can use the command line to point to locations in the filesystem

```shell
# The root (top) of the entire filesystem (used for writing full paths).
$ /

# Here, in my current directory (used for writing relative paths).
$ ./

# Up one directory from my current directory (a relative path).
$ ../
```

We can use the 'ls' command we learned to see files and folders in different locations in the filesystem

```shell
# Show files and folders in your current directory
$ ls ./

# show files and folders in another location on the filesystem
$ ls -l data/
```

_What do you think the default argument for 'ls' is?_



Now, lets learn a new command to move around the filesystem

```shell
# move to a new location. This becomes your new cur dir.
$ cd data/
```

_What files and folders are in the data directory_



Let’s go back to our data-shell directory on the Desktop and use ls to see what it contains:

```shell
$ pwd
$ ls
```
Let’s create a new directory called thesis using the command mkdir thesis (which has no output):

```shell
 $ mkdir thesis
``` 

As you might guess from its name, mkdir means ‘make directory’. Since thesis is a relative path (i.e., does not have a leading slash, like /what/ever/thesis), the new directory is created in the current working directory:

```shell
$ ls
```

Since we’ve just created the thesis directory, there’s nothing in it yet:

```shell
$ ls thesis
```

Let’s change our working directory to thesis using cd, then run a text editor called Nano to create a file called draft.txt:

```shell
$ cd thesis
$ nano.txt
```

![Nano](nano-screenshot.png)

nano doesn’t leave any output on the screen after it exits, but ls now shows that we have created a file called draft.txt:

```shell
$ ls
```

Returning to the data-shell directory,

```shell
$ cd ..
```

In our thesis directory we have a file draft.txt which isn’t a particularly informative name, so let’s change the file’s name using mv, which is short for ‘move’:

```shell
$ mv thesis/draft.txt thesis/quotes.txt
```

The first argument tells mv what we’re ‘moving’, while the second is where it’s to go. In this case, we’re moving thesis/draft.txt to thesis/quotes.txt, which has the same effect as renaming the file. Sure enough, ls shows us that thesis now contains one file called quotes.txt:

```shell
$ ls thesis
```

Let’s move quotes.txt into the current working directory. We use mv once again, but this time we’ll use just the name of a directory as the second argument to tell mv that we want to keep the filename, but put the file somewhere new. (This is why the command is called ‘move’.) In this case, the directory name we use is the special directory name . that we mentioned earlier.

```shell
$ mv thesis/quotes.txt .
```
The effect is to move the file from the directory it was in to the current working directory. ls now shows us that thesis is empty:

 
```shell
$ ls thesis
```

Further, ls with a filename or directory name as an argument only lists that file or directory. We can use this to see that quotes.txt is still in our current directory:

```shell
$ ls quotes.txt
```

The cp command works very much like mv, except it copies a file instead of moving it. We can check that it did the right thing using ls with two paths as arguments — like most Unix commands, ls can be given multiple paths at once:

```shell
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
```

We can also copy a directory and all its contents by using the recursive option -r, e.g. to back up a directory:

```shell
$ cp -r thesis thesis_backup
```

We can check the result by listing the contents of both the thesis and thesis_backup directory:

```shell
$ ls thesis thesis_backup
```

Returning to the data-shell directory, let’s tidy up this directory by removing the quotes.txt file we created. The Unix command we’ll use for this is rm (short for ‘remove’):

```shell
$ rm quotes.txt
```

We can confirm the file has gone using ls:

```shell
$ ls quotes.txt
```

* is a wildcard, which matches zero or more characters. Let’s consider the data-shell/molecules directory: *.pdb matches ethane.pdb, propane.pdb, and every file that ends with ‘.pdb’. On the other hand, p*.pdb only matches pentane.pdb and propane.pdb, because the ‘p’ at the front only matches filenames that begin with the letter ‘p’.

? is also a wildcard, but it matches exactly one character. So ?ethane.pdb would match methane.pdb whereas *ethane.pdb matches both ethane.pdb, and methane.pdb.

Wildcards can be used in combination with each other e.g. ???ane.pdb matches three characters followed by ane.pdb, giving cubane.pdb ethane.pdb octane.pdb.

When the shell sees a wildcard, it expands the wildcard to create a list of matching filenames before running the command that was asked for. As an exception, if a wildcard expression does not match any file, Bash will pass the expression as an argument to the command as it is. For example typing ls *.pdf in the molecules directory (which contains only files with names ending with .pdb) results in an error message that there is no file called *.pdf. However, generally commands like wc and ls see the lists of file names matching these expressions, but not the wildcards themselves. It is the shell, not the other programs, that deals with expanding wildcards, and this is another example of orthogonal design.

[Files and Folders Exercise](FFexercise/)