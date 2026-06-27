# Դաս 07 — Users, Groups and sudo

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-users%20groups%20sudo-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը ծածկում է Linux users, groups և `sudo` concepts-ը, որոնք կարևոր են DevOps-ի ամենօրյա աշխատանքում։

Linux systems-ը users և groups է օգտագործում files, directories, services և administrative commands-ի access-ը կառավարելու համար։ DevOps Engineer-ը պետք է հասկանա՝ ինչպես տեսնել current user-ը, inspect անել user IDs, ստուգել group membership և safe օգտագործել `sudo`։

Այս դասում ես practice արեցի `whoami`, `id`, `groups`, `sudo`, `getent passwd` և `getent group` commands-ը։

---

## Learning Objectives

Այս դասը ավարտելուց հետո ես սովորեցի՝

* ստուգել current Linux user-ը
* inspect անել UID և GID information
* տեսնել group membership
* հասկանալ regular user-ի և root user-ի տարբերությունը
* օգտագործել `sudo` administrative commands-ի համար
* ստուգել user-ը sudo group-ում կա թե ոչ
* inspect անել user information system user database-ից
* inspect անել group information system group database-ից
* հասկանալ ինչու root user-ով միշտ աշխատելը վտանգավոր է
* հասկանալ least privilege principle-ը
* safe validate անել user և group information

---

## Key Concepts

| Concept | Meaning |
| ------- | ------- |
| User | Account, որով login են անում և commands run անում |
| Group | Users-ի collection, որը կարող է share անել permissions |
| UID | User ID, numeric identifier |
| GID | Group ID, numeric identifier |
| root | Linux-ի ամենահզոր administrative user-ը |
| sudo | Թույլ է տալիս permitted user-ին run անել commands elevated privileges-ով |
| Least privilege | Տալ միայն այն permissions-ը, որն անհրաժեշտ է task-ի համար |

---

## Commands Learned

| Command | Purpose | Example |
| ------- | ------- | ------- |
| `whoami` | Shows current user | `whoami` |
| `id` | Shows UID, GID and groups | `id` |
| `groups` | Shows current user's groups | `groups` |
| `groups $USER` | Shows groups for current user variable | `groups $USER` |
| `sudo command` | Runs command with elevated privileges | `sudo whoami` |
| `sudo -l` | Lists allowed sudo commands | `sudo -l` |
| `getent passwd $USER` | Shows user database entry | `getent passwd $USER` |
| `getent group sudo` | Shows sudo group entry | `getent group sudo` |

---

## Lab Structure

In this lab, I created the following structure:

```text
lesson-07-users-groups-sudo/
|-- groups.txt
|-- identity.txt
|-- notes.md
|-- sudo-check.txt
|-- system-groups.txt
`-- system-users.txt
```

---

## Practical Commands Used

Create lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-07-users-groups-sudo
cd lesson-07-users-groups-sudo
```

Create lab files:

```bash
touch identity.txt groups.txt sudo-check.txt system-users.txt system-groups.txt
```

Check current user:

```bash
whoami
```

Save current user:

```bash
whoami > identity.txt
```

Save UID/GID/groups:

```bash
id >> identity.txt
```

View identity file:

```bash
cat identity.txt
```

Check groups:

```bash
groups
```

Save groups:

```bash
groups > groups.txt
```

Check sudo access:

```bash
sudo whoami
```

Expected result:

```text
root
```

Save sudo result:

```bash
sudo whoami > sudo-check.txt
```

Check current user system entry:

```bash
getent passwd $USER
```

Save user entry:

```bash
getent passwd $USER > system-users.txt
```

Check sudo group:

```bash
getent group sudo
```

Save sudo group:

```bash
getent group sudo > system-groups.txt
```

---

## Understanding `whoami`

`whoami` command-ը ցույց է տալիս, թե որ user-ով ես հիմա աշխատում։

```bash
whoami
```

Example output:

```text
phantom
```

Սա նշանակում է current shell-ը աշխատում է `phantom` user-ով։

