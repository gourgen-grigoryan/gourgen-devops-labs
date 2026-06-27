# Lesson 07 — Users, Groups and sudo

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-users%20groups%20sudo-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers Linux users, groups and `sudo`, which are important concepts in daily DevOps work.

Linux systems use users and groups to control access to files, directories, services and administrative commands. A DevOps Engineer must understand how to identify the current user, inspect user IDs, check group membership and use `sudo` safely.

In this lesson, I practiced using `whoami`, `id`, `groups`, `sudo`, `getent passwd` and `getent group`.

---

## Learning Objectives

By completing this lesson, I learned how to:

* check the current Linux user
* inspect user ID and group ID information
* view group membership
* understand the difference between a regular user and the root user
* use `sudo` to run administrative commands
* check whether a user belongs to the sudo group
* inspect user information from the system user database
* inspect group information from the system group database
* understand why working directly as root is risky
* understand the principle of least privilege
* validate user and group information safely

---

## Key Concepts

| Concept         | Meaning                                                          |
| --------------- | ---------------------------------------------------------------- |
| User            | An account used to log in and run commands                       |
| Group           | A collection of users that can share permissions                 |
| UID             | User ID, a numeric identifier for a user                         |
| GID             | Group ID, a numeric identifier for a group                       |
| root            | The most powerful administrative user in Linux                   |
| sudo            | Allows a permitted user to run commands with elevated privileges |
| Least privilege | Giving only the permissions required for a task                  |

---

## Commands Learned

