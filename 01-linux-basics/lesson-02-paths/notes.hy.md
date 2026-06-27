# Դաս 02 — Linux Paths

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-linux%20paths-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը բացատրում է, թե ինչպես են աշխատում paths-ը Linux-ում։

Paths-ը հասկանալը DevOps-ում շատ կարևոր է, որովհետև գրեթե ամեն command կախված է նրանից, թե որ directory-ում ես գտնվում։ Սխալ path-ը կարող է բերել սխալ file խմբագրելու, սխալ project-ում command աշխատացնելու կամ սխալ directory ջնջելու։

---

## Learning Objectives

Այս դասը ավարտելուց հետո ես սովորեցի՝

* ինչ է absolute path-ը
* ինչ է relative path-ը
* ինչպես օգտագործել `.`
* ինչպես օգտագործել `..`
* ինչպես օգտագործել `~`
* ինչու պետք է ստուգել current location-ը `pwd`-ով
* ինչպես անվտանգ շարժվել directory-ների միջև

---

## Path Types

| Type | Meaning | Example |
| ---- | ------- | ------- |
| Absolute path | Full path, որը սկսվում է `/`-ից | `/home/phantom/devops-labs` |
| Relative path | Path current directory-ից | `cd 01-linux-basics` |
| Current directory | Այն directory-ն, որտեղ հիմա գտնվում եմ | `.` |
| Parent directory | Մեկ մակարդակ վերև directory | `..` |
| Home shortcut | Իմ home directory-ի shortcut | `~` |

---

## Absolute Path

Absolute path-ը միշտ սկսվում է՝

```text
/
```

Օրինակ՝

```text
/home/phantom/devops-labs
```

Այս path-ը աշխատում է ցանկացած տեղից, որովհետև ամբողջական location է Linux root-ից սկսած։

```bash
cd /home/phantom/devops-labs
```

---

## Relative Path

Relative path-ը չի սկսվում `/`-ով։

Այն հաշվարկվում է current directory-ից։

Օրինակ՝

```bash
cd 01-linux-basics
```

Սա ճիշտ կաշխատի միայն եթե ես գտնվում եմ՝

```text
/home/phantom/devops-labs
```

---

## Special Path Symbols

| Symbol | Meaning | Example |
| ------ | ------- | ------- |
| `.` | Current directory | `ls .` |
| `..` | Parent directory | `cd ..` |
| `../..` | Two levels up | `cd ../..` |
| `~` | My home directory | `cd ~` |

---

## Practical Commands Used

Show current directory:

```bash
pwd
```

List current directory:

```bash
ls .
```

Go one level up:

```bash
cd ..
pwd
```

Go to home directory:

```bash
cd ~
pwd
```

Go to DevOps workspace using absolute path:

```bash
cd /home/phantom/devops-labs
pwd
```

Go to Linux basics folder using relative path:

```bash
cd 01-linux-basics
pwd
```

---

## Why Paths Matter in DevOps

DevOps-ում path-ի սխալը կարող է վտանգավոր լինել։

Մինչև configuration file edit անել, script աշխատացնել, files ջնջել կամ Git commit անել, պետք է համոզվել, որ ճիշտ directory-ում ես։

Ամենակարևոր սովորությունը՝

```bash
pwd
```

Հետո՝

```bash
ls
tree -a -I .git -L 3 --charset=ascii
```

---

## Safety Rule

Մինչև files ստեղծելը, փոփոխելը, տեղափոխելը կամ ջնջելը, միշտ ստուգել current location-ը՝

```bash
pwd
```

Սա օգնում է խուսափել՝

* սխալ file խմբագրելուց
* սխալ folder ջնջելուց
* սխալ directory-ից commit անելուց
* սխալ տեղից script աշխատացնելուց

---

## Common Mistakes

| Mistake | Problem | Correct Practice |
| ------- | ------- | ---------------- |
| Relative path օգտագործել սխալ location-ից | Command-ը կարող է fail անել կամ գնալ սխալ տեղ | Նախ run անել `pwd` |
| Շփոթել `.` և `..` | Կարող ես սխալ directory inspect անել | `.` current է, `..` parent է |
| Միշտ long path գրել | Ավելի շատ սխալվելու հնարավորություն | Օգտագործել `~` shortcut |
| Delete անել առանց path ստուգելու | Կարող է սխալ file ջնջվել | Նախ `pwd`, `ls`, `tree` |

---

## Path Quick Reference

| Item | Meaning | Command |
| ---- | ------- | ------- |
| Absolute path | Full path from `/` | `cd /home/phantom/devops-labs` |
| Relative path | Path from current directory | `cd 01-linux-basics` |
| Current directory | Current folder | `ls .` |
| Parent directory | One level up | `cd ..` |
| Home directory | User home | `cd ~` |
| Check location | Show current path | `pwd` |

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

Expected result՝

* `pwd` shows the correct current directory
* `.` represents the current directory
* `..` moves one level up
* `~` returns to `/home/phantom`
* absolute paths work from anywhere
* relative paths depend on current location

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

## Troubleshooting Notes

Եթե relative path-ը չի աշխատում, ստուգել՝

```bash
pwd
ls
```

Եթե չգիտես որտեղ ես, վերադառնալ project root՝

```bash
cd ~/devops-labs
```

Եթե պետք է տեսնել ամբողջ structure-ը՝

```bash
tree -a -I .git -L 3 --charset=ascii
```

---

## Git Workflow

Դասը ավարտելուց հետո աշխատանքը պահվել է Git-ում՝

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-02-paths
git commit -m "Add Linux paths notes"
git push
```

---

## What I Learned

Այս դասում ես սովորեցի, որ Linux paths-ը command-line safety-ի հիմքերից է։

Absolute path-ը սկսվում է `/`-ից, իսկ relative path-ը կախված է այն directory-ից, որտեղ հիմա գտնվում եմ։

Ես նաև սովորեցի, որ `.`, `..` և `~` նշանները կարևոր shortcuts են navigation-ը արագ և անվտանգ դարձնելու համար։

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
