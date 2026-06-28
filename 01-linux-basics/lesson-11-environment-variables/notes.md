# Lesson 11 — Environment Variables

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-environment%20variables-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers Linux environment variables, shell variables, `$PATH`, `export`, `unset`, `.bashrc`, `source` and safe secret handling.

Environment variables are key/value values used by shells, commands, scripts and applications. They are commonly used to provide configuration such as application mode, ports, paths, API URLs and credentials.

In DevOps, environment variables are important because they allow applications and automation tools to receive configuration without hardcoding values directly into scripts or source code.

In this lesson, I practiced viewing environment variables, checking important built-in variables, understanding `$PATH`, creating shell variables, exporting environment variables, testing child shell behavior, removing variables and documenting safe secret handling.

---

## Learning Objectives

By completing this lesson, I learned how to:

* understand what environment variables are
* understand the difference between shell variables and environment variables
* list environment variables using `printenv`
* inspect common variables such as `HOME`, `USER`, `SHELL` and `PATH`
* understand how `$PATH` helps Linux find commands
* create a temporary shell variable
* use `export` to make a variable available to child processes
* test variable visibility in a child shell
* remove variables using `unset`
* understand temporary vs permanent variables
* understand the purpose of `.bashrc`
* understand how `source ~/.bashrc` reloads shell configuration
* understand safe secret handling in DevOps
* avoid committing secrets to GitHub

---

## Key Concepts

| Concept | Meaning |
| ------- | ------- |
| Variable | A named value used by the shell or a program |
| Shell variable | A variable available only in the current shell |
| Environment variable | An exported variable available to child processes |
| `printenv` | Command used to list environment variables |
| `export` | Command used to make a shell variable available to child processes |
| `unset` | Command used to remove a variable from the current shell |
| `$PATH` | List of directories where Linux searches for executable commands |
| `.bashrc` | Shell startup configuration file for interactive Bash sessions |
| `source` | Command used to reload shell configuration in the current shell |
| Secret | Sensitive value such as a password, token, API key or private key |

---

## Commands Learned

| Command | Purpose | Example |
| ------- | ------- | ------- |
| `printenv` | Shows environment variables | `printenv` |
| `echo $VARIABLE` | Prints the value of a variable | `echo $HOME` |
| `echo $PATH` | Shows the command search path | `echo $PATH` |
| `which COMMAND` | Shows where a command is located | `which ls` |
| `VARIABLE=value` | Creates a shell variable | `MY_LESSON="Environment Variables"` |
| `export VARIABLE=value` | Creates an environment variable | `export APP_ENV="dev"` |
| `bash -c 'COMMAND'` | Runs a command in a child shell | `bash -c 'echo $MY_LESSON'` |
| `unset VARIABLE` | Removes a variable from the current shell | `unset MY_LESSON` |
| `source ~/.bashrc` | Reloads Bash configuration | `source ~/.bashrc` |
| `cat FILE` | Prints file contents | `cat safe-secrets-note.txt` |
| `tee FILE` | Prints output and writes it to a file | `echo "$PATH" | tee path.txt` |

---

## Lab Structure

In this lab, I created the following structure:

```text
lesson-11-environment-variables/
|-- bashrc-note.txt
|-- child-shell-after-export.txt
|-- child-shell-before-export.txt
|-- env-list.txt
|-- env-variable.txt
|-- home-user-shell.txt
|-- notes.hy.md
|-- notes.md
|-- path-explanation.txt
|-- path.txt
|-- safe-secrets-note.txt
|-- shell-variable.txt
`-- unset-variable.txt
```

---

## Practical Commands Used

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-11-environment-variables
cd lesson-11-environment-variables
```

Create lab files:

```bash
touch env-list.txt path.txt home-user-shell.txt shell-variable.txt env-variable.txt child-shell-before-export.txt child-shell-after-export.txt unset-variable.txt bashrc-note.txt path-explanation.txt safe-secrets-note.txt
```

List environment variables:

```bash
printenv
```

Save the first environment variables:

