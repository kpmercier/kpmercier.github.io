---
layout: page_nohead
title: Commandline Workshop - Toolkit4
permalink: /CLworkshop/Toolkit4/
---

__Task Answer__

The solution is 3.

1. shows all files whose names contain zero or more characters (*) followed by the letter t, then zero or more characters (*) followed by ane.pdb. This gives ethane.pdb methane.pdb octane.pdb pentane.pdb.

2. shows all files whose names start with zero or more characters (*) followed by the letter t, then a single character (?), then ne. followed by zero or more characters (*). This will give us octane.pdb and pentane.pdb but doesn’t match anything which ends in thane.pdb.

3. fixes the problems of option 2 by matching two characters (??) between t and ne. This is the solution.

4. only shows files starting with ethane.

### _Pipes and Filters_

Now that we know a few basic commands, we can finally look at the shell’s most powerful feature: the ease with which it lets us combine existing programs in new ways. We’ll start with a directory called molecules that contains six files describing some simple organic molecules. The .pdb extension indicates that these files are in Protein Data Bank format, a simple text format that specifies the type and position of each atom in the molecule.

```shell
$ ls molecules
cubane.pdb    ethane.pdb    methane.pdb
octane.pdb    pentane.pdb   propane.pdb
```

Let’s go into that directory with cd and run the command wc *.pdb. wc is the ‘word count’ command: it counts the number of lines, words, and characters in files (from left to right, in that order).

The * in *.pdb matches zero or more characters, so the shell turns *.pdb into a list of all .pdb files in the current directory:

```shell
$ cd molecules
$ wc *.pdb
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
  20  cubane.pdb
  12  ethane.pdb
   9  methane.pdb
  30  octane.pdb
  21  pentane.pdb
  15  propane.pdb
 107  total
 ```
 
[Task Answer & Next Module](/CLworkshop/Toolkit5/)
