# Logging In to Hyak

This section walks you through logging in to Hyak using the command line and introduces the **shell**, which is your primary interface for working on the cluster.

Hyak has multiple systems, and the login process differs slightly between **Klone** and **Tillicum**. This tutorial is focused on **Klone**, with Tillicum-specific notes included where relevant.

If you have not yet set up your account, 2FA, or an SSH client, please review the  
[**Prerequisites section**](./00-prereqs.md) before continuing.

## Logging in to Klone

Once you have a terminal (shell) open on your local machine, log in to Klone by running the following command. Replace `UWNetID` with your UW NetID.

```bash
ssh UWNetID@klone.hyak.uw.edu
```

You will be prompted for your UW NetID password (*Note: your Hyak password is the same password for all your UW Services*), followed by your Duo two-factor authentication method:
```bash
Password: ***********
Duo two-factor login for UWNetID

Enter a passcode or select one of the following options:

1. Duo Push to XXX-XXX-XXXX
2. Phone call to XXX-XXX-XXXX

Passcode or option (1-2): 1
Success. Logging you in...
```

If login is successful, you will see a welcome banner similar to the following:
```bash
     _    _                    _                 _
    | | _| | ___  _ __   ___  | |__  _   _  __ _| | __
    | |/ / |/ _ \| '_ \ / _ \ | '_ \| | | |/ _` | |/ /
    |   <| | (_) | | | |  __/ | | | | |_| | (_| |   <
    |_|\_\_|\___/|_| |_|\___| |_| |_|\__, |\__,_|_|\_\
                                     |___/
```

Too many incorrect login attempts may result in a temporary IP ban lasting up to an hour.

## Logging in to Tillicum (for comparison)
Tillicum uses a different hostname but the same login workflow. To connect, run:
```bash
ssh UWNetID@tillicum.hyak.uw.edu
```
After entering your password and Duo authentication, you will see a Tillicum-specific welcome banner reminding you that login nodes are for preparing work, not running compute-intensive jobs.

You do not need Tillicum access to complete this tutorial, but many of the concepts you learn here apply directly to both systems.

---

> ### Common Login Issues
>
> If you’re having trouble logging in to Hyak, the issues below account for most problems we see.
> 
> **1. Lost or Expired Access**
> 
> If your login attempt fails even though your password and 2FA are correct, your Hyak access may have expired or been removed.
> 
> * Contact **UWIT Research Computing** or your **Hyak account administrator** for your research group to confirm your access.
> * Students using shared or instructional allocations (such as STF) may need to [**reapply for access**](https://depts.washington.edu/uwrcc/hyak_access/).
>   * In many cases, STF access does not automatically renew between quarters.
>
> **2. Incorrect Username or Password**
> 
> Be sure that:
> 
> * You are using your **UW NetID** (not an email address)
> * Your password is typed correctly (passwords are not shown as you type)
> 
> ***Too many incorrect login attempts may result in a temporary IP ban lasting up to an hour.***
>
> If you believe you may have triggered a temporary ban, wait and try again later.
> 
> **3. Network Issues (On Campus)**
>
> If you are connecting from campus, make sure you are using the [**`eduroam`**](https://uwconnect.uw.edu/it?id=kb_article_view&sysparm_article=KB0034255#howtouse) wireless network.
>
> * The **“University of Washington”** network is known to be less stable for SSH connections
> * Switching to **eduroam** often resolves intermittent login failures
>
> **4. Internet Connectivity Problems**
>
> Unstable internet connections—both on campus and off campus—can interfere with SSH logins.
>
> If login fails unexpectedly:
> * Check your internet connection
> * Wait a few minutes and try again
> * Try reconnecting from a different network if possible
> 
> **Still Having Trouble?**
> 
> If your login issues persist after checking the items above, please contact UW support:
> 
> **Email:** help@uw.edu  
> **Subject line:** "Hyak login issue"
> Including “Hyak” in the subject line helps route your request to the appropriate support team.

---

## What Is a Shell?

The **shell** is a program that allows you to interact with a computer by typing commands. On Hyak, the shell is your primary way of navigating the filesystem, launching programs, and preparing work to run on compute nodes.

When you use `ssh` to log in to Klone or Tillicum, you are connected to a shell called Bash (the <ins>**B**</ins>ourne <ins>**A**</ins>gain <ins>**SH**</ins>ell). If you successfully logged in and see text waiting for input, you are looking at a shell.

***Think of the shell as your view into the cluster.***

## The Command Prompt

When you first log in, you’ll see a prompt that looks something like this:
```bash
[UWNetID@klone-login01 ~]$
```
Here’s what each part means:

* **UWNetID** — your username on Hyak
* **klone-login01** (or similar) — the login node you are connected to Login nodes are the “front door” of the cluster. All users start here.
* **~** — shorthand for your home directory, your default starting location
* **$** — indicates the shell is ready for a command

In Linux, the term **directory** is used instead of folder. While graphical interfaces often use “folder,” “directory” is the correct term in the command-line environment.

We will discuss the filesystem, directories, and storage locations in more detail in the next section.

> ### A Note on Login Nodes
>
>Login nodes are shared by all users and are intended for:
>
> * Editing files
> * Navigating directories
> * Transferring data
> * Submitting jobs to the scheduler
>
> ***Compute- or memory-intensive work should not be run on login nodes.*** **Arbiter** is the tool which automates login node monitoring and enforces usage limits to ensure stability and ensure fair access.
>
> **Arbiter monitors resource usage on login nodes and will:**
> * Slow or halt processes that exceed permitted thresholds.
> * Terminate processes outright if necessary.
> 
> You will learn how to request compute resources later in this tutorial.

---

## Practice (Optional)

Once logged in, try running the following commands. We’ll explain each of these in more detail later in the tutorial.

### 1. Check your current location

```bash
pwd
```

### 2. List files in your home directory

```bash
ls -l
```

This shows files and directories along with details such as size and permissions.

### 3. Confirm which node you’re on

```bash
hostname
```

This prints the name of the login node you’re connected to (for example, `klone-login01`).

Continue to **[02-filesystem.md](./02-filesystem.md)** to learn about the file system on Klone.
