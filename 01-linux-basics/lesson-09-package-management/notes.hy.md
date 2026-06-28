# Lesson 09 — Package Management

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-package%20management-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը բացատրում է Linux package management-ի հիմունքները՝ օգտագործելով `apt` գործիքը, որը օգտագործվում է Debian-based համակարգերում, օրինակ՝ Ubuntu-ում։

Package management-ը DevOps-ի հիմնական skill-ներից է, որովհետև server-ներում հաճախ պետք է install անել software, անել updates, մաքրել unused packages և կատարել controlled maintenance։

DevOps Engineer-ը պետք է հասկանա՝ ինչպես թարմացնել package index-ը, install անել tools, upgrade անել installed packages, անվտանգ remove անել software և մաքրել unused dependencies։

Այս դասում օգտագործվում են `apt update`, `apt upgrade`, `apt install`, `apt remove`, `apt purge` և `apt autoremove` հրամանները։

---

## Learning Objectives

Այս դասից հետո ես սովորեցի՝

* ինչ է package manager-ը
* ինչ են Linux repositories-ը
* ինչպես թարմացնել local package index-ը `apt update` հրամանով
* ինչպես ստուգել՝ որ packages կարող են upgrade լինել
* ինչպես անվտանգ preview անել upgrade-ը simulation mode-ով
* ինչպես upgrade անել installed packages-ը `apt upgrade` հրամանով
* ինչպես install անել package `apt install` հրամանով
* ինչպես ստուգել installed command-ը `which` հրամանով
* ինչպես ստուգել installed package-ը `dpkg` հրամանով
* ինչպես remove անել package `apt remove` հրամանով
* ինչպես ամբողջությամբ ջնջել package-ը և config files-ը `apt purge` հրամանով
* ինչպես մաքրել unused dependencies-ը `apt autoremove` հրամանով
* ինչու production server-ում package upgrade անելիս պետք է զգույշ լինել

---

## Key Concepts

| Concept         | Բացատրություն                                                     |
| --------------- | ----------------------------------------------------------------- |
| Package         | Software, որը տարածվում է install անելու համար պատրաստ format-ով  |
| Package manager | Գործիք, որը install, update, remove և manage է անում software-ը   |
| Repository      | Software source, որտեղից package manager-ը վերցնում է packages    |
| Package index   | Local list, որտեղ պահվում են հասանելի packages և versions         |
| Dependency      | Package, որը պետք է մեկ այլ package-ի ճիշտ աշխատանքի համար        |
| Upgrade         | Installed packages-ը նոր version-ների թարմացնելը                  |
| Remove          | Package-ը ջնջել, բայց config files-ը կարող են մնալ                |
| Purge           | Package-ը և դրա config files-ը ամբողջությամբ ջնջել                |
| Autoremove      | Չօգտագործվող dependency packages-ը ջնջել                          |

---

## Commands Learned

| Command                       | Նպատակ                                             | Օրինակ                       |
| ----------------------------- | -------------------------------------------------- | ----------------------------- |
| `sudo apt update`             | Թարմացնում է local package index-ը                 | `sudo apt update`             |
| `apt list --upgradable`       | Ցույց է տալիս upgrade անելիք packages              | `apt list --upgradable`       |
| `sudo apt upgrade`            | Թարմացնում է installed packages-ը                  | `sudo apt upgrade`            |
| `sudo apt upgrade --simulate` | Preview է անում upgrade-ը առանց համակարգը փոխելու  | `sudo apt upgrade --simulate` |
| `sudo apt install PACKAGE`    | Install է անում package                            | `sudo apt install tree`       |
| `sudo apt remove PACKAGE`     | Ջնջում է package-ը, բայց config files-ը կարող են մնալ | `sudo apt remove tree`     |
| `sudo apt purge PACKAGE`      | Ջնջում է package-ը և config files-ը                | `sudo apt purge tree`         |
| `sudo apt autoremove`         | Ջնջում է unused dependencies                       | `sudo apt autoremove`         |
| `which COMMAND`               | Ցույց է տալիս command-ի executable path-ը          | `which tree`                  |
| `dpkg -l | grep PACKAGE`      | Ստուգում է package-ը installed է, թե ոչ            | `dpkg -l | grep tree`         |

