# Lesson 12 — Linux Review Lab

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-linux%20review%20lab-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson is the final review lab for Phase 01 — Linux Fundamentals.

The goal of this lab is to review and combine the core Linux skills learned in previous lessons. Instead of learning one new command group, this lab connects filesystem navigation, path usage, file operations, log reading, search and filtering, permissions, users and groups, process monitoring, package management, service inspection and environment variables into one practical DevOps-style workflow.

This lesson helps confirm that I can use Linux fundamentals together in a realistic terminal lab.

---

## Learning Objectives

By completing this lesson, I reviewed how to:

* navigate the Linux filesystem
* understand absolute and relative paths
* create, copy, move and read files
* read logs using common text commands
* search and filter log content
* manage basic file permissions
* inspect users, groups and sudo access
* inspect running processes and system resources
* use package management basics with `apt`
* inspect Linux services with `systemctl`
* read service logs with `journalctl`
* inspect environment variables
* understand safe secret handling
* validate a complete Linux lab
* prepare a portfolio-ready Linux Fundamentals review

---

## Key Concepts

| Concept | Meaning |
| ------- | ------- |
| Filesystem | Linux directory structure starting from `/` |
| Absolute path | Full path starting from `/` |
| Relative path | Path based on the current working directory |
| Log file | File that records application or system events |
| Filtering | Searching and extracting useful information from command output |
| Permission | Access control for reading, writing and executing files |
| User | Linux account used to run commands and own files |
| Group | Collection of users used for permission management |
| Process | Running program or command |
| Package | Installable software managed by a package manager |
| Service | Background program managed by the system |
| Environment variable | Key/value configuration available to shell processes |

---

## Commands Reviewed

| Area | Commands |
| ---- | -------- |
| Filesystem and paths | `pwd`, `ls`, `realpath`, `cd` |
| File operations | `mkdir`, `touch`, `echo`, `cat`, `cp`, `mv`, `find` |
| Log reading | `cat`, `head`, `tail`, `wc -l` |
| Search and filtering | `grep`, `grep -i`, `grep -n`, `grep -v`, `find` |
| Permissions | `chmod`, `ls -l`, `stat` |
| Users and groups | `whoami`, `id`, `groups`, `sudo`, `getent` |
| Processes and monitoring | `ps`, `kill`, `uptime`, `free -h`, `df -h`, `du -sh` |
| Package management | `apt update`, `apt list --upgradable`, `apt upgrade --simulate`, `apt install`, `apt remove`, `apt autoremove` |
| Services | `systemctl`, `journalctl` |
| Environment variables | `printenv`, `echo $VAR`, `export`, `unset`, `which` |
| Validation | `tree`, `find`, `git status` |

---

## Lab Structure

In this lab, I created the following structure:

```text
lesson-12-linux-review-lab/
|-- environment-review.txt
|-- file-operations-review.txt
|-- filesystem-review.txt
|-- final-validation.txt
|-- logs-review.txt
|-- notes.hy.md
|-- notes.md
|-- packages-review.txt
|-- paths-review.txt
|-- permissions-review.txt
|-- processes-review.txt
|-- review-files/
|   |-- app.log
|   `-- archive/
|       `-- app-archived.log
|-- search-review.txt
|-- services-review.txt
`-- users-review.txt
```

---

## Practical Commands Used

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-12-linux-review-lab
cd lesson-12-linux-review-lab
```

Create review files:

```bash
touch filesystem-review.txt paths-review.txt file-operations-review.txt logs-review.txt search-review.txt permissions-review.txt users-review.txt processes-review.txt packages-review.txt services-review.txt environment-review.txt final-validation.txt
```

---

## Filesystem Review

Review Linux filesystem locations:

```bash
{
  echo "Current directory:"
  pwd

  echo
  echo "Home directory:"
  echo "$HOME"

  echo
  echo "Root directory sample:"
  ls /

  echo
  echo "/etc sample:"
  ls /etc | head

  echo
  echo "/var sample:"
  ls /var | head

  echo
  echo "/tmp sample:"
  ls /tmp | head
} | tee filesystem-review.txt
```

This reviews `/`, `/home`, `~`, `/etc`, `/var` and `/tmp`.

---

## Paths Review

Review absolute and relative paths:

```bash
{
  echo "PWD:"
  pwd

  echo
  echo "Absolute path to this lesson:"
  realpath .

  echo
  echo "Parent directory:"
  realpath ..

  echo
  echo "Home shortcut:"
  echo ~

  echo
  echo "List parent directory:"
  ls ..
} | tee paths-review.txt
```

Important rule:

```text
Absolute paths start from /
Relative paths depend on the current directory
```

---

## File Operations Review

Create, copy, move and read files:

```bash
mkdir -p review-files/archive

echo "Linux review lab" > review-files/app.log
echo "INFO app started" >> review-files/app.log
echo "ERROR database connection failed" >> review-files/app.log
echo "INFO retrying connection" >> review-files/app.log
echo "WARN disk usage high" >> review-files/app.log

cp review-files/app.log review-files/app-copy.log
mv review-files/app-copy.log review-files/archive/app-archived.log

{
  echo "Review files structure:"
  find review-files -maxdepth 3 -type f | sort

  echo
  echo "Main log content:"
  cat review-files/app.log

  echo
  echo "Archived log content:"
  cat review-files/archive/app-archived.log
} | tee file-operations-review.txt
```

This reviews `mkdir`, `echo`, `>`, `>>`, `cp`, `mv`, `cat` and `find`.

---

## Log Reading Review

Read log files with common commands:

```bash
{
  echo "Full log:"
  cat review-files/app.log

  echo
  echo "First 3 lines:"
  head -n 3 review-files/app.log

  echo
  echo "Last 3 lines:"
  tail -n 3 review-files/app.log

  echo
  echo "Line count:"
  wc -l review-files/app.log
} | tee logs-review.txt
```

This reviews `cat`, `head`, `tail` and `wc -l`.

---

## Search and Filtering Review

Search and filter log content:

```bash
{
  echo "Find ERROR lines:"
  grep "ERROR" review-files/app.log

  echo
  echo "Find error case-insensitive:"
  grep -i "error" review-files/app.log

  echo
  echo "Find ERROR with line numbers:"
  grep -n "ERROR" review-files/app.log

  echo
  echo "Show lines without INFO:"
  grep -v "INFO" review-files/app.log

  echo
  echo "Find all .log files:"
  find . -name "*.log"
} | tee search-review.txt
```

This reviews `grep`, `grep -i`, `grep -n`, `grep -v` and `find`.

---

## Permissions Review

Create a script and a secret-style file with correct permissions:

```bash
mkdir -p permissions-demo

cat > permissions-demo/health-check.sh <<'EOF'
#!/bin/bash
echo "Health check OK"
EOF

echo "SECRET_TOKEN=demo-only-not-real-secret" > permissions-demo/secret.env

chmod 755 permissions-demo/health-check.sh
chmod 600 permissions-demo/secret.env

{
  echo "Permissions:"
  ls -l permissions-demo

  echo
  echo "Run script:"
  ./permissions-demo/health-check.sh

  echo
  echo "Secret file permission should be 600:"
  stat -c "%a %n" permissions-demo/secret.env
} | tee permissions-review.txt
```

Important permissions:

| Permission | Use case |
| ---------- | -------- |
| `755` | Executable scripts |
| `600` | Private or secret files |

---

## Users, Groups and sudo Review

Inspect current user and group information:

```bash
{
  echo "Current user:"
  whoami

  echo
  echo "User and group IDs:"
  id

  echo
  echo "Groups:"
  groups

  echo
  echo "Sudo check:"
  sudo -v && echo "sudo access OK"

  echo
  echo "User entry:"
  getent passwd "$(whoami)"

  echo
  echo "Primary group entry:"
  getent group "$(id -gn)"
} | tee users-review.txt
```

This reviews `whoami`, `id`, `groups`, `sudo`, `getent passwd` and `getent group`.

---

## Processes and Monitoring Review

Create, inspect and stop a safe background process:

```bash
sleep 300 &
echo $! > review-process.pid

{
  echo "Current shell PID:"
  echo $$

  echo
  echo "Demo process PID:"
  cat review-process.pid

  echo
  echo "Process details:"
  ps -p "$(cat review-process.pid)"

  echo
  echo "Top processes sample:"
  ps aux | head

  echo
  echo "System uptime:"
  uptime

  echo
  echo "Memory usage:"
  free -h

  echo
  echo "Disk usage:"
  df -h

  echo
  echo "Current folder size:"
  du -sh .
} | tee processes-review.txt

kill "$(cat review-process.pid)"
```

Verify that the process stopped:

```bash
ps -p "$(cat review-process.pid)"
```

This reviews `ps`, `sleep`, `$!`, `kill`, `uptime`, `free -h`, `df -h` and `du -sh`.

---

## Package Management Review

Review package update and upgrade simulation:

```bash
{
  echo "APT update preview:"
  sudo apt update

  echo
  echo "Upgradable packages:"
  apt list --upgradable 2>/dev/null | head

  echo
  echo "Upgrade simulation:"
  sudo apt upgrade --simulate | head -n 30
} | tee packages-review.txt
```

Optional package practice with `tree`:

```bash
sudo apt install tree
tree --version
which tree
dpkg -l | grep tree
sudo apt remove tree
sudo apt autoremove
```

If `tree` should remain installed:

```bash
sudo apt install tree
```

---

## Services Review

Review `systemd`, `systemctl`, `cron` and `journalctl`:

```bash
{
  echo "PID 1:"
  ps -p 1 -o comm=

  echo
  echo "systemctl version:"
  systemctl --version | head -n 5

  echo
  echo "Running services sample:"
  systemctl list-units --type=service --state=running --no-pager | head -n 20

  echo
  echo "Cron active state:"
  systemctl is-active cron 2>/dev/null || echo "cron active state unavailable"

  echo
  echo "Cron enabled state:"
  systemctl is-enabled cron 2>/dev/null || echo "cron enabled state unavailable"

  echo
  echo "Cron logs sample:"
  journalctl -u cron --no-pager -n 10 2>/dev/null || echo "cron logs unavailable"
} | tee services-review.txt
```

If `cron` is not installed:

```bash
sudo apt update
sudo apt install cron
sudo systemctl start cron
sudo systemctl enable cron
```

---

## Environment Variables Review

Review environment variables, `$PATH`, shell variables and exported variables:

```bash
{
  echo "Environment variables sample:"
  printenv | head -n 20

  echo
  echo "HOME USER SHELL:"
  echo "HOME=$HOME"
  echo "USER=$USER"
  echo "SHELL=$SHELL"

  echo
  echo "PATH:"
  echo "$PATH"

  echo
  echo "Command paths:"
  which ls
  which bash

  echo
  echo "Shell variable test:"
  REVIEW_VAR="linux-review"
  echo "Current shell sees REVIEW_VAR=$REVIEW_VAR"

  echo
  echo "Child shell before export:"
  bash -c 'echo "Child shell sees REVIEW_VAR=$REVIEW_VAR"'

  echo
  echo "Child shell after export:"
  export REVIEW_VAR="linux-review"
  bash -c 'echo "Child shell sees REVIEW_VAR=$REVIEW_VAR"'

  echo
  echo "Unset variable:"
  unset REVIEW_VAR
  echo "After unset REVIEW_VAR=$REVIEW_VAR"
} | tee environment-review.txt
```

---

## Final Validation

Validate the full lab:

```bash
{
  echo "Final Linux Review Lab Validation"
  echo "================================="

  echo
  echo "Current path:"
  pwd

  echo
  echo "Files:"
  ls -la

  echo
  echo "Directory tree:"
  tree -a --charset=ascii . 2>/dev/null || find . -maxdepth 3 | sort

  echo
  echo "Review files created:"
  ls *.txt

  echo
  echo "Git status:"
  cd ~/devops-labs
  git status --short
} | tee ~/devops-labs/01-linux-basics/lesson-12-linux-review-lab/final-validation.txt
```

Return to the lesson folder:

```bash
cd ~/devops-labs/01-linux-basics/lesson-12-linux-review-lab
```

Read all review outputs:

```bash
cat filesystem-review.txt
cat paths-review.txt
cat file-operations-review.txt
cat logs-review.txt
cat search-review.txt
cat permissions-review.txt
cat users-review.txt
cat processes-review.txt
cat packages-review.txt
cat services-review.txt
cat environment-review.txt
cat final-validation.txt
```

---

## Why This Review Lab Matters in DevOps

This review lab matters because DevOps work rarely uses commands in isolation.

A real troubleshooting session may require navigating directories, reading logs, searching errors, checking permissions, inspecting users, reviewing processes, checking disk usage, verifying services and validating environment variables.

This lab connects those skills into one practical workflow.

---

## Important Safety Notes

Important safety rules reviewed in this lab:

* do not delete files without checking paths first
* do not use `rm -rf` carelessly
* do not kill random processes
* do not expose real secrets in files or GitHub
* do not restart production services blindly
* review package upgrades before applying them
* use safe test files and safe test processes for practice

---

## Common Mistakes

