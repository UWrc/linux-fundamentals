# Prerequisites

Before starting this tutorial, you should have the following in place:

* A UW NetID  
* An active Hyak account (Klone or Tillicum)  
* Two-factor authentication (2FA) enabled  
* Access to an SSH client on your local computer  

If you do not yet have a Hyak account, you can request access for training purposes by completing  
[**this form for a Klone demonstration account**](https://uwconnect.uw.edu/sp?id=sc_cat_item&sys_id=f5caba8fdbe108101ba12968489619e0).

Students should apply for a `stf` account (**Student Technology Fee**) which are managed by the [**Research Computing Club**](https://depts.washington.edu/uwrcc/). Students can use STF-funded CPU and GPU resources with priority, on-demand (queue times vary). [**Apply now for your `stf` account**](https://depts.washington.edu/uwrcc/hyak_access/). 

## Two-Factor Authentication (2FA)

UW policy requires **two-factor authentication (2FA)** for all UWIT services, including Hyak. You must have 2FA enabled and configured before you can log in to any Research Computing cluster.

Please visit the UW 2FA page to confirm your setup:

[**UW Two-Factor Authentication**](https://identity.uw.edu/2fa/)

## SSH Clients

You will access Hyak primarily using **Secure Shell (SSH)**, a command-line tool that allows you to connect securely to remote systems.

Most users already have an SSH client available:

**MacOS and Linux**  
SSH is included by default. You can open the **Terminal** application and use the `ssh` command directly.

**Windows**  
Recent versions of Windows include native SSH support via:
* **Command Prompt**
* **HIGHLY RECOMMENDED - Windows PowerShell**
* **Windows Subsystem for Linux (WSL)** 

Alternative SSH clients commonly used on Windows include:
* [**PuTTY**](https://www.putty.org/)
* [**Git Bash**](https://carpentries.github.io/workshop-template/install_instructions/#shell) (includes a Bash shell and SSH)

You only need **one** SSH client installed to complete this tutorial.

## What’s Next

Once your account is active, 2FA is configured, and you have an SSH client available, you’re ready to log in to Klone and begin working through the tutorial.

Continue to **[01-logging-in.md](./01-logging-in.md)** to get started.
