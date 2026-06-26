# Lesson 01 — Linux File System

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-linux%20filesystem-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers the basic structure of the Linux file system and explains the most important paths used in daily DevOps work.

Understanding the Linux file system is important because most production servers, logs, configuration files, applications and services are managed through Linux directories.

---

## Learning Objectives

By completing this lesson, I learned:

* what the Linux root directory `/` means
* where my Linux user home directory is located
* how `~` works as a shortcut
* how Windows files are mounted inside WSL
* where Linux configuration files are usually stored
* where Linux log files are usually stored
* why DevOps projects should be kept inside the Linux file system

---

## Key Linux Paths

| Path            | Meaning                                    | DevOps Usage                                 |
| --------------- | ------------------------------------------ | -------------------------------------------- |
| `/`             | Root of the Linux file system              | Starting point of all Linux directories      |
| `/home/phantom` | My Linux user home directory               | Personal files, labs and projects            |
| `~`             | Shortcut for `/home/phantom`               | Quick navigation to my home directory        |
| `/mnt/c`        | Windows C drive mounted inside Linux       | Accessing Windows files from WSL             |
| `/etc`          | System and application configuration files | Nginx, SSH, systemd and other configs        |
| `/var/log`      | Log files                                  | Troubleshooting services and applications    |
| `/tmp`          | Temporary files                            | Short-term files, not for important projects |

---

## Path Examples

```bash
cd /
pwd
```

Shows the Linux root directory.

```bash
cd ~
pwd
```

Goes to my Linux home directory.

```bash
cd ~/devops-labs
pwd
```

Goes to my DevOps learning workspace.

```bash
ls /etc
```

Lists system configuration files and directories.

```bash
ls /var/log
```

Lists system log files.

```bash
ls /mnt/c
```

Lists the Windows C drive from inside WSL.

---

## Important Concepts

### Root Directory

The root directory is:

```text
/
```

It is the starting point of the entire Linux file system.

### Home Directory

My Linux home directory is:

```text
/home/phantom
```

This is where I keep my personal files, labs and DevOps projects.

### Home Shortcut

The `~` symbol is a shortcut for my home directory:

```text
~ = /home/phantom
```

### Windows Drive in WSL

The Windows C drive is available inside Linux at:

```text
/mnt/c
```

This is useful for accessing Windows files, but my DevOps projects should stay inside the Linux file system.

---

## Important DevOps Rule

I should keep my DevOps projects inside the Linux file system, for example:

```text
~/devops-labs
```

I should avoid keeping active Linux/DevOps projects inside:

```text
/mnt/c/Users/...
```

because Linux tools, Git, permissions, scripts and future Docker workflows work better inside the Linux file system.

---

## Validation

Commands used to validate this lesson:

```bash
pwd
ls /
ls /etc | head
ls /var/log | head
ls /mnt/c
```

Expected result:

* `/` shows the main Linux system directories
* `/home/phantom` is my user home directory
* `/etc` contains configuration-related files
* `/var/log` contains log files
* `/mnt/c` gives access to the Windows C drive

---

## Quiz Review

| Question | Correct Answer | Status |
| --- | --- | --- |
| What does `/` mean in Linux? | `/` is the root of the Linux file system. | Passed |
| What is `/home/phantom`? | It is my Linux user home directory. | Passed |
| What does `~` mean? | `~` is a shortcut for `/home/phantom`. | Passed |
| What is `/mnt/c` used for in WSL? | It gives access to the Windows C drive from inside Linux. | Passed |
| Where are configuration files usually stored? | Configuration files are commonly stored under `/etc`. | Passed |
| Where are log files usually stored? | Log files are commonly stored under `/var/log`. | Passed |
| Where should I keep DevOps projects in WSL? | Inside the Linux file system, for example `~/devops-labs`. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## What I Learned

In this lesson, I learned that Linux uses one main file system tree starting from `/`.

I also learned that `/home/phantom` is my user workspace, while `/mnt/c` is only a mounted Windows drive.

For DevOps work, I should always know where I am in the file system before creating, editing or deleting files.

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
