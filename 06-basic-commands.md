# Basic Linux Commands

In this section, we will review more commands to get you comfortable doing basic things on Hyak. Some of the data and exercises for this tutorial were sampled from [<ins>**The Unix Shell by Software Carpentry**</ins>](https://swcarpentry.github.io/shell-novice/index.html), but have been tailored to fit most Hyak users. Sampled materials are under the Copyright of Software Carpentry and are made available under the Creative Commons Attribution license (CC BY 4.0).

We'll use some commands you already know like `pwd`, `cd`, and `ls`, but we'll cover these commands and concepts for the first time: 
* [`wget`  - web get](#wget-or-web-get-to-download-data-from-a-webpage)
* [`../` - relative path](#use-relative-paths-with-)
* [`mkdir` - make directory](#mkdir-or-make-directory-to-make-an-empty-directory)
* [`nano` - for editing files](#edit-files-with-nano)
* [`cat` - concatenate](#cat-or-concatenate-a-file-to-print-its-contentss)
* [`head`, `tail`, `more`, `less` - viewing options](#view-with-head-tail-more-less)
* [`cp` - copy](#cp-or-copy-files)
* [`mv` - move](#mv-or-move-file-to-a-new-name-rename)
* [`rm` - remove](#rm-or-remove-a-file)
* [`touch` - create a file](#create-an-empty-file-with-touch)

## Setup: Preparing Your Tutorial Workspace

You should have already completed these steps earlier in the tutorial, but before we continue, let’s make sure everyone is starting from the same place.

For the remainder of this tutorial, **your working directory will be**:

```bash
/gscratch/scrubbed/$USER/linux-fundamentals
```
Navigate to your working directory before moving on: 
```bash
cd /gscratch/scrubbed/$USER/linux-fundamentals
```

If this you don't have you working directory yet, [return to the Filesystem Scrubbed section](./02-filesystem.md#scrubbed-storage--our-tutorial-workspace) to set it up. 

## `wget` or "web get" to download data from a webpage

Download example data from the Software Carpentry github repository for the next exercises.

```bash
wget https://swcarpentry.github.io/shell-novice/data/shell-lesson-data.zip
```

List your working directory to show the zipped version of the lesson directory `shell-lesson-data.zip`.

```bash
ls
```

Unzip the lesson directory with the `unzip` command.

```bash
unzip shell-lesson-data.zip
```

`ls` should show a unzipped version of the shell-lesson-data directory as well as the zipped version.

Change directory to go into shell-lesson-data/exercise-data/writing/

```bash
cd shell-lesson-data/exercise-data/writing/
```

Print your working directory to understand where you are.

```bash
pwd
```

List the writing directory

```bash
ls 
```

The expected result is:

```bash
haiku.txt  LittleWomen.txt
```

## Use relative paths with `../`

Another way to move around the directories on the filesystem is with relative paths. Use `../` to move backwards (toward the root) one directory at a time. 

Print your working directory to understand where you are.

```bash
cd ../
```

Print working directory to see the result of `cd ../`

```bash
pwd
```

Use `cd` and `../` twice to go backward 2 directories

```bash
cd ../../
```

Print working directory again to see the result 

```bash
pwd
```

You can list the contents of the directory "above" where we are now without changing directory.

```bash

ls ../

```

## `mkdir` or "make directory" to make an empty directory 

Let's go back to `shell-lesson-data/exercise-data/writing` and practice making a directory.

```bash
cd shell-lesson-data/exercise-data/writing
```

Make a directory called "thesis"

```bash
mkdir thesis
```

Note that `mkdir` is not limited to creating single directories one at a time. The `-p` option for "path" allows `mkdir` to create a directory with nested subdirectories in a single operation:

```bash
# make a directory called project with subdirectories data and results
# make these one directory "above" where we are now 
mkdir -p ../project/data ../project/results
```

`-F` option with ls puts a `/` after directories to differentiate them from other objects.

```bash
ls -F
```

The `-R` option to the ls command will list all nested subdirectories within a directory. Let’s use `ls -FR` to recursively list the new directory hierarchy we just created in the project directory:

```bash
ls -FR ../project
```

> ⚠️ **WARNING:** Avoid complicated names for files and directories
> 
> * **Avoid spaces** - Spaces separate arguments on the command line, so they often cause unexpected behavior. Use `-` or `_` instead (for example, `north-pacific-gyre/` rather than `north pacific gyre/`).
> * **Don’t start names with `-` (dash)** - Anything beginning with `-` is interpreted as a command option, not a filename.
> * **Stick to safe characters** - Use letters, numbers, `.`, `-`, and `_`. Many other characters have special meanings in the shell and can cause commands to fail or behave in unexpected ways.

## Edit files with `nano`

To edit files on Klone we need to go back to basic text editors. You will not have access to a word processor, and formatting and syntax doesn't always translate from Microsoft Word or similar software to executable commands on Klone. Next, we will create a file called `draft.txt` and open it in the text editor `nano`.

First change directory to thesis:

```bash
cd /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/writing/thesis
```

The create and open a file called draft.txt with the command:

```bash
nano draft.txt
```

> **NOTE:** There are other text editors you could choose from. `vim` is a popular choice. `nano` is beginner friendly, so that is what we will use here.

Let's type a few lines of text.

![Screenshot of nano text editor showing draft.txt and the example text.](./img/draft_nano.png 'nano')
*Screenshot of `nano` text editor showing draft.txt and the example text.*

Once we’re happy with our text, we can press `Ctrl`+`O` (press the `Ctrl` or `Control` key and, while holding it down, press the `O` key) to write our data to disk. We will be asked to provide a name for the file that will contain our text. Press Return to accept the suggested default of `draft.txt`.

Once our file is saved, we can use `Ctrl`+`X` to quit the editor and return to the shell.

## `cat` or "concatenate" a file to print its contents

Let's view our work. 

```bash
cat draft.txt
```

> **Important concept:** Paths and Access
>
> On the command line, your location determines what you have access to. To demonstrate this important concept, consider the following example:
> 
> There is a dataset of sequences from a mythical creature called a Basilisk (from the Harry Potter Universe). If you wanted to execute anything on `basilisk.dat` you would not be able to unless you are inside of the directory where it is stored or using its **absolute path**. Let's go find it and print its contents to the shell with `cat`.
> 
> ```bash
> cd /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/creatures
> ```
> 
> List the directory.
> 
> ```bash
> ls
> ```
> 
> `cat` the Basilisk data
> 
> ```bash
> cat basilisk.dat 
> ```
> 
> To illustrate the concept of paths and access. Let's go back to our previous directory (likely `/gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/writing/thesis` if you have been following along) and try to `cat` the Basilisk data. 
> 
> ```bash
> cd -
> 
> cat basilisk.dat
> ```
> 
> The expected output:
> 
> ```bash
> cat: basilisk.dat: No such file or directory
> ```
> 
> We get an error because we can't access `basilisk.dat` from our location without more information. However, we can provide the relative or absolute path to access `basilisk.dat`:
> 
> ```bash
> cat ../../creatures/basilisk.dat
> ```
>or with the absolute path:
> ```bash
> cat /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/creatures/basilisk.dat
> ```
> 
> In this example, we have provided more information about the location of `basilisk.dat` ***relative*** to our location (i.e., using `../` to indicate the position relative to our current directory location) and are able to access it and execute the `cat` command upon it. 
> 
> We can also use ***absolute*** paths to access a file from **ANY** location on the Klone filesystem. This is a error-proof method of making sure you can execute commands on files no matter where on the filesystem the command is issued. Let's use an ***absolute*** path to see a file from elsewhere on the filesystem. There is a dataset called `animals.csv` under `/mmfs1/sw/hyak101/basics/data/`. Let's view it with `cat` from our current directory.
> 
> ```bash
> # first print your working directory to see your location
> pwd
> ```
> 
> Now use the absolute path to `animals.csv` to `cat` it
> 
> ```bash
> cat /mmfs1/sw/hyak101/basics/data/animals.csv
> ```
> 
> To summarize, to access a file or directory (i.e., item) you must be: 
> * inside of the directory where the item is
> * provide a relative path to the item from your current directory
> * provide an absolute path to the item
> 

## View with `head`, `tail`, `more`, `less`

These four commands are other ways to view file contents, great for viewing smaller chunks of longer files.

```bash
# change directory to creatures data
cd /gscratch/scrubbed/$USER/linux-fundamentals/shell-lesson-data/exercise-data/creatures/

head basilisk.dat # displays the first part of a file

tail basilisk.dat # displays the last part of a file

more basilisk.dat # displays file contents one page at a time
# exit the more command with Q

less basilisk.dat # displays file contents one page at a time
# exit the less command with Q
```

By default, `head` and `tail` commands display the first and last 10 lines of a file. To view a specific number of lines use `-n` followed by the desired number of lines.

```bash
head -n 20 basilisk.dat
```

## `cp` or "copy" files

Move to top of working directory.

```bash
cd /gscratch/scrubbed/$USER
pwd
```

Copy `animals.csv` to your current directory using the shorthand `.` to mean "here"

```bash
cp /mmfs1/sw/hyak101/basics/data/animals.csv .
```

Copy a directory with all its contents using recursive copy

```bash
cp -r /mmfs1/sw/hyak101/basics/data/ .
```

## `mv` or "move" file to a new name (rename)

```bash
mv animals.csv dataset.csv
```

## `rm` or "remove" a file

> ⚠️ **WARNING:** `rm` permanently deletes a file. This action is irreversible.

```bash
rm dataset.csv
```

Remove a directory with recursive rm.

```bash
cd shell-lesson-data/exercise-data/writing/
ls
# Use extreme caution with this command
rm -r thesis
```

## Create an empty file with `touch`

```bash
cd /gscratch/scrubbed/$USER
pwd
touch file1.txt file2.txt file3.txt
ls # make sure the .txt files were created
```

#### `touch` is also useful for updating the timestamp of a file

``` bash
ls -l file1.txt # -l will list the current timestamp of a file
touch file1.txt # touch will update the timestamp
ls -l file1.txt # -l will list the current timestamp of a file
```

Continue to **[07-filtering.md](./07-filtering.md)** to learn more command line tools for working with files and text.





