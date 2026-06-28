# Lesson 09 — Package Management

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-package%20management-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers Linux package management using `apt`, the standard package management tool used on Debian-based systems such as Ubuntu.

Package management is a core DevOps skill because Linux servers often need software installation, updates, cleanup and controlled maintenance. A DevOps Engineer must understand how to refresh package indexes, install tools, upgrade installed packages, remove software safely and clean unused dependencies.

In this lesson, I practiced using `apt update`, `apt upgrade`, `apt install`, `apt remove`, `apt purge` and `apt autoremove`.

---

## Learning Objectives

By completing this lesson, I learned how to:

* understand what a Linux package manager is
* understand what repositories are
* refresh the local package index using `apt update`
* check which packages can be upgraded
* preview upgrades safely using simulation mode
* upgrade installed packages using `apt upgrade`
* install packages using `apt install`
* verify installed commands with `which`
* check installed packages with `dpkg`
* remove packages using `apt remove`
* fully remove packages and configuration files using `apt purge`
* clean unused dependencies using `apt autoremove`
* understand why package upgrades must be handled carefully on production servers

---

## Key Concepts

| Concept         | Meaning                                                  |
| --------------- | -------------------------------------------------------- |
| Package         | Software distributed in an installable format            |
| Package manager | Tool used to install, update, remove and manage software |
| Repository      | Software source used by the package manager              |
| Package index   | Local list of available packages and versions            |
| Dependency      | Another package required by a package to work correctly  |
| Upgrade         | Updating installed packages to newer available versions  |
| Remove          | Deleting a package while configuration files may remain  |
| Purge           | Deleting a package and its configuration files           |
| Autoremove      | Removing unused dependency packages                      |

---

## Commands Learned

| Command                       | Purpose                                            | Example                       |
| ----------------------------- | -------------------------------------------------- | ----------------------------- |
| `sudo apt update`             | Refreshes the local package index                  | `sudo apt update`             |
| `apt list --upgradable`       | Shows packages that can be upgraded                | `apt list --upgradable`       |
| `sudo apt upgrade`            | Upgrades installed packages                        | `sudo apt upgrade`            |
| `sudo apt upgrade --simulate` | Previews upgrades without changing the system      | `sudo apt upgrade --simulate` |
| `sudo apt install PACKAGE`    | Installs a package                                 | `sudo apt install tree`       |
| `sudo apt remove PACKAGE`     | Removes a package but may keep configuration files | `sudo apt remove tree`        |
| `sudo apt purge PACKAGE`      | Removes a package and its configuration files      | `sudo apt purge tree`         |
| `sudo apt autoremove`         | Removes unused dependencies                        | `sudo apt autoremove`         |
| `which COMMAND`               | Shows the executable path of a command             | `which tree`                  |
| `dpkg -l | grep PACKAGE`      | Checks whether a package is installed              | `dpkg -l | grep tree`         |

---

## Lab Structure

