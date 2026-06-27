# Դաս 05 — Search and Filtering

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-search%20and%20filtering-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը ծածկում է Linux search և filtering commands-ը, որոնք օգտագործվում են DevOps-ի ամենօրյա աշխատանքում։

Search և filtering skills-ը կարևոր են, որովհետև DevOps Engineer-ը հաճախ պետք է analyze անի logs, գտնի configuration files, փնտրի errors, հաշվի results և միացնի commands terminal-ի մեջ։

Այս դասում ես practice արեցի `grep`, `find`, `wc` և pipes օգտագործելով։

---

## Learning Objectives

Այս դասը ավարտելուց հետո ես սովորեցի՝

* text որոնել files-ի ներսում `grep`-ով
* search անել առանց uppercase/lowercase տարբերության
* ցույց տալ matching line numbers
* exclude անել matching lines output-ից
* recursive search անել directories-ի մեջ
* գտնել files/directories `find`-ով
* գտնել files name, type, size և modification time-ով
* հաշվել lines, words և bytes `wc`-ով
* միացնել commands pipes-ով
* հաշվել matching log entries
* խուսափել common search mistakes-ից

---

## Commands Learned

| Command | Purpose | Example |
| ------- | ------- | ------- |
| `grep "text" file` | Search text inside file | `grep "ERROR" system.log` |
| `grep -i "text" file` | Case-insensitive search | `grep -i "error" system.log` |
| `grep -n "text" file` | Show line numbers | `grep -n "ERROR" system.log` |
| `grep -v "text" file` | Exclude matching lines | `grep -v "INFO" system.log` |
| `grep -r "text" .` | Recursive search | `grep -r "ERROR" .` |
| `grep -E "A\|B" file` | Search multiple patterns | `grep -E "ERROR\|WARNING" system.log` |
| `find . -name "*.log"` | Find files by name pattern | `find . -name "*.log"` |
| `find . -type f` | Find files only | `find . -type f` |
| `find . -type d` | Find directories only | `find . -type d` |
| `wc -l file` | Count lines | `wc -l system.log` |
| `wc -w file` | Count words | `wc -w system.log` |
| `wc -c file` | Count bytes | `wc -c system.log` |
| `command1 \| command2` | Pipe output to another command | `grep "ERROR" system.log \| wc -l` |

---

## Lab Structure

In this lab, I created the following structure:

```text
lesson-05-search-filtering/
|-- notes.md
|-- system.log
`-- users.txt
```

---

## Sample Log File

```text
INFO Server started successfully
INFO Loading configuration file
WARNING Disk usage is above 70%
ERROR Failed to connect to database
INFO Retrying connection
ERROR Database connection timeout
INFO User login successful
WARNING Memory usage is high
ERROR Payment service unavailable
INFO Server health check passed
```

---

## Sample Users File

```text
gourgen admin active
anna user active
aram user inactive
mariam manager active
testuser guest inactive
```

---

## Practical Commands Used

Create lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-05-search-filtering
cd lesson-05-search-filtering
```

Create sample log file:

```bash
cat > system.log <<'EOF'
INFO Server started successfully
INFO Loading configuration file
WARNING Disk usage is above 70%
ERROR Failed to connect to database
INFO Retrying connection
ERROR Database connection timeout
INFO User login successful
WARNING Memory usage is high
ERROR Payment service unavailable
INFO Server health check passed
EOF
```

Create sample users file:

```bash
cat > users.txt <<'EOF'
gourgen admin active
anna user active
aram user inactive
mariam manager active
testuser guest inactive
EOF
```

Find all `ERROR` lines:

```bash
grep "ERROR" system.log
```

Find `ERROR` lines with line numbers:

```bash
grep -n "ERROR" system.log
```

Count `ERROR` lines:

```bash
grep "ERROR" system.log | wc -l
```

Find `WARNING` lines:

```bash
grep "WARNING" system.log
```

Count `WARNING` lines:

```bash
grep "WARNING" system.log | wc -l
```

Find all `.log` files:

```bash
find . -name "*.log"
```

Find all files:

```bash
find . -type f
```

Find active users correctly:

```bash
grep " active$" users.txt
```

Find `ERROR` or `WARNING`:

```bash
grep -E "ERROR|WARNING" system.log
```

---

## `grep` Examples

`grep` command-ը text է փնտրում files-ի ներսում։

Basic search:

```bash
grep "ERROR" system.log
```

Case-insensitive search:

```bash
grep -i "error" system.log
```

Line numbers:

```bash
grep -n "ERROR" system.log
```

Exclude `INFO` lines:

```bash
grep -v "INFO" system.log
```

Recursive search:

```bash
grep -r "ERROR" .
```

Multiple patterns:

```bash
grep -E "ERROR|WARNING" system.log
```

---

## `find` Examples

`find` command-ը փնտրում է files և directories։

Find file by name:

```bash
find . -name "system.log"
```

