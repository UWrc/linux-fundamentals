# Navigating the Filesystem & Understanding Storage

In this section, you’ll learn how to navigate the Hyak filesystem and understand where your files live.
We’ll focus on **Klone**, while noting important differences for **Tillicum** where they exist.

Working effectively on Hyak depends on two core ideas:

1. **Knowing where you are** in the filesystem  
2. **Knowing which storage space you are using**

Both of these are controlled through the Linux command line.

## CLI vs. GUI: A Mental Model

If you are familiar with **Windows File Explorer** or **macOS Finder**, you already understand the basic idea of a filesystem.

When you click through folders in a graphical interface, you are:
* Moving between directories
* Viewing file contents
* Opening or running programs

The **command-line interface (CLI)** does the same things, but through typed commands instead of clicks.
This gives you:
* More precision
* Better performance on remote systems
* The ability to automate tasks

Throughout this section, we’ll use commands to answer three questions:
* *Where am I?*
* *What’s here?*
* *How do I move somewhere else?*

## Klone Storage Overview

On **Klone**, your primary storage locations live under `/mmfs1/`, which is a shared, high-performance filesystem accessible from all login and compute nodes.

**Key locations you will encounter include:**

* `/mmfs1/home/UWNetID/` — your **Home directory**. 
> ⚠️ **WARNING:** Home directories on Tillicum have **limited quota** (10GB). Active research data, training datasets, and large outputs should be stored in project or scrubbed storage, not in $HOME.
>
> Your **Home directory** is intended only for:
> - Configuration files
> - Small scripts
> - Lightweight code
* `/mmfs1/gscratch/group-name/` — shared group and project storage. Variable total capacity based on hardware holdings.
    * `/mmfs1/gscratch/scrubbed/` - free community storage for temporary, high-capacity workloads. Data stored in scrubbed locations will be automatically removed after 21 days of inactivity, so it should only be used for intermediate or reproducible data. User limit of 10TB, but amount is not guarenteed and may not be available. 
* `/mmfs1/sw/` — centrally managed software and shared materials

