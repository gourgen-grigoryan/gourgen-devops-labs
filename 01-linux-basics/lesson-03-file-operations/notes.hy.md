# Դաս 03 — File Operations

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-file%20operations-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը ծածկում է Linux-ի basic file և directory operations-ը։

Այս commands-ը DevOps-ում օգտագործվում են ամեն օր՝ project folders ստեղծելու, configuration files խմբագրելու, backups copy անելու, files տեղափոխելու, logs կարդալու և ավելորդ files անվտանգ ջնջելու համար։

---

## Learning Objectives

Այս դասը ավարտելուց հետո ես սովորեցի՝

* ստեղծել files
* ստեղծել directories
* ստեղծել nested directories
* copy անել files
* copy անել directories recursively
* move անել files
* rename անել files
* remove անել files
* remove անել empty directories
* գրել text files-ի մեջ
* append անել text files-ի վերջում
* inspect անել file content
* զգույշ օգտագործել delete commands

---

## Commands Learned

| Command | Purpose | Example |
| ------- | ------- | ------- |
| `touch` | Creates an empty file | `touch app.log` |
| `mkdir` | Creates a directory | `mkdir logs` |
| `mkdir -p` | Creates parent directories if needed | `mkdir -p backups/2026/june` |
| `cp` | Copies files | `cp app.log app-copy.log` |
| `cp -r` | Copies directories recursively | `cp -r logs logs-backup` |
| `mv` | Moves or renames files/directories | `mv app.conf application.conf` |
| `rm` | Removes files | `rm app.log` |
| `rmdir` | Removes empty directories | `rmdir empty-folder` |
| `cat` | Prints file content | `cat app.log` |
| `echo "text" > file` | Writes and overwrites content | `echo "Hello" > notes.txt` |
| `echo "text" >> file` | Appends text to a file | `echo "Line 2" >> notes.txt` |

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

Inspect final structure:

```bash
tree -a --charset=ascii
```

---

## Important Concepts

### Copy vs Move

`cp` command-ը ստեղծում է file-ի կամ directory-ի copy։

Original file-ը մնում է իր տեղում։

```bash
cp logs/app.log backups/app-backup.log
```

`mv` command-ը move կամ rename է անում file/directory-ն։

```bash
mv configs/app.conf configs/application.conf
```

---

### `>` vs `>>`

`>` operator-ը գրում է text file-ի մեջ և overwrite է անում existing content-ը։

```bash
echo "Line 1" > notes.txt
```

`>>` operator-ը ավելացնում է text-ը file-ի վերջում։

```bash
echo "Line 2" >> notes.txt
```

Սա կարևոր է, որովհետև սխալմամբ `>` օգտագործելը կարող է ջնջել հին content-ը։

---

### `rm` vs `rmdir`

`rm` command-ը ջնջում է files։

```bash
rm app.log
```

`rmdir` command-ը ջնջում է միայն empty directories։

```bash
rmdir empty-folder
```

Non-empty directory ջնջելու համար օգտագործվում է `rm -r` կամ `rm -rf`, բայց դրանք պետք է օգտագործել շատ զգույշ։

---

## Safety Rule

Delete commands-ը պետք է օգտագործել զգուշությամբ։

Մինչև այսպիսի command-ներ run անելը՝

```bash
rm file
rm -r folder
rm -rf folder
```

պետք է ստուգել current location-ը՝

```bash
pwd
```

և inspect անել files/folders-ը՝

```bash
ls
tree -a --charset=ascii
```

---

## Why `rm -rf` Is Dangerous

```bash
rm -rf folder
```

կարող է ջնջել directory-ն և ամբողջ content-ը առանց հարցնելու։

DevOps-ում սա վտանգավոր է, որովհետև սխալ տեղում run անելու դեպքում կարող է ջնջել project files, configs կամ production data։

---

## Common Mistakes

| Mistake | Problem | Correct Practice |
| ------- | ------- | ---------------- |
| `>` օգտագործել append-ի փոխարեն | Existing content-ը ջնջվում է | Append-ի համար օգտագործել `>>` |
| `rm -rf` run անել առանց ստուգելու | Կարող է ջնջել սխալ folder | Նախ `pwd`, `ls`, `tree` |
| `rmdir` օգտագործել non-empty folder-ի համար | Command-ը fail է անում | Պետք է հասկանալ folder content-ը |
| `cp` և `mv` շփոթել | Կարող է file-ը տեղափոխվել copy-ի փոխարեն | `cp` copies, `mv` moves/renames |

---

## File Operations Quick Reference

| Action | Command |
| ------ | ------- |
| Create empty file | `touch file.txt` |
| Create directory | `mkdir logs` |
| Create nested directories | `mkdir -p backups/2026/june` |
| Copy file | `cp source destination` |
| Copy directory | `cp -r source destination` |
| Move/Rename | `mv old new` |
| Remove file | `rm file` |
| Remove empty directory | `rmdir folder` |
| Write content | `echo "text" > file` |
| Append content | `echo "text" >> file` |

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

Expected result՝

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

## Troubleshooting Notes

Եթե file-ը չի գտնվում՝

```bash
pwd
ls
tree -a --charset=ascii
```

Եթե append-ի փոխարեն overwrite ես արել, ստուգել Git diff-ը՝

```bash
git diff
```

Եթե directory-ն չի ջնջվում `rmdir`-ով, նշանակում է այն դատարկ չէ։

---

## Git Workflow

After completing the lab, I saved the work using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-03-file-operations
git commit -m "Add Linux file operations notes"
git push
```

---

## What I Learned

Այս դասում ես սովորեցի Linux-ում files և directories կառավարել command-line tools-ով։

Ես նաև սովորեցի, որ current location-ը ստուգելը շատ կարևոր սովորություն է, հատկապես create, move, rename կամ delete commands-ից առաջ։

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