Find all `.log` files:

```bash
find . -name "*.log"
```

Find only files:

```bash
find . -type f
```

Find only directories:

```bash
find . -type d
```

Find files larger than 1 MB:

```bash
find . -type f -size +1M
```

Find files modified in last 24 hours:

```bash
find . -type f -mtime -1
```

---

## `wc` Examples

`wc` նշանակում է word count։

Count lines:

```bash
wc -l system.log
```

Count words:

```bash
wc -w system.log
```

Count bytes:

```bash
wc -c system.log
```

Only number of lines:

```bash
wc -l < system.log
```

---

## Pipes

Pipe symbol `|`-ը մի command-ի output-ը փոխանցում է հաջորդ command-ին։

```bash
grep "ERROR" system.log | wc -l
```

Սա նշանակում է՝

1. գտնել `ERROR` տողերը
2. փոխանցել դրանք `wc -l`-ին
3. հաշվել matching lines-ը

Expected result:

```text
3
```

---

## Important Search Detail

Այս command-ը կարող է սխալ result տալ՝

```bash
grep "active" users.txt
```

քանի որ `inactive` բառի մեջ նույնպես կա `active`։

Ավելի ճիշտ command՝

```bash
grep " active$" users.txt
```

`$` նշանակում է line-ի վերջ։

---

## Common Mistakes

| Mistake | Problem | Correct Version |
| ------- | ------- | --------------- |
| `grep "active" users.txt` | Also matches `inactive` | `grep " active$" users.txt` |
| `find . "*.log"` | Incorrect `find` syntax | `find . -name "*.log"` |
| `wc system.log` | Shows lines, words and bytes together | `wc -l system.log` |
| Using `grep` to find files | `grep` searches inside files | Use `find` |
| Forgetting quotes | Search patterns may break | `grep "ERROR" system.log` |

---

## Search and Filtering Quick Reference

| Task | Command |
| ---- | ------- |
| Find text | `grep "ERROR" system.log` |
| Ignore case | `grep -i "error" system.log` |
| Show line numbers | `grep -n "ERROR" system.log` |
| Count matches | `grep "ERROR" system.log | wc -l` |
| Find log files | `find . -name "*.log"` |
| Find files only | `find . -type f` |
| Find directories only | `find . -type d` |
| ERROR or WARNING | `grep -E "ERROR|WARNING" system.log` |

---

## Validation

Commands used to validate this lab:

```bash
pwd
tree -a --charset=ascii
cat system.log
cat users.txt
grep "ERROR" system.log
grep -n "ERROR" system.log
grep "ERROR" system.log | wc -l
grep "WARNING" system.log | wc -l
find . -name "*.log"
find . -type f
grep " active$" users.txt
grep -E "ERROR|WARNING" system.log
```

Expected result՝

* `system.log` exists
* `users.txt` exists
* `notes.md` exists
* `grep "ERROR" system.log` shows 3 error lines
* `grep -n "ERROR"` shows lines 4, 6 and 9
* `grep "ERROR" system.log | wc -l` returns `3`
* `grep "WARNING" system.log | wc -l` returns `2`
* `find . -name "*.log"` returns `./system.log`

---

## Quiz Review

| Question | Correct Answer | Status |
| --- | --- | --- |
| What is `grep` used for? | `grep` searches for text inside files. | Passed |
| What does `grep -i` do? | It searches without caring about uppercase or lowercase letters. | Passed |
| What does `grep -n` do? | It shows matching line numbers. | Passed |
| What does `grep -r` do? | It searches recursively inside directories. | Passed |
| What is `find` used for? | `find` searches for files and directories. | Passed |
| What does `find . -name "*.log"` do? | It finds `.log` files from the current directory downward. | Passed |
| What does `wc -l` do? | It counts lines. | Passed |
| What does pipe `|` do? | It sends output from one command to another command. | Passed |
| How do I count `ERROR` lines in a log? | `grep "ERROR" system.log | wc -l`. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

Եթե `find . -name "*.log"` չի ցույց տալիս `./system.log`, ստուգել current directory՝

```bash
pwd
ls
tree -a --charset=ascii
```

Եթե `grep "ERROR" system.log` result չի տալիս՝

```bash
ls
cat system.log
```

Եթե `grep "active" users.txt` ցույց է տալիս inactive users նույնպես՝

```bash
grep " active$" users.txt
```

---

## Git Workflow

After completing the lab, I saved the work using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-05-search-filtering
git commit -m "Add Linux search and filtering notes"
git push
```

---

## What I Learned

Այս դասում ես սովորեցի search և filter անել data Linux terminal-ից։

Ես սովորեցի, որ `grep`-ը օգտագործվում է text search-ի համար files-ի ներսում, իսկ `find`-ը՝ files և directories գտնելու համար։

Ես նաև սովորեցի օգտագործել `wc -l` lines հաշվելու համար և pipe-երով կառուցել useful DevOps workflows։

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
