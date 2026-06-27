# Lesson 08 — Processes and System Monitoring

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-processes%20and%20monitoring-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers basic Linux process management and system monitoring commands used in daily DevOps work.

Processes are running programs on a Linux system. A DevOps Engineer must understand how to inspect running processes, identify process IDs, monitor CPU and memory usage, check system uptime, review disk usage and safely stop test processes when needed.

In this lesson, I practiced using `ps`, `top`, `htop`, `kill`, `uptime`, `free`, `df` and `du`.

---

## Learning Objectives

By completing this lesson, I learned how to:

* understand what a Linux process is
* inspect running processes using `ps`
* understand what a PID is
* check the current shell PID
* start a safe test background process
* inspect a process by PID
* stop a process safely using `kill`
* monitor system uptime
* check memory usage
* check disk usage
* check directory size
* use interactive monitoring tools like `top` and `htop`
* understand why process and resource monitoring are important in DevOps

---

## Key Concepts

| Concept            | Meaning                                                            |
| ------------------ | ------------------------------------------------------------------ |
| Process            | A running program or command                                       |
| PID                | Process ID, a unique number assigned to a running process          |
| Background process | A process running in the background while the shell remains usable |
| CPU usage          | How much processor capacity a process or system is using           |
| Memory usage       | How much RAM is being used                                         |
| Disk usage         | How much storage space is used or available                        |
| Load average       | A summary of system workload over time                             |

---

## Commands Learned

| Command     | Purpose                                       | Example      |
| ----------- | --------------------------------------------- | ------------ |
| `ps`        | Shows processes for the current shell         | `ps`         |
| `ps aux`    | Shows detailed process information            | `ps aux`     |
| `ps -p PID` | Shows information for a specific process      | `ps -p 1234` |
| `top`       | Opens an interactive process monitor          | `top`        |
| `htop`      | Opens an improved interactive process monitor | `htop`       |
| `kill PID`  | Sends a termination signal to a process       | `kill 1234`  |
| `uptime`    | Shows system uptime and load average          | `uptime`     |
| `free -h`   | Shows memory usage in human-readable format   | `free -h`    |
| `df -h`     | Shows filesystem disk usage                   | `df -h`      |
| `du -sh .`  | Shows current directory size                  | `du -sh .`   |
| `echo $$`   | Shows current shell PID                       | `echo $$`    |
| `echo $!`   | Shows the PID of the last background process  | `echo $!`    |

---

## Lab Structure