```bash
printenv | head -n 30 | tee env-list.txt
```

Check common environment variables:

```bash
echo $HOME
echo $USER
echo $SHELL
```

Save common variables:

```bash
{
  echo "HOME=$HOME"
  echo "USER=$USER"
  echo "SHELL=$SHELL"
} | tee home-user-shell.txt
```

Check `$PATH`:

```bash
echo $PATH
```

Save `$PATH`:

```bash
echo "$PATH" | tee path.txt
```

Check where common commands are located:

```bash
which ls
which bash
which systemctl
```

Save path explanation:

```bash
{
  echo "PATH is a list of directories where Linux searches for executable commands."
  echo "Example command paths:"
  which ls
  which bash
  which systemctl 2>/dev/null || echo "systemctl not found in PATH"
} | tee path-explanation.txt
```

Create a shell variable:

```bash
MY_LESSON="Environment Variables"
echo $MY_LESSON
```

Save shell variable output:

```bash
{
  MY_LESSON="Environment Variables"
  echo "MY_LESSON=$MY_LESSON"
} | tee shell-variable.txt
```

Test child shell before export:

```bash
MY_LESSON="Environment Variables"
bash -c 'echo "Child shell before export sees MY_LESSON=$MY_LESSON"' | tee child-shell-before-export.txt
```

Export the variable:

```bash
export MY_LESSON="Environment Variables"
echo $MY_LESSON
```

Save exported variable output:

```bash
export MY_LESSON="Environment Variables"
echo "MY_LESSON=$MY_LESSON" | tee env-variable.txt
```

Test child shell after export:

```bash
bash -c 'echo "Child shell after export sees MY_LESSON=$MY_LESSON"' | tee child-shell-after-export.txt
```

Remove the variable:

```bash
unset MY_LESSON
echo $MY_LESSON
```

Save unset output:

```bash
unset MY_LESSON
echo "After unset, MY_LESSON=$MY_LESSON" | tee unset-variable.txt
```

Create `.bashrc` note:

```bash
cat > bashrc-note.txt <<'EOF'
Permanent environment variables can be added to ~/.bashrc.

Example:

export APP_ENV="dev"

After editing ~/.bashrc, reload it with:

source ~/.bashrc

Important: Be careful when editing PATH or secrets in shell config files.
EOF
```

Create safe secrets note:

```bash
cat > safe-secrets-note.txt <<'EOF'
Secrets should not be committed to GitHub.

Examples of secrets:
- API_KEY
- DATABASE_URL
- TOKEN
- PASSWORD
- PRIVATE_KEY

Good practice:
- use environment variables
- use .env files locally
- add .env to .gitignore
- use GitHub Actions Secrets for CI/CD
- use cloud secret managers in production
EOF
```

---

## Understanding Environment Variables

An environment variable is a named key/value value available to a shell process and its child processes.

Example:

```bash
HOME=/home/gourgen
USER=gourgen
PATH=/usr/local/bin:/usr/bin:/bin
```

Environment variables are often used to configure applications and tools without hardcoding values into source code.

Common DevOps examples include:

* application environment
* application port
* database URL
* API URL
* log level
* tokens
* deployment settings

---

## Understanding Shell Variables

A shell variable is available only inside the current shell unless it is exported.

Example:

```bash
MY_LESSON="Environment Variables"
echo $MY_LESSON
```

This variable exists in the current shell, but a child process will not automatically receive it.

---

## Shell Variable vs Environment Variable

| Type | Visibility |
| ---- | ---------- |
| Shell variable | Available only in the current shell |
| Environment variable | Available in the current shell and child processes |

The difference becomes clear when using a child shell:

```bash
MY_LESSON="Environment Variables"
bash -c 'echo "$MY_LESSON"'
```

Before export, the child shell does not receive the value.

After export:

```bash
export MY_LESSON="Environment Variables"
bash -c 'echo "$MY_LESSON"'
```

The child shell can see the variable.

---

## Understanding `printenv`

The `printenv` command lists environment variables.

```bash
printenv
```

To limit the output:

