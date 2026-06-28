# Lesson 12 — Linux Review Lab

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-linux%20review%20lab-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը Phase 01 — Linux Fundamentals-ի վերջնական review lab-ն է։

Այս lab-ի նպատակը մինչև հիմա սովորած Linux հիմնական հմտությունները մեկտեղ օգտագործելն է։ Այստեղ նոր մեծ թեմա չենք ավելացնում, այլ կրկնում ենք filesystem navigation, paths, file operations, log reading, search/filtering, permissions, users/groups, process monitoring, package management, services և environment variables։

Այս lesson-ը ցույց է տալիս, որ ես կարողանում եմ Linux-ի հիմունքները օգտագործել միասին՝ որպես DevOps beginner-ի practical workflow։

---

## Learning Objectives

Այս դասից հետո ես կրկնեցի՝

* ինչպես navigate անել Linux filesystem-ում
* absolute և relative paths-ի տարբերությունը
* ինչպես ստեղծել, copy անել, move անել և կարդալ files
* ինչպես կարդալ logs common text commands-ով
* ինչպես search/filter անել log content-ը
* ինչպես կառավարել basic file permissions
* ինչպես ստուգել users, groups և sudo access
* ինչպես ստուգել running processes և system resources
* ինչպես օգտագործել package management basics-ը `apt`-ով
* ինչպես inspect անել Linux services-ը `systemctl`-ով
* ինչպես կարդալ service logs-ը `journalctl`-ով
* ինչպես ստուգել environment variables-ը
* ինչպես մտածել safe secret handling-ի մասին
* ինչպես validate անել ամբողջական Linux lab-ը
* ինչպես պատրաստել portfolio-ready Linux Fundamentals review

---

## Key Concepts

| Concept | Բացատրություն |
| ------- | ------------- |
| Filesystem | Linux directory structure, որը սկսվում է `/`-ից |
| Absolute path | Full path, որը սկսվում է `/`-ից |
| Relative path | Path, որը կախված է current working directory-ից |
| Log file | File, որտեղ գրանցվում են application կամ system events |
| Filtering | Command output-ից օգտակար information որոնել և առանձնացնել |
| Permission | File read, write և execute access control |
| User | Linux account, որով աշխատում են commands և ownership |
| Group | Users-ի collection permission management-ի համար |
| Process | Աշխատող program կամ command |
| Package | Installable software, որը կառավարվում է package manager-ով |
| Service | Background-ում աշխատող program, որը կառավարվում է system-ի կողմից |
| Environment variable | Key/value configuration, որը հասանելի է shell processes-ին |

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

Այս lab-ում ստեղծվում է հետևյալ structure-ը՝

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

