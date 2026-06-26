# Lesson 06 — Permissions and Ownership

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-permissions%20and%20ownership-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers basic Linux file permissions and ownership concepts used in daily DevOps work.

Permissions are important because Linux systems protect files and directories using access rules. A DevOps Engineer must understand who can read, write or execute files, how to make scripts executable, how to protect secret files and how to troubleshoot permission-related errors.

In this lesson, I practiced using `chmod`, `chown`, permission numbers, executable scripts and safe permissions for scripts, configuration files, logs and secrets.

---

## Learning Objectives

By completing this lesson, I learned how to:

* read Linux permissions using `ls -l`
* understand `r`, `w` and `x`
* understand owner, group and others
* use numeric permissions such as `755`, `644` and `600`
* make a script executable using `chmod`
* set safe permissions for configuration files
* protect secret files with restricted permissions
* understand file ownership
* use `chown` to change owner and group
* validate permissions using `stat`
* troubleshoot common permission errors

---

## Permission Basics

Linux permissions are usually shown with `ls -l`.

Example:

```bash
ls -l
```

Example output:

```text
-rwxr-xr-x 1 phantom phantom 120 Jun 26 deploy.sh
-rw-r--r-- 1 phantom phantom 80 Jun 26 app.conf
```

The first part shows the file type and permissions:

```text
-rwxr-xr-x
```

This can be divided into sections:

```text
-   rwx   r-x   r-x
|    |     |     |
|    |     |     others
|    |     group
|    owner
file type
```

---

## Permission Symbols

| Symbol | Meaning       |
| ------ | ------------- |
| `r`    | read          |
| `w`    | write         |
| `x`    | execute       |
| `-`    | no permission |

Example:

```text
-rw-r--r--
```

This means:

| User Type | Permission     |
| --------- | -------------- |
| Owner     | read and write |
| Group     | read only      |
| Others    | read only      |

---

## Numeric Permissions

Linux permissions can also be written as numbers.

| Number | Permission |
| ------ | ---------- |
| `4`    | read       |
| `2`    | write      |
| `1`    | execute    |

These numbers are added together.

| Number | Meaning                 |
| ------ | ----------------------- |
| `7`    | read, write and execute |
| `6`    | read and write          |
| `5`    | read and execute        |
| `4`    | read only               |
| `0`    | no permissions          |

---

## Common Permission Values

| Permission | Meaning                                               | Common Use                     |
| ---------- | ----------------------------------------------------- | ------------------------------ |
| `755`      | Owner can read/write/execute, others can read/execute | Scripts and directories        |
| `644`      | Owner can read/write, others can read                 | Config files and regular files |
| `600`      | Only owner can read/write                             | Secrets and private files      |
| `700`      | Only owner has full access                            | Private directories or scripts |

---

## Commands Learned

| Command                         | Purpose                                 | Example                                      |
| ------------------------------- | --------------------------------------- | -------------------------------------------- |
| `ls -l`                         | Shows file permissions and ownership    | `ls -l`                                      |
| `chmod +x file`                 | Adds execute permission                 | `chmod +x scripts/deploy.sh`                 |
| `chmod 755 file`                | Sets executable script permissions      | `chmod 755 scripts/deploy.sh`                |
| `chmod 644 file`                | Sets standard readable file permissions | `chmod 644 configs/app.conf`                 |
| `chmod 600 file`                | Restricts file to owner only            | `chmod 600 secrets/.env`                     |
| `chown user file`               | Changes file owner                      | `sudo chown phantom file`                    |
| `chown user:group file`         | Changes owner and group                 | `sudo chown phantom:phantom file`            |
| `stat -c "%A %a %U:%G %n" file` | Shows detailed permission info          | `stat -c "%A %a %U:%G %n" scripts/deploy.sh` |

---

## Lab Structure

In this lab, I created the following structure:

```text
lesson-06-permissions-ownership/
|-- configs
|   `-- app.conf
|-- logs
|   `-- app.log
|-- notes.md
|-- scripts
|   `-- deploy.sh
`-- secrets
    `-- .env
```

---

## Practical Commands Used

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-06-permissions-ownership
cd lesson-06-permissions-ownership
```

Create lab directories and files:

```bash
mkdir scripts configs logs secrets
touch configs/app.conf logs/app.log secrets/.env
```

Create a deployment script:

