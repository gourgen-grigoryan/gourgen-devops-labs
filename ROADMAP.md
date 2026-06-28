# Gourgen DevOps Professional Roadmap

![Status](https://img.shields.io/badge/status-in%20progress-yellow)
![Focus](https://img.shields.io/badge/focus-DevOps-blue)
![Level](https://img.shields.io/badge/level-zero%20to%20professional-lightgrey)
![Portfolio](https://img.shields.io/badge/portfolio-ready-success)
![Documentation](https://img.shields.io/badge/docs-English%20%2B%20Armenian-blueviolet)

A structured, hands-on DevOps learning roadmap focused on Linux, networking, automation, cloud, CI/CD, infrastructure, monitoring, security and portfolio-ready projects.

---

## Current Status

| Item                      | Value                                                          |
| ------------------------- | -------------------------------------------------------------- |
| Current Phase             | 02 — Networking with CCNA-Level Foundations                    |
| Current Lesson            | Lesson 01 — Networking Basics                                  |
| Current Lesson Status     | Planned                                                        |
| Recently Completed        | Lesson 12 — Linux Review Lab                                   |
| Main Repository Style     | Portfolio-ready DevOps learning repository                     |
| English Notes             | `notes.md`                                                     |
| Armenian Notes            | `notes.hy.md`                                                  |
| Roadmap Source of Truth   | `ROADMAP.md`                                                   |
| Future Documentation Site | MkDocs Material or Docusaurus with real English / Հայերեն tabs |

---

## Status Legend

| Status      | Meaning                                                      |
| ----------- | ------------------------------------------------------------ |
| Completed   | Lesson finished, quiz passed, committed and pushed to GitHub |
| In Progress | Currently being studied, documented or validated             |
| Planned     | Planned for a later roadmap stage                            |

---

## Roadmap Overview

| Phase | Topic                                  | Status      |
| ----- | -------------------------------------- | ----------- |
| 00    | Setup and Local DevOps Workspace       | Completed   |
| 01    | Linux Fundamentals                     | Completed   |
| 02    | Networking with CCNA-Level Foundations | In Progress |
| 03    | Git and GitHub Workflows               | Planned     |
| 04    | Bash Scripting                         | Planned     |
| 05    | Database Fundamentals for DevOps       | Planned     |
| 06    | Nginx and systemd                      | Planned     |
| 07    | Docker                                 | Planned     |
| 08    | GitHub Actions CI/CD                   | Planned     |
| 09    | Cloud Infrastructure                   | Planned     |
| 10    | Terraform                              | Planned     |
| 11    | Monitoring, Logging and Security       | Planned     |
| 12    | Kubernetes                             | Planned     |
| 13    | Professional Portfolio                 | Planned     |

---

## Table of Contents

* [Phase 00 — Setup and Local DevOps Workspace](#phase-00--setup-and-local-devops-workspace)
* [Phase 01 — Linux Fundamentals](#phase-01--linux-fundamentals)
* [Phase 02 — Networking with CCNA-Level Foundations](#phase-02--networking-with-ccna-level-foundations)
* [Phase 03 — Git and GitHub Workflows](#phase-03--git-and-github-workflows)
* [Phase 04 — Bash Scripting](#phase-04--bash-scripting)
* [Phase 05 — Database Fundamentals for DevOps](#phase-05--database-fundamentals-for-devops)
* [Phase 06 — Nginx and systemd](#phase-06--nginx-and-systemd)
* [Phase 07 — Docker](#phase-07--docker)
* [Phase 08 — GitHub Actions CI/CD](#phase-08--github-actions-cicd)
* [Phase 09 — Cloud Infrastructure](#phase-09--cloud-infrastructure)
* [Phase 10 — Terraform](#phase-10--terraform)
* [Phase 11 — Monitoring, Logging and Security](#phase-11--monitoring-logging-and-security)
* [Phase 12 — Kubernetes](#phase-12--kubernetes)
* [Phase 13 — Professional Portfolio](#phase-13--professional-portfolio)
* [Final Portfolio Projects](#final-portfolio-projects)
* [Documentation Rules](#documentation-rules)
* [Git Workflow Rule](#git-workflow-rule)
* [Current Progress Summary](#current-progress-summary)

---

# Phase 00 — Setup and Local DevOps Workspace

![Status](https://img.shields.io/badge/phase-completed-brightgreen)

## Lesson 00.01 — Local Workspace Setup

**Status:** Completed

**Topics:**

* Windows + WSL2 Ubuntu
* Linux user environment
* DevOps workspace structure
* Git installation
* Git global config
* GitHub SSH connection
* Repository initialization
* First commit and push

---

# Phase 01 — Linux Fundamentals

![Status](https://img.shields.io/badge/phase-completed-brightgreen)

## Lesson 01 — Linux File System

**Status:** Completed

**Topics:**

* `/`
* `/home`
* `~`
* `/mnt/c`
* `/etc`
* `/var/log`
* `/tmp`
* WSL file system rules

---

## Lesson 02 — Linux Paths

**Status:** Completed

**Topics:**

* absolute paths
* relative paths
* `.`
* `..`
* `~`
* `pwd`
* safe navigation habits

---

## Lesson 03 — File Operations

**Status:** Completed

**Topics:**

* `touch`
* `mkdir`
* `mkdir -p`
* `cp`
* `cp -r`
* `mv`
* `rm`
* `rmdir`
* `cat`
* `>`
* `>>`
* delete safety

---

## Lesson 04 — Log Reading Basics

**Status:** Completed

**Topics:**

* `cat`
* `less`
* `head`
* `tail`
* `tail -f`
* `wc -l`
* searching inside `less`
* reading small and large logs safely

---

## Lesson 05 — Search and Filtering

**Status:** Completed

**Topics:**

* `grep`
* `grep -i`
* `grep -n`
* `grep -v`
* `grep -r`
* `grep -E`
* `find`
* `wc`
* pipes `|`
* filtering logs and files

---

## Lesson 06 — Permissions and Ownership

**Status:** Completed

**Topics:**

* `r`, `w`, `x`
* owner, group, others
* `chmod`
* `chown`
* `755`
* `644`
* `600`
* executable scripts
* secret file permissions
* permission troubleshooting

---

## Lesson 07 — Users, Groups and sudo

**Status:** Completed

**Topics:**

* `whoami`
* `id`
* `groups`
* `sudo`
* `root`
* UID
* GID
* `getent passwd`
* `getent group`
* least privilege

---

## Lesson 08 — Processes and System Monitoring

**Status:** Completed

**Topics:**

* process
* PID
* `ps`
* `ps aux`
* `top`
* `htop`
* `kill`
* `uptime`
* `free -h`
* `df -h`
* `du -sh`
* CPU/RAM/disk basics

---

## Lesson 09 — Package Management

**Status:** Completed

**Topics:**

* `apt update`
* `apt upgrade`
* `apt install`
* `apt remove`
* `apt purge`
* `apt autoremove`
* package search
* checking installed packages
* safe update habits

---

## Lesson 10 — Linux Services Basics

**Status:** Completed

**Topics:**

* `systemctl`
* service status
* start service
* stop service
* restart service
* enable service
* disable service
* service troubleshooting
* `journalctl`

---

## Lesson 11 — Environment Variables

**Status:** Completed

**Topics:**

* environment variables
* `$PATH`
* `printenv`
* `export`
* shell variables
* `.bashrc`
* `.profile`
* safe secret handling

---

## Lesson 12 — Linux Review Lab

**Status:** Completed

**Topics:**

* full Linux fundamentals review
* file system
* paths
* files
* logs
* search
* permissions
* users
* processes
* packages
* services
* final quiz
* portfolio cleanup

---

# Phase 02 — Networking with CCNA-Level Foundations

![Status](https://img.shields.io/badge/phase-in%20progress-yellow)

## Lesson 01 — Networking Basics

**Status:** Planned

**Topics:**

* what a network is
* LAN
* WAN
* client/server
* IP address
* gateway
* DNS
* ports

---

## Lesson 02 — IP Addressing

**Status:** Planned

**Topics:**

* IPv4
* private IP
* public IP
* subnet mask
* CIDR
* default gateway
* loopback address

---

## Lesson 03 — DNS Basics

**Status:** Planned

**Topics:**

* domain names
* DNS records
* A record
* CNAME
* MX
* TXT
* `nslookup`
* `dig`

---

## Lesson 04 — Ports and Protocols

**Status:** Planned

**Topics:**

* TCP
* UDP
* HTTP
* HTTPS
* SSH
* DNS
* common ports
* checking listening ports

---

## Lesson 05 — Network Troubleshooting

**Status:** Planned

**Topics:**

* `ping`
* `curl`
* `wget`
* `ss`
* `netstat`
* `traceroute`
* `ip addr`
* `ip route`

---

## Lesson 06 — Firewalls and Basic Rules

**Status:** Planned

**Topics:**

* firewall concept
* inbound traffic
* outbound traffic
* `ufw`
* allow rules
* deny rules
* port security

---

## Lesson 07 — Networking Review Lab

**Status:** Planned

**Topics:**

* DNS troubleshooting
* port checks
* HTTP checks
* SSH checks
* firewall basics
* network debugging workflow

---

# Phase 03 — Git and GitHub Workflows

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — Git Fundamentals

**Status:** Planned

**Topics:**

* repository
* working tree
* staging area
* commits
* `git status`
* `git add`
* `git commit`
* `git log`

---

## Lesson 02 — Branches

**Status:** Planned

**Topics:**

* branches
* `git branch`
* `git checkout`
* `git switch`
* merge basics
* branch naming

---

## Lesson 03 — Remote Repositories

**Status:** Planned

**Topics:**

* origin
* remote URL
* `git push`
* `git pull`
* `git fetch`
* upstream branch

---

## Lesson 04 — Pull Requests

**Status:** Planned

**Topics:**

* PR workflow
* code review
* merge commits
* squash merge
* GitHub UI basics

---

## Lesson 05 — Git Troubleshooting

**Status:** Planned

**Topics:**

* undo changes
* restore files
* reset basics
* merge conflicts
* safe recovery

---

## Lesson 06 — Professional Git Workflow Lab

**Status:** Planned

**Topics:**

* feature branch
* clean commits
* pull request
* review
* merge
* GitHub portfolio workflow

---

# Phase 04 — Bash Scripting

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — Bash Script Basics

**Status:** Planned

**Topics:**

* shebang
* executable scripts
* variables
* echo
* comments
* script structure

---

## Lesson 02 — Arguments and Input

**Status:** Planned

**Topics:**

* `$1`
* `$2`
* `$@`
* `read`
* input validation

---

## Lesson 03 — Conditions

**Status:** Planned

**Topics:**

* `if`
* `else`
* `elif`
* test expressions
* file checks
* string checks
* numeric checks

---

## Lesson 04 — Loops

**Status:** Planned

**Topics:**

* `for`
* `while`
* loop over files
* loop over command output
* safe loops

---

## Lesson 05 — Functions

**Status:** Planned

**Topics:**

* function syntax
* reusable logic
* return codes
* script organization

---

## Lesson 06 — Bash Automation Lab

**Status:** Planned

**Topics:**

* log checker script
* backup script
* disk usage checker
* service status checker
* portfolio-ready automation scripts

---

# Phase 05 — Database Fundamentals for DevOps

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — SQL Basics

**Status:** Planned

**Topics:**

* database
* table
* row
* column
* SELECT
* INSERT
* UPDATE
* DELETE

---

## Lesson 02 — PostgreSQL Setup

**Status:** Planned

**Topics:**

* install PostgreSQL
* users
* databases
* roles
* `psql`
* connection basics

---

## Lesson 03 — Database Permissions

**Status:** Planned

**Topics:**

* database users
* grants
* privileges
* least privilege for databases

---

## Lesson 04 — Backup and Restore

**Status:** Planned

**Topics:**

* `pg_dump`
* restore
* backup files
* backup validation
* safe restore workflow

---

## Lesson 05 — Migrations Basics

**Status:** Planned

**Topics:**

* schema changes
* migration files
* rollback concept
* migration safety

---

## Lesson 06 — PostgreSQL DevOps Lab

**Status:** Planned

**Topics:**

* create database
* create user
* permissions
* backup
* restore
* documentation

---

# Phase 06 — Nginx and systemd

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — Nginx Basics

**Status:** Planned

**Topics:**

* web server concept
* install Nginx
* default site
* config files
* static hosting

---

## Lesson 02 — Nginx Server Blocks

**Status:** Planned

**Topics:**

* server block
* domain config
* root directory
* index file
* config test

---

## Lesson 03 — Reverse Proxy

**Status:** Planned

**Topics:**

* proxy_pass
* backend app
* headers
* localhost ports
* reverse proxy troubleshooting

---

## Lesson 04 — systemd Services

**Status:** Planned

**Topics:**

* unit files
* service start
* service restart
* enable on boot
* logs with `journalctl`

---

## Lesson 05 — SSL Basics

**Status:** Planned

**Topics:**

* HTTPS
* certificates
* Let's Encrypt concept
* Certbot basics
* redirect HTTP to HTTPS

---

## Lesson 06 — Nginx + systemd Portfolio Lab

**Status:** Planned

**Topics:**

* app service
* reverse proxy
* logs
* restart workflow
* validation
* security notes

---

# Phase 07 — Docker

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — Docker Basics

**Status:** Planned

**Topics:**

* container
* image
* Dockerfile
* registry
* Docker Hub
* container lifecycle

---

## Lesson 02 — Running Containers

**Status:** Planned

**Topics:**

* `docker run`
* `docker ps`
* `docker stop`
* `docker logs`
* port mapping
* volumes

---

## Lesson 03 — Dockerfile

**Status:** Planned

**Topics:**

* base image
* copy files
* install dependencies
* expose port
* command
* build image

---

## Lesson 04 — Docker Compose

**Status:** Planned

**Topics:**

* compose file
* services
* networks
* volumes
* environment variables
* multi-container apps

---

## Lesson 05 — Docker Troubleshooting

**Status:** Planned

**Topics:**

* container logs
* failed builds
* port conflicts
* volume issues
* networking issues

---

## Lesson 06 — Dockerized Application Stack Lab

**Status:** Planned

**Topics:**

* app container
* database container
* Nginx container
* compose workflow
* portfolio documentation

---

# Phase 08 — GitHub Actions CI/CD

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — CI/CD Basics

**Status:** Planned

**Topics:**

* continuous integration
* continuous delivery
* pipeline
* workflow
* job
* step

---

## Lesson 02 — GitHub Actions Basics

**Status:** Planned

**Topics:**

* `.github/workflows`
* YAML
* triggers
* jobs
* runners
* actions

---

## Lesson 03 — Automated Checks

**Status:** Planned

**Topics:**

* lint
* tests
* build checks
* status checks
* failed pipeline troubleshooting

---

## Lesson 04 — Deployment Workflow

**Status:** Planned

**Topics:**

* deploy job
* environment variables
* secrets
* deployment safety
* rollback concept

---

## Lesson 05 — CI/CD Portfolio Lab

**Status:** Planned

**Topics:**

* automated validation
* GitHub Actions workflow
* build pipeline
* deployment simulation
* documentation

---

# Phase 09 — Cloud Infrastructure

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — Cloud Basics

**Status:** Planned

**Topics:**

* cloud provider
* regions
* zones
* compute
* storage
* network
* billing awareness

---

## Lesson 02 — Virtual Machines

**Status:** Planned

**Topics:**

* create VM
* SSH access
* firewall rules
* public IP
* Linux server setup

---

## Lesson 03 — Cloud Networking

**Status:** Planned

**Topics:**

* VPC
* subnets
* firewall
* public/private access
* ports

---

## Lesson 04 — Cloud Deployment

**Status:** Planned

**Topics:**

* deploy app to VM
* configure Nginx
* systemd service
* domain
* SSL

---

## Lesson 05 — Cloud Cost Safety

**Status:** Planned

**Topics:**

* free tier
* budgets
* alerts
* stopping resources
* avoiding unexpected billing

---

## Lesson 06 — Cloud VM Portfolio Lab

**Status:** Planned

**Topics:**

* VM provisioning
* SSH
* firewall
* Nginx
* SSL
* deployment documentation

---

# Phase 10 — Terraform

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — Infrastructure as Code

**Status:** Planned

**Topics:**

* IaC concept
* Terraform basics
* providers
* resources
* state

---

## Lesson 02 — Terraform Project Structure

**Status:** Planned

**Topics:**

* `main.tf`
* `variables.tf`
* `outputs.tf`
* `.tfvars`
* formatting

---

## Lesson 03 — Terraform Commands

**Status:** Planned

**Topics:**

* `terraform init`
* `terraform plan`
* `terraform apply`
* `terraform destroy`
* `terraform fmt`
* `terraform validate`

---

## Lesson 04 — Variables and Outputs

**Status:** Planned

**Topics:**

* input variables
* output values
* locals
* reusable configuration

---

## Lesson 05 — Terraform Cloud Resource Lab

**Status:** Planned

**Topics:**

* provision VM
* firewall rule
* output IP
* destroy safely
* documentation

---

# Phase 11 — Monitoring, Logging and Security

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — Linux Monitoring Basics

**Status:** Planned

**Topics:**

* CPU
* RAM
* disk
* uptime
* load average
* `top`
* `htop`
* `free`
* `df`
* `du`

---

## Lesson 02 — Logs Deep Dive

**Status:** Planned

**Topics:**

* `/var/log`
* `journalctl`
* service logs
* auth logs
* application logs
* log filtering
* log rotation concept

---

## Lesson 03 — Uptime Kuma

**Status:** Planned

**Topics:**

* uptime monitoring
* HTTP checks
* TCP checks
* website monitoring
* status pages
* notifications

---

## Lesson 04 — Netdata

**Status:** Planned

**Topics:**

* real-time server dashboard
* CPU/RAM/disk/network monitoring
* quick troubleshooting
* Netdata vs Prometheus/Grafana

---

## Lesson 05 — Prometheus Basics

**Status:** Planned

**Topics:**

* metrics
* targets
* scrape
* time-series data
* `prometheus.yml`
* Prometheus UI

---

## Lesson 06 — Node Exporter

**Status:** Planned

**Topics:**

* Linux server metrics
* CPU metrics
* memory metrics
* disk metrics
* filesystem metrics
* network metrics
* Prometheus target config

---

## Lesson 07 — Grafana Dashboards

**Status:** Planned

**Topics:**

* Grafana datasource
* Prometheus datasource
* dashboards
* panels
* queries
* CPU/RAM/disk/network visualization

---

## Lesson 08 — Alerts

**Status:** Planned

**Topics:**

* alert rules
* CPU alerts
* disk alerts
* uptime alerts
* service down alerts
* notification channels

---

## Lesson 09 — Zabbix Intro

**Status:** Planned

**Topics:**

* Zabbix server
* Zabbix agent
* hosts
* items
* triggers
* templates
* alerts
* enterprise monitoring concept

---

## Lesson 10 — Cloud Monitoring Tools

**Status:** Planned

**Topics:**

* Google Cloud Monitoring
* AWS CloudWatch
* Azure Monitor
* cloud metrics
* cloud alerts
* billing/resource monitoring

---

## Lesson 11 — Basic Security Hardening

**Status:** Planned

**Topics:**

* users
* groups
* sudo
* permissions
* updates
* SSH hardening
* firewall
* least privilege

---

## Lesson 12 — SSH Security

**Status:** Planned

**Topics:**

* SSH keys
* disable root login
* password login risks
* `sshd_config`
* allowed users
* SSH troubleshooting

---

## Lesson 13 — Firewall and Fail2ban

**Status:** Planned

**Topics:**

* `ufw`
* open ports
* allow/deny rules
* Fail2ban
* brute-force protection
* SSH protection

---

## Lesson 14 — Monitoring and Security Portfolio Project

**Status:** Planned

**Topics:**

* monitored Linux server
* Prometheus
* Node Exporter
* Grafana
* Uptime Kuma
* security hardening checklist
* alerts
* documentation
* screenshots

---

# Phase 12 — Kubernetes

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — Kubernetes Basics

**Status:** Planned

**Topics:**

* cluster
* node
* pod
* deployment
* service
* namespace
* container orchestration

---

## Lesson 02 — kubectl Basics

**Status:** Planned

**Topics:**

* `kubectl get`
* `kubectl describe`
* `kubectl logs`
* `kubectl apply`
* `kubectl delete`

---

## Lesson 03 — Deployments and Services

**Status:** Planned

**Topics:**

* deployment YAML
* service YAML
* scaling
* rolling updates
* service exposure

---

## Lesson 04 — ConfigMaps and Secrets

**Status:** Planned

**Topics:**

* ConfigMap
* Secret
* environment variables
* safe configuration

---

## Lesson 05 — Kubernetes Troubleshooting

**Status:** Planned

**Topics:**

* pod errors
* image pull errors
* crash loop
* logs
* events
* service connectivity

---

## Lesson 06 — Kubernetes Portfolio Lab

**Status:** Planned

**Topics:**

* deploy app
* service
* config
* logs
* troubleshooting
* documentation

---

# Phase 13 — Professional Portfolio

![Status](https://img.shields.io/badge/phase-planned-lightgrey)

## Lesson 01 — Portfolio Repository Cleanup

**Status:** Planned

**Topics:**

* README quality
* folder structure
* badges
* links
* screenshots
* documentation consistency

---

## Lesson 02 — Documentation Site

**Status:** Planned

**Topics:**

* MkDocs Material or Docusaurus
* English / Հայերեն tabs
* navigation
* lesson pages
* portfolio pages

---

## Lesson 03 — Architecture Diagrams

**Status:** Planned

**Topics:**

* diagrams
* network flows
* CI/CD flows
* monitoring architecture
* cloud architecture

---

## Lesson 04 — Final Portfolio Projects

**Status:** Planned

**Topics:**

* Linux admin lab
* Docker stack
* CI/CD pipeline
* cloud deployment
* Terraform infrastructure
* monitoring stack
* security checklist

---

## Lesson 05 — Resume and GitHub Presentation

**Status:** Planned

**Topics:**

* GitHub profile
* project descriptions
* resume bullets
* LinkedIn summary
* DevOps interview preparation

---

# Final Portfolio Projects

## Project 01 — Linux Server Administration Lab

**Includes:**

* users
* groups
* permissions
* logs
* services
* monitoring basics
* security notes

---

## Project 02 — Networking Troubleshooting Lab

**Includes:**

* DNS
* ports
* curl
* ping
* firewall
* routing basics

---

## Project 03 — PostgreSQL DevOps Lab

**Includes:**

* PostgreSQL setup
* users
* permissions
* backups
* restore
* documentation

---

## Project 04 — Dockerized Application Stack

**Includes:**

* app container
* database container
* Nginx
* Docker Compose
* logs
* troubleshooting

---

## Project 05 — CI/CD Pipeline Lab

**Includes:**

* GitHub Actions
* automated checks
* build
* deploy simulation
* secrets handling

---

## Project 06 — Cloud VM Deployment Lab

**Includes:**

* cloud VM
* SSH
* firewall
* Nginx
* systemd
* SSL
* deployment validation

---

## Project 07 — Terraform Infrastructure Lab

**Includes:**

* Terraform project
* provider
* resources
* variables
* outputs
* safe destroy

---

## Project 08 — Monitoring and Security Stack

**Includes:**

* Prometheus
* Node Exporter
* Grafana
* Uptime Kuma
* Netdata comparison
* Zabbix intro
* alerts
* security checklist

---

# Documentation Rules

For every lesson:

```text
notes.md    = English portfolio version
notes.hy.md = Armenian learning version
```

Each lesson should include:

* badges
* overview
* learning objectives
* commands learned
* lab structure
* practical commands used
* detailed explanations
* common mistakes
* quick reference
* validation
* quiz review
* quiz result
* troubleshooting notes
* Git workflow
* what I learned
* final status

Final status format:

```text
Lesson completed, quiz passed, committed and pushed to GitHub.
```

---

# Git Workflow Rule

After every completed lesson:

```bash
cd ~/devops-labs
git status
git add .
git commit -m "Clear professional commit message"
git push
git status
```

Expected final result:

```text
nothing to commit, working tree clean
```

---

# Current Progress Summary

| #  | Lesson / Phase            | Status    |
| -- | ------------------------- | --------- |
| 00 | Setup                     | Completed |
| 01 | Linux File System         | Completed |
| 02 | Linux Paths               | Completed |
| 03 | File Operations           | Completed |
| 04 | Log Reading               | Completed |
| 05 | Search and Filtering      | Completed |
| 06 | Permissions and Ownership | Completed |
| 07 | Users, Groups and sudo    | Completed |
| 08 | Processes and Monitoring  | Completed |
| 09 | Package Management        | Completed |
| 10 | Linux Services Basics     | Completed |
| 11 | Environment Variables     | Completed |
| 12 | Linux Review Lab          | Completed |
| 02.01 | Networking Basics       | Planned   |

---

## Roadmap Maintenance Rule

`ROADMAP.md` is the source of truth for the full DevOps learning path.

At the end of every completed lesson, update:

* current lesson status
* phase status if needed
* lesson status inside the phase
* Current Progress Summary
* next lesson status when starting it

Then commit the lesson folder and `ROADMAP.md` together.

Example:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-12-linux-review-lab ROADMAP.md
git commit -m "Complete Linux fundamentals review lab"
git push
git status
```

Expected final result:

```text
nothing to commit, working tree clean
```
