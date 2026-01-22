# Linux Fundamentals on Hyak (Klone & Tillicum)

Welcome to the **Linux Fundamentals Tutorial** for Hyak, a hands-on introduction to working on UW Research Computing systems using the Linux command line.

This tutorial is designed for **new or early-stage Hyak users** who are developing core Linux skills needed to work effectively on the Klone cluster. Where applicable, differences for **Tillicum** are noted explicitly so users who work across both systems can build transferable skills.

The materials in this repository are intentionally practical and task-oriented, emphasizing workflows you will use repeatedly when working on Hyak.

## Goals & Rationale

Many Hyak users arrive with strong research backgrounds but limited experience with Linux or high-performance computing environments. While [**Hyak Documentation**](https://hyak.uw.edu/docs/) covers many tools and services in depth, it can be difficult for new users to know where to start.

The goal of this tutorial is to:

* Provide a **gentle, structured introduction** to Linux fundamentals
* Build confidence working at the command line
* Establish best practices for navigating files, managing data, and transferring files
* Prepare users to work independently on Hyak and advance to more specialized workflows

By the end of this tutorial, you should feel comfortable logging in, navigating the filesystem, moving data, and completing basic tasks on Klone.

## Learning Objectives

By completing this tutorial, you will learn how to:

* Understand the role of the command line interface (CLI) in HPC environments
* Log in to Hyak systems securely
* Navigate the Linux filesystem using core commands
* Understand your Home directory and storage policies on Hyak
* Use Open OnDemand’s file explorer for basic file management
* Transfer files to and from Hyak using `scp` and Globus
* Use essential Linux commands for inspecting and manipulating files
* Combine multiple skills to complete a short, hands-on task

## Repository Structure

Each topic in this tutorial is contained in its own Markdown file for easy navigation and reuse:

| Section | Description |
|-------|-------------|
| [**00-prereqs.md**](./00-prereqs.md) | Account and access prerequisites |
| [**01-logging-in.md**](./01-logging-in.md) | Logging in to Hyak (Klone) via SSH |
| [**02-filesystem.md**](./02-filesystem.md) | Home directory, storage locations, and navigating the filesystem |
| [**03-user-tools.md**](./03-user-tools.md) | Introduction to Hyak user tools |
| [**04-ood-files.md**](./04-ood-files.md) | Using Open OnDemand’s file explorer |
| [**05-file-transfer.md**](./05-file-transfer.md) | Transferring files with `scp` and Globus |
| [**06-basic-commands.md**](./06-basic-commands.md) | Essential Linux commands for daily use |
| [**07-filtering.md**](./07-filtering.md) | Commands for data and text wrangling |
| [**08-task.md**](./08-task.md) | Hands-on task combining multiple skills |

## Scope Notes: Klone vs. Tillicum

This tutorial is **Klone-first**, as Klone is the primary entry point for most new Hyak users.

Where workflows or commands differ on **Tillicum**, those differences are clearly labeled and explained. In many cases, the same Linux concepts apply directly across both systems.

## Introduction Video

An optional introduction video accompanies this tutorial and provides a high-level walkthrough of the concepts covered:

*Linux Fundamentals on Hyak*  - Video coming soon. 

[**Slide Deck**](./slide_deck_linux_fundamentals.pdf) from live tutorial on January 22, 2026. 

## Acknowledgements

Some concepts and exercises in this tutorial are inspired by  
[**The Unix Shell**](https://swcarpentry.github.io/shell-novice/index.html)  
from Software Carpentry and have been adapted to reflect Hyak-specific systems and policies.

Materials derived from Software Carpentry are licensed under  
**Creative Commons Attribution (CC BY 4.0)**.

## Feedback

Your feedback helps improve Hyak trainings and documentation.

After completing this tutorial or attending a related workshop, please share your thoughts using our  
[**feedback form**](https://forms.office.com/r/Sm45HEeXxy).

## Additional Resources

* [**Hyak Short How-To Video Collection**](https://hyak.uw.edu/learn)
    * [**Hyak Klone Login**](https://youtu.be/gbse1xqezqk)
    * [**Hyak Home Directories**](https://youtu.be/OhLwqAZIBOo)
    * [**Hyak Klone Filesystem**](https://youtu.be/VFGREiZ37x0)
    * [**Hyak Klone Slurm**](https://youtu.be/jgHXB7IfGPQ?si=0lFpU_ujrQoUUmyb)
* [**Hyak Documentation**](https://hyak.uw.edu/docs/)
* [**Tillicum Documentation**](https://hyak.uw.edu/docs/tillicum/)
* [**Tillicum Tutorials Series**](https://hyak.uw.edu/learn)
   * [**Tillicum Onboarding Tutorial**](https://github.com/UWrc/tillicum-onboarding)
   * [**Tillicum Slurm Tutorial**](https://github.com/UWrc/tillicum-slurm)
   * [**Tillicum Containers Tutorial**](https://github.com/UWrc/tillicum-containers) 
   * [**Fine-tuning LLMs on Tillicum**](https://github.com/josecols/ft-llms-tillicum)
* [**Open OnDemand**](https://hyak.uw.edu/docs/ood/start)
* [**Globus on Hyak**](https://hyak.uw.edu/docs/storage/globus)
* [**Software Carpentry: The Unix Shell**](https://swcarpentry.github.io/shell-novice/index.html)