---

## Lab Structure

Այս lab-ում ստեղծվում է հետևյալ structure-ը՝

```text
lesson-09-package-management/
|-- autoremove-output.txt
|-- installed-tree.txt
|-- notes.hy.md
|-- notes.md
|-- package-index.txt
|-- repo-tree.txt
|-- tree-path.txt
|-- tree-version.txt
|-- upgradable-packages.txt
`-- upgrade-simulation.txt
```

---

## Practical Commands Used

Ստեղծել lesson directory՝

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-09-package-management
cd lesson-09-package-management
```

Ստեղծել lab files՝

```bash
touch package-index.txt upgradable-packages.txt upgrade-simulation.txt tree-version.txt tree-path.txt installed-tree.txt repo-tree.txt autoremove-output.txt
```

Թարմացնել package index-ը՝

```bash
sudo apt update
```

Պահել package index update output-ը՝

```bash
sudo apt update | tee package-index.txt
```

Ստուգել available package upgrades-ը՝

```bash
apt list --upgradable
```

Պահել available upgrades output-ը՝

```bash
apt list --upgradable 2>/dev/null | tee upgradable-packages.txt
```

Անվտանգ preview անել package upgrades-ը՝

```bash
sudo apt upgrade --simulate
```

Պահել upgrade simulation output-ը՝

```bash
sudo apt upgrade --simulate | tee upgrade-simulation.txt
```

Install անել `tree` package-ը՝

```bash
sudo apt install tree
```

Ստուգել installed package-ի version-ը՝

```bash
tree --version
```

Պահել version output-ը՝

```bash
tree --version | tee tree-version.txt
```

Ստուգել՝ `tree` command-ը որտեղից է աշխատում՝

```bash
which tree
```

Պահել command path-ը՝

```bash
which tree | tee tree-path.txt
```

Ստուգել՝ package-ը installed է, թե ոչ՝

```bash
dpkg -l | grep tree
```

Պահել installed package information-ը՝

```bash
dpkg -l | grep tree | tee installed-tree.txt
```

Օգտագործել `tree` repository structure-ը տեսնելու համար՝

```bash
cd ~/devops-labs
tree -L 2
```

Պահել repository structure output-ը՝

```bash
tree -L 2 | tee 01-linux-basics/lesson-09-package-management/repo-tree.txt
```

Remove անել `tree` package-ը՝

```bash
sudo apt remove tree
```

Ստուգել, որ command-ը այլևս հասանելի չէ՝

```bash
tree --version
```

Նորից install անել `tree` package-ը purge practice-ի համար՝

```bash
sudo apt install tree
```

Purge անել `tree` package-ը՝

```bash
sudo apt purge tree
```

Ստուգել, որ command-ը այլևս հասանելի չէ՝

```bash
tree --version
```

Մաքրել unused dependencies-ը՝

```bash
sudo apt autoremove
```

Պահել autoremove output-ը՝

```bash
sudo apt autoremove | tee 01-linux-basics/lesson-09-package-management/autoremove-output.txt
```

---

## Package Management Explanation

Package management նշանակում է Linux համակարգում software install, update, remove և maintain անել։

Package manager-ը օգնում է, որ software-ը install լինի organized և consistent ձևով։

Փոխարենը random ֆայլեր manually ներբեռնելու՝ Linux-ը սովորաբար software-ը install է անում trusted repositories-ից։

Ubuntu/Debian համակարգերում հիմնական package management command-ն է՝

```bash
apt
```

Package manager-ը կարող է՝

