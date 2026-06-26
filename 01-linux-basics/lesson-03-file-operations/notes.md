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

| Question | Correct Answer | Status |
| --- | --- | --- |
| What does `touch` do? | It creates an empty file. | Passed |
| What does `mkdir` do? | It creates a directory. | Passed |
| What does `mkdir -p` do? | It creates parent directories if needed. | Passed |
| What is the difference between `cp` and `mv`? | `cp` copies files, while `mv` moves or renames them. | Passed |
| What is the difference between `>` and `>>`? | `>` overwrites file content, while `>>` appends to the file. | Passed |
| What does `rmdir` remove? | It removes empty directories only. | Passed |
| Why is `rm -rf` dangerous? | It can delete directories and their contents without confirmation. | Passed |
| What should I check before delete commands? | I should check `pwd`, `ls` and `tree` before deleting files. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
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

Lesson completed, quiz passed, committed and pushed to GitHub.
