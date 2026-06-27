# Gourgen DevOps Professional Roadmap

## Current Status

```text
Current phase: 01 — Linux Fundamentals
Current lesson: Lesson 08 — Processes and System Monitoring
Documentation style:
  notes.md    = English portfolio version
  notes.hy.md = Armenian learning version
Future docs site:
  MkDocs Material or Docusaurus with real English | Հայերեն tabs
```

---

# Phase 00 — Setup and Local DevOps Workspace

## Lesson 00.01 — Local Workspace Setup

Topics:

* Windows + WSL2 Ubuntu
* Linux user environment
* DevOps workspace structure
* Git installation
* Git global config
* GitHub SSH connection
* Repository initialization
* First commit and push

Status:

```text
Completed
```

---

# Phase 01 — Linux Fundamentals

## Lesson 01 — Linux File System

Topics:

* `/`
* `/home`
* `~`
* `/mnt/c`
* `/etc`
* `/var/log`
* `/tmp`
* WSL file system rules

Status:

```text
Completed
```

## Lesson 02 — Linux Paths

Topics:

* absolute paths
* relative paths
* `.`
* `..`
* `~`
* `pwd`
* safe navigation habits

Status:

```text
Completed
```

## Lesson 03 — File Operations

Topics:

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

Status:

```text
Completed
```

## Lesson 04 — Log Reading Basics

Topics:

* `cat`
* `less`
* `head`
* `tail`
* `tail -f`
* `wc -l`
* searching inside `less`
* reading small and large logs safely

Status:

```text
Completed
```

## Lesson 05 — Search and Filtering

Topics:

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

Status:

```text
Completed
```

## Lesson 06 — Permissions and Ownership

Topics:

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

Status:

```text
Completed
```

## Lesson 07 — Users, Groups and sudo

Topics:

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

Status:

```text
Completed
```

## Lesson 08 — Processes and System Monitoring

Topics:

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

Status:

```text
In Progress
```

## Lesson 09 — Package Management

Topics:

* `apt update`
* `apt upgrade`
* `apt install`
* `apt remove`
* `apt purge`
* `apt autoremove`
* package search
* checking installed packages
* safe update habits

Status:

```text
Planned
```

## Lesson 10 — Linux Services Basics

Topics:

* `systemctl`
* service status
* start service
* stop service
* restart service
* enable service
* disable service
* service troubleshooting
* `journalctl`

Status:

```text
Planned
```

## Lesson 11 — Environment Variables

Topics:

* environment variables
* `$PATH`
* `printenv`
* `export`
* shell variables
* `.bashrc`
* `.profile`
* safe secret handling

Status:

```text
Planned
```

## Lesson 12 — Linux Review Lab

Topics:

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

Status:

```text
Planned
```

---

# Phase 02 — Networking with CCNA-Level Foundations

## Lesson 01 — Networking Basics

Topics:

* what a network is
* LAN
* WAN
* client/server
* IP address
* gateway
* DNS
* ports

Status:

```text
Planned
```

## Lesson 02 — IP Addressing

Topics:

* IPv4
* private IP
* public IP
* subnet mask
* CIDR
* default gateway
* loopback address

Status:

```text
Planned
```

## Lesson 03 — DNS Basics

Topics:

* domain names
* DNS records
* A record
* CNAME
* MX
* TXT
* `nslookup`
* `dig`

Status:

```text
Planned
```

## Lesson 04 — Ports and Protocols

Topics:

* TCP
* UDP
* HTTP
* HTTPS
* SSH
* DNS
* common ports
* checking listening ports

Status:

```text
Planned
```

## Lesson 05 — Network Troubleshooting

Topics:

* `ping`
* `curl`
* `wget`
* `ss`
* `netstat`
* `traceroute`
* `ip addr`
* `ip route`

Status:

```text
Planned
```

## Lesson 06 — Firewalls and Basic Rules

Topics:

* firewall concept
* inbound traffic
* outbound traffic
* `ufw`
* allow rules
* deny rules
* port security

Status:

```text
Planned
```

## Lesson 07 — Networking Review Lab

Topics:

* DNS troubleshooting
* port checks
* HTTP checks
* SSH checks
* firewall basics
* network debugging workflow

Status:

```text
Planned
```

---

# Phase 03 — Git and GitHub Workflows

## Lesson 01 — Git Fundamentals

Topics:

* repository
* working tree
* staging area
* commits
* `git status`
* `git add`
* `git commit`
* `git log`

Status:

```text
Planned
```

## Lesson 02 — Branches

Topics:

* branches
* `git branch`
* `git checkout`
* `git switch`
* merge basics
* branch naming

Status:

```text
Planned
```

## Lesson 03 — Remote Repositories

Topics:

* origin
* remote URL
* `git push`
* `git pull`
* `git fetch`
* upstream branch