* install անել software
* թարմացնել package information
* upgrade անել installed software
* remove անել software
* մաքրել unused dependencies
* automatic manage անել dependencies

---

## Repositories Explanation

Repositories-ը software sources են, որոնք օգտագործվում են operating system-ի կողմից։

Երբ package ենք install անում `apt`-ով, system-ը այն ներբեռնում է configured repositories-ից։

Սա կարևոր է, որովհետև repositories-ը տալիս են controlled և trusted software versions։

Package install կամ upgrade անելուց առաջ պետք է թարմացնել local package index-ը։

---

## `apt update` Explanation

`apt update` հրամանը թարմացնում է local package index-ը։

```bash
sudo apt update
```

Այս հրամանը չի upgrade անում installed software-ը։

Այն միայն թարմացնում է local list-ը՝ հասանելի packages և versions-ի մասին։

Պարզ ասած՝ system-ին ասում է՝

```text
Ստուգիր repositories-ը և թարմացրու հասանելի package versions-ի ցուցակը։
```

Այս command-ը սովորաբար պետք է run անել package install կամ upgrade անելուց առաջ։

---

## `apt list --upgradable` Explanation

`apt list --upgradable` հրամանը ցույց է տալիս installed packages-ը, որոնց համար ավելի նոր version կա։

```bash
apt list --upgradable
```

Սա օգտակար է run անելուց հետո՝

```bash
sudo apt update
```

Այն օգնում է հասկանալ՝ ինչ packages կարող են upgrade լինել մինչև իրական upgrade անելը։

---

## `apt upgrade` Explanation

`apt upgrade` հրամանը թարմացնում է installed packages-ը նոր հասանելի version-ների։

```bash
sudo apt upgrade
```

Մինչև իրական upgrade անելը ավելի անվտանգ է preview անել փոփոխությունները՝

```bash
sudo apt upgrade --simulate
```

Simulation mode-ը չի փոխում system-ը։ Այն միայն ցույց է տալիս՝ ինչ կկատարվեր։

Սա օգտակար է upgrade-ի ազդեցությունը հասկանալու համար։

---

## `apt install` Explanation

`apt install` հրամանը install է անում package։

Օրինակ՝

```bash
sudo apt install tree
```

`tree` package-ը փոքր command-line utility է, որը folder structure-ը ցույց է տալիս ծառի տեսքով։

Install-ից հետո command-ը կարելի է ստուգել՝

```bash
tree --version
```

Executable path-ը կարելի է ստուգել՝

```bash
which tree
```

Օրինակ output՝

```text
/usr/bin/tree
```

---

## `dpkg -l` Explanation

`dpkg -l` հրամանը ցույց է տալիս installed packages-ը։

Կոնկրետ package որոնելու համար՝

```bash
dpkg -l | grep tree
```

Եթե package-ը installed է, output-ը սովորաբար սկսվում է՝

```text
ii
```

`ii` նշանակում է, որ package-ը installed է։

---

## `apt remove` Explanation

`apt remove` հրամանը ջնջում է package-ը։

```bash
sudo apt remove tree
```

Բայց configuration files-ը կարող են մնալ system-ում։

Սա օգտակար է, երբ ուզում ենք package-ը ջնջել, բայց հնարավոր է հետագայում նույն configuration-ը պետք գա։

---

## `apt purge` Explanation

`apt purge` հրամանը ջնջում է package-ը և դրա configuration files-ը։

```bash
sudo apt purge tree
```

Սա ավելի խորը cleanup է, քան `apt remove`-ը։

`purge` օգտագործվում է, երբ ուզում ենք package-ը և դրա config-ը ամբողջությամբ հեռացնել system-ից։

---

## `apt autoremove` Explanation

Երբ package ենք install անում, դրա հետ կարող են install լինել լրացուցիչ dependency packages։

Եթե հետո main package-ը ջնջում ենք, որոշ dependencies կարող են այլևս պետք չլինել։