| Command               | Purpose                                    | Example               |
| --------------------- | ------------------------------------------ | --------------------- |
| `whoami`              | Shows the current user                     | `whoami`              |
| `id`                  | Shows UID, GID and group membership        | `id`                  |
| `groups`              | Shows the groups of the current user       | `groups`              |
| `groups $USER`        | Shows groups for the current user variable | `groups $USER`        |
| `sudo command`        | Runs a command with elevated privileges    | `sudo whoami`         |
| `sudo -l`             | Lists allowed sudo commands for the user   | `sudo -l`             |
| `getent passwd $USER` | Shows user database entry                  | `getent passwd $USER` |
| `getent group sudo`   | Shows sudo group entry                     | `getent group sudo`   |

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

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-07-users-groups-sudo
cd lesson-07-users-groups-sudo
```

Create lab files:

```bash
touch identity.txt groups.txt sudo-check.txt system-users.txt system-groups.txt
```

Check the current user:

```bash
whoami
```

Save the current user to a file:

```bash
whoami > identity.txt
```

Save UID, GID and group information:

```bash
id >> identity.txt
```

View the identity file:

```bash
cat identity.txt
```

Check current user groups:

```bash
groups
```

Save groups to a file:

```bash
groups > groups.txt
```

View the groups file:

```bash
cat groups.txt
```

Check sudo access by running a command as root:

```bash
sudo whoami
```

Expected result:

```text
root
```

Save sudo check result:

```bash
sudo whoami > sudo-check.txt
```

View sudo check file:

```bash
cat sudo-check.txt
```

Check current user entry in the system user database:

```bash
getent passwd $USER
```

Save user database entry:

```bash
getent passwd $USER > system-users.txt
```

View user database result:

```bash
cat system-users.txt
```

Check sudo group entry:

```bash
getent group sudo
```

Save sudo group entry:

```bash
getent group sudo > system-groups.txt
```

View sudo group result:

```bash
cat system-groups.txt
```

---

## Understanding `whoami`

The `whoami` command shows which user is currently running commands.

Example:

```bash
whoami
```

Example output:

```text
phantom
```

This means the current shell is running as the `phantom` user.

---

## Understanding `id`

The `id` command shows detailed identity information.

Example:

```bash
id
```

Example output:

```text
uid=1000(phantom) gid=1000(phantom) groups=1000(phantom),27(sudo)
```

This output includes:

| Field    | Meaning                                       |
| -------- | --------------------------------------------- |
| `uid`    | User ID                                       |
| `gid`    | Primary Group ID                              |
| `groups` | All groups the user belongs to                |
| `sudo`   | Indicates the user can use sudo if configured |

---

## Understanding `groups`

The `groups` command shows which groups the current user belongs to.

Example:

```bash
groups
```

Example output:

```text
phantom sudo
```

If the user belongs to the `sudo` group, the user can usually run administrative commands with `sudo`.

---

## Understanding `sudo`

The `sudo` command allows a permitted user to run a command with elevated privileges.

Example:

```bash
sudo whoami
```

Expected output:

```text
root
```

This means the command was executed with root privileges.

Important note: `sudo` should be used only when elevated privileges are required.

---

## Root User

The `root` user is the most powerful user in Linux.

The root user can:

* modify system files
* install and remove packages
* change permissions and ownership
* create and delete users
* manage services
* change critical system configuration

Because root has full control, mistakes made as root can damage the system.

A safer practice is to work as a regular user and use `sudo` only when necessary.

---

## System User Database

Linux stores user account information in the system user database.

A safe way to query this information is:

```bash
getent passwd $USER
```

Example output:

```text
phantom:x:1000:1000:,,,:/home/phantom:/bin/bash
```

Common fields:

| Field           | Meaning              |
| --------------- | -------------------- |
| `phantom`       | Username             |
| `x`             | Password placeholder |
| `1000`          | UID                  |
| `1000`          | GID                  |
| `/home/phantom` | Home directory       |
| `/bin/bash`     | Login shell          |

---

## System Group Database

Linux stores group information in the system group database.

A safe way to query the sudo group is:

```bash
getent group sudo
```

Example output:

```text
sudo:x:27:phantom
```

This means the `sudo` group exists, and the user may be listed as a member.

---

## Why Users, Groups and sudo Matter in DevOps

Users, groups and sudo help answer important operational questions:

* Which user is running this command?
* Which user owns this file?
* Does this user have sudo access?
* Is this service running as the correct user?
* Does the application user have enough permissions?
* Does the application user have too many permissions?
* Which group should have access to this directory?
* Should this command be run as root or a regular user?

In real DevOps work, these concepts are used when working with:

* servers
* deployment users
* CI/CD runners
* Linux services
* SSH access
* web server users
* application users
* file permissions
* production security

---

## Least Privilege Principle

The principle of least privilege means that a user, service or process should only have the permissions required to do its job.

Bad practice:

```text
Run everything as root.
```

Better practice:

```text
Use a regular user and run only required administrative commands with sudo.
```

Examples:

| Situation           | Better Practice                              |
| ------------------- | -------------------------------------------- |
| Daily work          | Use a regular user                           |
| Admin command       | Use `sudo` only when needed                  |
| Application service | Run with a dedicated service user            |
| Secret files        | Restrict access with safe permissions        |
| Shared access       | Use groups instead of giving everyone access |

---

## Important Safety Notes

Avoid working directly as root for normal tasks.

Avoid using `sudo` unless the command actually needs administrative privileges.

Avoid changing system users, groups or sudo configuration without understanding the impact.

Avoid editing sudo configuration files directly with a normal text editor.

If sudo configuration must be edited, the safer tool is:

```bash
sudo visudo
```

`visudo` checks syntax before saving, which helps prevent breaking sudo access.

---

## Common Mistakes

| Mistake                        | Problem                               | Correct Practice                         |
| ------------------------------ | ------------------------------------- | ---------------------------------------- |
| Running everything as root     | Increases risk of damaging the system | Use regular user + sudo only when needed |
| Using `sudo` for every command | Too much privilege                    | Use sudo only for admin tasks            |
| Not checking `whoami`          | May run commands as the wrong user    | Run `whoami`                             |
| Not checking groups            | User may not have required access     | Run `groups` or `id`                     |
| Editing sudoers incorrectly    | Can break sudo access                 | Use `sudo visudo`                        |
| Giving services root access    | Security risk                         | Use dedicated service users              |

---

## `chmod`, `chown` and `sudo`

These commands are related but different.

| Command | Purpose                                 |
| ------- | --------------------------------------- |
| `chmod` | Changes file permissions                |
| `chown` | Changes file owner and group            |
| `sudo`  | Runs a command with elevated privileges |

Example:

```bash
chmod 755 scripts/deploy.sh
```

This changes what users can do with a file.

Example:

```bash
sudo chown $USER:$USER file
```

This changes file ownership using elevated privileges.

Example:

```bash
sudo whoami
```

This runs `whoami` as root.

---

## Users, Groups and sudo Quick Reference

| Item                  | Meaning                                 | Example                              |
| --------------------- | --------------------------------------- | ------------------------------------ |
| `whoami`              | Shows the current user                  | `whoami`                             |
| `id`                  | Shows UID, GID and groups               | `id`                                 |
| `groups`              | Shows group membership                  | `groups`                             |
| `root`                | Full administrative user                | `sudo whoami` returns `root`         |
| `sudo`                | Runs a command with elevated privileges | `sudo apt update`                    |
| `getent passwd $USER` | Shows current user's system entry       | `getent passwd $USER`                |
| `getent group sudo`   | Shows sudo group entry                  | `getent group sudo`                  |
| Least privilege       | Use only required permissions           | Regular user + sudo only when needed |

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

Expected result:

* lesson directory exists
* `identity.txt` exists
* `groups.txt` exists
* `sudo-check.txt` exists
* `system-users.txt` exists
* `system-groups.txt` exists
* `whoami` shows the current user
* `id` shows UID, GID and groups
* `groups` shows user group membership
* `sudo whoami` returns `root`
* `getent passwd $USER` shows current user information
* `getent group sudo` shows sudo group information

---

## Quiz Review

| Question                                             | Correct Answer                                   | Status |
| ---------------------------------------------------- | ------------------------------------------------ | ------ |
| What does `whoami` show?                             | It shows the current user.                       | Passed |
| What does `id` show?                                 | It shows UID, GID and group membership.          | Passed |
| What does `groups` show?                             | It shows the groups a user belongs to.           | Passed |
| What is root?                                        | The most powerful administrative user in Linux.  | Passed |
| What does `sudo` do?                                 | It runs a command with elevated privileges.      | Passed |
| What is the result of `sudo whoami`?                 | `root`                                           | Passed |
| Why should root not be used for everything?          | Because mistakes as root can damage the system.  | Passed |
| What does least privilege mean?                      | Give only the permissions required for the task. | Passed |
| What command checks the current user's system entry? | `getent passwd $USER`                            | Passed |
| What command checks the sudo group?                  | `getent group sudo`                              | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

If `sudo whoami` asks for a password, I should enter my Linux user password.

If `sudo whoami` says the user is not in the sudoers file, it means the current user does not have sudo privileges.

If `getent group sudo` returns nothing, the system may use a different admin group name depending on the Linux distribution.

If I am not sure which user I am using, I should run:

```bash
whoami
```

If I need to check full identity information, I should run:

```bash
id
```

If I need to check groups, I should run:

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

In this lesson, I learned how Linux users, groups and sudo work.

I learned how to check the current user with `whoami`, inspect identity details with `id`, view group membership with `groups` and run administrative commands safely with `sudo`.

I also learned why working directly as root is risky and why DevOps Engineers should follow the principle of least privilege.

These concepts are essential for server management, SSH access, deployments, service users, file permissions and production security.

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
