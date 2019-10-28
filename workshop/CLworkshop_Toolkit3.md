---
layout: page_nohead
title: Commandline Workshop - Toolkit3
permalink: /CLworkshop/Toolkit3/
---

### Pipes and Filters

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
 
 ------
 
 
 Nelle’s Pipeline: Checking Files
 Nelle has run her samples through the assay machines and created 17 files in the north-pacific-gyre/2012-07-03 directory described earlier. As a quick sanity check, starting from her home directory, Nelle types:

```shell
$ cd north-pacific-gyre/2012-07-03
$ wc -l *.txt
```
 
 The output is 18 lines that look like this:
 
```shell
 300 NENE01729A.txt
 300 NENE01729B.txt
 300 NENE01736A.txt
 300 NENE01751A.txt
 300 NENE01751B.txt
 300 NENE01812A.txt
```
 
 ... ...
 Now she types this:

```shell
$ wc -l *.txt | sort -n | head -n 5
  240 NENE02018B.txt
  300 NENE01729A.txt
  300 NENE01729B.txt
  300 NENE01736A.txt
  300 NENE01751A.txt
```
  
 Whoops: one of the files is 60 lines shorter than the others. When she goes back and checks it, she sees that she did that assay at 8:00 on a Monday morning — someone was probably in using the machine on the weekend, and she forgot to reset it. Before re-running that sample, she checks to see if any files have too much data:

```shell
 $ wc -l *.txt | sort -n | tail -n 5
  300 NENE02040B.txt
  300 NENE02040Z.txt
  300 NENE02043A.txt
  300 NENE02043B.txt
 5040 total
 ```
 
 Those numbers look good — but what’s that ‘Z’ doing there in the third-to-last line? All of her samples should be marked ‘A’ or ‘B’; by convention, her lab uses ‘Z’ to indicate samples with missing information. To find others like it, she does this:

```shell
 $ ls *Z.txt
 NENE01971Z.txt    NENE02040Z.txt
 ```
 
 Sure enough, when she checks the log on her laptop, there’s no depth recorded for either of those samples. Since it’s too late to get the information any other way, she must exclude those two files from her analysis. She could delete them using rm, but there are actually some analyses she might do later where depth doesn’t matter, so instead, she’ll have to be careful later on to select files using the wildcard expression *[AB].txt. As always, the * matches any number of characters; the expression [AB] matches either an ‘A’ or a ‘B’, so this matches all the valid data files she has.
 
[Loops](/CLworkshop/Toolkit4/)