`apt autoremove` հրամանը ջնջում է unused dependencies-ը՝

```bash
sudo apt autoremove
```

Սա օգնում է system-ը մաքուր պահել։

---

## update vs upgrade

| Command       | Ինչ է անում                        |
| ------------- | ---------------------------------- |
| `apt update`  | Թարմացնում է package index-ը       |
| `apt upgrade` | Թարմացնում է installed packages-ը  |

---

## remove vs purge

| Command              | Ինչ է անում                                             |
| -------------------- | -------------------------------------------------------- |
| `apt remove PACKAGE` | Ջնջում է package-ը, բայց config files-ը կարող են մնալ    |
| `apt purge PACKAGE`  | Ջնջում է package-ը և դրա config files-ը                 |

---

## Why Package Management Matters in DevOps

Package management-ը կարևոր է DevOps-ի համար, որովհետև server-ները պետք է ճիշտ պատրաստել, maintain անել և secure պահել։

DevOps Engineer-ը package management օգտագործում է՝

* նոր server պատրաստելիս
* deployment tools install անելիս
* web server install անելիս
* monitoring tools install անելիս
* security updates անելիս
* unused packages մաքրելիս
* missing command troubleshooting անելիս
* installed software versions ստուգելիս

DevOps աշխատանքի ընթացքում հաճախ install արվող packages՝

```bash
sudo apt install git
sudo apt install curl
sudo apt install wget
sudo apt install unzip
sudo apt install nginx
sudo apt install docker.io
```

---

## Important Safety Notes

Production server-ներում package upgrades-ը պետք է անել զգուշությամբ։

Package upgrade-ը կարող է ազդել running services-ի վրա, օրինակ՝

* Nginx
* Docker
* PostgreSQL
* Redis
* OpenSSL
* monitoring agents
* application dependencies

Ճիշտ production practice՝

* նախ ստուգել՝ ինչ packages են փոխվելու
* հնարավորության դեպքում օգտագործել simulation կամ review mode
* ուշադիր կարդալ upgrade output-ը
* հնարավորության դեպքում test անել staging environment-ում
* անհրաժեշտության դեպքում ունենալ backup
* critical systems-ի համար ընտրել maintenance window

---

## Common Mistakes

| Սխալ                                      | Խնդիր                                  | Ճիշտ մոտեցում                                  |
| ----------------------------------------- | -------------------------------------- | ---------------------------------------------- |
| Մտածել, որ `apt update`-ը upgrade է անում | Այն միայն package index է թարմացնում   | Installed packages թարմացնելու համար `upgrade` |
| Production-ում blind upgrade անել         | Կարող է ազդել running services-ի վրա   | Նախ review անել փոփոխությունները              |
| Մոռանալ `sudo` օգտագործել                 | Package changes-ի համար պետք է admin permission | Package changes-ի համար օգտագործել `sudo` |
| Շփոթել `remove` և `purge`                 | Config files-ը կարող են մնալ remove-ից հետո | Full cleanup-ի համար օգտագործել `purge`   |
| Ignoring unused dependencies              | System-ում կարող են մնալ unnecessary packages | Run անել `sudo apt autoremove`             |
| Package install անելուց հետո չստուգել     | Command-ը կարող է expected ձևով հասանելի չլինել | Ստուգել `which` կամ `--version` հրամանով |

---

## Package Management Quick Reference

| Task                         | Command                       |
| ---------------------------- | ----------------------------- |
| Թարմացնել package index-ը    | `sudo apt update`             |
| Ցույց տալ upgradable packages | `apt list --upgradable`       |
| Preview անել upgrades-ը      | `sudo apt upgrade --simulate` |
| Upgrade անել installed packages-ը | `sudo apt upgrade`        |
| Install անել package         | `sudo apt install PACKAGE`    |
| Remove անել package          | `sudo apt remove PACKAGE`     |
| Purge անել package           | `sudo apt purge PACKAGE`      |
| Remove անել unused dependencies | `sudo apt autoremove`      |
| Ստուգել command path-ը       | `which COMMAND`               |
| Ստուգել installed package-ը  | `dpkg -l | grep PACKAGE`      |