```bash
printenv | head -n 30
```

This is useful when checking current shell configuration.

---

## Understanding Common Variables

Common environment variables include:

| Variable | Meaning |
| -------- | ------- |
| `HOME` | Current user's home directory |
| `USER` | Current username |
| `SHELL` | Current user's default shell |
| `PATH` | Directories used to search for commands |
| `PWD` | Current working directory |

Examples:

```bash
echo $HOME
echo $USER
echo $SHELL
echo $PATH
```

---

## Understanding PATH

`PATH` is a list of directories where Linux searches for executable commands.

When a command is typed, Linux checks the directories listed in `$PATH`.

Example:

```bash
echo $PATH
```

Check where a command is located:

```bash
which ls
```

Example output:

```text
/usr/bin/ls
```

This means the `ls` executable is located in `/usr/bin`.

---

## Understanding export

The `export` command makes a variable available to child processes.

Example:

```bash
export APP_ENV="dev"
```

After exporting, scripts or child shells started from the current shell can access the variable.

Example:

```bash
bash -c 'echo "$APP_ENV"'
```

---

## Understanding unset

The `unset` command removes a variable from the current shell.

Example:

```bash
unset APP_ENV
```

After unset, the variable value is no longer available in the current shell.

---

## Temporary vs Permanent Variables

Variables created directly in the terminal are usually temporary.

Example:

```bash
export APP_ENV="dev"
```

This value exists only in the current terminal session.

After closing and reopening the terminal, the variable will usually disappear.

To make a variable permanent for Bash sessions, it can be added to `~/.bashrc`.

---

## Understanding `.bashrc`

`.bashrc` is a shell configuration file loaded by interactive Bash sessions.

A permanent variable can be added like this:

```bash
export APP_ENV="dev"
```

After editing `.bashrc`, reload it with:

```bash
source ~/.bashrc
```

Important: `.bashrc` should be edited carefully, especially when changing `PATH`.

---

## Understanding `source`

The `source` command runs a script or config file inside the current shell.

Example:

```bash
source ~/.bashrc
```

This reloads `.bashrc` without closing and reopening the terminal.

---

## Safe Secret Handling

Secrets are sensitive values that should not be committed to GitHub.

Examples of secrets include:

* API keys
* tokens
* passwords
* database URLs with credentials
* private keys

Bad practice:

```bash
export DATABASE_URL="postgres://user:password@host:5432/db"
git add .
git commit -m "Add config"
```

Good practice:

* use environment variables
* use `.env` files locally
* add `.env` to `.gitignore`
* use GitHub Actions Secrets for CI/CD
* use cloud secret managers in production
* never commit real passwords or tokens

---

## DevOps Examples

Environment variables are often used to configure applications:

```bash
export APP_ENV="production"
export APP_PORT="3000"
export LOG_LEVEL="info"
export DATABASE_URL="postgres://user:pass@host:5432/db"
```

Local `.env` example:

```env
APP_ENV=development
APP_PORT=3000
DATABASE_URL=postgres://localhost:5432/app
```

`.gitignore` should include:

```gitignore
.env
.env.local
```

---

## Why Environment Variables Matter in DevOps

Environment variables are important because they separate configuration from application code.

They are used in:

* local development
* deployment scripts
* CI/CD pipelines
* Docker containers
* systemd services
* cloud deployments
* application configuration
* secret management

A DevOps Engineer must understand how variables are passed to processes and how to avoid exposing secrets.

---

## Important Safety Notes

Environment variables can contain sensitive information.

Important safety rules:

* do not commit secrets to GitHub
* do not paste real secrets into public documentation
* do not print secrets unnecessarily in logs
* use `.gitignore` for local `.env` files
* use CI/CD secret storage for pipelines
* use cloud secret managers for production
* be careful when editing `PATH`

---

## Common Mistakes

