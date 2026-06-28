# Lesson 10 — Linux Services Basics

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-linux%20services-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը բացատրում է Linux service management-ի հիմունքները՝ օգտագործելով `systemctl`, իսկ service logs-ը դիտելու համար՝ `journalctl`։

Linux service-ը background-ում աշխատող ծրագիր է, որը կառավարվում է operating system-ի կողմից։ Real DevOps աշխատանքում Nginx, Docker, PostgreSQL, Redis, SSH, cron, Prometheus և Grafana նման գործիքները հաճախ աշխատում են որպես services։

DevOps Engineer-ը պետք է կարողանա ստուգել service-ի status-ը, start անել, stop անել, restart անել, enable անել boot-ի ժամանակ, disable անել boot-ի ժամանակ և կարդալ service logs-ը։

Այս դասում ես սովորեցի ստուգել՝ systemd-ը հասանելի է, թե ոչ, տեսնել running services-ը, կառավարել safe service՝ `cron`, և կարդալ logs `journalctl`-ով։

---

## Learning Objectives

Այս դասից հետո ես սովորեցի՝

* ինչ է Linux service-ը
* ինչ է `systemd`-ը
* ինչպես ստուգել՝ system-ը օգտագործում է systemd, թե ոչ
* ինչ է անում `systemctl` հրամանը
* ինչպես տեսնել running services-ը
* ինչպես ստուգել service status-ը
* ինչպես ստուգել service-ը active է, թե ոչ
* ինչպես ստուգել service-ը enabled է boot-ի ժամանակ, թե ոչ
* ինչպես start անել service
* ինչպես stop անել service
* ինչպես restart անել service
* ինչպես enable անել service-ը boot-ի ժամանակ
* ինչպես disable անել service-ը boot-ի ժամանակ
* ինչպես կարդալ service logs-ը `journalctl`-ով
* ինչ տարբերություն կա `start` և `enable` հրամանների միջև
* ինչու service management-ը կարևոր է DevOps-ում

---

## Key Concepts

| Concept | Բացատրություն |
| ------- | ------------- |
| Service | Background-ում աշխատող ծրագիր, որը կառավարվում է system-ի կողմից |
| systemd | Linux init և service manager, որը օգտագործվում է շատ ժամանակակից distributions-ում |
| systemctl | Command, որով կառավարվում են systemd services-ը |
| journalctl | Command, որով կարդում ենք systemd journal logs-ը |
| Active | Service-ը հիմա աշխատում է |
| Inactive | Service-ը հիմա կանգնած է |
| Enabled | Service-ը configured է boot-ի ժամանակ ավտոմատ միանալու համար |
| Disabled | Service-ը configured չէ boot-ի ժամանակ ավտոմատ միանալու համար |
| Restart | Service-ը stop անել և նորից start անել |
| Unit | systemd-ի կողմից կառավարվող object, օրինակ՝ service |

---

## Commands Learned

| Command | Նպատակ | Օրինակ |
| ------- | ------ | ------ |
| `ps -p 1 -o comm=` | Ցույց է տալիս PID 1 process-ը | `ps -p 1 -o comm=` |
| `systemctl --version` | Ցույց է տալիս systemctl/systemd version-ը | `systemctl --version` |
| `systemctl list-units --type=service --state=running --no-pager` | Ցույց է տալիս running services-ը | `systemctl list-units --type=service --state=running --no-pager` |
| `systemctl status SERVICE --no-pager` | Ցույց է տալիս service status-ը | `systemctl status cron --no-pager` |
| `systemctl is-active SERVICE` | Ցույց է տալիս service-ը active է, թե ոչ | `systemctl is-active cron` |
| `systemctl is-enabled SERVICE` | Ցույց է տալիս service-ը enabled է boot-ի համար, թե ոչ | `systemctl is-enabled cron` |
| `sudo systemctl start SERVICE` | Start է անում service-ը հիմա | `sudo systemctl start cron` |
| `sudo systemctl stop SERVICE` | Stop է անում service-ը հիմա | `sudo systemctl stop cron` |
| `sudo systemctl restart SERVICE` | Restart է անում service-ը | `sudo systemctl restart cron` |
| `sudo systemctl enable SERVICE` | Enable է անում service-ը boot-ի ժամանակ | `sudo systemctl enable cron` |
| `sudo systemctl disable SERVICE` | Disable է անում service-ի boot auto-start-ը | `sudo systemctl disable cron` |
| `journalctl -u SERVICE --no-pager -n 20` | Ցույց է տալիս service-ի վերջին logs-ը | `journalctl -u cron --no-pager -n 20` |