```bash
cat > scripts/deploy.sh <<'EOF'
#!/bin/bash

echo "Starting deployment..."
echo "Checking application files..."
echo "Deployment completed successfully."
EOF
```

Try to run the script before adding execute permission:

```bash
./scripts/deploy.sh
```

Expected problem:

```text
Permission denied
```

Make the script executable:

```bash
chmod 755 scripts/deploy.sh
```

Run the script again:

```bash
./scripts/deploy.sh
```

Expected result:

```text
Starting deployment...
Checking application files...
Deployment completed successfully.
```

Create a config file:

```bash
cat > configs/app.conf <<'EOF'
APP_NAME=devops-lab
APP_ENV=development
APP_PORT=3000
LOG_FILE=logs/app.log
EOF
```

Set safe config permissions:

```bash
chmod 644 configs/app.conf
```

Create a secret file:

```bash
cat > secrets/.env <<'EOF'
DB_USER=admin
DB_PASSWORD=super-secret-password
API_KEY=devops-demo-key
EOF
```

Protect the secret file:

```bash
chmod 600 secrets/.env
```

Create a log file:

```bash
echo "INFO Application started" > logs/app.log
echo "ERROR Example permission issue" >> logs/app.log
```

Set log file permissions:

```bash
chmod 644 logs/app.log
```

Validate permissions:

```bash
stat -c "%A %a %U:%G %n" scripts/deploy.sh configs/app.conf logs/app.log secrets/.env
```

---

## Expected Permission Results

Expected result:

```text
-rwxr-xr-x 755 phantom:phantom scripts/deploy.sh
-rw-r--r-- 644 phantom:phantom configs/app.conf
-rw-r--r-- 644 phantom:phantom logs/app.log
-rw------- 600 phantom:phantom secrets/.env
```

The username and group may be different depending on the Linux user.

Important permissions:

| File                | Expected Permission |
| ------------------- | ------------------- |
| `scripts/deploy.sh` | `755`               |
| `configs/app.conf`  | `644`               |
| `logs/app.log`      | `644`               |
| `secrets/.env`      | `600`               |

---

## `chmod` Examples

Make a script executable:

```bash
chmod +x scripts/deploy.sh
```

Set script permissions:

```bash
chmod 755 scripts/deploy.sh
```

Set regular config file permissions:

```bash
chmod 644 configs/app.conf
```

Set private secret file permissions:

```bash
chmod 600 secrets/.env
```

Set private directory permissions:

```bash
chmod 700 secrets
```

---

## `chown` Examples

Check current owner and group:

```bash
ls -l
```

Change file owner:

```bash
sudo chown $USER configs/app.conf
```

Change owner and group:

```bash
sudo chown $USER:$USER configs/app.conf
```

Change ownership recursively:

```bash
sudo chown -R $USER:$USER lesson-06-permissions-ownership
```

Important note: recursive ownership changes should be used carefully, especially on system directories.

---

## Why Permissions Matter in DevOps

Permissions help answer important troubleshooting questions:

* Why can I not execute this script?
* Why does the application say `Permission denied`?
* Can the application read its configuration file?
* Can the application write to its log file?
* Is a secret file too open?
* Who owns this file?
* Does the service user have access to this directory?

In real DevOps work, permissions are commonly used when working with:

* deployment scripts
* configuration files
* log files
* SSH private keys
* environment files
* web server directories
* application directories
* CI/CD runners
* Linux services

---

## Important Safety Notes

Secret files should not be readable by everyone.

Good example:

```bash
chmod 600 secrets/.env
```

Private SSH keys usually require strict permissions:

```bash
chmod 600 ~/.ssh/id_rsa
```

Scripts need execute permission before they can be run directly:

```bash
chmod 755 scripts/deploy.sh
```

Configuration files are often readable but only writable by the owner:

```bash
chmod 644 configs/app.conf
```

Avoid using very open permissions such as:

```bash
chmod 777 file
```

`777` gives everyone read, write and execute access. It is usually unsafe and should not be used unless there is a very specific reason.

---

## Common Mistakes

| Mistake                                     | Problem                      | Correct Version                                        |
| ------------------------------------------- | ---------------------------- | ------------------------------------------------------ |
| Running a script without execute permission | `Permission denied`          | `chmod 755 script.sh`                                  |
| Using `chmod 777`                           | Too open and unsafe          | Use `755`, `644` or `600`                              |
| Giving secrets `644`                        | Others can read secrets      | `chmod 600 secrets/.env`                               |
| Confusing `chmod` and `chown`               | Wrong tool for the task      | `chmod` changes permissions, `chown` changes ownership |
| Running `chown -R` on the wrong directory   | Can break system permissions | Always check `pwd` before recursive changes            |

