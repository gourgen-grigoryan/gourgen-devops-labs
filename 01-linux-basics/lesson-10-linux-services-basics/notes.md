# Lesson 10 — Linux Services Basics

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-linux%20services-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers Linux service management using `systemctl` and service logs using `journalctl`.

Linux services are background programs managed by the operating system. In real DevOps work, services such as Nginx, Docker, PostgreSQL, Redis, SSH, cron, Prometheus and Grafana often run in the background and must be started, stopped, restarted, enabled, disabled and inspected.

In this lesson, I practiced checking whether `systemd` is available, listing running services, checking service status, starting and stopping a safe service, restarting it, enabling and disabling boot auto-start and reading service logs.

---

## Learning Objectives

By completing this lesson, I learned how to:

* understand what a Linux service is
* understand what `systemd` is
* check whether the system is using `systemd`
* understand what `systemctl` does
* list running services
* check service status
* check whether a service is active
* check whether a service is enabled at boot
* start a service
* stop a service
* restart a service
* enable a service at boot
* disable a service at boot
* read service logs using `journalctl`
* understand the difference between `start` and `enable`
* understand why service management is important in DevOps

---

## Key Concepts

| Concept | Meaning |
| ------- | ------- |
| Service | A background program managed by the system |
| systemd | Linux init and service manager used on many modern distributions |
| systemctl | Command used to manage systemd services |
| journalctl | Command used to read systemd journal logs |
| Active | The service is currently running |
| Inactive | The service is currently stopped |
| Enabled | The service is configured to start automatically at boot |
| Disabled | The service is not configured to start automatically at boot |
| Restart | Stop and start the service again |
| Unit | A systemd-managed object such as a service |

---

## Commands Learned

| Command | Purpose | Example |
| ------- | ------- | ------- |
| `ps -p 1 -o comm=` | Shows the process running as PID 1 | `ps -p 1 -o comm=` |
| `systemctl --version` | Shows systemctl/systemd version information | `systemctl --version` |
| `systemctl list-units --type=service --state=running --no-pager` | Lists running services | `systemctl list-units --type=service --state=running --no-pager` |
| `systemctl status SERVICE --no-pager` | Shows service status | `systemctl status cron --no-pager` |
| `systemctl is-active SERVICE` | Shows whether a service is active | `systemctl is-active cron` |
| `systemctl is-enabled SERVICE` | Shows whether a service is enabled at boot | `systemctl is-enabled cron` |
| `sudo systemctl start SERVICE` | Starts a service now | `sudo systemctl start cron` |
| `sudo systemctl stop SERVICE` | Stops a service now | `sudo systemctl stop cron` |
| `sudo systemctl restart SERVICE` | Restarts a service | `sudo systemctl restart cron` |
| `sudo systemctl enable SERVICE` | Enables service auto-start at boot | `sudo systemctl enable cron` |
| `sudo systemctl disable SERVICE` | Disables service auto-start at boot | `sudo systemctl disable cron` |
| `journalctl -u SERVICE --no-pager -n 20` | Shows recent logs for a service | `journalctl -u cron --no-pager -n 20` |

---

## Lab Structure

In this lab, I created the following structure:

```text
lesson-10-linux-services-basics/
|-- cron-active.txt
|-- cron-after-restart.txt
|-- cron-after-start.txt
|-- cron-after-stop.txt
|-- cron-disabled.txt
|-- cron-enabled.txt
|-- cron-logs.txt
|-- cron-reenabled.txt
|-- cron-status.txt
|-- notes.hy.md
|-- notes.md
|-- running-services.txt
|-- systemctl-version.txt
`-- systemd-pid1.txt
```

---

## Practical Commands Used

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-10-linux-services-basics
cd lesson-10-linux-services-basics
```

Create lab files:

```bash
touch systemd-pid1.txt systemctl-version.txt running-services.txt cron-status.txt cron-active.txt cron-enabled.txt cron-after-stop.txt cron-after-start.txt cron-after-restart.txt cron-disabled.txt cron-reenabled.txt cron-logs.txt
```

Check whether PID 1 is `systemd`:

```bash
ps -p 1 -o comm=
```

Save PID 1 output:

```bash
ps -p 1 -o comm= | tee systemd-pid1.txt
```

Check `systemctl` version:

```bash
systemctl --version
```

Save version output:

```bash
systemctl --version | head -n 5 | tee systemctl-version.txt
```

List running services:

```bash
systemctl list-units --type=service --state=running --no-pager | head -n 20
```

Save running services output:

```bash
systemctl list-units --type=service --state=running --no-pager | head -n 20 | tee running-services.txt
```

Install `cron` if needed:

```bash
sudo apt update
sudo apt install cron
```

Check cron service status:

```bash
systemctl status cron --no-pager
```

Save cron status output:

```bash
systemctl status cron --no-pager | tee cron-status.txt
```

Check whether cron is active:

```bash
systemctl is-active cron
```

Save active state:

```bash
systemctl is-active cron | tee cron-active.txt
```

Check whether cron is enabled:

```bash
systemctl is-enabled cron
```

Save enabled state:

```bash
systemctl is-enabled cron | tee cron-enabled.txt
```

Stop cron:

```bash
sudo systemctl stop cron
```

Check and save state after stop:

```bash
systemctl is-active cron | tee cron-after-stop.txt
```

Start cron:

```bash
sudo systemctl start cron
```

Check and save state after start:

```bash
systemctl is-active cron | tee cron-after-start.txt
```

Restart cron:

```bash
sudo systemctl restart cron
```

Save status after restart:

```bash
systemctl status cron --no-pager | tee cron-after-restart.txt
```

Disable cron auto-start at boot:

```bash
sudo systemctl disable cron
```

Check and save disabled state:

```bash
systemctl is-enabled cron | tee cron-disabled.txt
```

Re-enable cron auto-start at boot:

```bash
sudo systemctl enable cron
```

Check and save enabled state:

```bash
systemctl is-enabled cron | tee cron-reenabled.txt
```

Read recent cron logs:

```bash
journalctl -u cron --no-pager -n 20
```

Save recent cron logs:

```bash
journalctl -u cron --no-pager -n 20 | tee cron-logs.txt
```

---

## Understanding Linux Services

A Linux service is a background program managed by the operating system.

Services usually run without direct user interaction and provide important system or application functionality.

Examples of common services include:

* `cron`
* `ssh`
* `nginx`
* `docker`
* `postgresql`
* `redis`
* `prometheus`
* `grafana-server`

A DevOps Engineer must be able to inspect, start, stop, restart and troubleshoot services.

---

## Understanding systemd

`systemd` is a modern Linux init system and service manager.

It is responsible for starting and managing many services on the system.

To check whether `systemd` is running as PID 1:

```bash
ps -p 1 -o comm=
```

Expected output on a systemd-enabled system:

```text
systemd
```

If the output is not `systemd`, some `systemctl` commands may not work correctly.

---

## WSL systemd Note

In WSL, `systemd` may need to be enabled manually.

If `systemctl` shows an error such as:

```text
System has not been booted with systemd
```

then `/etc/wsl.conf` should include:

```ini
[boot]
systemd=true
```

After changing this file, WSL must be restarted from Windows PowerShell:

```powershell
wsl --shutdown
```

Then Ubuntu should be opened again and PID 1 should be checked:

```bash
ps -p 1 -o comm=
```

---

## Understanding systemctl

`systemctl` is the main command used to manage systemd services.

It can be used to:

* check service status
* start services
* stop services
* restart services
* enable services at boot
* disable services at boot
* list running services

Example:

```bash
systemctl status cron --no-pager
```

---

## Understanding Service Status

