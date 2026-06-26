# Lesson 03 — File Operations

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-file%20operations-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers basic Linux file and directory operations.

These commands are used daily in DevOps work when creating project folders, editing configuration files, copying backups, moving files, reading logs and safely removing unnecessary files.

---

## Learning Objectives

By completing this lesson, I learned how to:

* create files
* create directories
* create nested directories
* copy files
* copy directories recursively
* move files
* rename files
* remove files
* remove empty directories
* write text into files
* append text to files
* inspect file contents safely
* use delete commands carefully

---

## Commands Learned

| Command               | Purpose                                     | Example                        |
| --------------------- | ------------------------------------------- | ------------------------------ |
| `touch`               | Creates an empty file                       | `touch app.log`                |
| `mkdir`               | Creates a directory                         | `mkdir logs`                   |
| `mkdir -p`            | Creates parent directories if needed        | `mkdir -p backups/2026/june`   |
| `cp`                  | Copies files                                | `cp app.log app-copy.log`      |
| `cp -r`               | Copies directories recursively              | `cp -r logs logs-backup`       |
| `mv`                  | Moves or renames files/directories          | `mv app.conf application.conf` |
| `rm`                  | Removes files                               | `rm app.log`                   |
| `rmdir`               | Removes empty directories                   | `rmdir empty-folder`           |
| `cat`                 | Prints file content                         | `cat app.log`                  |
| `echo "text" > file`  | Writes text and overwrites existing content | `echo "Hello" > notes.txt`     |
| `echo "text" >> file` | Appends text to the end of a file           | `echo "Line 2" >> notes.txt`   |

---

## Lab Structure

In this lab, I created the following structure:

```text
lesson-03-file-operations/
|-- backups
|   `-- app-backup.log
|-- configs
|   `-- application.conf
|-- logs
|   |-- app.log
|   `-- error.log
`-- notes.md
```

---

## Practical Commands Used

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-03-file-operations
cd lesson-03-file-operations
```

Create directories and files:

```bash
mkdir logs backups configs
touch logs/app.log logs/error.log configs/app.conf
```

Write content into files:

```bash
echo "Application started successfully" > logs/app.log
echo "No errors found" > logs/error.log
echo "APP_ENV=development" > configs/app.conf
```

Read file contents:

```bash
cat logs/app.log
cat logs/error.log
cat configs/app.conf
```

Copy a log file into the backup directory:

```bash
cp logs/app.log backups/app-backup.log
```

Rename a configuration file:

```bash
mv configs/app.conf configs/application.conf
```

Inspect the final structure:

```bash
tree -a --charset=ascii
```

---

## Important Concepts

### Copy vs Move

`cp` creates a copy of a file or directory.

The original file remains in its original location.

```bash
cp logs/app.log backups/app-backup.log
```

`mv` moves or renames a file or directory.

The original path no longer keeps the same file under the old name.

```bash
mv configs/app.conf configs/application.conf
```

---

### `>` vs `>>`

The `>` operator writes text to a file and overwrites existing content.

```bash
echo "Line 1" > notes.txt
```

The `>>` operator appends text to the end of a file.

```bash
echo "Line 2" >> notes.txt
```

This is important because using `>` by mistake can erase previous file content.

---

### `rm` vs `rmdir`

`rm` removes files.

```bash
rm app.log
```

`rmdir` removes only empty directories.

```bash
rmdir empty-folder
```

To remove non-empty directories, `rm -r` or `rm -rf` can be used, but these commands must be handled carefully.

---

## Safety Rule

Delete commands must be used carefully.

Before running commands such as:

```bash
rm file
rm -r folder
rm -rf folder
```

I should always check my current location:

```bash
pwd
```

Then inspect the files or folders:

```bash
ls
tree -a --charset=ascii
```

Only after confirming the correct location and target should I run delete commands.

---

## Why `rm -rf` Is Dangerous

The command:

```bash
rm -rf folder
```

can remove a directory and all of its contents without asking for confirmation.

This is dangerous in DevOps because running it in the wrong location can delete important project files, configuration files or production data.

---

## Validation

Commands used to validate this lab:

```bash
pwd
tree -a --charset=ascii
cat logs/app.log
cat logs/error.log
cat backups/app-backup.log
cat configs/application.conf
```

Expected result:

* `logs/app.log` exists
* `logs/error.log` exists
* `backups/app-backup.log` exists
* `configs/application.conf` exists
* `configs/app.conf` no longer exists because it was renamed
* all content can be viewed using `cat`

---

## Quiz Review

### 1. What does `touch` do?

The `touch` command creates an empty file.

Example:

```bash
touch app.log
```

This creates a file named `app.log` if it does not already exist.

---

### 2. What does `mkdir -p` do?

The command `mkdir -p` creates a directory and also creates parent directories if they do not already exist.

Example:

```bash
mkdir -p backups/2026/june
```

This is useful when creating nested directory structures.

---

### 3. What is the difference between `cp` and `mv`?

`cp` copies a file or directory.

The original file stays in its original location.

```bash
cp logs/app.log backups/app-backup.log
```

`mv` moves or renames a file or directory.

The original file no longer remains under the old path or old name.

```bash
mv configs/app.conf configs/application.conf
```

---

### 4. What is the difference between `>` and `>>`?

The `>` operator writes text to a file and overwrites existing content.

```bash
echo "Line 1" > notes.txt
```

The `>>` operator appends text to the end of a file without removing existing content.

```bash
echo "Line 2" >> notes.txt
```

This is important because using `>` by mistake can delete previous file content.

---

### 5. Why should delete commands be used carefully?

Delete commands such as `rm`, `rm -r` and especially `rm -rf` can permanently remove files or directories.

Before running delete commands, I should always check my current location:

```bash
pwd
```

Then inspect the files or folders:

```bash
ls
tree -a --charset=ascii
```

This helps prevent deleting the wrong files or directories.

---

### 6. Why is `rm -rf` dangerous?

The command:

```bash
rm -rf folder
```

removes a directory and all of its contents without asking for confirmation.

It is dangerous because running it in the wrong location can delete important project files, configuration files or production data.

---

### Quiz Result

```text
touch usage: Passed
mkdir -p usage: Passed
cp vs mv: Passed
> vs >>: Passed
delete safety: Passed
rm -rf danger: Passed
```

Lesson quiz passed successfully.

---

## Git Workflow

After completing the lab, I saved the work using Git:

```bash
cd ~/devops-labs
git status
git add .
git commit -m "Add Linux file operations notes"
git push
```

After improving the lesson documentation, I saved the updated notes using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-03-file-operations/notes.md
git commit -m "Add file operations quiz review"
git push
```

---

## What I Learned

In this lesson, I learned how to manage files and directories in Linux using common command-line tools.

I also learned the importance of checking my current location before running commands that create, move, rename or delete files.

This is an important DevOps habit because many production mistakes happen when commands are executed in the wrong directory.

---

## Status

Lesson completed, committed and pushed to GitHub.