Status:

```text
Planned
```

## Lesson 04 — Pull Requests

Topics:

* PR workflow
* code review
* merge commits
* squash merge
* GitHub UI basics

Status:

```text
Planned
```

## Lesson 05 — Git Troubleshooting

Topics:

* undo changes
* restore files
* reset basics
* merge conflicts
* safe recovery

Status:

```text
Planned
```

## Lesson 06 — Professional Git Workflow Lab

Topics:

* feature branch
* clean commits
* pull request
* review
* merge
* GitHub portfolio workflow

Status:

```text
Planned
```

---

# Phase 04 — Bash Scripting

## Lesson 01 — Bash Script Basics

Topics:

* shebang
* executable scripts
* variables
* echo
* comments
* script structure

Status:

```text
Planned
```

## Lesson 02 — Arguments and Input

Topics:

* `$1`
* `$2`
* `$@`
* `read`
* input validation

Status:

```text
Planned
```

## Lesson 03 — Conditions

Topics:

* `if`
* `else`
* `elif`
* test expressions
* file checks
* string checks
* numeric checks

Status:

```text
Planned
```

## Lesson 04 — Loops

Topics:

* `for`
* `while`
* loop over files
* loop over command output
* safe loops

Status:

```text
Planned
```

## Lesson 05 — Functions

Topics:

* function syntax
* reusable logic
* return codes
* script organization

Status:

```text
Planned
```

## Lesson 06 — Bash Automation Lab

Topics:

* log checker script
* backup script
* disk usage checker
* service status checker
* portfolio-ready automation scripts

Status:

```text
Planned
```

---

# Phase 05 — Database Fundamentals for DevOps

## Lesson 01 — SQL Basics

Topics:

* database
* table
* row
* column
* SELECT
* INSERT
* UPDATE
* DELETE

Status:

```text
Planned
```

## Lesson 02 — PostgreSQL Setup

Topics:

* install PostgreSQL
* users
* databases
* roles
* `psql`
* connection basics

Status:

```text
Planned
```

## Lesson 03 — Database Permissions

Topics:

* database users
* grants
* privileges
* least privilege for databases

Status:

```text
Planned
```

## Lesson 04 — Backup and Restore

Topics:

* `pg_dump`
* restore
* backup files
* backup validation
* safe restore workflow

Status:

```text
Planned
```

## Lesson 05 — Migrations Basics

Topics:

* schema changes
* migration files
* rollback concept
* migration safety

Status:

```text
Planned
```

## Lesson 06 — PostgreSQL DevOps Lab

Topics:

* create database
* create user
* permissions
* backup
* restore
* documentation

Status:

```text
Planned
```

---

# Phase 06 — Nginx and systemd

## Lesson 01 — Nginx Basics

Topics:

* web server concept
* install Nginx
* default site
* config files
* static hosting

Status:

```text
Planned
```

## Lesson 02 — Nginx Server Blocks

Topics:

* server block
* domain config
* root directory
* index file
* config test

Status:

```text
Planned
```

## Lesson 03 — Reverse Proxy

Topics:

* proxy_pass
* backend app
* headers
* localhost ports
* reverse proxy troubleshooting

Status:

```text
Planned
```

## Lesson 04 — systemd Services

Topics:

* unit files
* service start
* service restart
* enable on boot
* logs with `journalctl`

Status:

```text
Planned
```

## Lesson 05 — SSL Basics

Topics:

* HTTPS
* certificates
* Let's Encrypt concept
* Certbot basics
* redirect HTTP to HTTPS

Status:

```text
Planned
```

## Lesson 06 — Nginx + systemd Portfolio Lab

Topics:

* app service
* reverse proxy
* logs
* restart workflow
* validation
* security notes

Status:

```text
Planned
```

---

# Phase 07 — Docker

## Lesson 01 — Docker Basics

Topics:

* container
* image
* Dockerfile
* registry
* Docker Hub
* container lifecycle

Status:

```text
Planned
```

## Lesson 02 — Running Containers

Topics:

* `docker run`
* `docker ps`
* `docker stop`
* `docker logs`
* port mapping
* volumes

Status:

```text
Planned
```

## Lesson 03 — Dockerfile

Topics:

* base image
* copy files
* install dependencies
* expose port
* command
* build image

Status:

```text
Planned
```

## Lesson 04 — Docker Compose

Topics:

* compose file
* services
* networks
* volumes
* environment variables
* multi-container apps

Status:

```text
Planned
```

## Lesson 05 — Docker Troubleshooting

Topics:

* container logs
* failed builds
* port conflicts
* volume issues
* networking issues

Status:

```text
Planned
```

## Lesson 06 — Dockerized Application Stack Lab

Topics:

* app container
* database container
* Nginx container
* compose workflow
* portfolio documentation

Status:

```text
Planned
```

---

# Phase 08 — GitHub Actions CI/CD

## Lesson 01 — CI/CD Basics

Topics:

* continuous integration
* continuous delivery
* pipeline
* workflow
* job
* step

Status:

```text
Planned
```

## Lesson 02 — GitHub Actions Basics

Topics:

* `.github/workflows`
* YAML
* triggers
* jobs
* runners
* actions

Status:

```text
Planned
```

## Lesson 03 — Automated Checks

Topics:

* lint
* tests
* build checks
* status checks
* failed pipeline troubleshooting

Status:

```text
Planned
```

## Lesson 04 — Deployment Workflow

Topics:

* deploy job
* environment variables
* secrets
* deployment safety
* rollback concept

Status:

```text
Planned
```

## Lesson 05 — CI/CD Portfolio Lab

Topics:

* automated validation
* GitHub Actions workflow
* build pipeline
* deployment simulation
* documentation

Status:

```text
Planned
```

---

# Phase 09 — Cloud Infrastructure

## Lesson 01 — Cloud Basics

Topics:

* cloud provider
* regions
* zones
* compute
* storage
* network
* billing awareness

Status:

```text
Planned
```

## Lesson 02 — Virtual Machines

Topics:

* create VM
* SSH access
* firewall rules
* public IP
* Linux server setup

Status:

```text
Planned
```

## Lesson 03 — Cloud Networking

Topics:

* VPC
* subnets
* firewall
* public/private access
* ports

Status:

```text
Planned
```

## Lesson 04 — Cloud Deployment

Topics:

* deploy app to VM
* configure Nginx
* systemd service
* domain
* SSL

Status:

```text
Planned
```

## Lesson 05 — Cloud Cost Safety

Topics:

* free tier
* budgets
* alerts
* stopping resources
* avoiding unexpected billing

Status:

```text
Planned
```

## Lesson 06 — Cloud VM Portfolio Lab

Topics:

* VM provisioning
* SSH
* firewall
* Nginx
* SSL
* deployment documentation

Status:

```text
Planned
```

---

# Phase 10 — Terraform

## Lesson 01 — Infrastructure as Code

Topics:

* IaC concept
* Terraform basics
* providers
* resources
* state

Status:

```text
Planned
```

## Lesson 02 — Terraform Project Structure

Topics:

* `main.tf`
* `variables.tf`
* `outputs.tf`
* `.tfvars`
* formatting

Status:

```text
Planned
```

## Lesson 03 — Terraform Commands

Topics:

* `terraform init`
* `terraform plan`
* `terraform apply`
* `terraform destroy`
* `terraform fmt`
* `terraform validate`

Status:

```text
Planned
```

## Lesson 04 — Variables and Outputs

Topics:

* input variables
* output values
* locals
* reusable configuration

Status:

```text
Planned
```

## Lesson 05 — Terraform Cloud Resource Lab

Topics:

* provision VM
* firewall rule
* output IP
* destroy safely
* documentation

Status:

```text
Planned
```

---

# Phase 11 — Monitoring, Logging and Security

## Lesson 01 — Linux Monitoring Basics

Topics:

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

Status:

```text
Planned
```

## Lesson 02 — Logs Deep Dive

Topics:

* `/var/log`
* `journalctl`
* service logs
* auth logs
* application logs
* log filtering
* log rotation concept

Status:

```text
Planned
```

## Lesson 03 — Uptime Kuma

Topics:

* uptime monitoring
* HTTP checks
* TCP checks
* website monitoring
* status pages
* notifications

Status:

```text
Planned
```

## Lesson 04 — Netdata

Topics:

* real-time server dashboard
* CPU/RAM/disk/network monitoring
* quick troubleshooting
* Netdata vs Prometheus/Grafana

Status:

```text
Planned
```

## Lesson 05 — Prometheus Basics

Topics:

* metrics
* targets
* scrape
* time-series data
* `prometheus.yml`
* Prometheus UI

Status:

```text
Planned
```

## Lesson 06 — Node Exporter

Topics:

* Linux server metrics
* CPU metrics
* memory metrics
* disk metrics
* filesystem metrics
* network metrics
* Prometheus target config

Status:

```text
Planned
```

## Lesson 07 — Grafana Dashboards

Topics:

* Grafana datasource
* Prometheus datasource
* dashboards
* panels
* queries
* CPU/RAM/disk/network visualization

Status:

```text
Planned
```

## Lesson 08 — Alerts

Topics:

* alert rules
* CPU alerts
* disk alerts
* uptime alerts
* service down alerts
* notification channels

Status:

```text
Planned
```

## Lesson 09 — Zabbix Intro

Topics:

* Zabbix server
* Zabbix agent
* hosts
* items
* triggers
* templates
* alerts
* enterprise monitoring concept

Status:

```text
Planned
```

## Lesson 10 — Cloud Monitoring Tools

Topics:

* Google Cloud Monitoring
* AWS CloudWatch
* Azure Monitor
* cloud metrics
* cloud alerts
* billing/resource monitoring

Status:

```text
Planned
```

## Lesson 11 — Basic Security Hardening

Topics:

* users
* groups
* sudo
* permissions
* updates
* SSH hardening
* firewall
* least privilege

Status:

```text
Planned
```

## Lesson 12 — SSH Security

Topics:

* SSH keys
* disable root login
* password login risks
* `sshd_config`
* allowed users
* SSH troubleshooting

Status:

```text
Planned
```

## Lesson 13 — Firewall and Fail2ban

Topics:

* `ufw`
* open ports
* allow/deny rules
* Fail2ban
* brute-force protection
* SSH protection

Status:

```text
Planned
```

## Lesson 14 — Monitoring and Security Portfolio Project

Topics:

* monitored Linux server
* Prometheus
* Node Exporter
* Grafana
* Uptime Kuma
* security hardening checklist
* alerts
* documentation
* screenshots

Status:

```text
Planned
```

---

# Phase 12 — Kubernetes

## Lesson 01 — Kubernetes Basics

Topics:

* cluster
* node
* pod
* deployment
* service
* namespace
* container orchestration

Status:

```text
Planned
```

## Lesson 02 — kubectl Basics

Topics:

* `kubectl get`
* `kubectl describe`
* `kubectl logs`
* `kubectl apply`
* `kubectl delete`

Status:

```text
Planned
```

## Lesson 03 — Deployments and Services

Topics:

* deployment YAML
* service YAML
* scaling
* rolling updates
* service exposure

Status:

```text
Planned
```

## Lesson 04 — ConfigMaps and Secrets

Topics:

* ConfigMap
* Secret
* environment variables
* safe configuration

Status:

```text
Planned
```

## Lesson 05 — Kubernetes Troubleshooting

Topics:

* pod errors
* image pull errors
* crash loop
* logs
* events
* service connectivity

Status:

```text
Planned
```

## Lesson 06 — Kubernetes Portfolio Lab

Topics:

* deploy app
* service
* config
* logs
* troubleshooting
* documentation

Status:

```text
Planned
```

---

# Phase 13 — Professional Portfolio

## Lesson 01 — Portfolio Repository Cleanup

Topics:

* README quality
* folder structure
* badges
* links
* screenshots
* documentation consistency

Status:

```text
Planned
```

## Lesson 02 — Documentation Site

Topics:

* MkDocs Material or Docusaurus
* English | Հայերեն tabs
* navigation
* lesson pages
* portfolio pages

Status:

```text
Planned
```

## Lesson 03 — Architecture Diagrams

Topics:

* diagrams
* network flows
* CI/CD flows
* monitoring architecture
* cloud architecture

Status:

```text
Planned
```

## Lesson 04 — Final Portfolio Projects

Topics:

* Linux admin lab
* Docker stack
* CI/CD pipeline
* cloud deployment
* Terraform infrastructure
* monitoring stack
* security checklist

Status:

```text
Planned
```

## Lesson 05 — Resume and GitHub Presentation

Topics:

* GitHub profile
* project descriptions
* resume bullets
* LinkedIn summary
* DevOps interview preparation

Status:

```text
Planned
```

---

# Final Portfolio Projects

## Project 01 — Linux Server Administration Lab

Includes:

* users
* groups
* permissions
* logs
* services
* monitoring basics
* security notes

## Project 02 — Networking Troubleshooting Lab

Includes:

* DNS
* ports
* curl
* ping
* firewall
* routing basics

## Project 03 — PostgreSQL DevOps Lab

Includes:

* PostgreSQL setup
* users
* permissions
* backups
* restore
* documentation

## Project 04 — Dockerized Application Stack

Includes:

* app container
* database container
* Nginx
* Docker Compose
* logs
* troubleshooting

## Project 05 — CI/CD Pipeline Lab

Includes:

* GitHub Actions
* automated checks
* build
* deploy simulation
* secrets handling

## Project 06 — Cloud VM Deployment Lab

Includes:

* cloud VM
* SSH
* firewall
* Nginx
* systemd
* SSL
* deployment validation

## Project 07 — Terraform Infrastructure Lab

Includes:

* Terraform project
* provider
* resources
* variables
* outputs
* safe destroy

## Project 08 — Monitoring and Security Stack

Includes:

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

```text
00 Setup                         Completed
01 Linux File System             Completed
02 Linux Paths                   Completed
03 File Operations               Completed
04 Log Reading                   Completed
05 Search and Filtering          Completed
06 Permissions and Ownership     Completed
07 Users, Groups and sudo        Completed
08 Processes and Monitoring      In Progress
```

