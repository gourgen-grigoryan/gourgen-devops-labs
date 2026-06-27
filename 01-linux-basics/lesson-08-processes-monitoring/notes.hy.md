# Lesson 08 — Processes and System Monitoring

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-processes%20and%20monitoring-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը բացատրում է Linux process-ները և system monitoring-ի հիմնական հրամանները։

DevOps Engineer-ը պետք է կարողանա հասկանալ՝ ինչ process-ներ են աշխատում server-ում, որ process-ն է օգտագործում CPU/RAM, արդյոք disk-ը լցվում է, որքան RAM կա, որքան է system uptime-ը և ինչպես անվտանգ stop անել test process-ը։

Այս դասում օգտագործվում են `ps`, `top`, `htop`, `kill`, `uptime`, `free`, `df`, `du` հրամանները։

---

## Learning Objectives

Այս դասից հետո ես սովորեցի՝

* ինչ է Linux process-ը
* ինչ է PID-ը
* ինչպես տեսնել running process-ները
* ինչպես տեսնել current shell-ի PID-ը
* ինչպես ստեղծել safe background process
* ինչպես ստուգել process-ը PID-ով
* ինչպես անվտանգ stop անել process-ը
* ինչպես ստուգել system uptime-ը
* ինչպես ստուգել RAM usage-ը
* ինչպես ստուգել disk usage-ը
* ինչպես ստուգել folder-ի չափը
* ինչպես օգտագործել `top` և `htop`
* ինչու monitoring-ը կարևոր է DevOps-ում

---

## Key Concepts

| Concept            | Բացատրություն                          |
| ------------------ | -------------------------------------- |
| Process            | Աշխատող ծրագիր կամ command             |
| PID                | Process ID՝ process-ի unique number-ը  |
| Background process | Process, որը աշխատում է background-ում |
| CPU usage          | Processor-ի օգտագործման չափը           |
| Memory usage       | RAM-ի օգտագործման չափը                 |
| Disk usage         | Disk/storage-ի օգտագործման չափը        |
| Load average       | System workload-ի ընդհանուր ցուցանիշ   |

---

## Commands Learned

| Command     | Նպատակ                                      | Օրինակ       |
| ----------- | ------------------------------------------- | ------------ |
| `ps`        | Ցույց է տալիս current shell-ի process-ները  | `ps`         |
| `ps aux`    | Ցույց է տալիս մանրամասն process list        | `ps aux`     |
| `ps -p PID` | Ցույց է տալիս կոնկրետ process-ը PID-ով      | `ps -p 1234` |
| `top`       | Բացում է live process monitor               | `top`        |
| `htop`      | Ավելի հարմար live process monitor           | `htop`       |
| `kill PID`  | Stop է անում process-ը PID-ով               | `kill 1234`  |
| `uptime`    | Ցույց է տալիս uptime և load average         | `uptime`     |
| `free -h`   | Ցույց է տալիս RAM usage-ը                   | `free -h`    |
| `df -h`     | Ցույց է տալիս filesystem disk usage-ը       | `df -h`      |
| `du -sh .`  | Ցույց է տալիս current folder-ի չափը         | `du -sh .`   |
| `echo $$`   | Ցույց է տալիս current shell PID-ը           | `echo $$`    |
| `echo $!`   | Ցույց է տալիս last background process PID-ը | `echo $!`    |

---

## Lab Structure

Այս lab-ում ստեղծվում է հետևյալ structure-ը՝

```text
lesson-08-processes-monitoring/
|-- demo-process.txt
|-- disk-usage.txt
|-- disk.txt
|-- memory.txt
|-- notes.hy.md
|-- notes.md
|-- process-details.txt
|-- process-list.txt
`-- uptime.txt
```

---

## Practical Commands Used

Ստեղծել lesson directory՝

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-08-processes-monitoring
cd lesson-08-processes-monitoring
```

Ստեղծել lab files՝

```bash
touch process-list.txt process-details.txt uptime.txt memory.txt disk.txt disk-usage.txt demo-process.txt
```

