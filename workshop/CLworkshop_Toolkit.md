---
layout: page_nohead
title: Commandline Workshop - Toolkit
permalink: /CLworkshop/Toolkit
---

28 October 2019 \| Kathryn Mercier \| CUNY Graduate Center

This lab has been modified from the [Software Carpentry](https://software-carpentry.org/) lesson [The Unix Shell](http://swcarpentry.github.io/shell-novice/)

## __Objectives__

1. Understand why the command line is useful
2. Gain a basic toolkit to start using the command line
3. Be able to find resources to build your personal toolkit

## __2. Gain a basic toolkit to start using the command line__

### _Fundamentals_

When you start up a terminal you will see a prompt

```shell
$ 
```

Lines beginning with # are comments and are not executed. The command line is used to run programs, which may have options and arguements

```shell
# This is the general format of unix command line tools
$ program -option1 -option2 argument
```

Here is an example of two programs

```shell
# The 'pwd' program with no option or argument prints your current location
$ pwd

# The 'ls' program with no option or argument prints the files and folders in your current location
$ ls 
```

You can find information about programs, including its options and arguments, using the help option

```shell
# Running a program with the -h option (short for 'help') will print information on that programs usage
$ ls -h
```

_What is your current location and what files and folders are in that location?_

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

### _Finding Things_

In the same way that many of us now use ‘Google’ as a verb meaning ‘to find’, Unix programmers often use the word ‘grep’. ‘grep’ is a contraction of ‘global/regular expression/print’, a common sequence of operations in early Unix text editors. It is also the name of a very useful command-line program.

grep finds and prints lines in files that match a pattern. For our examples, we will use a file that contains three haikus taken from a 1998 competition in Salon magazine. For this set of examples, we’re going to be working in the writing subdirectory:

```shell
$ cd
$ cd Desktop/data-shell/writing
$ cat haiku.txt
```

Let’s find lines that contain the word ‘not’:

```shell
$ grep not haiku.txt
```
Here, not is the pattern we’re searching for. The grep command searches through the file, looking for matches to the pattern specified. To use it type grep, then the pattern we’re searching for and finally the name of the file (or files) we’re searching in.

The output is the three lines in the file that contain the letters ‘not’.

By default, grep searches for a pattern in a case-sensitive way. In addition, the search pattern we have selected does not have to form a complete word, as we will see in the next example.

Let’s search for the pattern: ‘The’.

```shell
$ grep The haiku.txt
```

grep’s real power doesn’t come from its options, though; it comes from the fact that patterns can include wildcards. (The technical name for these is regular expressions, which is what the ‘re’ in ‘grep’ stands for.) Regular expressions are both complex and powerful; if you want to do complex searches, please look at the lesson on our website. As a taster, we can find lines that have an ‘o’ in the second position like this:

```shell
$ grep -E '^.o' haiku.txt
```


[Finding Things exercise](FTExercise/)

### _Loops_

Loops are a programming construct which allow us to repeat a command or set of commands for each item in a list. As such they are key to productivity improvements through automation. Similar to wildcards and tab completion, using loops also reduces the amount of typing required (and hence reduces the number of typing mistakes).

Suppose we have several hundred genome data files named basilisk.dat, minotaur.dat, and unicorn.dat. For this example, we’ll use the creatures directory which only has three example files, but the principles can be applied to many many more files at once.

The structure of these files is the same: the common name, classification, and updated date are presented on the first three lines, with DNA sequences on the following lines. Let’s look at the files:

```shell
$ head -n 5 basilisk.dat minotaur.dat unicorn.dat
```

We would like to print out the classification for each species, which is given on the second line of each file. For each file, we would need to execute the command head -n 2 and pipe this to tail -n 1. We’ll use a loop to solve this problem, but first let’s look at the general form of a loop:

```shell
$ for thing in list_of_things
> do
>     operation_using $thing    # Indentation within the loop is not required, but aids legibility
> done
```

and we can apply this to our example like this:

```shell
$ for filename in basilisk.dat minotaur.dat unicorn.dat
> do
>    head -n 2 $filename | tail -n 1
> done
```


### _Shell scripts_


## __3. Find resources to build your personal toolkit__

[Command Line Cheat Sheet](https://www.git-tower.com/blog/command-line-cheat-sheet/) PDF with listing common commands with short explanations

[Software Carpentry](https://software-carpentry.org/) lesson [The Unix Shell](http://swcarpentry.github.io/shell-novice/)

[Code Academy, Learn the command line](https://www.codecademy.com/learn/learn-the-command-line)
