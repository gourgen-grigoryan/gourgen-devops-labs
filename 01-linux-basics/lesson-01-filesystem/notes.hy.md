# Դաս 01 — Linux File System

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-linux%20filesystem-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը բացատրում է Linux file system-ի հիմնական կառուցվածքը և այն կարևոր path-երը, որոնք օգտագործվում են DevOps-ի ամենօրյա աշխատանքում։

Linux file system-ը հասկանալը շատ կարևոր է, որովհետև production server-ներում configuration files, logs, applications և services հիմնականում պահվում և կառավարվում են Linux directory-ների մեջ։

---

## Learning Objectives

Այս դասը ավարտելուց հետո ես սովորեցի՝

* ինչ է նշանակում Linux root directory `/`
* որտեղ է գտնվում իմ Linux home directory-ն
* ինչպես է աշխատում `~` shortcut-ը
* ինչպես են Windows files-ը երևում WSL-ի ներսում
* որտեղ են սովորաբար պահվում configuration files-ը
* որտեղ են սովորաբար պահվում log files-ը
* ինչու DevOps project-ները պետք է պահել Linux file system-ի ներսում

---

## Key Linux Paths

| Path | Նշանակություն | DevOps Usage |
| ---- | ------------- | ------------ |
| `/` | Linux file system-ի root-ը | Բոլոր directory-ների սկզբնակետը |
| `/home/phantom` | Իմ Linux user-ի home directory-ն | Անձնական files, labs և projects |
| `~` | `/home/phantom`-ի shortcut | Արագ անցում home directory |
| `/mnt/c` | Windows C drive-ը Linux-ի ներսում | Windows files-ին հասանելիություն WSL-ից |
| `/etc` | System և application configuration files | Nginx, SSH, systemd configs |
| `/var/log` | Log files | Troubleshooting services և applications |
| `/tmp` | Temporary files | Ժամանակավոր files, ոչ կարևոր projects-ի համար |

---

## Path Examples

Linux root directory գնալու համար՝

```bash
cd /
pwd
```

Home directory գնալու համար՝

```bash
cd ~
pwd
```

DevOps workspace գնալու համար՝

```bash
cd ~/devops-labs
pwd
```

System configuration files-ը տեսնելու համար՝

```bash
ls /etc
```

System log files-ը տեսնելու համար՝

```bash
ls /var/log
```

Windows C drive-ը WSL-ից տեսնելու համար՝

```bash
ls /mnt/c
```

---

## Important Concepts

### Root Directory

Root directory-ն Linux file system-ի սկիզբն է՝

```text
/
```

Linux-ում բոլոր directory-ները սկսվում են այստեղից։

### Home Directory

Իմ Linux user-ի home directory-ն է՝

```text
/home/phantom
```

Այստեղ կարելի է պահել personal files, labs և DevOps projects։

### Home Shortcut

`~` նշանը home directory-ի shortcut-ն է՝

```text
~ = /home/phantom
```

### Windows Drive in WSL

Windows C drive-ը WSL-ի ներսում հասանելի է այստեղ՝

```text
/mnt/c
```

Սա օգտակար է Windows files տեսնելու համար, բայց DevOps active projects-ը ավելի լավ է պահել Linux file system-ի մեջ։

---

## Important DevOps Rule

DevOps project-ները պետք է պահել Linux file system-ի ներսում, օրինակ՝

```text
~/devops-labs
```

Պետք է խուսափել active Linux/DevOps project-ները պահել այստեղ՝

```text
/mnt/c/Users/...
```

քանի որ Git, Linux permissions, scripts և Docker workflows ավելի ճիշտ են աշխատում Linux file system-ի մեջ։

---

## Common Mistakes

| Mistake | Problem | Correct Practice |
| ------- | ------- | ---------------- |
| Project պահել `/mnt/c`-ում | Linux tools-ը կարող են դանդաղ կամ սխալ աշխատել | Պահել `~/devops-labs`-ում |
| Չստուգել current location-ը | Կարող ես սխալ folder-ում աշխատել | Օգտագործել `pwd` |
| Շփոթել `/` և `~` | Կարող ես գնալ սխալ path | Հիշել՝ `/` root է, `~` home է |
| Active project պահել Desktop/Documents-ում | WSL/Linux workflow-ի համար լավ չէ | Պահել Linux home directory-ում |

---

## Linux File System Quick Reference

| Item | Meaning | Command |
| ---- | ------- | ------- |
| Root directory | Linux-ի ամենասկզբնական directory | `cd /` |
| Home directory | Current user-ի workspace | `cd ~` |
| Current location | Տեսնել որտեղ ես գտնվում | `pwd` |
| Config files | System/application configs | `ls /etc` |
| Logs | System/application logs | `ls /var/log` |
| Windows drive | Windows C drive inside WSL | `ls /mnt/c` |

---

## Validation

Այս դասը ստուգելու համար օգտագործված command-ները՝

```bash
pwd
ls /
ls /etc | head
ls /var/log | head
ls /mnt/c
```

Expected result՝

* `/` ցույց է տալիս Linux system-ի հիմնական directories-ը
* `/home/phantom` իմ user home directory-ն է
* `/etc` պարունակում է configuration files
* `/var/log` պարունակում է log files
* `/mnt/c` տալիս է Windows C drive-ի հասանելիություն

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

## Troubleshooting Notes

Եթե command-ները սխալ folder-ում են աշխատում, նախ ստուգել՝

```bash
pwd
```

Եթե չես գտնում project folder-ը՝

```bash
cd ~/devops-labs
ls
```

Եթե Windows files պետք է տեսնել WSL-ից՝

```bash
ls /mnt/c
```

---

## Git Workflow

Դասը ավարտելուց հետո աշխատանքը պահվել է Git-ում՝

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-01-filesystem/notes.hy.md
git commit -m "Add Armenian notes for Linux filesystem lesson"
git push
```

---

## What I Learned

Այս դասում ես սովորեցի, որ Linux-ը ունի մեկ հիմնական file system tree, որը սկսվում է `/`-ից։

Ես նաև սովորեցի, որ `/home/phantom`-ը իմ user workspace-ն է, իսկ `/mnt/c`-ը Windows drive-ի mounted տարբերակն է։

DevOps-ի համար շատ կարևոր է միշտ հասկանալ, թե որ directory-ում եմ գտնվում, հատկապես files ստեղծելու, փոփոխելու կամ ջնջելուց առաջ։

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