---

## Lab Structure

Այս lab-ում ստեղծվում է հետևյալ structure-ը՝

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

Ստեղծել lesson directory՝

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-10-linux-services-basics
cd lesson-10-linux-services-basics
```

Ստեղծել lab files՝

```bash
touch systemd-pid1.txt systemctl-version.txt running-services.txt cron-status.txt cron-active.txt cron-enabled.txt cron-after-stop.txt cron-after-start.txt cron-after-restart.txt cron-disabled.txt cron-reenabled.txt cron-logs.txt
```

Ստուգել՝ PID 1-ը `systemd` է, թե ոչ՝

```bash
ps -p 1 -o comm=
```

Պահել PID 1 output-ը՝

```bash
ps -p 1 -o comm= | tee systemd-pid1.txt
```

Ստուգել `systemctl` version-ը՝

```bash
systemctl --version
```

Պահել version output-ը՝

```bash
systemctl --version | head -n 5 | tee systemctl-version.txt
```

Տեսնել running services-ը՝

```bash
systemctl list-units --type=service --state=running --no-pager | head -n 20
```

Պահել running services output-ը՝

```bash
systemctl list-units --type=service --state=running --no-pager | head -n 20 | tee running-services.txt
```

Install անել `cron`, եթե անհրաժեշտ է՝

```bash
sudo apt update
sudo apt install cron
```

Ստուգել cron service status-ը՝

```bash
systemctl status cron --no-pager
```

Պահել cron status output-ը՝

```bash
systemctl status cron --no-pager | tee cron-status.txt
```

Ստուգել՝ cron-ը active է, թե ոչ՝

```bash
systemctl is-active cron
```

Պահել active state-ը՝

```bash
systemctl is-active cron | tee cron-active.txt
```

Ստուգել՝ cron-ը enabled է boot-ի համար, թե ոչ՝

```bash
systemctl is-enabled cron
```

Պահել enabled state-ը՝

```bash
systemctl is-enabled cron | tee cron-enabled.txt
```

Stop անել cron-ը՝

```bash
sudo systemctl stop cron
```

Ստուգել և պահել stop-ից հետո state-ը՝

```bash
systemctl is-active cron | tee cron-after-stop.txt
```

Start անել cron-ը՝

```bash
sudo systemctl start cron
```

Ստուգել և պահել start-ից հետո state-ը՝

```bash
systemctl is-active cron | tee cron-after-start.txt
```

Restart անել cron-ը՝

```bash
sudo systemctl restart cron
```

Պահել restart-ից հետո status-ը՝

```bash
systemctl status cron --no-pager | tee cron-after-restart.txt
```

Disable անել cron auto-start-ը boot-ի ժամանակ՝

```bash
sudo systemctl disable cron
```

Ստուգել և պահել disabled state-ը՝

```bash
systemctl is-enabled cron | tee cron-disabled.txt
```

Նորից enable անել cron auto-start-ը boot-ի ժամանակ՝

```bash
sudo systemctl enable cron
```

Ստուգել և պահել enabled state-ը՝

```bash
systemctl is-enabled cron | tee cron-reenabled.txt
```

Կարդալ cron-ի վերջին logs-ը՝

```bash
journalctl -u cron --no-pager -n 20
```

Պահել cron logs-ը՝

```bash
journalctl -u cron --no-pager -n 20 | tee cron-logs.txt
```

---

## Linux Services Explanation

Linux service-ը background-ում աշխատող ծրագիր է, որը կառավարվում է operating system-ի կողմից։

Service-ները սովորաբար աշխատում են առանց user-ի անմիջական interaction-ի և ապահովում են system կամ application functionality։

Օրինակներ՝

* `cron`
* `ssh`
* `nginx`
* `docker`
* `postgresql`
* `redis`
* `prometheus`
* `grafana-server`

DevOps Engineer-ը պետք է կարողանա service-ները inspect անել, start անել, stop անել, restart անել և troubleshoot անել։

---

## systemd Explanation

`systemd`-ը modern Linux init system և service manager է։

Այն պատասխանատու է system-ում բազմաթիվ services start և manage անելու համար։

Ստուգել՝ systemd-ը PID 1 է, թե ոչ՝

```bash
ps -p 1 -o comm=
```

Սպասվող output systemd-enabled համակարգում՝

```text
systemd
```

Եթե output-ը `systemd` չէ, որոշ `systemctl` commands կարող են ճիշտ չաշխատել։

---

## WSL systemd Note

WSL-ում `systemd`-ը երբեմն պետք է միացնել manual։

Եթե `systemctl`-ը ցույց է տալիս error՝

```text
System has not been booted with systemd
```

ապա `/etc/wsl.conf` ֆայլում պետք է լինի՝

```ini
[boot]
systemd=true
```

Այդ փոփոխությունից հետո պետք է Windows PowerShell-ում restart անել WSL-ը՝

```powershell
wsl --shutdown
```

Հետո նորից բացել Ubuntu-ն և ստուգել PID 1-ը՝

```bash
ps -p 1 -o comm=
```

---

## systemctl Explanation

`systemctl`-ը հիմնական command-ն է, որով կառավարում ենք systemd services-ը։

Այն օգտագործվում է՝

* service status ստուգելու համար
* services start անելու համար
* services stop անելու համար
* services restart անելու համար
* services enable անելու համար boot-ի ժամանակ
* services disable անելու համար boot-ի ժամանակ
* running services տեսնելու համար

Օրինակ՝

```bash
systemctl status cron --no-pager
```

---

## Service Status Explanation

`status` command-ը ցույց է տալիս service-ի մանրամասն վիճակը՝

```bash
systemctl status cron --no-pager
```

Այն կարող է ցույց տալ՝

* service-ը loaded է, թե ոչ
* active է, թե inactive
* service PID
* վերջին log lines
* service unit file path
* errors կամ warnings

Troubleshooting-ի ժամանակ սա սովորաբար առաջին command-ն է։

---

## Active State Explanation

`is-active` command-ը ստուգում է՝ service-ը այս պահին աշխատում է, թե ոչ՝

```bash
systemctl is-active cron
```

Հնարավոր output-ներ՝

```text
active
inactive
failed
```

`active` նշանակում է՝ service-ը հիմա աշխատում է։

---

## Enabled State Explanation

`is-enabled` command-ը ստուգում է՝ service-ը configured է boot-ի ժամանակ ավտոմատ միանալու համար, թե ոչ՝

```bash
systemctl is-enabled cron
```

Հնարավոր output-ներ՝

```text
enabled
disabled
```

`enabled` չի նշանակում, որ service-ը անպայման հիմա աշխատում է։ Այն նշանակում է, որ service-ը configured է system boot-ի ժամանակ ավտոմատ start լինելու համար։

---

## start vs enable

| Command | Ինչ է անում |
| ------- | ----------- |
| `systemctl start SERVICE` | Start է անում service-ը հիմա |
| `systemctl enable SERVICE` | Config է անում, որ service-ը boot-ի ժամանակ ավտոմատ start լինի |

Կարևոր կանոն՝

```text
start չի նշանակում enable
enable չի նշանակում, որ service-ը անպայման հիմա աշխատում է
```

---

## stop vs disable

| Command | Ինչ է անում |
| ------- | ----------- |
| `systemctl stop SERVICE` | Stop է անում service-ը հիմա |
| `systemctl disable SERVICE` | Կանխում է service-ի boot auto-start-ը |

Կարևոր կանոն՝

```text
stop չի նշանակում disable
disable չի նշանակում, որ service-ը անպայման հիմա stopped է
```

---

## restart Explanation

`restart` command-ը service-ը stop է անում և նորից start է անում՝

```bash
sudo systemctl restart cron
```

Սա հաճախ օգտագործվում է configuration changes-ից հետո կամ այն դեպքում, երբ service-ը stuck է։

Production service restart-ը պետք է անել զգույշ, որովհետև այն կարող է interrupt անել users-ին կամ applications-ին։

---

## journalctl Explanation

`journalctl`-ը օգտագործվում է systemd journal logs-ը կարդալու համար։

Կոնկրետ service-ի logs տեսնելու համար՝

```bash
journalctl -u cron --no-pager -n 20
```

Command մասերը՝

| Part | Meaning |
| ---- | ------- |
| `journalctl` | Կարդում է systemd journal logs |
| `-u cron` | Ցույց է տալիս միայն cron service-ի logs |
| `--no-pager` | Output-ը ցույց է տալիս անմիջապես, առանց pager բացելու |
| `-n 20` | Ցույց է տալիս վերջին 20 log line-ը |

Logs-ը շատ կարևոր են service failure troubleshooting-ի համար։

---

## Why Linux Services Matter in DevOps

Linux services-ը real DevOps աշխատանքում օգտագործվում են շատ հաճախ։

DevOps Engineer-ը հաճախ պետք է պատասխանի այս հարցերին՝

* Service-ը աշխատո՞ւմ է
* Service-ը failed եղե՞լ է
* Logs-ը ինչ են ասում
* Պետք է restart անե՞լ service-ը
* Service-ը enabled է boot-ի ժամանակ, թե ոչ
* Reboot-ից հետո service-ը կաշխատի՞
* Deployment-ը կոտրե՞լ է service-ը

Real server command examples՝

```bash
sudo systemctl status nginx
sudo systemctl restart nginx
sudo systemctl enable nginx
journalctl -u nginx --no-pager -n 50
```

---

## Important Safety Notes

Service management commands-ը կարող են ազդել running applications-ի վրա։

Սխալ service stop կամ restart անելը կարող է interrupt անել users-ին, կոտրել deployment-ը կամ կանգնեցնել կարևոր infrastructure։

Մինչև service stop կամ restart անել լավ practice է՝

* ստուգել service status-ը
* հասկանալ՝ service-ը ինչ է անում
* ստուգել վերջին logs-ը
* հաստատել, որ service-ը safe է restart անելու համար
* կարևոր production services-ի համար օգտագործել maintenance window

---

## Common Mistakes

| Սխալ | Խնդիր | Ճիշտ մոտեցում |
| ---- | ----- | ------------- |
| Շփոթել `start` և `enable` | Service-ը կարող է հիմա start լինել, բայց reboot-ից հետո չաշխատել | Boot auto-start-ի համար օգտագործել `enable` |
| Շփոթել `stop` և `disable` | Service-ը կարող է հիմա stop լինել, բայց reboot-ից հետո նորից start լինել | Boot auto-start-ը կանխելու համար օգտագործել `disable` |
| Production services blindly restart անել | Կարող է interrupt անել users-ին կամ applications-ին | Նախ ստուգել status և logs |
| Logs-ը անտեսել | Service failures-ը հաճախ բացատրված են logs-ում | Օգտագործել `journalctl -u SERVICE` |
| Մոռանալ `sudo` | Service changes-ը հաճախ պահանջում են admin privileges | Start, stop, restart, enable, disable-ի համար օգտագործել `sudo` |
| WSL-ում systemd-ը չմիացնել | `systemctl`-ը կարող է չաշխատել | Ստուգել PID 1 և անհրաժեշտության դեպքում enable անել systemd |

---

## Linux Services Quick Reference

| Task | Command |
| ---- | ------- |
| Ստուգել PID 1 | `ps -p 1 -o comm=` |
| Ստուգել systemctl version | `systemctl --version` |
| Տեսնել running services | `systemctl list-units --type=service --state=running --no-pager` |
| Ստուգել service status | `systemctl status SERVICE --no-pager` |
| Ստուգել service-ը running է, թե ոչ | `systemctl is-active SERVICE` |
| Ստուգել service-ը boot-ի ժամանակ start կլինի, թե ոչ | `systemctl is-enabled SERVICE` |
| Start անել service հիմա | `sudo systemctl start SERVICE` |
| Stop անել service հիմա | `sudo systemctl stop SERVICE` |
| Restart անել service | `sudo systemctl restart SERVICE` |
| Enable անել service boot-ի ժամանակ | `sudo systemctl enable SERVICE` |
| Disable անել service boot-ի ժամանակ | `sudo systemctl disable SERVICE` |
| Տեսնել service logs | `journalctl -u SERVICE --no-pager -n 20` |

---

## Validation

Այս lab-ը ստուգելու համար օգտագործվում են՝

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

Expected result՝

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
* systemd availability-ը ստուգվել է
* running services-ը list է արվել
* cron status-ը ստուգվել է
* cron start, stop և restart practiced է
* cron enable և disable practiced է
* cron logs-ը ստուգվել է `journalctl`-ով

---

## Quiz Review

| Question | Correct Answer | Status |
| -------- | -------------- | ------ |
| What is a Linux service? | Background-ում աշխատող ծրագիր, որը կառավարվում է system-ի կողմից։ | Passed |
| What does `systemctl status SERVICE` show? | Այն ցույց է տալիս service-ի վիճակը՝ active/inactive status, PID, logs և այլ details։ | Passed |
| What is the difference between `start` and `enable`? | `start` միացնում է service-ը հիմա, իսկ `enable` կարգավորում է, որ service-ը boot/restart-ից հետո ավտոմատ միանա։ | Passed |
| What is the difference between `stop` and `disable`? | `stop` կանգնեցնում է service-ը հիմա, իսկ `disable` կանխում է, որ service-ը boot/restart-ից հետո ավտոմատ միանա։ | Passed |
| What does `journalctl -u SERVICE` show? | Այն ցույց է տալիս տվյալ service-ի logs-ը։ | Passed |
| Why should production services be restarted carefully? | Production-ում restart-ը կարող է կանգնեցնել կարևոր service-ներ և ազդել users/applications-ի վրա։ | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

Եթե `systemctl`-ը WSL-ում չի աշխատում, ստուգիր PID 1-ը՝

```bash
ps -p 1 -o comm=
```

Եթե PID 1-ը `systemd` չէ, enable արա systemd-ը `/etc/wsl.conf` ֆայլում՝

```ini
[boot]
systemd=true
```

Հետո Windows PowerShell-ում restart արա WSL-ը՝

```powershell
wsl --shutdown
```

Եթե service-ը չի աշխատում, նախ ստուգիր status-ը՝

```bash
systemctl status SERVICE --no-pager
```

Եթե service-ը չի start լինում, ստուգիր logs-ը՝

```bash
journalctl -u SERVICE --no-pager -n 50
```

Եթե service-ը հիմա աշխատում է, բայց reboot-ից հետո չի start լինում, ստուգիր enabled state-ը՝

```bash
systemctl is-enabled SERVICE
```

Եթե service-ը stop ես արել, բայց reboot-ից հետո նորից start է լինում, հնարավոր է այն դեռ enabled է՝

```bash
systemctl is-enabled SERVICE
```

---

## Git Workflow

Lesson-ը ավարտելուց և quiz-ը անցնելուց հետո աշխատանքը պահվելու է Git-ով՝

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

Այս դասում ես սովորեցի, թե ինչպես են Linux services-ը կառավարվում `systemctl`-ով և ինչպես են service logs-ը ստուգվում `journalctl`-ով։

Ես սովորեցի ստուգել systemd-ի հասանելիությունը, տեսնել running services-ը, ստուգել service status-ը, start և stop անել service, restart անել service, enable և disable անել boot auto-start-ը և կարդալ service logs։

Այս գիտելիքները կարևոր են DevOps-ի համար, որովհետև real server tools-ի մեծ մասը աշխատում են որպես services և պետք է կարողանալ դրանք safe ձևով monitor, restart, enable և troubleshoot անել։

---

## Status

Lesson completed, quiz passed, ready to commit and push.