Տեսնել current shell-ի process-ները՝

```bash
ps
```

Տեսնել ավելի մանրամասն process list՝

```bash
ps aux | head
```

Պահել process list-ը ֆայլի մեջ՝

```bash
ps aux | head -n 10 > process-list.txt
cat process-list.txt
```

Տեսնել current shell PID-ը՝

```bash
echo $$
```

Պահել current shell PID-ը՝

```bash
echo "Current shell PID: $$" > process-details.txt
cat process-details.txt
```

Ստեղծել safe test background process՝

```bash
sleep 300 &
```

Պահել վերջին background process-ի PID-ը՝

```bash
echo $! > demo-process.pid
cat demo-process.pid
```

Ստուգել demo process-ը PID-ով՝

```bash
ps -p $(cat demo-process.pid)
```

Պահել demo process info-ն՝

```bash
ps -p $(cat demo-process.pid) > demo-process.txt
cat demo-process.txt
```

Stop անել demo process-ը՝

```bash
kill $(cat demo-process.pid)
```

Ստուգել, որ demo process-ը կանգնել է՝

```bash
ps -p $(cat demo-process.pid)
```

Ստուգել uptime-ը՝

```bash
uptime
```

Պահել uptime output-ը՝

```bash
uptime > uptime.txt
cat uptime.txt
```

Ստուգել memory usage-ը՝

```bash
free -h
```

Պահել memory output-ը՝

```bash
free -h > memory.txt
cat memory.txt
```

Ստուգել disk usage-ը՝

```bash
df -h
```

Պահել disk output-ը՝

```bash
df -h > disk.txt
cat disk.txt
```

Ստուգել current directory-ի չափը՝

```bash
du -sh .
```

Պահել directory size output-ը՝

```bash
du -sh . > disk-usage.txt
cat disk-usage.txt
```

Բացել live monitor՝

```bash
top
```

Դուրս գալ `top`-ից՝

```text
q
```

Բացել `htop`, եթե installed է՝

```bash
htop
```

Դուրս գալ `htop`-ից՝

```text
F10
```

կամ՝

```text
q
```

---

## Process Explanation

Process-ը Linux-ում աշխատող ծրագիր կամ command է։

Օրինակ՝ երբ terminal-ում command ես աշխատացնում, Linux-ը դրա համար ստեղծում է process։

Process կարող է լինել՝

* shell session
* command
* background job
* system service
* web server
* database server
* monitoring agent

Ամեն process ունի իր unique number-ը՝ PID։

---

## PID Explanation

PID նշանակում է Process ID։

Linux-ը PID-ով ճանաչում և կառավարում է process-ները։

Օրինակ՝

```bash
echo $$
```

ցույց է տալիս current shell-ի PID-ը։

Իսկ՝

```bash
sleep 300 &
echo $!
```

ցույց է տալիս վերջին background process-ի PID-ը։

---

## `ps` Explanation

`ps` հրամանը ցույց է տալիս process-ները։

Basic տարբերակ՝

```bash
ps
```

Մանրամասն տարբերակ՝

```bash
ps aux
```

Միայն առաջին տողերը՝

```bash
ps aux | head
```

Կոնկրետ process PID-ով՝

```bash
ps -p PID
```

Օրինակ՝

```bash
ps -p $(cat demo-process.pid)
```

---

## `top` and `htop` Explanation

`top`-ը live process monitor է։

Այն ցույց է տալիս՝

* process-ներ
* CPU usage
* memory usage
* load average
* PID-եր

Բացել՝

```bash
top
```

Դուրս գալ՝

```text
q
```

`htop`-ը ավելի user-friendly տարբերակ է։

Բացել՝

```bash
htop
```

Դուրս գալ՝

```text
F10
```

կամ՝

```text
q
```

---

## `kill` Explanation

`kill` command-ը signal է ուղարկում process-ին։

Հաճախ այն օգտագործվում է process-ը stop անելու համար։

Օրինակ՝

```bash
kill 1234
```

Այս lab-ում `kill` օգտագործում ենք միայն մեր ստեղծած safe demo process-ի վրա՝