---

## Understanding `id`

`id` command-ը ցույց է տալիս detailed identity information։

```bash
id
```

Example:

```text
uid=1000(phantom) gid=1000(phantom) groups=1000(phantom),27(sudo)
```

| Field | Meaning |
| ----- | ------- |
| `uid` | User ID |
| `gid` | Primary Group ID |
| `groups` | User-ի բոլոր groups-ը |
| `sudo` | Նշում է, որ user-ը կարող է օգտագործել sudo, եթե configured է |

---

## Understanding `groups`

`groups` command-ը ցույց է տալիս current user-ի group membership-ը։

```bash
groups
```

Example:

```text
phantom sudo
```

Եթե user-ը ունի `sudo` group, սովորաբար կարող է administrative commands run անել `sudo`-ով։

---

## Understanding `sudo`

`sudo` command-ը թույլ է տալիս permitted user-ին command run անել elevated privileges-ով։

```bash
sudo whoami
```

Expected output:

```text
root
```

Սա նշանակում է command-ը execute է եղել root privileges-ով։

---

## Root User

`root` user-ը Linux-ի ամենահզոր user-ն է։

Root user-ը կարող է՝

* փոփոխել system files
* install/remove անել packages
* փոխել permissions և ownership
* ստեղծել և ջնջել users
* manage անել services
* փոխել critical system configuration

Root-ով սխալ command-ը կարող է վնասել system-ը, դրա համար ավելի safe է աշխատել regular user-ով և `sudo` օգտագործել միայն անհրաժեշտ պահին։

---

## System User Database

Current user-ի system entry-ն տեսնելու safe command՝

```bash
getent passwd $USER
```

Example:

```text
phantom:x:1000:1000:,,,:/home/phantom:/bin/bash
```

| Field | Meaning |
| ----- | ------- |
| `phantom` | Username |
| `x` | Password placeholder |
| `1000` | UID |
| `1000` | GID |
| `/home/phantom` | Home directory |
| `/bin/bash` | Login shell |

---

## System Group Database

Sudo group-ը տեսնելու safe command՝

```bash
getent group sudo
```

Example:

```text
sudo:x:27:phantom
```

Սա նշանակում է `sudo` group-ը կա և user-ը կարող է listed լինել այդ group-ում։

---

## Why Users, Groups and sudo Matter in DevOps

Այս concepts-ը օգնում են հասկանալ՝

* Ո՞ր user-ն է command run անում
* Ո՞վ է file owner-ը
* User-ը ունի՞ sudo access
* Service-ը run է լինում ճիշտ user-ով
* Application user-ը ունի՞ բավական permissions
* Application user-ը շատ permissions ունի՞
* Ո՞ր group-ը պետք է access ունենա directory-ին
* Command-ը պետք է run անել root-ո՞վ, թե regular user-ով

DevOps-ում սա օգտագործվում է servers, deployment users, CI/CD runners, Linux services, SSH access, web server users, application users և production security-ի մեջ։

---

## Least Privilege Principle

Least privilege նշանակում է user-ին, service-ին կամ process-ին տալ միայն այն permissions-ը, որն անհրաժեշտ է իր task-ը անելու համար, ոչ ավել։

Bad practice:

```text
Run everything as root.
```

Better practice:

```text
Use a regular user and run only required administrative commands with sudo.
```

| Situation | Better Practice |
| --------- | --------------- |
| Daily work | Use regular user |
| Admin command | Use `sudo` only when needed |
| Application service | Run with dedicated service user |
| Secret files | Restrict access with safe permissions |
| Shared access | Use groups instead of everyone access |

---

## Important Safety Notes

Avoid working directly as root for normal tasks.

Avoid using `sudo` unless command actually needs admin privileges.

Avoid changing system users/groups/sudo configuration without understanding impact.

Եթե sudo configuration պետք է edit անել, safe tool-ը՝

```bash
sudo visudo
```

`visudo` checks syntax before saving, որպեսզի sudo access-ը չկոտրվի։