| Mistake | Problem | Correct Practice |
| ------- | ------- | ---------------- |
| Confusing shell variables and environment variables | Child processes may not see the value | Use `export` when child processes need the variable |
| Forgetting to reload `.bashrc` | New variables may not apply immediately | Use `source ~/.bashrc` |
| Editing `PATH` incorrectly | Commands may stop working | Backup and edit carefully |
| Committing `.env` files | Secrets may leak publicly | Add `.env` to `.gitignore` |
| Printing secrets in logs | Sensitive values may be exposed | Avoid echoing real secrets |
| Hardcoding configuration | App becomes less portable and less secure | Use environment variables |

---

## Environment Variables Quick Reference

| Task | Command |
| ---- | ------- |
| List environment variables | `printenv` |
| Show a variable | `echo $VARIABLE` |
| Show home directory | `echo $HOME` |
| Show current user | `echo $USER` |
| Show shell | `echo $SHELL` |
| Show command search path | `echo $PATH` |
| Find command path | `which COMMAND` |
| Create shell variable | `VARIABLE=value` |
| Export variable | `export VARIABLE=value` |
| Remove variable | `unset VARIABLE` |
| Run child shell command | `bash -c 'COMMAND'` |
| Reload `.bashrc` | `source ~/.bashrc` |

---

## Validation

Commands used to validate this lab:

```bash
pwd
tree -a --charset=ascii
cat env-list.txt
cat path.txt
cat home-user-shell.txt
cat shell-variable.txt
cat child-shell-before-export.txt
cat env-variable.txt
cat child-shell-after-export.txt
cat unset-variable.txt
cat bashrc-note.txt
cat path-explanation.txt
cat safe-secrets-note.txt
printenv | head
echo $PATH
which ls
```

Expected result:

* lesson directory exists
* `notes.md` exists
* `notes.hy.md` exists
* `env-list.txt` exists
* `path.txt` exists
* `home-user-shell.txt` exists
* `shell-variable.txt` exists
* `child-shell-before-export.txt` exists
* `env-variable.txt` exists
* `child-shell-after-export.txt` exists
* `unset-variable.txt` exists
* `bashrc-note.txt` exists
* `path-explanation.txt` exists
* `safe-secrets-note.txt` exists
* environment variables were listed
* common variables were inspected
* `$PATH` was inspected
* shell variable behavior was tested
* exported environment variable behavior was tested
* variable removal was practiced
* safe secret handling was documented

---

## Quiz Review

| Question | Correct Answer | Status |
| -------- | -------------- | ------ |
| What is an environment variable? | A key/value value available to the shell or processes. | Passed |
| What is the difference between a shell variable and an environment variable? | A shell variable is available only in the current shell, while an environment variable is available to the current shell and child processes. | Passed |
| What does `export` do? | It makes a variable available to child processes. | Passed |
| What does `$PATH` do? | It lists directories where Linux searches for executable commands. | Passed |
| What does `unset` do? | It removes a variable from the current shell. | Passed |
| Why should secrets not be committed to GitHub? | Secrets should not be committed for security reasons because passwords, tokens or API keys can be exposed. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

If a variable is empty, check whether it was created in the current shell:

```bash
echo $VARIABLE
```

If a child shell cannot see a variable, export it first:

```bash
export VARIABLE=value
```

If a `.bashrc` change does not apply immediately, reload it:

```bash
source ~/.bashrc
```

If a command is not found, check `$PATH`:

```bash
echo $PATH
which COMMAND
```

If secrets were accidentally added to a file, do not commit the file. Remove the secret and check Git status:

```bash
git status
```

If a `.env` file exists, make sure `.gitignore` includes:

```gitignore
.env
.env.local
```

---

## Git Workflow

After completing the lesson and passing the quiz, the work will be saved using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-11-environment-variables ROADMAP.md
git commit -m "Complete Linux environment variables lesson"
git push
git status
```

---

## What I Learned

In this lesson, I learned how environment variables work in Linux.

I learned the difference between shell variables and environment variables, how to use `printenv`, `export`, `unset`, `$PATH`, `.bashrc` and `source`.

I also learned why environment variables are important in DevOps and why secrets should never be committed to GitHub.

---

## Status

Lesson completed, quiz passed, ready to commit and push.
