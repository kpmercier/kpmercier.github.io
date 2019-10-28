---
layout: page_nohead
title: Commandline Workshop - Toolkit5
permalink: /CLworkshop/Toolkit5/
---

### _Loops_

Loops are a programming construct which allow us to repeat a command or set of commands for each item in a list. As such they are key to productivity improvements through automation. Similar to wildcards and tab completion, using loops also reduces the amount of typing required (and hence reduces the number of typing mistakes).

Suppose we have several hundred genome data files named basilisk.dat, minotaur.dat, and unicorn.dat. For this example, we’ll use the creatures directory which only has three example files, but the principles can be applied to many many more files at once.

The structure of these files is the same: the common name, classification, and updated date are presented on the first three lines, with DNA sequences on the following lines. Let’s look at the files:

```shell
$ head -n 5 basilisk.dat minotaur.dat unicorn.dat
```
```
==> basilisk.dat <==
COMMON NAME: basilisk
CLASSIFICATION: basiliscus vulgaris
UPDATED: 1745-05-02
CCCCAACGAG
GAAACAGATC

==> minotaur.dat <==
COMMON NAME: minotaur
CLASSIFICATION: bos hominus
UPDATED: 1765-02-17
CCCGAAGGAC
CGACATCTCT

==> unicorn.dat <==
COMMON NAME: unicorn
CLASSIFICATION: equus monoceros
UPDATED: 1738-11-24
AGCCGGGTCG
CTTTACCTTA
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
```
CLASSIFICATION: basiliscus vulgaris
CLASSIFICATION: bos hominus
CLASSIFICATION: equus monoceros
```

When the shell sees the keyword _for_, it knows to repeat a command (or group of commands) once for each item in a list. Each time the loop runs (called an iteration), an item in the list is assigned in sequence to the variable, and the commands inside the loop are executed, before moving on to the next item in the list. Inside the loop, we call for the variable’s value by putting $ in front of it. The $ tells the shell interpreter to treat the variable as a variable name and substitute its value in its place, rather than treat it as text or an external command.

In this example, the list is three filenames: basilisk.dat, minotaur.dat, and unicorn.dat. Each time the loop iterates, it will assign a file name to the variable _filename_ and run the _head_ command. The first time through the loop, _$filename_ is basilisk.dat. The interpreter runs the command _head_ on basilisk.dat and pipes the first two lines to the _tail_ command, which then prints the second line of basilisk.dat. For the second iteration, _$filename_ becomes minotaur.dat. This time, the shell runs head on monotaur.dat and pipes the first two lines to the tail command, which then prints the second line of monotaur.dat. For the third iteration, $filename becomes unicorn.dat, so the shell runs the head command on that file, and tail on the output of that. Since the list was only three items, the shell exits the for loop.

---

__Task__

This exercise refers to the data-shell/molecules directory. ls gives the following output:

```
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```

What is the output of the following code?

```shell
$ for datafile in *.pdb
> do
>    ls *.pdb
> done
```

Now, what is the output of the following code?

```shell
$ for datafile in *.pdb
> do
>    ls $datafile
> done
```

Why do these two loops give different outputs?

__Solution__

The first code block gives the same output on each iteration through the loop. Bash expands the wildcard *.pdb within the loop body (as well as before the loop starts) to match all files ending in .pdb and then lists them using ls. The expanded loop would look like this:

```shell
$ for datafile in cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> do
>    ls cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
> done
```
```
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
cubane.pdb  ethane.pdb  methane.pdb  octane.pdb  pentane.pdb  propane.pdb
```

The second code block lists a different file on each loop iteration. The value of the datafile variable is evaluated using $datafile, and then listed using ls.

```
cubane.pdb
ethane.pdb
methane.pdb
octane.pdb
pentane.pdb
propane.pdb
```

---

Let’s continue with our example in the data-shell/creatures directory. Here’s a slightly more complicated loop:

```shell
$ for filename in *.dat
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20
> done
```

The shell starts by expanding *.dat to create the list of files it will process. The loop body then executes two commands for each of those files. The first command, echo, prints its command-line arguments to standard output. For example:

```shell
$ echo hello there
```

prints:

```
hello there
```

In this case, since the shell expands $filename to be the name of a file, echo $filename prints the name of the file. Note that we can’t write this as:

```shell
$ for filename in *.dat
> do
>     $filename
>     head -n 100 $filename | tail -n 20
> done
```

because then the first time through the loop, when $filename expanded to basilisk.dat, the shell would try to run basilisk.dat as a program. Finally, the head and tail combination selects lines 81-100 from whatever file is being processed (assuming the file has at least 100 lines).

We would like to modify each of the files in data-shell/creatures, but also save a version of the original files, naming the copies original-basilisk.dat and original-unicorn.dat. We can’t use:

```shell
$ cp *.dat original-*.dat
```

because that would expand to:

```shell
$ cp basilisk.dat minotaur.dat unicorn.dat original-*.dat
```

This wouldn’t back up our files, instead we get an error:

```
cp: target `original-*.dat' is not a directory
```

