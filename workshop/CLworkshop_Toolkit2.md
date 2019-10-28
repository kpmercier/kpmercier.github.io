---
layout: page_nohead
title: Commandline Workshop - Toolkit2
permalink: /CLworkshop/Toolkit2/
---

### __Working with files and folders__

Let’s go back to our data-shell directory and use ls to see what it contains:

```shell
$ pwd
```
```
/Users/Katie/Desktop/data-shell
$ ls
```
```
creatures  data  molecules  north-pacific-gyre  notes.txt  pizza.cfg  solar.pdf  writing
```
Let’s create a new directory called thesis using the command mkdir thesis (which has no output):

```shell
$ mkdir thesis
$ ls
```
```
creatures  data  molecules  north-pacific-gyre  notes.txt  pizza.cfg  solar.pdf  thesis  writing
```

Since we’ve just created the thesis directory, there’s nothing in it yet:

```shell
$ ls thesis

```

Let’s change our working directory to thesis using cd, then run a text editor called Nano to create a file called draft.txt:

```shell
$ cd thesis
$ nano draft.txt
```

![Nano](nano-screenshot.png)

nano doesn’t leave any output on the screen after it exits, but ls now shows that we have created a file called draft.txt:

```shell
$ ls
```
```
draft.txt
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
```
quotes.txt
```

Let’s move quotes.txt into the current working directory. We use mv once again, but this time we’ll use just the name of a directory as the second argument to tell mv that we want to keep the filename, but put the file somewhere new. (This is why the command is called ‘move’.) In this case, the directory name we use is the special directory name . that we mentioned earlier.

```shell
$ mv thesis/quotes.txt .
```
The effect is to move the file from the directory it was in to the current working directory. ls now shows us that thesis is empty:

 
```shell
$ ls thesis

```

The cp command works very much like mv, except it copies a file instead of moving it. We can check that it did the right thing using ls with two paths as arguments — like most Unix commands, ls can be given multiple paths at once:

```shell
$ cp quotes.txt thesis/quotations.txt
$ ls quotes.txt thesis/quotations.txt
```
```
quotes.txt   thesis/quotations.txt
```

We can also copy a directory and all its contents by using the recursive option -r, e.g. to back up a directory:

```shell
$ cp -r thesis thesis_backup
```

We can check the result by listing the contents of both the thesis and thesis_backup directory:

```shell
$ ls thesis thesis_backup
```
```
thesis:
quotations.txt

thesis_backup:
quotations.txt
```

---

__Task__

Suppose that you created a file in your current directory to contain a list of the statistical tests you will need to do to analyze your data, and named it: statstics.txt

After creating and saving this file you realize you misspelled the filename! You want to correct the mistake, which of the following commands could you use to do so?

__Solution__

1. mv statstics.txt statistics.txt

---

Returning to the data-shell directory, let’s tidy up this directory by removing the quotes.txt file we created. The Unix command we’ll use for this is rm (short for ‘remove’):

```shell
$ rm quotes.txt
```

We can confirm the file has gone using ls:

```shell
$ ls quotes.txt
```
```
ls: cannot access 'quotes.txt': No such file or directory
```

---

__Task__

For this exercise, you can test the commands in the data-shell/data directory.

In the example below, what does cp do when given several filenames and a directory name?

```shell
$ mkdir backup
$ cp amino-acids.txt animals.txt backup/
```

In the example below, what does cp do when given three or more file names?

```shell
$ ls
```
```
amino-acids.txt  animals.txt  backup/  elements/  morse.txt  pdb/  planets.txt  salmon.txt  sunspot.txt
$ cp amino-acids.txt animals.txt morse.txt
```

__Solution__

If given more than one file name followed by a directory name (i.e. the destination directory must be the last argument), cp copies the files to the named directory.

If given three file names, cp throws an error such as the one below, because it is expecting a directory name as the last argument.

```shell
cp: target ‘morse.txt’ is not a directory
```

---

[Next Module: Finding Things](/CLworkshop/Toolkit3/)
