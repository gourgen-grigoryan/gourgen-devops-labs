# Դաս 06 — Permissions and Ownership

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-permissions%20and%20ownership-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը ծածկում է Linux file permissions և ownership concepts-ը, որոնք օգտագործվում են DevOps-ի ամենօրյա աշխատանքում։

Permissions-ը կարևոր են, որովհետև Linux systems-ը պաշտպանում է files և directories access rules-ով։ DevOps Engineer-ը պետք է հասկանա՝ ով կարող է read, write կամ execute անել files-ը, ինչպես դարձնել script-ը executable, ինչպես պաշտպանել secrets և ինչպես troubleshoot անել permission errors։

Այս դասում ես practice արեցի `chmod`, `chown`, numeric permissions, executable scripts և safe permissions scripts, configs, logs և secrets-ի համար։

---

## Learning Objectives

Այս դասը ավարտելուց հետո ես սովորեցի՝

* կարդալ Linux permissions `ls -l`-ով
* հասկանալ `r`, `w`, `x`
* հասկանալ owner, group և others
* օգտագործել numeric permissions՝ `755`, `644`, `600`
* դարձնել script-ը executable `chmod`-ով
* դնել safe permissions config files-ի համար
* պաշտպանել secret files restricted permissions-ով
* հասկանալ file ownership
* օգտագործել `chown` owner/group փոխելու համար
* validate անել permissions `stat`-ով
* troubleshoot անել permission errors

---

## Permission Basics

Linux permissions-ը սովորաբար երևում են `ls -l` command-ով։

```bash
ls -l
```

Example output:

```text
-rwxr-xr-x 1 phantom phantom 120 Jun 26 deploy.sh
-rw-r--r-- 1 phantom phantom 80 Jun 26 app.conf
```

Առաջին մասը permissions-ն է՝

```text
-rwxr-xr-x
```

Բաժանում՝

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

| Symbol | Meaning |
| ------ | ------- |
| `r` | read |
| `w` | write |
| `x` | execute |
| `-` | no permission |

Example:

```text
-rw-r--r--
```

Meaning:

| User Type | Permission |
| --------- | ---------- |
| Owner | read and write |
| Group | read only |
| Others | read only |

---

## Numeric Permissions

Linux permissions-ը կարելի է գրել նաև թվերով։

| Number | Permission |
| ------ | ---------- |
| `4` | read |
| `2` | write |
| `1` | execute |

Թվերը գումարվում են։

| Number | Meaning |
| ------ | ------- |
| `7` | read, write and execute |
| `6` | read and write |
| `5` | read and execute |
| `4` | read only |
| `0` | no permissions |

---

## Common Permission Values

| Permission | Meaning | Common Use |
| ---------- | ------- | ---------- |
| `755` | Owner can read/write/execute, others can read/execute | Scripts and directories |
| `644` | Owner can read/write, others can read | Config files and regular files |
| `600` | Only owner can read/write | Secrets and private files |
| `700` | Only owner has full access | Private directories or scripts |

---

## Commands Learned

| Command | Purpose | Example |
| ------- | ------- | ------- |
| `ls -l` | Shows permissions and ownership | `ls -l` |
| `chmod +x file` | Adds execute permission | `chmod +x scripts/deploy.sh` |
| `chmod 755 file` | Sets executable script permissions | `chmod 755 scripts/deploy.sh` |
| `chmod 644 file` | Sets regular file permissions | `chmod 644 configs/app.conf` |
| `chmod 600 file` | Restricts file to owner only | `chmod 600 secrets/.env` |
| `chown user file` | Changes file owner | `sudo chown phantom file` |
| `chown user:group file` | Changes owner and group | `sudo chown phantom:phantom file` |
| `stat -c "%A %a %U:%G %n" file` | Shows detailed permission info | `stat -c "%A %a %U:%G %n" scripts/deploy.sh` |

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

Create lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-06-permissions-ownership
cd lesson-06-permissions-ownership
```

Create directories/files:

```bash
mkdir scripts configs logs secrets
touch configs/app.conf logs/app.log secrets/.env
```

Create deployment script:

```bash
cat > scripts/deploy.sh <<'EOF'
#!/bin/bash

