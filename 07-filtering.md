# Working with Files and Command-Line Tools

This section introduces powerful command-line tools for working with files and text, including wildcards, searching, sorting, and counting. You’ll also learn how to combine commands using redirection and pipes to build efficient workflows on the Linux command line. Here again , we have sampled some of the data and exercises from [<ins>**The Unix Shell by Software Carpentry**</ins>](https://swcarpentry.github.io/shell-novice/index.html), but have been tailored to fit most Hyak users. Sampled materials are under the Copyright of Software Carpentry and are made available under the Creative Commons Attribution license (CC BY 4.0).

We'll use some commands you already know, but we'll cover these commands and concepts for the first time: 
* [Wildcards](#wildcards)
* [`wc` - word count](#apply-word-count-with-wc)
* [`>` - redirect](#redirect-output-to-a-file-with-)
* [`>>` - append](#append-output-to-a-file-with-)
* [`sort`](#sort-numbers-and-other-text)
* [`|` - pipe](#use-a--or-pipe-character-to-string-commands-together)
* [`grep`](#search-for-a-patter-with-grep)
* [`history` - command history](#view-your-command-history-history)
* [`find`](#view-your-command-history-history)


## Wildcards 

Wildcards are special characters used as a shorthand.

### `?` and `[]`

```bash
# ? represents any singular character
ls file?.txt  

# lists all file.txt files with a singular character using a range of values
ls file[2-3].txt

# lists all file.txt files with a singular character using a range of values
rm file[1-3].txt
```

### `*`

```bash
cd /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/alkanes/

# list all files
ls

# lists all files ending with .pdb
ls *.pdb

# further examples
ls /sw/hyak101/basics/*.slurm
ls /sw/hyak101/basics/locator*
ls /sw/hyak101/basics/locator_NN*
```

## Apply "word count" with `wc`

```bash
# in alkanes/
wc cubane.pdb

# find more flags
wc --help

# use word count with wildcard *
wc *.pdb
```

### `wc -l` counts lines

```bash
wc -l *.pdb
```

## "Redirect" output to a file with `>`

```bash
# list lengths for all files ending in .pub and redirect result to file
wc -l *.pdb > lengths.txt

cat lengths.txt
```

> ⚠️ **WARNING:** If the file already exists, it will be overwritten.

## "Append" output to a file with `>>`

```bash
cd /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/animal-counts/
cat animals.csv
```

The expected output is as follows:

```bash
2012-11-05,deer,5
2012-11-05,rabbit,22
2012-11-05,raccoon,7
2012-11-06,rabbit,19
2012-11-06,deer,2
2012-11-06,fox,4
2012-11-07,rabbit,16
2012-11-07,bear,1
```

Using `wc -l` to count the lines of the above output

```bash
wc -l animals.csv
```

```bash
8 animals.csv
```

To create a subset of `animals.csv`, we can combine `head`, `tail`, `>`, and `>>` commands.

```bash
head -n 3 animals.csv > animals-subset.csv
cat animals-subset.csv
```

`animals-subset.csv` should now contain the first 3 lines of `animals.csv`:

```bash
2012-11-05,deer,5
2012-11-05,rabbit,22
2012-11-05,raccoon,7
```

Because we do not want to override `animals-subset.csv` file contents, use `>>` to append rather than `>`:

```bash
tail -n 2 animals.csv >> animals-subset.csv
cat animals-subset.csv
```

Now, the subset reads as follows:

```bash
2012-11-05,deer,5
2012-11-05,rabbit,22
2012-11-05,raccoon,7
2012-11-07,rabbit,16
2012-11-07,bear,1
```

## `sort` numbers and other text

```bash
cd ../
# You should now be in the exercise-data directory
pwd
# /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/
cat numbers.txt
```

The expected output:

```bash
10
2
19
22
6
```

The `sort` command by itself will sort a text file's contents in ascending order:

```bash
sort numbers.txt
```

Notice how the output is sorted in lexicographical order:

```bash
10
19
2
22
6
```

To sort the numbers based on their numerical value, use the `-n` option

```bash
sort -n numbers.txt
```

Now, the file contents will be interpreted as numbers rather than strings and `numbers.txt` will be sorted in ascending numerical order:

```bash
2
6
10
19
22
```

> **NOTE:**
>The `sort` command will sort lines alphabetically or numerically. Lines with numbers and letters are sorted as follows:
>
> 1. Numbers
> 2. Capital letters
> 3. Lowercase letters
>
> Other sorting options include `-r` which sorts lines in reverse order and `-u` which removes duplicate lines.


Going back to the `alkanes` directory

```bash
cd alkanes
pwd
# /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/alkanes
cat lengths.txt
sort -n lengths.txt
```

Expected output:

```bash
9 methane.pdb
12 ethane.pdb
15 propane.pdb
20 cubane.pdb
21 pentane.pdb
30 octane.pdb
107 total
```

Create a sorted list of the alkane lengths and check the first output line:

```bash
sort -n lengths.txt > sorted-lengths.txt
head -n 1 sorted-lengths.txt
```

> ⚠️ **WARNING:**
>
> Empty file resulting from `>`. The following code will cause the contents of `lengths.txt` to be deleted:
>
>```bash
>sort -n lengths.txt > lengths.txt
>cat lengths.txt
>```
>
>Notice how `lengths.txt` is now an empty file. To get `lengths.txt` back, backtrack to the original command:
>
>```bash
> wc -l *.pdb > lengths.txt
> ```

## Use a `|` or "pipe" character to string commands together

Alternatively, the alkane lengths can sorted by using one line of code:

```bash
wc -l *.pdb | sort -n

wc -l *.pdb | sort -n > sorted_lengths_v2.txt

cat sorted_lengths_v2.txt
```

## Search for a patter with `grep`

`grep` finds and prints lines in files that match a pattern

```bash
cd /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/writing
cat haiku.txt
grep not haiku.txt 
```

Only the lines containing "not" will print out. Now try the following `grep` command:

```bash
grep The haiku.txt
```

Notice how longer words containing "The" are also printed out. Use the `-w` option to ensure that `grep` is only matching whole words:

```bash
grep -w The haiku.txt
```

`grep` also works with multiple words at a time:

```bash
grep -w "is not" haiku.txt
```

Other options include `-n` which displays line numbers:

```bash
grep -n "it" haiku.txt
```

Combining options `-n` and `-w`:

```bash
grep -n -w "the" haiku.txt
```

The `-r` (recursive) option:

```bash
grep -r Yesterday .
```

This searches for the word Yesterday in your current directory (writing).

## View your command history `history`

```bash
history
```

Use `history`, `|`, and `grep` together to find all times the `cat` command was used.

```bash
history |grep cat
```

## `find` files or files matching a pattern

```bash
cd ../
pwd
# /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/
find . -name numbers.txt
```
This will print out the location of numbers.txt :

Use `*` to find all .txt files starting in your current directory :

```bash
find . -name "*.txt"
```

Use `grep` and `find` together to search for files with specific words or phrases:

```bash
grep "searching" $(find . -name "*.txt")
```

The output shows the file location and the lines with the word "searching".