```bash
sleep 300 &
echo $! > demo-process.pid
kill $(cat demo-process.pid)
```

Պետք չէ պատահական PID kill անել, որովհետև կարող ես կանգնեցնել կարևոր service կամ application։

---

## `uptime` Explanation

`uptime` ցույց է տալիս՝ system-ը որքան ժամանակ է աշխատում։

```bash
uptime
```

Սովորաբար ցույց է տալիս՝

* current time
* system uptime
* logged-in users
* load average

---

## `free` Explanation

`free` ցույց է տալիս memory/RAM usage-ը։

```bash
free -h
```

Այստեղ կարելի է տեսնել՝

* total memory
* used memory
* free memory
* available memory
* swap usage

---

## `df` Explanation

`df` ցույց է տալիս filesystem disk usage-ը։

```bash
df -h
```

Այս command-ը օգնում է հասկանալ՝

* որքան disk կա
* որքան է օգտագործված
* որ filesystem-ն է լցվում

---

## `du` Explanation

`du` ցույց է տալիս ֆայլի կամ folder-ի չափը։

```bash
du -sh .
```

Սա ցույց է տալիս current folder-ի ընդհանուր չափը։

Օգտակար տարբերակ՝

```bash
du -sh *
```

սա ցույց է տալիս current folder-ի ներսի item-ների չափերը։

---

## Why This Matters in DevOps

Այս command-ները օգնում են պատասխանել կարևոր հարցերի՝

* ինչ է աշխատում server-ում
* որ process-ն է շատ CPU օգտագործում
* որ process-ն է շատ RAM օգտագործում
* RAM-ը հերիքո՞ւմ է
* disk-ը լցվո՞ւմ է
* system-ը overload եղա՞ծ է
* որ process-ը պետք է stop անել

Real DevOps-ում սրանք օգտագործվում են՝

* slow server debug անելիս
* high CPU issue-ի ժամանակ
* high memory issue-ի ժամանակ
* stuck process-ի դեպքում
* full disk-ի դեպքում
* failed deployment-ի ժամանակ
* production incident-ի ժամանակ

---

## Important Safety Notes

Պետք չէ random process kill անել։

Ճիշտ մոտեցումը՝ նախ ստուգել process-ը՝

```bash
ps -p PID
```

Հետո միայն stop անել՝

```bash
kill PID
```

`kill -9` պետք է օգտագործել միայն անհրաժեշտության դեպքում։

```bash
kill -9 PID
```

`kill -9` process-ին հնարավորություն չի տալիս նորմալ cleanup անել, դրա համար այն առաջին ընտրությունը չէ։

---

## Common Mistakes

| Սխալ                              | Խնդիր                               | Ճիշտ մոտեցում                                 |
| --------------------------------- | ----------------------------------- | --------------------------------------------- |
| Random PID kill անել              | Կարող է կանգնեցնել կարևոր service   | Նախ ստուգել `ps -p PID`                       |
| Միանգամից օգտագործել `kill -9`    | Շատ forceful է                      | Սկզբում օգտագործել `kill PID`                 |
| Disk usage չստուգել               | Full disk-ը կարող է կոտրել app/logs | Ստուգել `df -h`                               |
| Շփոթել `df` և `du`                | Սխալ command սխալ հարցի համար       | `df` filesystem-ի համար է, `du` folder size-ի |
| Միայն free memory-ին նայել        | Linux-ը cache/buffer է օգտագործում  | Նայել available memory-ին `free -h`-ով        |
| Չիմանալ ինչպես դուրս գալ `top`-ից | Terminal-ը մնում է monitor view-ում | Սեղմել `q`                                    |

---

## Processes and Monitoring Quick Reference