In this lab, I created the following structure:

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

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-09-package-management
cd lesson-09-package-management
```

Create lab files:

```bash
touch package-index.txt upgradable-packages.txt upgrade-simulation.txt tree-version.txt tree-path.txt installed-tree.txt repo-tree.txt autoremove-output.txt
```

Refresh the package index:

```bash
sudo apt update
```

Save package index update output:

```bash
sudo apt update | tee package-index.txt
```

Check available package upgrades:

```bash
apt list --upgradable
```

Save available upgrades output:

```bash
apt list --upgradable 2>/dev/null | tee upgradable-packages.txt
```

Preview package upgrades safely:

```bash
sudo apt upgrade --simulate
```

Save upgrade simulation output:

```bash
sudo apt upgrade --simulate | tee upgrade-simulation.txt
```

Install the `tree` package:

```bash
sudo apt install tree
```

Verify the installed package version:

```bash
tree --version
```

Save the version output:

```bash
tree --version | tee tree-version.txt
```

Check where the `tree` command is located:

```bash
which tree
```

Save the command path:

```bash
which tree | tee tree-path.txt
```

Check if the package is installed:

```bash
dpkg -l | grep tree
```

Save installed package information:

```bash
dpkg -l | grep tree | tee installed-tree.txt
```

Use `tree` to display the repository structure:

```bash
cd ~/devops-labs
tree -L 2
```

Save repository structure output:

```bash
tree -L 2 | tee 01-linux-basics/lesson-09-package-management/repo-tree.txt
```

Remove the `tree` package:

```bash
sudo apt remove tree
```

Verify that the command is no longer available:

```bash
tree --version
```

Install `tree` again for purge practice:

```bash
sudo apt install tree
```

Purge the `tree` package:

```bash
sudo apt purge tree
```

Verify that the command is no longer available:

```bash
tree --version
```

Clean unused dependencies:

```bash
sudo apt autoremove
```

Save autoremove output:

```bash
sudo apt autoremove | tee 01-linux-basics/lesson-09-package-management/autoremove-output.txt
```

---

## Understanding Package Management

Package management means installing, updating, removing and maintaining software on a Linux system.

A package manager helps keep software organized and consistent. Instead of downloading random files manually, Linux systems usually install software from trusted repositories.

On Ubuntu and Debian-based systems, the common package management command is:

```bash
apt
```

A package manager can:

* install software
* update package information
* upgrade installed software
* remove software
* clean unused dependencies
* manage required dependencies automatically

---

## Understanding Repositories

Repositories are software sources used by the operating system.

When a package is installed with `apt`, the system downloads it from configured repositories.

This is important because repositories provide controlled and trusted software versions.

Before installing or upgrading packages, the local package index should be refreshed.

---

## Understanding `apt update`

The `apt update` command refreshes the local package index.

```bash
sudo apt update
```

This command does not upgrade installed software.

It only updates the local list of available packages and versions from configured repositories.

In simple terms, it tells the system:

```text
Check the repositories and refresh the list of available package versions.
```

This command is usually run before installing or upgrading packages.

---

## Understanding `apt list --upgradable`

The `apt list --upgradable` command shows installed packages that have newer versions available.

```bash
apt list --upgradable
```

This is useful after running:

```bash
sudo apt update
```

It helps understand what packages could be upgraded before actually upgrading them.

---

## Understanding `apt upgrade`

The `apt upgrade` command upgrades installed packages to newer available versions.

```bash
sudo apt upgrade
```

Before running a real upgrade, it is safer to preview the changes:

```bash
sudo apt upgrade --simulate
```

Simulation mode does not change the system. It only shows what would happen.

This is useful for understanding upgrade impact before making real changes.

---

## Understanding `apt install`

The `apt install` command installs a package.

Example:

```bash
sudo apt install tree
```

The `tree` package is a small command-line utility that displays directories in a tree-like structure.

After installation, the command can be verified:

```bash
tree --version
```

The executable path can be checked with:

```bash
which tree
```

Example output:

```text
/usr/bin/tree
```

---

## Understanding `dpkg -l`

The `dpkg -l` command lists installed packages.

To search for a specific package:

```bash
dpkg -l | grep tree
```

If the package is installed, the output usually starts with:

```text
ii
```

The `ii` status means the package is installed.

---

## Understanding `apt remove`

The `apt remove` command removes a package.

```bash
sudo apt remove tree
```

However, configuration files may remain on the system.

This is useful when the package should be removed but its configuration may be kept for future reuse.

---

## Understanding `apt purge`

The `apt purge` command removes a package and its configuration files.

```bash
sudo apt purge tree
```

This is a deeper cleanup than `apt remove`.

Use `purge` when the package and its configuration should be fully removed from the system.

---

## Understanding `apt autoremove`

When a package is installed, additional dependency packages may also be installed.

If the main package is removed later, some dependencies may no longer be needed.

The `apt autoremove` command removes unused dependencies:

```bash
sudo apt autoremove
```

This helps keep the system clean.

---

## update vs upgrade

| Command       | What it does                |
| ------------- | --------------------------- |
| `apt update`  | Refreshes the package index |
| `apt upgrade` | Upgrades installed packages |

---

## remove vs purge

| Command              | What it does                                         |
| -------------------- | ---------------------------------------------------- |
| `apt remove PACKAGE` | Removes the package but may keep configuration files |
| `apt purge PACKAGE`  | Removes the package and its configuration files      |

---

## Why Package Management Matters in DevOps

Package management is important in DevOps because servers must be prepared, maintained and secured.

DevOps Engineers use package management when:

* preparing new servers
* installing deployment tools
* installing web servers
* installing monitoring tools
* applying security updates
* cleaning unused packages
* troubleshooting missing commands
* checking installed software versions

Common packages installed during DevOps work include:

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

Package upgrades should be handled carefully on production servers.

Upgrading packages can affect running services such as:

* Nginx
* Docker
* PostgreSQL
* Redis
* OpenSSL
* monitoring agents
* application dependencies

Good production practice includes:

* checking what packages will change
* using simulation or review mode when possible
* reading upgrade output carefully
* testing changes in staging environments
* taking backups when needed
* scheduling maintenance windows for critical systems

---

## Common Mistakes

| Mistake                                 | Problem                                  | Correct Practice                                |
| --------------------------------------- | ---------------------------------------- | ----------------------------------------------- |
| Thinking `apt update` upgrades software | It only refreshes the package index      | Use `apt upgrade` to upgrade installed packages |
| Running upgrades blindly on production  | May affect running services              | Review changes before upgrading                 |
| Forgetting `sudo`                       | Package changes require admin privileges | Use `sudo` for package changes                  |
| Confusing `remove` and `purge`          | Config files may remain after remove     | Use `purge` for full cleanup                    |
| Ignoring unused dependencies            | System can keep unnecessary packages     | Run `sudo apt autoremove`                       |
| Installing packages without verifying   | The command may not be available         | Verify with `which` or `--version`              |

---

## Package Management Quick Reference

| Task                       | Command                       |
| -------------------------- | ----------------------------- |
| Refresh package index      | `sudo apt update`             |
| Show upgradable packages   | `apt list --upgradable`       |
| Preview upgrades           | `sudo apt upgrade --simulate` |
| Upgrade installed packages | `sudo apt upgrade`            |
| Install a package          | `sudo apt install PACKAGE`    |
| Remove a package           | `sudo apt remove PACKAGE`     |
| Purge a package            | `sudo apt purge PACKAGE`      |
| Remove unused dependencies | `sudo apt autoremove`         |
| Check command path         | `which COMMAND`               |
| Check installed package    | `dpkg -l | grep PACKAGE`      |

---

## Validation

Commands used to validate this lab:

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

Expected result:

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
* package index update was practiced
* upgrade simulation was practiced
* package installation was practiced
* package removal was practiced
* package purge was practiced
* unused dependency cleanup was practiced

---

## Quiz Review

| Question | Correct Answer | Status |
| -------- | -------------- | ------ |
| What does `apt update` do? | It refreshes the local package index. | Passed |
| What does `apt upgrade` do? | It upgrades installed packages to newer available versions. | Passed |
| What is the difference between `remove` and `purge`? | `apt remove` removes the package, while `apt purge` also removes configuration files. | Passed |
| What does `apt autoremove` do? | It removes unused dependency packages. | Passed |
| Why should production upgrades be handled carefully? | Upgrades can affect running services, so package changes should be reviewed first. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

If `apt install` fails, first refresh the package index:

```bash
sudo apt update
```

If a command is not found after installing a package, check the executable path:

```bash
which COMMAND
```

If a package does not appear installed, check with:

```bash
dpkg -l | grep PACKAGE
```

If package upgrades look risky, preview them first:

```bash
sudo apt upgrade --simulate
```

If unused dependencies remain after package removal, clean them with:

```bash
sudo apt autoremove
```

If `tree` is missing after `remove` or `purge`, that is expected because the package was removed.

---

## Git Workflow

After completing the lesson and passing the quiz, the work will be saved using Git:

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

In this lesson, I learned how Linux package management works with `apt`.

I learned how to refresh the package index, check available upgrades, preview upgrades safely, install packages, verify installed commands, remove packages, purge packages and clean unused dependencies.

These skills are essential for DevOps because package management is used when preparing servers, installing tools, applying updates, troubleshooting missing commands and maintaining clean Linux environments.

---

## Status

Lesson completed, quiz passed, ready to commit and push.
