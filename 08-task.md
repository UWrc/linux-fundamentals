# Capstone Task: Interactive Data Exploration on Klone

> 🎯 **GOAL:** Use an interactive Slurm job and core Linux tools to explore, filter, and summarize a dataset, producing a reproducible text-based result.

### Overview
* [0. Preparation](#0-preparation)
* [1. Start an Interactive Job](#1-start-an-interactive-job)
* [2. Set Up Your Workspace](#3-inspect-and-understand-the-dataset)
* [3. Inspect and Understand the Dataset](#4-generate-a-reproducible-summary)
* [4. Generate a Reproducible Summary](#4-generate-a-reproducible-summary)
* [5. Filter the Dataset](#5-filter-the-dataset)
* [6. Demonstrate Safe Cleanup](#6-demonstrate-safe-cleanup)
* [7. Exit Cleanly](#7-exit-cleanly)

## 0. Preparation

If you haven't already, follow the instructions in [01-logging-in](./01-logging-in.md) to log in to Hyak Klone and set up your working directory for the following exercise [02-filesystem - tutorial working directory](./02-filesystem.md#scrubbed-storage--our-tutorial-workspace).

## 1. Start an Interactive Job

Request an interactive job on a compute node:

```bash
salloc --partition=ckpt --time=00:30:00 --mem=4G --cpus-per-task=1
```
Confirm you are no longer on the login node.

```bash
hostname
```

## 2. Set Up Your Workspace

Navigate to your tutorial working directory and create a new subdirectory for this task:

```bash
cd /gscratch/scrubbed/$USER/linux-fundamentals
mkdir capstone
cd capstone
```

Copy the animal dataset into this directory:
```bash
cp ../shell-lesson-data/exercise-data/animal-counts/animals.csv .
ls
```

## 3. Inspect and Understand the Dataset

Without opening the file in an editor:
* Determine how many records are in the dataset.
* View the first and last 3 lines of the file.
* Identify how many unique animals appear in the dataset.

You should use a combination of:
* `wc`
* `head / tail`
* `cut, sort, uniq`

Example (not complete):
```bash
cut -d, -f2 animals.csv | sort | uniq
```

What is `cut -d, -f2 animals.csv` doing?

## 4. Generate a Reproducible Summary

Create a summary file called `animal_summary.txt` using command output redirection (not manual typing):

The file must include:
* Total number of records
* Alphabetically sorted list of unique animals
* A count of how many observations exist for each animal

> **Hint:** `uniq -c` counts unique occurances of a pattern

Append all outputs into a single file using `>` and `>>`.

Verify your file:
```bash
cat animal_summary.txt
```

## 5. Filter the Dataset

Create a new CSV file that includes only rabbit observations.

Requirements:
* File name: rabbit_counts.csv
* Must preserve the original CSV format
* Must be generated using `grep`

Confirm:
```bash
wc -l rabbit_counts.csv
cat rabbit_counts.csv
```

## 6. Demonstrate Safe Cleanup

Rename your summary file and remove the intermediate dataset copy:

```bash
mv animal_summary.txt final_summary.txt
rm animals.csv
ls
```

## 7. Exit Cleanly

Exit the interactive job:
```bash
exit
```