The `status` command shows detailed information about a service:

```bash
systemctl status cron --no-pager
```

It can show:

* whether the service is loaded
* whether it is active or inactive
* service PID
* recent log lines
* service unit file path
* errors or warnings

This is usually the first command to run when troubleshooting a service.

---

## Understanding Active State

The `is-active` command checks whether a service is currently running:

```bash
systemctl is-active cron
```

Common outputs:

```text
active
inactive
failed
```

`active` means the service is running now.

---

## Understanding Enabled State

The `is-enabled` command checks whether a service is configured to start automatically at boot:

```bash
systemctl is-enabled cron
```

Common outputs:

```text
enabled
disabled
```

`enabled` does not always mean the service is running right now. It means the service is configured to start automatically when the system boots.

---

## start vs enable

| Command | What it does |
| ------- | ------------ |
| `systemctl start SERVICE` | Starts the service now |
| `systemctl enable SERVICE` | Configures the service to start automatically at boot |

Important rule:

```text
start does not mean enable
enable does not always mean currently running
```

---

## stop vs disable

| Command | What it does |
| ------- | ------------ |
| `systemctl stop SERVICE` | Stops the service now |
| `systemctl disable SERVICE` | Prevents the service from starting automatically at boot |

Important rule:

```text
stop does not mean disable
disable does not always mean currently stopped
```

---

## Understanding restart

The `restart` command stops and starts a service again:

```bash
sudo systemctl restart cron
```

This is commonly used after configuration changes or when a service becomes stuck.

Restarting production services should be done carefully because it can interrupt users or applications.

---

## Understanding journalctl

`journalctl` is used to read logs from the systemd journal.

To read logs for a specific service:

```bash
journalctl -u cron --no-pager -n 20
```

Command parts:

| Part | Meaning |
| ---- | ------- |
| `journalctl` | Reads systemd journal logs |
| `-u cron` | Shows logs only for the cron service |
| `--no-pager` | Prints output directly without opening a pager |
| `-n 20` | Shows the last 20 log lines |

Logs are critical for troubleshooting service failures.

---

## Why Linux Services Matter in DevOps

Linux services are used constantly in real DevOps work.

A DevOps Engineer often needs to answer questions such as:

* Is the service running?
* Did the service fail?
* What do the logs say?
* Should the service be restarted?
* Is the service enabled at boot?
* Did the service start after reboot?
* Did a deployment break the service?

Examples from real server work:

```bash
sudo systemctl status nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
journalctl -u nginx --no-pager -n 50
```

---

## Important Safety Notes

Service management commands can affect running applications.

Stopping or restarting the wrong service can interrupt users, break deployments or stop critical infrastructure.

Before stopping or restarting a service, it is good practice to:

* check the service status
* understand what the service does
* review recent logs
* confirm that the service is safe to restart
* use a maintenance window for important production services

---

## Common Mistakes

| Mistake | Problem | Correct Practice |
| ------- | ------- | ---------------- |
| Confusing `start` and `enable` | A service may start now but not after reboot | Use `enable` for boot auto-start |
| Confusing `stop` and `disable` | A service may stop now but start again after reboot | Use `disable` to prevent boot auto-start |
| Restarting production services blindly | Can interrupt users or applications | Check status and logs first |
| Ignoring logs | Service failures are often explained in logs | Use `journalctl -u SERVICE` |
| Forgetting `sudo` | Service changes often require admin privileges | Use `sudo` for start, stop, restart, enable and disable |
| Using WSL without systemd enabled | `systemctl` may not work | Check PID 1 and enable systemd if needed |

---

## Linux Services Quick Reference