| Task                           | Command       |
| ------------------------------ | ------------- |
| Տեսնել current shell processes | `ps`          |
| Տեսնել detailed process list   | `ps aux`      |
| Տեսնել process PID-ով          | `ps -p PID`   |
| Տեսնել current shell PID       | `echo $$`     |
| Տեսնել last background PID     | `echo $!`     |
| Սկսել demo background process  | `sleep 300 &` |
| Stop անել process              | `kill PID`    |
| Live process monitor           | `top`         |
| Better live monitor            | `htop`        |
| Ստուգել uptime/load            | `uptime`      |
| Ստուգել memory                 | `free -h`     |
| Ստուգել disk usage             | `df -h`       |
| Ստուգել folder size            | `du -sh .`    |

---

## Validation

Այս lab-ը ստուգելու համար օգտագործվում են՝

```bash
pwd
tree -a --charset=ascii
cat process-list.txt
cat process-details.txt
cat demo-process.txt
cat uptime.txt
cat memory.txt
cat disk.txt
cat disk-usage.txt
ps aux | head
uptime
free -h
df -h
du -sh .
```

Expected result՝

* lesson directory exists
* `process-list.txt` exists
* `process-details.txt` exists
* `demo-process.txt` exists
* `uptime.txt` exists
* `memory.txt` exists
* `disk.txt` exists
* `disk-usage.txt` exists
* `ps aux | head` shows running processes
* `uptime` shows uptime and load average
* `free -h` shows memory usage
* `df -h` shows filesystem disk usage
* `du -sh .` shows current directory size
* demo process-ը safe ձևով start, inspect և stop է արվել

---

## Quiz Review

| Question                   | Correct Answer                                       | Status |
| -------------------------- | ---------------------------------------------------- | ------ |
| What is a process?         | Process-ը աշխատող ծրագիր կամ command է։              | Passed |
| What does PID mean?        | PID նշանակում է Process ID։                          | Passed |
| What does `ps` show?       | Այն ցույց է տալիս running processes։                 | Passed |
| What does `ps aux` show?   | Այն ցույց է տալիս detailed process information։      | Passed |
| What does `top` do?        | Այն բացում է live process monitor։                   | Passed |
| What does `kill PID` do?   | Այն signal է ուղարկում process-ին stop անելու համար։ | Passed |
| What does `uptime` show?   | Այն ցույց է տալիս uptime և load average։             | Passed |
| What does `free -h` show?  | Այն ցույց է տալիս memory usage human-readable ձևով։  | Passed |
| What does `df -h` show?    | Այն ցույց է տալիս filesystem disk usage։             | Passed |
| What does `du -sh .` show? | Այն ցույց է տալիս current directory-ի չափը։          | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

Եթե `top`-ը բացվել է և չես կարողանում դուրս գալ՝

```text
q
```

Եթե `htop`-ից պետք է դուրս գալ՝

```text
F10
```

կամ՝

```text
q
```

Եթե process-ը չի կանգնում normal `kill`-ով, նախ ստուգիր PID-ը՝

```bash
ps -p PID
```

Հետո միայն անհրաժեշտության դեպքում օգտագործիր՝

```bash
kill -9 PID
```

Եթե disk usage-ը բարձր է՝

```bash
df -h
```

Հետո ստուգիր folder sizes՝

```bash
du -sh *
```

Եթե memory usage-ը բարձր է՝

```bash
free -h
```

հետո՝

```bash
top
```

---

## Git Workflow

Lab-ը ավարտելուց հետո աշխատանքը պահվում է Git-ով՝

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-08-processes-monitoring
git commit -m "Add Linux processes and monitoring notes"
git push
```

---

## What I Learned

Այս դասում ես սովորեցի, թե ինչպես են Linux process-ները և basic system monitoring-ը աշխատում։

Ես սովորեցի օգտագործել `ps`, `top`, `htop`, `kill`, `uptime`, `free -h`, `df -h`, `du -sh` հրամանները։

Ես նաև սովորեցի, թե ինչպես safe ձևով ստեղծել demo background process, գտնել դրա PID-ը, ստուգել և stop անել այն։

Այս գիտելիքները կարևոր են DevOps-ի համար, որովհետև server-ի դանդաղ աշխատանքը, RAM/CPU/disk խնդիրները և stuck process-ները շատ հաճախ հանդիպող խնդիրներ են։

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.