---

## Validation

Այս lab-ը ստուգելու համար օգտագործվում են՝

```bash
pwd
tree -a --charset=ascii
cat package-index.txt
cat upgradable-packages.txt
cat upgrade-simulation.txt
cat tree-version.txt
cat tree-path.txt
cat installed-tree.txt
cat repo-tree.txt
cat autoremove-output.txt
apt list --upgradable
sudo apt upgrade --simulate
```

Expected result՝

* lesson directory exists
* `notes.md` exists
* `notes.hy.md` exists
* `package-index.txt` exists
* `upgradable-packages.txt` exists
* `upgrade-simulation.txt` exists
* `tree-version.txt` exists
* `tree-path.txt` exists
* `installed-tree.txt` exists
* `repo-tree.txt` exists
* `autoremove-output.txt` exists
* package index update-ը practiced է
* upgrade simulation-ը practiced է
* package installation-ը practiced է
* package removal-ը practiced է
* package purge-ը practiced է
* unused dependency cleanup-ը practiced է

---

## Quiz Review

| Question | Correct Answer | Status |
| -------- | -------------- | ------ |
| What does `apt update` do? | Այն թարմացնում է local package index-ը։ | Passed |
| What does `apt upgrade` do? | Այն թարմացնում է installed packages-ը նոր հասանելի version-ների։ | Passed |
| What is the difference between `remove` and `purge`? | `apt remove` ջնջում է package-ը, իսկ `apt purge` ջնջում է նաև configuration files-ը։ | Passed |
| What does `apt autoremove` do? | Այն ջնջում է այլևս չօգտագործվող dependency packages-ը։ | Passed |
| Why should production upgrades be handled carefully? | Upgrade-ը կարող է ազդել running services-ի վրա, դրա համար պետք է նախ ստուգել՝ ինչ packages են փոխվելու։ | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

Եթե `apt install`-ը error տա, նախ թարմացրու package index-ը՝

```bash
sudo apt update
```

Եթե command-ը install-ից հետո չի գտնվել, ստուգիր executable path-ը՝

```bash
which COMMAND
```

Եթե package-ը installed չի երևում, ստուգիր՝

```bash
dpkg -l | grep PACKAGE
```

Եթե package upgrade-ը risky է թվում, նախ preview արա՝

```bash
sudo apt upgrade --simulate
```

Եթե package remove-ից հետո unused dependencies են մնացել, մաքրիր՝

```bash
sudo apt autoremove
```

Եթե `remove` կամ `purge`-ից հետո `tree` command-ը missing է, դա նորմալ է, որովհետև package-ը ջնջվել է։

---

## Git Workflow

Lesson-ը ավարտելուց և quiz-ը անցնելուց հետո աշխատանքը պահվելու է Git-ով՝

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-09-package-management ROADMAP.md
git commit -m "Complete Linux package management lesson"
git push
git status
```

---

## What I Learned

Այս դասում ես սովորեցի, թե ինչպես է Linux package management-ը աշխատում `apt`-ով։

Ես սովորեցի թարմացնել package index-ը, ստուգել available upgrades-ը, անվտանգ preview անել upgrades-ը, install անել packages, ստուգել installed commands-ը, remove անել packages, purge անել packages և մաքրել unused dependencies։

Այս գիտելիքները կարևոր են DevOps-ի համար, որովհետև package management-ը օգտագործվում է server պատրաստելիս, tools install անելիս, updates անելիս, missing commands troubleshooting անելիս և Linux environments-ը մաքուր պահելիս։

---

## Status

Lesson completed, quiz passed, ready to commit and push.