| Task | Command |
| ---- | ------- |
| Check PID 1 | `ps -p 1 -o comm=` |
| Check systemctl version | `systemctl --version` |
| List running services | `systemctl list-units --type=service --state=running --no-pager` |
| Check service status | `systemctl status SERVICE --no-pager` |
| Check if service is running | `systemctl is-active SERVICE` |
| Check if service starts at boot | `systemctl is-enabled SERVICE` |
| Start service now | `sudo systemctl start SERVICE` |
| Stop service now | `sudo systemctl stop SERVICE` |
| Restart service | `sudo systemctl restart SERVICE` |
| Enable service at boot | `sudo systemctl enable SERVICE` |
| Disable service at boot | `sudo systemctl disable SERVICE` |
| Show service logs | `journalctl -u SERVICE --no-pager -n 20` |

---

## Validation

Commands used to validate this lab:

```bash
pwd
tree -a --charset=ascii
cat systemd-pid1.txt
cat systemctl-version.txt
cat running-services.txt
cat cron-status.txt
cat cron-active.txt
cat cron-enabled.txt
cat cron-after-stop.txt
cat cron-after-start.txt
cat cron-after-restart.txt
cat cron-disabled.txt
cat cron-reenabled.txt
cat cron-logs.txt
systemctl is-active cron
systemctl is-enabled cron
```

Expected result:

* lesson directory exists
* `notes.md` exists
* `notes.hy.md` exists
* `systemd-pid1.txt` exists
* `systemctl-version.txt` exists
* `running-services.txt` exists
* `cron-status.txt` exists
* `cron-active.txt` exists
* `cron-enabled.txt` exists
* `cron-after-stop.txt` exists
* `cron-after-start.txt` exists
* `cron-after-restart.txt` exists
* `cron-disabled.txt` exists
* `cron-reenabled.txt` exists
* `cron-logs.txt` exists
* systemd availability was checked
* running services were listed
* cron status was checked
* cron start, stop and restart were practiced
* cron enable and disable were practiced
* cron logs were checked with `journalctl`

---

## Quiz Review

| Question | Correct Answer | Status |
| -------- | -------------- | ------ |
| What is a Linux service? | A background program managed by the system. | Passed |
| What does `systemctl status SERVICE` show? | It shows service state, active/inactive status, PID, logs and details. | Passed |
| What is the difference between `start` and `enable`? | `start` starts the service now, while `enable` configures it to start automatically at boot. | Passed |
| What is the difference between `stop` and `disable`? | `stop` stops the service now, while `disable` prevents it from starting automatically at boot. | Passed |
| What does `journalctl -u SERVICE` show? | It shows logs for a specific service. | Passed |
| Why should production services be restarted carefully? | Restarting a production service can stop important running services and interrupt users or applications. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

If `systemctl` does not work in WSL, check PID 1:

```bash
ps -p 1 -o comm=
```

If PID 1 is not `systemd`, enable systemd in `/etc/wsl.conf`:

```ini
[boot]
systemd=true
```

Then restart WSL from Windows PowerShell:

```powershell
wsl --shutdown
```

If a service is not running, check status first:

```bash
systemctl status SERVICE --no-pager
```

If a service fails to start, check logs:

```bash
journalctl -u SERVICE --no-pager -n 50
```

If a service is running now but does not start after reboot, check whether it is enabled:

```bash
systemctl is-enabled SERVICE
```

If a service starts after reboot even after being stopped, it may still be enabled:

```bash
systemctl is-enabled SERVICE
```

---

## Git Workflow

After completing the lesson and passing the quiz, the work will be saved using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-10-linux-services-basics ROADMAP.md
git commit -m "Complete Linux services basics lesson"
git push
git status
```

---

## What I Learned

In this lesson, I learned how Linux services are managed with `systemctl` and how service logs are inspected with `journalctl`.

I learned how to check whether systemd is available, list running services, check service status, start and stop a service, restart a service, enable and disable boot auto-start and read service logs.

These skills are essential for DevOps because most real server tools run as services and must be monitored, restarted, enabled and troubleshot safely.

---

## Status

Lesson completed, quiz passed, ready to commit and push.