---

## `chmod` vs `chown`

| Command | Purpose                      |
| ------- | ---------------------------- |
| `chmod` | Changes file permissions     |
| `chown` | Changes file owner and group |

Example:

```bash
chmod 755 scripts/deploy.sh
```

This changes what users can do with the file.

Example:

```bash
sudo chown $USER:$USER configs/app.conf
```

This changes who owns the file.

---

## Quiz Review

| Question                                            | Correct Answer                                                                 |
| --------------------------------------------------- | ------------------------------------------------------------------------------ |
| What does `r` permission mean?                      | `r` means read. It allows reading file content or listing directory contents.  |
| What does `w` permission mean?                      | `w` means write. It allows modifying a file or changing directory contents.    |
| What does `x` permission mean?                      | `x` means execute. It allows running a script or entering a directory.         |
| Which command makes a script executable?            | `chmod 755 scripts/deploy.sh` or `chmod +x scripts/deploy.sh`                  |
| What permission is commonly used for scripts?       | `755`                                                                          |
| What permission is correct for secret `.env` files? | `600`                                                                          |
| What is the difference between `chmod` and `chown`? | `chmod` changes permissions, while `chown` changes owner and group.            |
| What does `644` mean?                               | Owner can read/write, group can read, others can read.                         |
| What does `755` mean?                               | Owner can read/write/execute, group can read/execute, others can read/execute. |
| Why should `chmod 777` usually be avoided?          | It gives everyone read, write and execute access, which is unsafe.             |

---

## Permission Quick Reference

| Permission | Symbol Form  | Meaning                                | Common Use                           |
| ---------- | ------------ | -------------------------------------- | ------------------------------------ |
| `600`      | `-rw-------` | Only owner can read/write              | Secrets, `.env`, private keys        |
| `644`      | `-rw-r--r--` | Owner can read/write, others can read  | Config files, normal files           |
| `755`      | `-rwxr-xr-x` | Owner full access, others read/execute | Scripts, directories                 |
| `777`      | `-rwxrwxrwx` | Everyone has full access               | Usually unsafe and should be avoided |

---

## Validation

Commands used to validate this lab:

```bash
pwd
tree -a --charset=ascii
ls -l
ls -l scripts/deploy.sh
ls -l configs/app.conf
ls -l logs/app.log
ls -l secrets/.env
./scripts/deploy.sh
stat -c "%A %a %U:%G %n" scripts/deploy.sh configs/app.conf logs/app.log secrets/.env
```

Expected result:

* `scripts/deploy.sh` exists
* `configs/app.conf` exists
* `logs/app.log` exists
* `secrets/.env` exists
* `scripts/deploy.sh` has `755` permissions
* `configs/app.conf` has `644` permissions
* `logs/app.log` has `644` permissions
* `secrets/.env` has `600` permissions
* `./scripts/deploy.sh` runs successfully
* `stat` shows expected permission values

---

## Troubleshooting Notes

If a script does not run and shows:

```text
Permission denied
```

I should check permissions:

```bash
ls -l scripts/deploy.sh
```

Then add execute permission:

```bash
chmod 755 scripts/deploy.sh
```

If a secret file is too open, I should restrict it:

```bash
chmod 600 secrets/.env
```

If ownership looks wrong, I should check owner and group:

```bash
ls -l
```

Then fix ownership carefully:

```bash
sudo chown $USER:$USER file
```

Before using recursive commands, I should always check my current directory:

```bash
pwd
```

---

## Git Workflow

After completing the lab, I saved the work using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-06-permissions-ownership
git commit -m "Add Linux permissions and ownership notes"
git push
```

---

## What I Learned

In this lesson, I learned how Linux permissions and ownership work.

I learned how to read permissions using `ls -l`, how to understand `r`, `w` and `x`, and how numeric permissions like `755`, `644` and `600` are used.

I also learned how to make scripts executable, protect secret files, set safe config permissions and understand the difference between `chmod` and `chown`.

These skills are essential for DevOps because permission issues are common when working with servers, deployments, logs, services and automation scripts.

---

## Status

Lesson completed, committed and pushed to GitHub.
