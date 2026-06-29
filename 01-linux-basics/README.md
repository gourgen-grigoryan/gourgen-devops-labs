<div align="center">

# 🐧 Linux Fundamentals

### A hands-on DevOps foundation module focused on practical Linux administration, troubleshooting, and system inspection.

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Phase](https://img.shields.io/badge/phase-01%20Linux%20Fundamentals-blue)
![Lessons](https://img.shields.io/badge/lessons-12-success)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)
![Focus](https://img.shields.io/badge/focus-DevOps%20Linux-orange)

</div>

---

## 📌 Module Overview

This module is the first completed phase of my DevOps learning roadmap.

It focuses on the Linux skills every DevOps Engineer needs before moving into networking, scripting, containers, CI/CD, cloud infrastructure, monitoring, and automation.

The goal of this module is not only to memorize Linux commands, but to practice them in realistic terminal workflows: navigating the filesystem, working with files, reading logs, searching errors, managing permissions, inspecting users, monitoring processes, working with packages, checking services, and using environment variables safely.

---

## 🎯 What This Module Demonstrates

By completing this Linux Fundamentals module, I practiced how to:

- Navigate and understand the Linux filesystem.
- Work confidently with absolute and relative paths.
- Create, copy, move, read, and organize files.
- Read and inspect logs using common Linux tools.
- Search and filter files and logs with `grep` and `find`.
- Manage basic permissions and ownership.
- Inspect users, groups, and sudo access.
- Monitor running processes and system resources.
- Use `apt` for package management.
- Inspect and manage Linux services with `systemctl`.
- Read service logs with `journalctl`.
- Use shell variables and environment variables.
- Understand safe handling of secrets and `.env` files.
- Combine all Linux basics into a final review lab.

---

## 🧭 Learning Path

| # | Lesson | Focus | Documentation |
|---:|---|---|---|
| 01 | Linux File System | Linux directory structure and core filesystem concepts | [notes.md](./lesson-01-filesystem/notes.md)<br>[notes.hy.md](./lesson-01-filesystem/notes.hy.md) |
| 02 | Linux Paths | Absolute paths, relative paths, and navigation | [notes.md](./lesson-02-paths/notes.md)<br>[notes.hy.md](./lesson-02-paths/notes.hy.md) |
| 03 | File Operations | Creating, copying, moving, reading, and organizing files | [notes.md](./lesson-03-file-operations/notes.md)<br>[notes.hy.md](./lesson-03-file-operations/notes.hy.md) |
| 04 | Log Reading Basics | Reading logs with `cat`, `head`, `tail`, and related tools | [notes.md](./lesson-04-log-reading/notes.md)<br>[notes.hy.md](./lesson-04-log-reading/notes.hy.md) |
| 05 | Search and Filtering | Finding useful information with `grep`, `find`, and filters | [notes.md](./lesson-05-search-filtering/notes.md)<br>[notes.hy.md](./lesson-05-search-filtering/notes.hy.md) |
| 06 | Permissions and Ownership | File permissions, executable scripts, and secure files | [notes.md](./lesson-06-permissions-ownership/notes.md)<br>[notes.hy.md](./lesson-06-permissions-ownership/notes.hy.md) |
| 07 | Users, Groups and sudo | User identity, groups, sudo access, and account inspection | [notes.md](./lesson-07-users-groups-sudo/notes.md)<br>[notes.hy.md](./lesson-07-users-groups-sudo/notes.hy.md) |
| 08 | Processes and System Monitoring | Process inspection, system resources, disk, memory, and uptime | [notes.md](./lesson-08-processes-monitoring/notes.md)<br>[notes.hy.md](./lesson-08-processes-monitoring/notes.hy.md) |
| 09 | Package Management | `apt update`, install, remove, purge, autoremove, and upgrade simulation | [notes.md](./lesson-09-package-management/notes.md)<br>[notes.hy.md](./lesson-09-package-management/notes.hy.md) |
| 10 | Linux Services Basics | `systemctl`, service status, start/stop/restart, enable/disable, and logs | [notes.md](./lesson-10-linux-services-basics/notes.md)<br>[notes.hy.md](./lesson-10-linux-services-basics/notes.hy.md) |
| 11 | Environment Variables | `printenv`, `$PATH`, `export`, `unset`, `.bashrc`, and safe secrets | [notes.md](./lesson-11-environment-variables/notes.md)<br>[notes.hy.md](./lesson-11-environment-variables/notes.hy.md) |
| 12 | Linux Review Lab | Full practical review of the entire Linux Fundamentals phase | [notes.md](./lesson-12-linux-review-lab/notes.md)<br>[notes.hy.md](./lesson-12-linux-review-lab/notes.hy.md) |

---

## 🧪 Final Review Lab

The final lesson, **Lesson 12 — Linux Review Lab**, combines the full module into one practical terminal workflow.

It reviews:

```text
filesystem navigation
absolute and relative paths
file operations
log reading
search and filtering
permissions
users, groups and sudo
process monitoring
package management
service inspection
environment variables
final validation
```

This lab is the proof that the individual Linux lessons were not learned separately only, but can be used together in a real DevOps-style workflow.

---

## 🛠️ Tools and Commands Practiced

| Category | Commands |
|---|---|
| Filesystem | `pwd`, `ls`, `cd`, `realpath`, `tree` |
| File Operations | `mkdir`, `touch`, `cat`, `cp`, `mv`, `echo`, `tee` |
| Log Reading | `cat`, `head`, `tail`, `wc -l` |
| Search and Filtering | `grep`, `grep -i`, `grep -n`, `grep -v`, `find` |
| Permissions | `chmod`, `ls -l`, `stat` |
| Users and Groups | `whoami`, `id`, `groups`, `getent`, `sudo` |
| Processes | `ps`, `kill`, `sleep`, `uptime` |
| System Resources | `free -h`, `df -h`, `du -sh` |
| Packages | `apt update`, `apt install`, `apt remove`, `apt purge`, `apt autoremove`, `apt upgrade --simulate` |
| Services | `systemctl`, `journalctl` |
| Environment | `printenv`, `echo $VAR`, `export`, `unset`, `which`, `source` |
| Git Validation | `git status`, `git add`, `git commit`, `git push` |

---

## 📁 Repository Structure

```text
01-linux-basics/
├── README.md
├── lesson-01-filesystem/
│   ├── notes.md
│   └── notes.hy.md
├── lesson-02-paths/
│   ├── notes.md
│   └── notes.hy.md
├── lesson-03-file-operations/
│   ├── notes.md
│   ├── notes.hy.md
│   ├── backups/
│   ├── configs/
│   └── logs/
├── lesson-04-log-reading/
│   ├── notes.md
│   ├── notes.hy.md
│   └── logs/
├── lesson-05-search-filtering/
│   ├── notes.md
│   ├── notes.hy.md
│   ├── system.log
│   └── users.txt
├── lesson-06-permissions-ownership/
│   ├── notes.md
│   ├── notes.hy.md
│   ├── configs/
│   ├── logs/
│   ├── scripts/
│   └── secrets/
├── lesson-07-users-groups-sudo/
│   ├── notes.md
│   ├── notes.hy.md
│   └── *.txt
├── lesson-08-processes-monitoring/
│   ├── notes.md
│   ├── notes.hy.md
│   └── *.txt
├── lesson-09-package-management/
│   ├── notes.md
│   └── notes.hy.md
├── lesson-10-linux-services-basics/
│   ├── notes.md
│   ├── notes.hy.md
│   └── *.txt
├── lesson-11-environment-variables/
│   ├── notes.md
│   ├── notes.hy.md
│   └── *.txt
└── lesson-12-linux-review-lab/
    ├── notes.md
    ├── notes.hy.md
    ├── review-files/
    ├── permissions-demo/
    └── *.txt
```

---

## 🌍 Documentation Languages

Each lesson includes two documentation files:

| File | Purpose |
|---|---|
| `notes.md` | Clean English portfolio documentation |
| `notes.hy.md` | Armenian learning and explanation version |

This structure allows the repository to be useful both as a professional DevOps portfolio and as a personal learning archive.

---

## 🔐 Security Practices Covered

Security-focused habits practiced in this module include:

- Checking paths before changing or deleting files.
- Understanding file permissions before making files executable.
- Using `chmod 600` for private or secret-style files.
- Avoiding unsafe use of `rm -rf`.
- Checking processes before stopping them.
- Reviewing package upgrades before applying them.
- Checking services and logs before restarting services.
- Avoiding committing real secrets to GitHub.
- Understanding why `.env` files should be protected.

---

## 🚀 DevOps Relevance

Linux is the base layer for many DevOps tools and environments.

This module prepares the foundation for:

- Networking fundamentals
- Bash scripting
- Git and GitHub workflows
- Docker and containers
- CI/CD pipelines
- Cloud servers
- Monitoring and logging
- Infrastructure automation
- Production troubleshooting

---

## ✅ Module Completion Status

| Phase | Status |
|---|---|
| Linux Fundamentals | ✅ Completed |
| Lessons Completed | ✅ 12 / 12 |
| Final Review Lab | ✅ Completed |
| Portfolio Documentation | ✅ Completed |
| Ready for Next Phase | ✅ Yes — Networking with CCNA-Level Foundations |

---

## 🏁 Next Step

The next phase of the roadmap is:

```text
Phase 02 — Networking with CCNA-Level Foundations
```

This Linux module provides the base needed to understand networking commands, servers, ports, DNS, SSH, firewalls, routing basics, and future cloud infrastructure work.

---

<div align="center">

### Built as part of a practical DevOps learning roadmap.

**Linux Fundamentals → Networking → Scripting → Git → Containers → CI/CD → Cloud → Monitoring → Automation**

</div>