> **NOTE: No storage location on Klone is backed up.**  
> This includes home directories, group storage, and scrubbed spaces.
> 
> Users are responsible for backing up any data they wish to preserve. We strongly recommend maintaining copies of important data outside of Klone.
> 
> UWIT Research Computing provides alternative storage services suitable for backups, including:
> 
> - [**Kopah**](https://uwconnect.uw.edu/it?id=kb_article_view&sysparm_article=KB0036083) — S3-compatible object storage
> - [**Lolo**](https://uwconnect.uw.edu/it?id=kb_article_view&sysparm_article=KB0036084) — long-term, geographically redundant storage
> 
> Backups to these services must be **configured and managed by users**. Klone should be treated as a high-performance computing environment, not a system of record for long-term data retention. 

![Diagrammatic representation of the Klone filesystem directory tree. The root directory appears at the top and contains several subdirectories. A truncated view highlights the mmfs1 directory and selected subdirectories within it, including home for user home directories, sw for shared software and scripts, and gscratch for project and lab group storage. Some directories are shown in blue to indicate they are also accessible via symbolic links from shorter top-level paths.](./img/filesystem_klone.jpg 'Klone filesystem')

*Simplified view of the Klone filesystem hierarchy. The root directory (`/`) contains all subdirectories. This diagram highlights `/mmfs1` and commonly used paths within it, including user home directories (`/mmfs1/home`), shared software and scripts (`/mmfs1/sw`), project and lab group storage (`/mmfs1/gscratch`), and [**common datasets**](https://hyak.uw.edu/docs/data-commons/requirements) (`/mmfs1/data`). Directories shown in blue indicate locations that are also available through symbolic links for convenience.*

> **NOTE: Symbolic Links on Klone**
>
> On Klone, some commonly used directories have symbolic links (also called symlinks) that provide shorter, easier-to-type paths.
>
> For example, the following paths refer to the same location:
> ```bash
> /mmfs1/gscratch
> /gscratch
> ```
> Symbolic links do not duplicate data. Instead, they act as pointers to the original directory. You can safely use either path when navigating the filesystem or writing job scripts.
> 
> ***You may see multiple paths that appear different but resolve to the same location. This is expected behavior on Klone and is used to improve usability.***


## Location Is Key

Linux provides a small set of commands that you’ll use constantly to navigate the file system. In this section, we will practice using these common commands to move around Huak Klone.

We’ll start with three essential ones:
* [`pwd` — Where am I?](./02-filesystem.md#pwd-where-am-i)
* [`cd` — Move somewhere else](./02-filesystem.md#cd-moving-between-directories)
* [`ls` — What’s here?](./02-filesystem.md#ls-listing-directory-contents)

### 1. `pwd`: Where Am I?

The `pwd` command prints your current directory.

```bash
pwd
```

When you first log in to Klone, you should see something like:
```bash
/mmfs1/home/UWNetID
```
This is the absolute path to your Home directory. An absolute path always starts at the root directory (`/`) and describes a full address to a location on the system.

### 2. `cd`: Moving Between Directories

The `cd` command changes your current directory.

For example, to move into a shared tutorial directory:
```bash
cd /mmfs1/sw/hyak101/basics
```

Your prompt will update to reflect your new location:
```bash
[UWNetID@klone-login01 basics]$
```

To return to your Home directory:
```bash
cd ~
```

Check your location again:
```bash
pwd
```

You should now be back in:
```bash
/mmfs1/home/UWNetID
```

> Useful `cd` Shortcuts:
> * `cd ~` Go to your Home directory
> * `cd` Also goes to Home
> * `cd /` Go to the root directory
> * `cd -` Go back to your previous directory

### 3. `ls`: Listing Directory Contents

The `ls` command shows the contents of a directory.
```bash
ls
```

If your Home directory is new or mostly empty, you may see little or no output.

To explore the broader filesystem, try listing the root directory:
```bash
cd /
ls
```

You’ll see many system directories, including `mmfs1`.

Now list what’s inside `mmfs1`:
```bash
ls /mmfs1
```

This includes:
* `home/` — user home directories
* `gscratch/` — group and project storage
* `sw/` — shared software and materials
* `data/` - [**common datasets**](https://hyak.uw.edu/docs/data-commons/requirements)

You do not need to be inside a directory to list its contents. You can provide a path directly to `ls`.

#### Listing Details and Hidden Files

Some useful `ls` options:
* `ls -l` Long format (permissions, size, owner, date)
* `ls -a` Include hidden files

Hidden files begin with a `.` (for example, `.bashrc`). These are common in your Home directory and usually control shell behavior.

## Node vs. Filesystem Location

Your command prompt shows two kinds of location:
```bash
[UWNetID@klone-login01 ~]$
```

* `klone-login01` — the node you are connected to
* `~` — your current directory

Even if you later move to a compute node, your filesystem paths (for example, `/mmfs1/home/UWNetID`) will remain the same across the cluster.

## Scrubbed Storage — Our Tutorial Workspace
Scrubbed storage is temporary scratch space for active computation. It’s not backed up and files are deleted automatically after **21 days** of inactivity.

Location:

```bash
/gscratch/scrubbed/
```

For this tutorial, we’ll use scrubbed space as our working directory. Create a personal folder there and move into it:

```bash
mkdir /gscratch/scrubbed/$USER
cd /gscratch/scrubbed/$USER
```

While we're at it, le'ts clone the git repository for this tutorial, we'll use some of the files later. 

```bash
git clone https://github.com/UWrc/linux-fundamentals.git
```

You can check the contens of your working directory and the contents of the git repository at any time with:

```bash
ls
ls linux-fundamentals
```


## Practice: Exploring the Klone Filesystem

Let’s practice a few commands to get familiar with the filesystem:

```bash
# Go to the root directory
cd /

# List top-level directories
ls

# Explore home directories
ls /mmfs1/home/

# Explore scrubbed storage
ls /gscratch/scrubbed/

# Enter your scrubbed working directory for this tutuorial
cd /gscratch/scrubbed/$USER

# Return to your home directory
cd ~
pwd
```

While continuing to explore the filesystem, if you see a message like “Permission denied”, that’s normal — not all directories are accessible to all users on a shared system.


## Tillicum Storage Overview (For Comparison)

Klone and Tillicum are both Linux systems, and so have a very similar filesystem layout, but there are some key differences. On **Tillicum**, all user-accessible storage lives under `/gpfs/`, a shared, high-performance filesystem mounted on all login and compute nodes.

Whenever you see a path like:

```bash
/gpfs/home/UWNetID
```
it means you are accessing your home directory on the GPFS storage system, not a local disk on the login node. Files stored on GPFS are available regardless of which node your job is running on.

Key locations you will encounter include:
* `/gpfs/home/UWNetID/` — your Home directory. 10GB limit. Backed up with daily snapshots. 
* `/gpfs/projects/group-name/` — shared project or lab storage. 1TB per principal investigator. Backed up with daily snapshots. Up to 100 TB per user.
* `/gpfs/scrubbed/` — large, temporary scratch storage for active computation. Data stored in scrubbed locations is not backed up and will be automatically removed after 60 days of inactivity, so it should only be used for intermediate or reproducible data. 
* `/gpfs/software/` — centrally managed software and shared tools
* `/gpfs/datasets/` — curated shared [**common datasets**](https://hyak.uw.edu/docs/data-commons/requirements) available to all users

![Diagrammatic representation of the Tillicum filesystem directory tree. The directory tree shows the root directory at the top which holds all subdirectories. The picture is a truncated view of the filesystem showing the root directory and a few directories within it, including GPFS and a few directories within GPFS/: home/ where the Home directories are, software/ where we keep software, datasets/ where common datasets are stored, scrubbed/ where users can utilize temporary storage, and projects/ where the lab groups their dedicated storage.](./img/filesystem_tillicum.jpg 'filesystem')

*Simplified view of the Tillicum filesystem hierarchy. The root directory (`/`) contains all subdirectories. This diagram highlights `/gpfs` and commonly used paths within it, including user home directories (`/gpfs/home`), shared software (`/gpfs/software`), curated [**common datasets**](https://hyak.uw.edu/docs/data-commons/requirements) (`/gpfs/datasets`), temporary scratch storage (`/gpfs/scrubbed`), and project or lab storage (`/gpfs/projects`).*

Continue to **[03-user-tools.md](./03-user-tools.md)** to learn about the resources you can access.