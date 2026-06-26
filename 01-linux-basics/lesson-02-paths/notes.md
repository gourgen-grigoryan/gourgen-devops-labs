# Lesson 02 — Linux Paths

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-linux%20paths-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson explains how paths work in Linux.

Understanding paths is important in DevOps because almost every command depends on the current location in the file system. A wrong path can lead to editing the wrong file, running commands in the wrong project, or deleting the wrong directory.

---

## Learning Objectives

By completing this lesson, I learned:

* what an absolute path is
* what a relative path is
* how to use `.`
* how to use `..`
* how to use `~`
* why I should check my current location with `pwd`
* how to move safely between directories

---

## Path Types

| Type              | Meaning                               | Example                     |
| ----------------- | ------------------------------------- | --------------------------- |
| Absolute path     | Full path starting from `/`           | `/home/phantom/devops-labs` |
| Relative path     | Path based on the current directory   | `cd 01-linux-basics`        |
| Current directory | The directory I am currently inside   | `.`                         |
| Parent directory  | One level above the current directory | `..`                        |
| Home shortcut     | Shortcut to my user home directory    | `~`                         |

---

## Absolute Path

An absolute path always starts from:

```text
/
```

Example:

```text
/home/phantom/devops-labs
```

This path works from anywhere because it describes the full location from the root of the Linux file system.

Example command:

```bash
cd /home/phantom/devops-labs
```

This command always goes to the DevOps workspace, no matter where I currently am.

---

## Relative Path

A relative path does not start with `/`.

It starts from the current directory.

Example:

```bash
cd 01-linux-basics
```

This works only if I am currently inside:

```text
/home/phantom/devops-labs
```

If I am in a different location, the same command may fail or go to a different place.

---

## Special Path Symbols

| Symbol  | Meaning           | Example    |
| ------- | ----------------- | ---------- |
| `.`     | Current directory | `ls .`     |
| `..`    | Parent directory  | `cd ..`    |
| `../..` | Two levels up     | `cd ../..` |
| `~`     | My home directory | `cd ~`     |

---

## Practical Examples

Show the current directory:

```bash
pwd
```

List the current directory:

```bash
ls .
```

Go one level up:

```bash
cd ..
pwd
```

Go to the home directory:

```bash
cd ~
pwd
```

Go to the DevOps workspace using an absolute path:

```bash
cd /home/phantom/devops-labs
pwd
```

Go to the Linux basics folder using a relative path:

```bash
cd 01-linux-basics
pwd
```

---

## Why Paths Matter in DevOps

In DevOps, path mistakes can be dangerous.

For example, before editing a configuration file, deleting files, running scripts or committing changes, I should always confirm where I am.

Important habit:

```bash
pwd
```

Then inspect the current directory:

```bash
ls
```

or:

```bash
tree -a -I .git -L 3 --charset=ascii
```

Only after that should I run important commands.

---

## Safety Rule

Before running commands that create, edit, move or delete files, I should always check my current location with:

```bash
pwd
```

This helps prevent mistakes such as:

* editing the wrong file
* deleting the wrong folder
* committing changes from the wrong directory
* running a script from the wrong location

---

## Validation

Commands used to validate this lesson:

```bash
cd ~/devops-labs/01-linux-basics
pwd
mkdir -p lesson-02-paths
cd lesson-02-paths
pwd
ls .
cd ..
pwd
cd lesson-02-paths
pwd
```

Expected result:

* `pwd` shows the correct current directory
* `.` represents the current directory
* `..` moves one level up
* `~` returns to `/home/phantom`
* absolute paths work from anywhere
* relative paths depend on the current location

---

## Quiz Review

| Question | Correct Answer | Status |
| --- | --- | --- |
| What is an absolute path? | A full path that starts from `/`. | Passed |
| What is a relative path? | A path that starts from the current directory. | Passed |
| What does `.` mean? | `.` means the current directory. | Passed |
| What does `..` mean? | `..` means the parent directory. | Passed |
| What does `~` mean? | `~` means my home directory, `/home/phantom`. | Passed |
| Why should I run `pwd` before important commands? | To confirm my current location and avoid working in the wrong directory. | Passed |
| Why do paths matter in DevOps? | Many commands create, edit, move or delete files based on the current path. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## What I Learned

In this lesson, I learned that Linux paths are extremely important for safe command-line work.

I learned that absolute paths start from `/`, while relative paths depend on where I currently am.

I also learned that `.`, `..` and `~` are important shortcuts that make navigation faster and safer.

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
