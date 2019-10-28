---
layout: page_nohead
title: Commandline Workshop - Toolkit3
permalink: /CLworkshop/Toolkit3/
---

### _Finding Things_

In the same way that many of us now use ‘Google’ as a verb meaning ‘to find’, Unix programmers often use the word ‘grep’. ‘grep’ is a contraction of ‘global/regular expression/print’, a common sequence of operations in early Unix text editors. It is also the name of a very useful command-line program.

grep finds and prints lines in files that match a pattern. For our examples, we will use a file that contains three haikus taken from a 1998 competition in Salon magazine. For this set of examples, we’re going to be working in the writing subdirectory:

```shell
$ cd
$ cd Desktop/data-shell/writing
$ cat haiku.txt

The Tao that is seen
Is not the true Tao, until
You bring fresh toner.

With searching comes loss
and the presence of absence:
"My Thesis" not found.

Yesterday it worked
Today it is not working
Software is like that.
```

Let’s find lines that contain the word ‘not’:

```shell
$ grep not haiku.txt
Is not the true Tao, until
"My Thesis" not found
Today it is not working
```

Here, not is the pattern we’re searching for. The grep command searches through the file, looking for matches to the pattern specified. To use it type grep, then the pattern we’re searching for and finally the name of the file (or files) we’re searching in.

The output is the three lines in the file that contain the letters ‘not’.

By default, grep searches for a pattern in a case-sensitive way. In addition, the search pattern we have selected does not have to form a complete word, as we will see in the next example.

Let’s search for the pattern: ‘The’.

```shell
$ grep The haiku.txt
The Tao that is seen
"My Thesis" not found.
```
This time, two lines that include the letters ‘The’ are outputted, one of which contained our search pattern within a larger word, ‘Thesis’.

grep’s real power doesn’t come from its options, though; it comes from the fact that patterns can include regular expressions, or wildcards.

\* is a wildcard, which matches zero or more characters. Let’s consider the data-shell/molecules directory: \*.pdb matches ethane.pdb, propane.pdb, and every file that ends with ‘.pdb’. On the other hand, p*.pdb only matches pentane.pdb and propane.pdb, because the ‘p’ at the front only matches filenames that begin with the letter ‘p’.

? is also a wildcard, but it matches exactly one character. So ?ethane.pdb would match methane.pdb whereas *ethane.pdb matches both ethane.pdb, and methane.pdb.

Wildcards can be used in combination with each other e.g. ???ane.pdb matches three characters followed by ane.pdb, giving cubane.pdb ethane.pdb octane.pdb.

When the shell sees a wildcard, it expands the wildcard to create a list of matching filenames before running the command that was asked for. As an exception, if a wildcard expression does not match any file, Bash will pass the expression as an argument to the command as it is. For example typing ls \*.pdf in the molecules directory (which contains only files with names ending with .pdb) results in an error message that there is no file called *.pdf. However, generally commands like wc and ls see the lists of file names matching these expressions, but not the wildcards themselves. It is the shell, not the other programs, that deals with expanding wildcards, and this is another example of orthogonal design.

------

__Task__

When run in the molecules directory, which ls command(s) will produce this output?

```shell
ethane.pdb methane.pdb
``` 

1. ls \*t\*ane.pdb
2. ls \*t?ne.\*
3. ls \*t??ne.pdb
4. ls ethane.\*


__Task Answer__

The solution is 3.

1. shows all files whose names contain zero or more characters (*) followed by the letter t, then zero or more characters (*) followed by ane.pdb. This gives ethane.pdb methane.pdb octane.pdb pentane.pdb.

2. shows all files whose names start with zero or more characters (*) followed by the letter t, then a single character (?), then ne. followed by zero or more characters (*). This will give us octane.pdb and pentane.pdb but doesn’t match anything which ends in thane.pdb.

3. fixes the problems of option 2 by matching two characters (??) between t and ne. This is the solution.

4. only shows files starting with ethane.


[Next Module: Pipes and Filers](/CLworkshop/Toolkit4/)