This problem arises when cp receives more than two inputs. When this happens, it expects the last input to be a directory where it can copy all the files it was passed. Since there is no directory named original-*.dat in the creatures directory we get an error.

Instead, we can use a loop:

```shell
$ for filename in *.dat
> do
>     cp $filename original-$filename
> done
```

This loop runs the cp command once for each filename. The first time, when $filename expands to basilisk.dat, the shell executes:

```shell
cp basilisk.dat original-basilisk.dat
```

The second time, the command is:

```shell
cp minotaur.dat original-minotaur.dat
```

The third and last time, the command is:

```shell
cp unicorn.dat original-unicorn.dat
```

Since the cp command does not normally produce any output, it’s hard to check that the loop is doing the correct thing. However, we learned earlier how to list files in a directory. Lets check that the correct files were made 

------

__Task__

You and your friend, having just finished reading Little Women by Louisa May Alcott, are in an argument. Of the four sisters in the book, Jo, Meg, Beth, and Amy, your friend thinks that Jo was the most mentioned. You, however, are certain it was Amy. Luckily, you have a file LittleWomen.txt containing the full text of the novel (data-shell/writing/data/LittleWomen.txt). Using a for loop, how would you tabulate the number of times each of the four sisters is mentioned?

__Solution__


```shell
$ for sis in Jo Meg Beth Amy
> do
>	echo $sis:
>	grep -w $sis LittleWomen.txt | wc -l
> done
```
This solution is not the best because _grep -w_ and _wc -l_ only reports the number of lines matched. The total number of matches reported by this method will be lower if there is more than one match per line.

Alternative solution:

```shell
$ for sis in Jo Meg Beth Amy
> do
>	echo $sis:
>	grep -ow $sis LittleWomen.txt | wc -l
> done
```

Perceptive observers may have noticed that character names sometimes appear in all-uppercase in chapter titles (e.g. ‘MEG GOES TO VANITY FAIR’). If you wanted to count these as well, you could add the -i option for case-insensitivity (though in this case, it doesn’t affect the answer to which sister is mentioned most frequently).

---

__Nelle’s Pipeline: Processing Files__
Nelle is now ready to process her data files using goostats — a shell script written by her supervisor. This calculates some statistics from a protein sample file, and takes two arguments:

an input file (containing the raw data)

an output file (to store the calculated statistics)

Since she’s still learning how to use the shell, she decides to build up the required commands in stages. Her first step is to make sure that she can select the right input files — remember, these are ones whose names end in ‘A’ or ‘B’, rather than ‘Z’. Starting from her home directory, Nelle types:

```shell
$ cd north-pacific-gyre/2012-07-03
$ for datafile in NENE*[AB].txt
> do
>     echo $datafile
> done
```
```
NENE01729A.txt
NENE01729B.txt
NENE01736A.txt
...
NENE02043A.txt
NENE02043B.txt
```

Her next step is to decide what to call the files that the goostats analysis program will create. Prefixing each input file’s name with ‘stats’ seems simple, so she modifies her loop to do that:

```shell
$ for datafile in NENE*[AB].txt
> do
>     echo $datafile stats-$datafile
> done
```
```
NENE01729A.txt stats-NENE01729A.txt
NENE01729B.txt stats-NENE01729B.txt
NENE01736A.txt stats-NENE01736A.txt
...
NENE02043A.txt stats-NENE02043A.txt
NENE02043B.txt stats-NENE02043B.txt
```

She hasn’t actually run goostats yet, but now she’s sure she can select the right files and generate the right output filenames.

Typing in commands over and over again is becoming tedious, though, and Nelle is worried about making mistakes, so instead of re-entering her loop, she presses the up arrow. In response, the shell redisplays the whole loop on one line (using semi-colons to separate the pieces):

```shell
$ for datafile in NENE*[AB].txt; do echo $datafile stats-$datafile; done
```

Using the left arrow key, Nelle backs up and changes the command echo to bash goostats:

```shell
$ for datafile in NENE*[AB].txt; do bash goostats $datafile stats-$datafile; done
```

When she presses Enter, the shell runs the modified command. However, nothing appears to happen — there is no output. After a moment, Nelle realizes that since her script doesn’t print anything to the screen any longer, she has no idea whether it is running, much less how quickly. She kills the running command by typing Ctrl-C, uses up-arrow to repeat the command, and edits it to read:

```shell
$ for datafile in NENE*[AB].txt; do echo $datafile; bash goostats $datafile stats-$datafile; done
```

[Next Module: Shell Scripts](/CLworkshop/Toolkit6)