In this lab, I created the following structure:

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

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-08-processes-monitoring
cd lesson-08-processes-monitoring
```

Create lab files:

```bash
touch process-list.txt process-details.txt uptime.txt memory.txt disk.txt disk-usage.txt demo-process.txt
```

List current shell processes:

```bash
ps
```

List detailed process information:

```bash
ps aux | head
```

Save process output:

```bash
ps aux | head -n 10 > process-list.txt
cat process-list.txt
```

Show the current shell PID:

```bash
echo $$
```

Save the current shell PID:

```bash
echo "Current shell PID: $$" > process-details.txt
cat process-details.txt
```

Start a safe test background process:

```bash
sleep 300 &
```

Save the PID of the last background process:

```bash
echo $! > demo-process.pid
cat demo-process.pid
```

Inspect the demo process by PID:

```bash
ps -p $(cat demo-process.pid)
```

Save demo process information:

```bash
ps -p $(cat demo-process.pid) > demo-process.txt
cat demo-process.txt
```

Stop the demo process:

```bash
kill $(cat demo-process.pid)
```

Verify that the demo process stopped:

```bash
ps -p $(cat demo-process.pid)
```

Check system uptime:

```bash
uptime
```

Save uptime output:

```bash
uptime > uptime.txt
cat uptime.txt
```

Check memory usage:

```bash
free -h
```

Save memory output:

```bash
free -h > memory.txt
cat memory.txt
```

Check filesystem disk usage:

```bash
df -h
```

Save disk output:

```bash
df -h > disk.txt
cat disk.txt
```

Check current directory size:

```bash
du -sh .
```

Save directory size output:

```bash
du -sh . > disk-usage.txt
cat disk-usage.txt
```

Open interactive process monitor:

```bash
top
```

Exit `top`:

```text
q
```

Open `htop` if installed:

```bash
htop
```

Exit `htop`:

```text
F10
```

or:

```text
q
```

---

## Understanding Processes

A process is a running program or command.

For example, when a command is executed in the terminal, Linux creates a process for it.

Examples of processes include:

* shell sessions
* running commands
* background jobs
* system services
* web servers
* database servers
* monitoring agents

Each process has a unique process ID called a PID.

---

## Understanding PID

PID means Process ID.

Linux uses PIDs to identify and manage running processes.

Example:

```bash
echo $$
```

This shows the PID of the current shell.

Example:

```bash
sleep 300 &
echo $!
```

The `$!` variable shows the PID of the last background process.

---

## Understanding `ps`

The `ps` command shows running processes.

Basic process list:

```bash
ps
```

Detailed process list:

```bash
ps aux
```

Show only the first lines:

```bash
ps aux | head
```

Check a specific process by PID:

```bash
ps -p PID
```

Example:

```bash
ps -p $(cat demo-process.pid)
```

---

## Understanding `top` and `htop`

`top` is an interactive process monitor.

It shows live information about:

* running processes
* CPU usage
* memory usage
* system load
* process IDs

Start `top`:

```bash
top
```

Exit `top`:

```text
q
```

`htop` is a more user-friendly interactive process monitor.

Start `htop`:

```bash
htop
```

Exit `htop`:

```text
F10
```

or:

```text
q
```

---

## Understanding `kill`

The `kill` command sends a signal to a process.

A common use is to stop a process by PID.

Example:

```bash
kill 1234
```

In this lab, I only used `kill` on a safe demo process:

```bash
sleep 300 &
echo $! > demo-process.pid
kill $(cat demo-process.pid)
```

Important note: `kill` should be used carefully. Stopping the wrong process can interrupt applications, services or system tasks.

---

## Understanding `uptime`

The `uptime` command shows how long the system has been running.

Example:

```bash
uptime
```

It usually shows:

* current time
* how long the system has been running
* number of logged-in users
* load average

Load average is a quick view of system workload over time.

---

## Understanding `free`

The `free` command shows memory usage.

Human-readable output:

```bash
free -h
```

It shows:

* total memory
* used memory
* free memory
* available memory
* swap usage

This is useful when checking if a server is running low on RAM.

---

## Understanding `df`

The `df` command shows filesystem disk usage.

Human-readable output:

```bash
df -h
```

It helps answer:

* How much disk space is available?
* Which filesystem is nearly full?
* Is the server running out of storage?

Disk usage problems can break applications, logging, deployments and databases.

---

## Understanding `du`

The `du` command shows file or directory size.

Example:

```bash
du -sh .
```

This shows the total size of the current directory.

Common usage:

```bash
du -sh *
```

This shows the size of items inside the current directory.

---

## Why Process and Monitoring Matter in DevOps

Process and monitoring commands help answer important operational questions:

* What is running on the server?
* Which process is using CPU?
* Which process is using memory?
* Is the server running out of RAM?
* Is the disk almost full?
* How long has the system been running?
* Is the server overloaded?
* Which process should be stopped safely?

In real DevOps work, these commands are used when troubleshooting:

* slow servers
* high CPU usage
* high memory usage
* stuck processes
* full disks
* failed deployments
* application crashes
* production incidents

---

## Important Safety Notes

Do not kill random processes without understanding what they are.

Good practice:

```bash
ps -p PID
```

Then stop only the intended process:

```bash
kill PID
```

Avoid using forceful kill commands unless absolutely necessary.

A regular stop signal is safer:

```bash
kill PID
```

A forceful signal should be used carefully:

```bash
kill -9 PID
```

`kill -9` does not allow the process to clean up before exiting, so it should not be the first choice.

---

## Common Mistakes

| Mistake                     | Problem                             | Correct Practice                                      |
| --------------------------- | ----------------------------------- | ----------------------------------------------------- |
| Killing a random PID        | Can stop an important service       | Inspect the process first with `ps -p PID`            |
| Using `kill -9` immediately | Forceful and may prevent cleanup    | Try normal `kill PID` first                           |
| Ignoring disk usage         | Full disk can break apps and logs   | Check with `df -h`                                    |
| Confusing `df` and `du`     | Wrong tool for the question         | `df` checks filesystems, `du` checks file/folder size |
| Looking only at free memory | Linux memory includes cache/buffers | Check available memory with `free -h`                 |
| Forgetting to exit `top`    | Terminal remains in monitor view    | Press `q`                                             |

---

## Processes and Monitoring Quick Reference

| Task                             | Command       |
| -------------------------------- | ------------- |
| Show current shell processes     | `ps`          |
| Show detailed process list       | `ps aux`      |
| Show a process by PID            | `ps -p PID`   |
| Show current shell PID           | `echo $$`     |
| Show last background process PID | `echo $!`     |
| Start a demo background process  | `sleep 300 &` |
| Stop a process                   | `kill PID`    |
| Monitor processes live           | `top`         |
| Monitor processes with htop      | `htop`        |
| Check uptime and load            | `uptime`      |
| Check memory                     | `free -h`     |
| Check filesystem disk usage      | `df -h`       |
| Check directory size             | `du -sh .`    |

---

## Validation

Commands used to validate this lab:

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

Expected result:

* lesson directory exists
* `process-list.txt` exists
* `process-details.txt` exists
* `demo-process.txt` exists
* `uptime.txt` exists
* `memory.txt` exists
* `disk.txt` exists
* `disk-usage.txt` exists
* `ps aux | head` shows running processes
* `uptime` shows system uptime and load average
* `free -h` shows memory usage
* `df -h` shows filesystem disk usage
* `du -sh .` shows current directory size
* the demo process was safely started, inspected and stopped

---

## Quiz Review

| Question                   | Correct Answer                                                  | Status |
| -------------------------- | --------------------------------------------------------------- | ------ |
| What is a process?         | A process is a running program or command.                      | Passed |
| What does PID mean?        | PID means Process ID.                                           | Passed |
| What does `ps` show?       | It shows running processes.                                     | Passed |
| What does `ps aux` show?   | It shows detailed process information.                          | Passed |
| What does `top` do?        | It opens an interactive live process monitor.                   | Passed |
| What does `kill PID` do?   | It sends a termination signal to a process.                     | Passed |
| What does `uptime` show?   | It shows how long the system has been running and load average. | Passed |
| What does `free -h` show?  | It shows memory usage in human-readable format.                 | Passed |
| What does `df -h` show?    | It shows filesystem disk usage.                                 | Passed |
| What does `du -sh .` show? | It shows the size of the current directory.                     | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

If `top` opens and I cannot return to the terminal, I should press:

```text
q
```

If `htop` opens and I want to exit, I should press:

```text
F10
```

or:

```text
q
```

If a process does not stop with normal `kill`, I should first confirm the PID:

```bash
ps -p PID
```

Then, only if needed, use a forceful signal carefully:

```bash
kill -9 PID
```

If disk usage looks high, I should check filesystem usage:

```bash
df -h
```

Then check folder sizes:

```bash
du -sh *
```

If memory usage looks high, I should inspect memory:

```bash
free -h
```

Then inspect processes with:

```bash
top
```

---

## Git Workflow

After completing the lab, I saved the work using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-08-processes-monitoring
git commit -m "Add Linux processes and monitoring notes"
git push
```

---

## What I Learned

In this lesson, I learned how Linux processes and basic system monitoring work.

I learned how to inspect running processes with `ps`, monitor live resource usage with `top` and `htop`, check system uptime, inspect memory usage with `free -h`, check disk usage with `df -h` and inspect directory size with `du -sh`.

I also learned how to safely create, inspect and stop a demo background process using PID-based commands.

These skills are essential for DevOps because process and resource issues are common during deployments, troubleshooting and production incidents.

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.