| Mistake | Problem | Correct Practice |
| ------- | ------- | ---------------- |
| Confusing absolute and relative paths | Commands may affect the wrong location | Check `pwd` and use `realpath` |
| Overwriting files with `>` accidentally | Existing content can be lost | Use `>>` when appending |
| Searching logs without line numbers | Harder to locate issues | Use `grep -n` |
| Giving secret files wide permissions | Sensitive data may be exposed | Use `chmod 600` |
| Killing unknown processes | Can stop important services | Check with `ps -p PID` first |
| Running upgrades blindly | Can affect services | Use `apt upgrade --simulate` |
| Restarting services without logs | Can hide the real issue | Check `systemctl status` and `journalctl` |
| Committing secrets | Security risk | Use `.gitignore` and secret managers |

---

## Linux Fundamentals Quick Reference

| Task | Command |
| ---- | ------- |
| Show current directory | `pwd` |
| List files | `ls -la` |
| Show absolute path | `realpath .` |
| Create directory | `mkdir -p DIR` |
| Create or overwrite file | `echo "text" > file` |
| Append to file | `echo "text" >> file` |
| Copy file | `cp source target` |
| Move file | `mv source target` |
| Read file | `cat file` |
| First lines | `head file` |
| Last lines | `tail file` |
| Count lines | `wc -l file` |
| Search text | `grep "text" file` |
| Search with line numbers | `grep -n "text" file` |
| Find files | `find . -name "*.log"` |
| Change permissions | `chmod 755 script.sh` |
| Show user | `whoami` |
| Show groups | `groups` |
| Show processes | `ps aux` |
| Check memory | `free -h` |
| Check disk | `df -h` |
| Check package upgrades | `apt list --upgradable` |
| Check service status | `systemctl status SERVICE --no-pager` |
| Show service logs | `journalctl -u SERVICE --no-pager -n 20` |
| List environment variables | `printenv` |
| Export variable | `export VAR=value` |
| Remove variable | `unset VAR` |

---

## Validation

Commands used to validate this lab:

```bash
pwd
tree -a --charset=ascii
cat filesystem-review.txt
cat paths-review.txt
cat file-operations-review.txt
cat logs-review.txt
cat search-review.txt
cat permissions-review.txt
cat users-review.txt
cat processes-review.txt
cat packages-review.txt
cat services-review.txt
cat environment-review.txt
cat final-validation.txt
git status
```

Expected result:

* lesson directory exists
* `notes.md` exists
* `notes.hy.md` exists
* all review output files exist
* filesystem review was completed
* paths review was completed
* file operations review was completed
* logs review was completed
* search review was completed
* permissions review was completed
* users review was completed
* processes review was completed
* package review was completed
* services review was completed
* environment variables review was completed
* final validation output was saved
* repository status was checked before commit

---

## Quiz Review

| Question | Correct Answer | Status |
| -------- | -------------- | ------ |
| What is the purpose of this Linux Review Lab? | To review and use the main Linux Fundamentals skills together in one practical lab. | Passed |
| What is the difference between absolute and relative paths? | An absolute path starts from the root directory `/`, while a relative path depends on the current working directory. | Passed |
| Which command searches text in logs? | `grep` searches text in logs and files. | Passed |
| Which permission is appropriate for a private secret file? | `600` is appropriate for a private or secret file. | Passed |
| Why should a process be checked before killing it? | A process should be checked first to avoid stopping an important service or application. | Passed |
| Why should secrets not be committed to GitHub? | Secrets should not be committed for security reasons because passwords, tokens or API keys can be exposed. | Passed |
| Why is this review useful for DevOps work? | It connects individual Linux skills into one practical troubleshooting and validation workflow. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

If a file is missing, check the current directory:

```bash
pwd
ls -la
```

If a command affects the wrong place, check the absolute path:

```bash
realpath .
```

If a log search returns nothing, check the file content first:

```bash
cat review-files/app.log
```

If a script does not run, check permissions:

```bash
ls -l permissions-demo/health-check.sh
chmod 755 permissions-demo/health-check.sh
```

If a process is still running, inspect it before stopping:

```bash
ps -p "$(cat review-process.pid)"
```

If `tree` is not installed, use `find` or install `tree`:

```bash
find . -maxdepth 3 | sort
sudo apt install tree
```

If service commands fail in WSL, check systemd:

```bash
ps -p 1 -o comm=
```

---

## Git Workflow

After completing the lesson and passing the quiz, the work will be saved using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-12-linux-review-lab ROADMAP.md
git commit -m "Complete Linux fundamentals review lab"
git push
git status
```

---

## What I Learned

In this lesson, I reviewed the full Linux Fundamentals phase.

I practiced filesystem navigation, paths, file operations, log reading, searching and filtering, permissions, users and groups, process monitoring, package management, service inspection and environment variables.

This review lab helped connect the individual lessons into a single practical DevOps workflow.

---

## Status

Lesson completed, quiz passed, ready to commit and push.
