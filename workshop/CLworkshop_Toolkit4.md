---
layout: page_nohead
title: Commandline Workshop - Toolkit4
permalink: /CLworkshop/Toolkit4
---


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


[Resources](Resources/)
