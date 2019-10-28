---
layout: page_nohead
title: Commandline Workshop - Toolkit5
permalink: /CLworkshop/Toolkit5/
---

__Task Answer__

A file called animals.txt (in the data-shell/data folder) contains the following data:

```shell
2012-11-05,deer
2012-11-05,rabbit
2012-11-05,raccoon
2012-11-06,rabbit
2012-11-06,deer
2012-11-06,fox
2012-11-07,rabbit
2012-11-07,bear
```

What text passes through each of the pipes and the final redirect in the pipeline below?

```shell
$ cat animals.txt | head -n 5 | tail -n 3 | sort -r > final.txt
```

Hint: build the pipeline up one command at a time to test your understanding

Solution
The head command extracts the first 5 lines from animals.txt. Then, the last 3 lines are extracted from the previous 5 by using the tail command. With the sort -r command those 3 lines are sorted in reverse order and finally, the output is redirected to a file final.txt. The content of this file can be checked by executing cat final.txt. The file should contain the following lines:

```shell
2012-11-06,rabbit
2012-11-06,deer
2012-11-05,raccoon
```

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
CLASSIFICATION: basiliscus vulgaris
CLASSIFICATION: bos hominus
CLASSIFICATION: equus monoceros
```

When the shell sees the keyword for, it knows to repeat a command (or group of commands) once for each item in a list. Each time the loop runs (called an iteration), an item in the list is assigned in sequence to the variable, and the commands inside the loop are executed, before moving on to the next item in the list. Inside the loop, we call for the variable’s value by putting $ in front of it. The $ tells the shell interpreter to treat the variable as a variable name and substitute its value in its place, rather than treat it as text or an external command.

In this example, the list is three filenames: basilisk.dat, minotaur.dat, and unicorn.dat. Each time the loop iterates, it will assign a file name to the variable filename and run the head command. The first time through the loop, $filename is basilisk.dat. The interpreter runs the command head on basilisk.dat and pipes the first two lines to the tail command, which then prints the second line of basilisk.dat. For the second iteration, $filename becomes minotaur.dat. This time, the shell runs head on monotaur.dat and pipes the first two lines to the tail command, which then prints the second line of monotaur.dat. For the third iteration, $filename becomes unicorn.dat, so the shell runs the head command on that file, and tail on the output of that. Since the list was only three items, the shell exits the for loop.

Let’s continue with our example in the data-shell/creatures directory. Here’s a slightly more complicated loop:

```shell
$ for filename in *.dat
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20
> done
```
------

We would like to modify each of the files in data-shell/creatures, but also save a version of the original files, naming the copies original-basilisk.dat and original-unicorn.dat. We can’t use:

```shell
$ cp *.dat original-*.dat
```

because that would expand to:

```shell
$ cp basilisk.dat minotaur.dat unicorn.dat original-*.dat
```

This wouldn’t back up our files, instead we get an error:

```shell
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

__Task Answer__


```shell
for sis in Jo Meg Beth Amy
do
	echo $sis:
	grep -ow $sis LittleWomen.txt | wc -l
done
```

Alternative, slightly inferior solution:

```shell
for sis in Jo Meg Beth Amy
do
	echo $sis:
	grep -ocw $sis LittleWomen.txt
done
```

This solution is inferior because grep -c only reports the number of lines matched. The total number of matches reported by this method will be lower if there is more than one match per line.

Perceptive observers may have noticed that character names sometimes appear in all-uppercase in chapter titles (e.g. ‘MEG GOES TO VANITY FAIR’). If you wanted to count these as well, you could add the -i option for case-insensitivity (though in this case, it doesn’t affect the answer to which sister is mentioned most frequently).


[Next Module: Shell Scripts](/CLworkshop/Toolkit6)
