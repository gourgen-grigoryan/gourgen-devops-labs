<p align="center">
  <img src="../assets/devops-labs-banner.svg" alt="Gourgen DevOps Labs Banner" width="100%" />
</p>

<h1 align="center">DevOps Lab 00 — Local Workspace Setup</h1>

<p align="center">
  <strong>Preparing a professional DevOps learning environment using Windows, WSL2 Ubuntu, Git and GitHub.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/status-completed-brightgreen" alt="Status" />
  <img src="https://img.shields.io/badge/focus-setup-blue" alt="Focus" />
  <img src="https://img.shields.io/badge/platform-Windows%20%2B%20WSL2-lightgrey" alt="Platform" />
  <img src="https://img.shields.io/badge/GitHub-pushed-success" alt="GitHub" />
</p>

---

## Overview

This lab documents the initial setup of my local DevOps learning environment.

The goal of this phase was to prepare a clean and reliable workspace for learning DevOps step by step, using a Windows host system with Ubuntu running inside WSL2.

---

## Lab Objectives

By completing this lab, I prepared:

* WSL2 Ubuntu on Windows
* A Linux user environment
* A dedicated DevOps workspace
* Required command-line tools
* Git global configuration
* A local Git repository
* SSH authentication with GitHub
* A remote GitHub repository for future labs

---

## Environment

| Component         | Value                 |
| ----------------- | --------------------- |
| Host OS           | Windows               |
| Linux environment | Ubuntu on WSL2        |
| Linux user        | `phantom`             |
| Main workspace    | `~/devops-labs`       |
| GitHub username   | `gourgen-grigoryan`   |
| Repository        | `gourgen-devops-labs` |

---

## Installed Tools

| Tool              | Purpose                                 |
| ----------------- | --------------------------------------- |
| `git`             | Version control                         |
| `curl`            | Testing URLs, APIs and server responses |
| `wget`            | Downloading files                       |
| `unzip`           | Extracting archive files                |
| `tree`            | Viewing directory structure             |
| `htop`            | Viewing processes and resource usage    |
| `nano`            | Editing files in the terminal           |
| `ca-certificates` | SSL certificate support                 |
| `gnupg`           | Package signing keys                    |
| `lsb-release`     | Linux distribution information          |

---

## Key Commands Practiced

```bash
wsl --status
wsl -l -v
whoami
pwd
cat /etc/os-release
sudo apt update
sudo apt upgrade -y
sudo apt install -y git curl wget unzip tree htop nano ca-certificates gnupg lsb-release
git config --global user.name "Gourgen Grigoryan"
git config --global user.email "grigoryan_gourgen@yahoo.com"
git config --global init.defaultBranch main
git init
git status
git add .
git commit -m "Initialize DevOps learning workspace"
ssh -T git@github.com
git remote -v
git push -u origin main
```

---

## Repository Structure Created

```text
devops-labs/
|-- 00-setup
|-- 01-linux-basics
|-- 02-networking-ccna-foundations
|-- 03-git-github
|-- 04-bash-scripting
|-- 05-database-fundamentals
|-- 06-nginx-systemd
|-- 07-docker
|-- 08-github-actions-cicd
|-- 09-cloud
|-- 10-terraform
|-- 11-monitoring-security
|-- 12-kubernetes
|-- 13-portfolio
|-- assets
`-- README.md
```

---

## Validation Checks

| Check                                  | Result    |
| -------------------------------------- | --------- |
| Ubuntu runs inside WSL2                | Completed |
| Linux user was created                 | Completed |
| DevOps workspace was created           | Completed |
| Required tools were installed          | Completed |
| Git global config was set              | Completed |
| Local Git repository was initialized   | Completed |
| SSH key was added to GitHub            | Completed |
| Remote GitHub repository was connected | Completed |
| First push to GitHub was completed     | Completed |

---

## Security Notes

Passwords, API keys, SSH private keys and secrets must never be written in:

* chat messages
* screenshots
* README files
* GitHub repositories
* public documentation

If a secret is accidentally committed, it must be removed from the code and rotated immediately.

---

## What I Learned

During this setup phase, I learned:

* why DevOps work is usually done in a Linux environment
* the difference between Windows paths and Linux paths
* why projects should be stored inside the Linux file system in WSL
* how to install basic DevOps tools
* how to configure Git properly
* how to initialize a repository
* how to connect a local repository to GitHub using SSH
* why security habits are important from the beginning

---

## Status

This lab is completed and pushed to GitHub.

Next phase: Linux fundamentals.