---

## Common Mistakes

| Mistake | Problem | Correct Practice |
| ------- | ------- | ---------------- |
| Running everything as root | Can damage system | Use regular user + sudo only when needed |
| Using `sudo` for every command | Too much privilege | Use sudo only for admin tasks |
| Not checking `whoami` | May run commands as wrong user | Run `whoami` |
| Not checking groups | User may not have access | Run `groups` or `id` |
| Editing sudoers incorrectly | Can break sudo access | Use `sudo visudo` |
| Giving services root access | Security risk | Use dedicated service users |

---

## `chmod`, `chown` and `sudo`

| Command | Purpose |
| ------- | ------- |
| `chmod` | Changes file permissions |
| `chown` | Changes file owner and group |
| `sudo` | Runs command with elevated privileges |

Example:

```bash
chmod 755 scripts/deploy.sh
```

Example:

```bash
sudo chown $USER:$USER file
```

Example:

```bash
sudo whoami
```

---

## Users, Groups and sudo Quick Reference

| Item | Meaning | Example |
| ---- | ------- | ------- |
| `whoami` | Shows current user | `whoami` |
| `id` | Shows UID, GID and groups | `id` |
| `groups` | Shows group membership | `groups` |
| `root` | Full administrative user | `sudo whoami` returns `root` |
| `sudo` | Runs command with elevated privileges | `sudo apt update` |
| `getent passwd $USER` | Shows current user's system entry | `getent passwd $USER` |
| `getent group sudo` | Shows sudo group entry | `getent group sudo` |
| Least privilege | Use only required permissions | Regular user + sudo only when needed |

---

## Validation

Commands used to validate this lab:

```bash
pwd
tree -a --charset=ascii
whoami
id
groups
sudo whoami
getent passwd $USER
getent group sudo
cat identity.txt
cat groups.txt
cat sudo-check.txt
cat system-users.txt
cat system-groups.txt
```

Expected result՝

* lesson directory exists
* lab files exist
* `whoami` shows current user
* `id` shows UID/GID/groups
* `groups` shows group membership
* `sudo whoami` returns `root`
* `getent passwd $USER` shows current user information
* `getent group sudo` shows sudo group information

---

## Quiz Review

| Question | Correct Answer | Status |
| --- | --- | --- |
| What does `whoami` show? | It shows the current user. | Passed |
| What does `id` show? | It shows UID, GID and group membership. | Passed |
| What does `groups` show? | It shows groups a user belongs to. | Passed |
| What is root? | The most powerful administrative user in Linux. | Passed |
| What does `sudo` do? | It runs a command with elevated privileges. | Passed |
| What is result of `sudo whoami`? | `root` | Passed |
| Why should root not be used for everything? | Mistakes as root can damage system. | Passed |
| What does least privilege mean? | Give only permissions required for task. | Passed |
| What command checks current user's system entry? | `getent passwd $USER` | Passed |
| What command checks sudo group? | `getent group sudo` | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

If `sudo whoami` asks for password, enter Linux user password.

If user is not in sudoers file, current user does not have sudo privileges.

If `getent group sudo` returns nothing, distribution may use another admin group name.

Check current user:

```bash
whoami
```

Check identity:

```bash
id
```

Check groups:

```bash
groups
```

---

## Git Workflow

After completing the lab, I saved the work using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-07-users-groups-sudo
git commit -m "Add Linux users groups and sudo notes"
git push
```

---

## What I Learned

Այս դասում ես սովորեցի, թե ինչպես են աշխատում Linux users, groups և sudo։

Ես սովորեցի ստուգել current user-ը `whoami`-ով, տեսնել identity details `id`-ով, view անել group membership `groups`-ով և safe օգտագործել `sudo` administrative commands-ի համար։

Ես նաև սովորեցի, թե ինչու root-ով միշտ աշխատելը վտանգավոր է և ինչու DevOps Engineer-ը պետք է հետևի least privilege principle-ին։

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