Ստեղծել lesson directory՝

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-12-linux-review-lab
cd lesson-12-linux-review-lab
```

Ստեղծել review files՝

```bash
touch filesystem-review.txt paths-review.txt file-operations-review.txt logs-review.txt search-review.txt permissions-review.txt users-review.txt processes-review.txt packages-review.txt services-review.txt environment-review.txt final-validation.txt
```

---

## Filesystem Review

Կրկնել Linux filesystem locations-ը՝

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

Սա կրկնում է `/`, `/home`, `~`, `/etc`, `/var` և `/tmp`։

---

## Paths Review

Կրկնել absolute և relative paths-ը՝

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

Կարևոր կանոն՝

```text
Absolute path-ը սկսվում է /
Relative path-ը կախված է current directory-ից
```

---

## File Operations Review

Ստեղծել, copy անել, move անել և կարդալ files՝

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

Սա կրկնում է `mkdir`, `echo`, `>`, `>>`, `cp`, `mv`, `cat` և `find`։

---

## Log Reading Review

Կարդալ log files common commands-ով՝

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

Սա կրկնում է `cat`, `head`, `tail` և `wc -l`։

---

## Search and Filtering Review

Search/filter անել log content-ը՝

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

Սա կրկնում է `grep`, `grep -i`, `grep -n`, `grep -v` և `find`։

---

## Permissions Review

Ստեղծել script և secret-style file ճիշտ permissions-ով՝

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

Կարևոր permissions՝

| Permission | Օգտագործում |
| ---------- | ----------- |
| `755` | Executable scripts-ի համար |
| `600` | Private կամ secret files-ի համար |

---

## Users, Groups and sudo Review

Ստուգել current user և group information-ը՝

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

Սա կրկնում է `whoami`, `id`, `groups`, `sudo`, `getent passwd` և `getent group`։

---

## Processes and Monitoring Review

Ստեղծել, ստուգել և stop անել safe background process՝

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

Ստուգել, որ process-ը կանգնել է՝

```bash
ps -p "$(cat review-process.pid)"
```

Սա կրկնում է `ps`, `sleep`, `$!`, `kill`, `uptime`, `free -h`, `df -h` և `du -sh`։

---

## Package Management Review

Կրկնել package update և upgrade simulation՝

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

Optional package practice `tree`-ով՝

```bash
sudo apt install tree
tree --version
which tree
dpkg -l | grep tree
sudo apt remove tree
sudo apt autoremove
```

Եթե ուզում ենք `tree`-ն մնա installed՝

```bash
sudo apt install tree
```

---

## Services Review

Կրկնել `systemd`, `systemctl`, `cron` և `journalctl`՝

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

Եթե `cron` installed չէ՝

```bash
sudo apt update
sudo apt install cron
sudo systemctl start cron
sudo systemctl enable cron
```

---

## Environment Variables Review

Կրկնել environment variables, `$PATH`, shell variables և exported variables՝

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

Validate անել ամբողջ lab-ը՝

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

Վերադառնալ lesson folder՝

```bash
cd ~/devops-labs/01-linux-basics/lesson-12-linux-review-lab
```

Կարդալ բոլոր review outputs-ը՝

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

Այս review lab-ը կարևոր է, որովհետև DevOps աշխատանքում commands-ը հազվադեպ են օգտագործվում մեկուսացված ձևով։

Real troubleshooting-ի ժամանակ պետք է navigate անել directories, կարդալ logs, որոնել errors, ստուգել permissions, inspect անել users, ստուգել processes, disk usage, services և environment variables։

Այս lab-ը այդ skill-ները միացնում է մեկ practical workflow-ի մեջ։

---

## Important Safety Notes

Այս lab-ում կրկնվող safety rules՝

* չջնջել files առանց path-ը ստուգելու
* չօգտագործել `rm -rf` անզգույշ
* random processes չkill անել
* real secrets չդնել files-ի կամ GitHub-ի մեջ
* production services blindly restart չանել
* package upgrades-ը review անել մինչև apply անելը
* practice-ի համար օգտագործել safe test files և safe test processes

---

## Common Mistakes

| Սխալ | Խնդիր | Ճիշտ մոտեցում |
| ---- | ----- | ------------- |
| Շփոթել absolute և relative paths-ը | Command-ը կարող է սխալ տեղում ազդել | Ստուգել `pwd` և օգտագործել `realpath` |
| Պատահաբար overwrite անել file-ը `>`-ով | Existing content-ը կարող է կորել | Append-ի համար օգտագործել `>>` |
| Logs որոնել առանց line numbers | Issue-ն գտնելը դժվարանում է | Օգտագործել `grep -n` |
| Secret files-ին wide permissions տալ | Sensitive data-ն կարող է exposed լինել | Օգտագործել `chmod 600` |
| Unknown process kill անել | Կարող է կանգնել կարևոր service | Նախ ստուգել `ps -p PID` |
| Blind upgrade անել | Կարող է ազդել services-ի վրա | Օգտագործել `apt upgrade --simulate` |
| Services restart անել առանց logs ստուգելու | Real issue-ն կարող է չերևալ | Ստուգել `systemctl status` և `journalctl` |
| Secrets commit անել | Security risk | Օգտագործել `.gitignore` և secret managers |

---

## Linux Fundamentals Quick Reference

| Task | Command |
| ---- | ------- |
| Ցույց տալ current directory | `pwd` |
| List անել files | `ls -la` |
| Ցույց տալ absolute path | `realpath .` |
| Ստեղծել directory | `mkdir -p DIR` |
| Ստեղծել կամ overwrite անել file | `echo "text" > file` |
| Append անել file-ի մեջ | `echo "text" >> file` |
| Copy անել file | `cp source target` |
| Move անել file | `mv source target` |
| Կարդալ file | `cat file` |
| Առաջին lines | `head file` |
| Վերջին lines | `tail file` |
| Count անել lines | `wc -l file` |
| Search անել text | `grep "text" file` |
| Search անել line numbers-ով | `grep -n "text" file` |
| Find անել files | `find . -name "*.log"` |
| Փոխել permissions | `chmod 755 script.sh` |
| Ցույց տալ user | `whoami` |
| Ցույց տալ groups | `groups` |
| Ցույց տալ processes | `ps aux` |
| Ստուգել memory | `free -h` |
| Ստուգել disk | `df -h` |
| Ստուգել package upgrades | `apt list --upgradable` |
| Ստուգել service status | `systemctl status SERVICE --no-pager` |
| Ցույց տալ service logs | `journalctl -u SERVICE --no-pager -n 20` |
| List անել environment variables | `printenv` |
| Export անել variable | `export VAR=value` |
| Ջնջել variable | `unset VAR` |

---

## Validation

Այս lab-ը ստուգելու համար օգտագործվում են՝

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

Expected result՝

* lesson directory exists
* `notes.md` exists
* `notes.hy.md` exists
* բոլոր review output files-ը գոյություն ունեն
* filesystem review-ը completed է
* paths review-ը completed է
* file operations review-ը completed է
* logs review-ը completed է
* search review-ը completed է
* permissions review-ը completed է
* users review-ը completed է
* processes review-ը completed է
* package review-ը completed է
* services review-ը completed է
* environment variables review-ը completed է
* final validation output-ը saved է
* repository status-ը ստուգվել է commit-ից առաջ

---

## Quiz Review

| Question | Correct Answer | Status |
| -------- | -------------- | ------ |
| What is the purpose of this Linux Review Lab? | Կրկնել և միասին օգտագործել ամբողջ Linux Fundamentals phase-ի հիմնական skills-ը։ | Passed |
| What is the difference between absolute and relative paths? | Absolute path-ը սկսվում է root-ից `/`, իսկ relative path-ը կախված է current working directory-ից։ | Passed |
| Which command searches text in logs? | `grep` command-ն է օգտագործվում logs/files-ի մեջ text որոնելու համար։ | Passed |
| Which permission is appropriate for a private secret file? | Private կամ secret file-ի համար ճիշտ permission-ը `600` է։ | Passed |
| Why should a process be checked before killing it? | Process-ը պետք է նախ ստուգել, որ պատահաբար կարևոր service կամ application չկանգնեցնենք։ | Passed |
| Why should secrets not be committed to GitHub? | Secrets-ը GitHub-ում չպետք է commit անել անվտանգության պատճառով, որպեսզի passwords, tokens կամ API keys չհայտնվեն ուրիշների ձեռքում։ | Passed |
| Why is this review useful for DevOps work? | Այս review-ը օգնում է հասկանալ՝ արդյոք Linux skills-ը կարողանում ենք օգտագործել միասին real DevOps workflow-ում։ | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

Եթե file չկա, ստուգիր current directory-ն՝

```bash
pwd
ls -la
```

Եթե command-ը ազդում է սխալ տեղում, ստուգիր absolute path-ը՝

```bash
realpath .
```

Եթե log search-ը ոչինչ չի վերադարձնում, նախ ստուգիր file content-ը՝

```bash
cat review-files/app.log
```

Եթե script-ը չի աշխատում, ստուգիր permissions-ը՝

```bash
ls -l permissions-demo/health-check.sh
chmod 755 permissions-demo/health-check.sh
```

Եթե process-ը դեռ աշխատում է, նախ inspect արա՝

```bash
ps -p "$(cat review-process.pid)"
```

Եթե `tree` installed չէ, օգտագործիր `find` կամ install արա `tree`՝

```bash
find . -maxdepth 3 | sort
sudo apt install tree
```

Եթե service commands-ը WSL-ում fail են լինում, ստուգիր systemd-ը՝

```bash
ps -p 1 -o comm=
```

---

## Git Workflow

Lesson-ը ավարտելուց և quiz-ը անցնելուց հետո աշխատանքը պահվելու է Git-ով՝

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

Այս դասում ես կրկնեցի ամբողջ Linux Fundamentals phase-ը։

Ես practiced արեցի filesystem navigation, paths, file operations, log reading, searching/filtering, permissions, users/groups, process monitoring, package management, service inspection և environment variables։

Այս review lab-ը օգնեց առանձին lessons-ը միացնել մեկ practical DevOps workflow-ի մեջ։

---

## Status

Lesson completed, quiz passed, ready to commit and push.