echo "Starting deployment..."
echo "Checking application files..."
echo "Deployment completed successfully."
EOF
```

Try to run before execute permission:

```bash
./scripts/deploy.sh
```

Expected problem:

```text
Permission denied
```

Make script executable:

```bash
chmod 755 scripts/deploy.sh
```

Run script:

```bash
./scripts/deploy.sh
```

Expected result:

```text
Starting deployment...
Checking application files...
Deployment completed successfully.
```

Create config:

```bash
cat > configs/app.conf <<'EOF'
APP_NAME=devops-lab
APP_ENV=development
APP_PORT=3000
LOG_FILE=logs/app.log
EOF
```

Set config permissions:

```bash
chmod 644 configs/app.conf
```

Create secret file:

```bash
cat > secrets/.env <<'EOF'
DB_USER=admin
DB_PASSWORD=super-secret-password
API_KEY=devops-demo-key
EOF
```

Protect secret:

```bash
chmod 600 secrets/.env
```

Create log file:

```bash
echo "INFO Application started" > logs/app.log
echo "ERROR Example permission issue" >> logs/app.log
```

Set log permissions:

```bash
chmod 644 logs/app.log
```

Validate permissions:

```bash
stat -c "%A %a %U:%G %n" scripts/deploy.sh configs/app.conf logs/app.log secrets/.env
```

---

## Expected Permission Results

```text
-rwxr-xr-x 755 phantom:phantom scripts/deploy.sh
-rw-r--r-- 644 phantom:phantom configs/app.conf
-rw-r--r-- 644 phantom:phantom logs/app.log
-rw------- 600 phantom:phantom secrets/.env
```

Username/group-ը կարող է տարբեր լինել։

| File | Expected Permission |
| ---- | ------------------- |
| `scripts/deploy.sh` | `755` |
| `configs/app.conf` | `644` |
| `logs/app.log` | `644` |
| `secrets/.env` | `600` |

---

## `chmod` Examples

Make script executable:

```bash
chmod +x scripts/deploy.sh
```

Set script permissions:

```bash
chmod 755 scripts/deploy.sh
```

Set config permissions:

```bash
chmod 644 configs/app.conf
```

Set secret permissions:

```bash
chmod 600 secrets/.env
```

Set private directory permissions:

```bash
chmod 700 secrets
```

---

## `chown` Examples

Check owner/group:

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

Recursive ownership change:

```bash
sudo chown -R $USER:$USER lesson-06-permissions-ownership
```

Recursive commands-ը պետք է օգտագործել շատ զգույշ։

---

## Why Permissions Matter in DevOps

Permissions-ը օգնում են պատասխանել՝

* Ինչու script-ը չի աշխատում
* Ինչու application-ը ցույց է տալիս `Permission denied`
* Application-ը կարո՞ղ է կարդալ config file-ը
* Application-ը կարո՞ղ է գրել log file-ի մեջ
* Secret file-ը շատ բա՞ց է
* Ո՞վ է file owner-ը
* Service user-ը ունի՞ access այդ directory-ին

---

## Important Safety Notes

Secret files-ը չպետք է readable լինեն everyone-ի համար։

```bash
chmod 600 secrets/.env
```

Private SSH keys-ի համար նույնպես սովորաբար պետք է՝

```bash
chmod 600 ~/.ssh/id_rsa
```

Scripts-ը պետք է ունենան execute permission՝

```bash
chmod 755 scripts/deploy.sh
```

Խուսափել՝

```bash
chmod 777 file
```

`777` տալիս է everyone-ին read/write/execute access և սովորաբար unsafe է։

---

## Common Mistakes

| Mistake | Problem | Correct Version |
| ------- | ------- | --------------- |
| Running script without execute permission | `Permission denied` | `chmod 755 script.sh` |
| Using `chmod 777` | Too open and unsafe | Use `755`, `644`, `600` |
| Giving secrets `644` | Others can read secrets | `chmod 600 secrets/.env` |
| Confusing `chmod` and `chown` | Wrong tool | `chmod` permissions, `chown` ownership |
| Running `chown -R` wrong directory | Can break permissions | Always check `pwd` first |

---

## `chmod` vs `chown`

| Command | Purpose |
| ------- | ------- |
| `chmod` | Changes file permissions |
| `chown` | Changes file owner and group |

---

## Permission Quick Reference

| Permission | Symbol Form | Meaning | Common Use |
| ---------- | ----------- | ------- | ---------- |
| `600` | `-rw-------` | Only owner can read/write | Secrets, `.env`, private keys |
| `644` | `-rw-r--r--` | Owner can read/write, others can read | Config files, normal files |
| `755` | `-rwxr-xr-x` | Owner full access, others read/execute | Scripts, directories |
| `777` | `-rwxrwxrwx` | Everyone has full access | Usually unsafe |

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

Expected result՝

* files exist
* `scripts/deploy.sh` has `755`
* `configs/app.conf` has `644`
* `logs/app.log` has `644`
* `secrets/.env` has `600`
* script runs successfully
* `stat` shows expected permissions

---

## Quiz Review

| Question | Correct Answer | Status |
| --- | --- | --- |
| What does `r` permission mean? | `r` means read permission. | Passed |
| What does `w` permission mean? | `w` means write permission. | Passed |
| What does `x` permission mean? | `x` means execute permission. | Passed |
| What command changes permissions? | `chmod` changes file or directory permissions. | Passed |
| What command changes ownership? | `chown` changes file owner and group. | Passed |
| What permission is commonly used for scripts? | `755` is commonly used for executable scripts. | Passed |
| What permission is correct for secret `.env` files? | `600` is safer for secret files. | Passed |
| What does `644` mean? | Owner can read/write, group and others can read. | Passed |
| Why should `chmod 777` usually be avoided? | It gives everyone read, write and execute access, which is unsafe. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

If script shows:

```text
Permission denied
```

check permissions:

```bash
ls -l scripts/deploy.sh
```

then fix:

```bash
chmod 755 scripts/deploy.sh
```

If secret file is too open:

```bash
chmod 600 secrets/.env
```

If ownership looks wrong:

```bash
ls -l
sudo chown $USER:$USER file
```

Before recursive commands:

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

Այս դասում ես սովորեցի, թե ինչպես են աշխատում Linux permissions և ownership-ը։

Ես սովորեցի կարդալ permissions `ls -l`-ով, հասկանալ `r`, `w`, `x`, և օգտագործել numeric permissions՝ `755`, `644`, `600`։

Այս skills-ը կարևոր են DevOps-ի համար, որովհետև permission issues-ը շատ հաճախ հանդիպում են servers, deployments, logs, services և automation scripts-ի մեջ։

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
