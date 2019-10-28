---
layout: page_nohead
title: Commandline Workshop - Toolkit4
permalink: /CLworkshop/Toolkit4/
---

### _Pipes and Filters_

Now that we know a few basic commands, we can finally look at the shell’s most powerful feature: the ease with which it lets us combine existing programs in new ways. We’ll start with a directory called molecules that contains six files describing some simple organic molecules. The .pdb extension indicates that these files are in Protein Data Bank format, a simple text format that specifies the type and position of each atom in the molecule.

```shell
$ ls molecules
```
```
cubane.pdb    ethane.pdb    methane.pdb
octane.pdb    pentane.pdb   propane.pdb
```

Let’s go into that directory with cd and run the command wc *.pdb. wc is the ‘word count’ command: it counts the number of lines, words, and characters in files (from left to right, in that order).

The \* in \*.pdb matches zero or more characters, so the shell turns \*.pdb into a list of all .pdb files in the current directory:

```shell
$ cd molecules
$ wc *.pdb
```
```
  20  156  1158  cubane.pdb
  12  84   622   ethane.pdb
   9  57   422   methane.pdb
  30  246  1828  octane.pdb
  21  165  1226  pentane.pdb
  15  111  825   propane.pdb
 107  819  6081  total
```
Note that wc *.pdb also shows the total number of all lines in the last line of the output.

If we run wc -l instead of just wc, the output shows only the number of lines per file:

```shell
$ wc -l *.pdb
```
```
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
 ```
We can also use -w to get only the number of words, or -c to get only the number of characters.
 
Which of these files contains the fewest lines? It’s an easy question to answer when there are only six files, but what if there were 6000? Our first step toward a solution is to run the command:

```shell
$ wc -l *.pdb > lengths.txt
```

The greater than symbol, >, tells the shell to redirect the command’s output to a file instead of printing it to the screen. (This is why there is no screen output: everything that wc would have printed has gone into the file lengths.txt instead.) The shell will create the file if it doesn’t exist. If the file exists, it will be silently overwritten, which may lead to data loss and thus requires some caution. ls lengths.txt confirms that the file exists:

```shell
$ ls lengths.txt
```
```
lengths.txt
```

We can now send the content of lengths.txt to the screen using cat lengths.txt. The cat command gets its name from ‘concatenate’ i.e. join together, and it prints the contents of files one after another. There’s only one file in this case, so cat just shows us what it contains:

```shell
$ cat lengths.txt
```
```
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
 ```
 Now let’s use the sort command to sort its contents.
 
 ```shell
$ sort -n lengths.txt
```
```
 9  methane.pdb
 12  ethane.pdb
 15  propane.pdb
 20  cubane.pdb
 21  pentane.pdb
 30  octane.pdb
107  total
```

We can put the sorted list of lines in another temporary file called sorted-lengths.txt by putting > sorted-lengths.txt after the command, just as we used > lengths.txt to put the output of wc into lengths.txt. Once we’ve done that, we can run another command called head to get the first few lines in sorted-lengths.txt:

```shell
$ sort -n lengths.txt > sorted-lengths.txt
$ head -n 1 sorted-lengths.txt
```
```
  9  methane.pdb
```

If you think this is confusing, you’re in good company: even once you understand what wc, sort, and head do, all those intermediate files make it hard to follow what’s going on. We can make it easier to understand by running sort and head together:

```shell
$ sort -n lengths.txt | head -n 1
```
```
  9  methane.pdb
```

The vertical bar, \|, between the two commands is called a pipe. It tells the shell that we want to use the output of the command on the left as the input to the command on the right.

Nothing prevents us from chaining pipes consecutively. That is, we can for example send the output of wc directly to sort, and then the resulting output to head. Thus we first use a pipe to send the output of wc to sort:

```shell
$ wc -l *.pdb | sort -n | head -n 1
```
```
   9  methane.pdb
```
---

__Task__

|A file called animals.txt (in the data-shell/data folder) contains the following data:

2012-11-05,deer
2012-11-05,rabbit
2012-11-05,raccoon
2012-11-06,rabbit
2012-11-06,deer
2012-11-06,fox
2012-11-07,rabbit
2012-11-07,bear

What text passes through each of the pipes and the final redirect in the pipeline below?

```shell
$ cat animals.txt | head -n 5 | tail -n 3 | sort -r > final.txt
```

Hint: build the pipeline up one command at a time to test your understanding


__Solution__

The head command extracts the first 5 lines from animals.txt. Then, the last 3 lines are extracted from the previous 5 by using the tail command. With the sort -r command those 3 lines are sorted in reverse order and finally, the output is redirected to a file final.txt. The content of this file can be checked by executing cat final.txt. The file should contain the following lines:

```shell
2012-11-06,rabbit
2012-11-06,deer
2012-11-05,raccoon
```
---

[Next Module: Loops](/CLworkshop/Toolkit5/)
