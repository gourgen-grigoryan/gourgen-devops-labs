# Lesson 05 — Search and Filtering

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-search%20and%20filtering-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers basic Linux search and filtering commands used in daily DevOps work.

Search and filtering skills are essential because DevOps Engineers often need to analyze logs, find configuration files, search for errors, count results, and combine commands directly from the terminal.

In this lesson, I practiced using `grep`, `find`, `wc`, and pipes to search inside files, locate files and directories, count matching results, and build simple command-line workflows.

---

## Learning Objectives

By completing this lesson, I learned how to:

* search text inside files using `grep`
* search without case sensitivity
* show matching line numbers
* exclude matching lines from output
* search recursively inside directories
* find files and directories using `find`
* find files by name, type, size and modification time
* count lines, words and bytes using `wc`
* combine commands using pipes
* count matching log entries
* avoid common search mistakes
* understand why search and filtering are important in DevOps troubleshooting

---

## Commands Learned

| Command                | Purpose                                  | Example                               |
| ---------------------- | ---------------------------------------- | ------------------------------------- |
| `grep "text" file`     | Searches for text inside a file          | `grep "ERROR" system.log`             |
| `grep -i "text" file`  | Searches without case sensitivity        | `grep -i "error" system.log`          |
| `grep -n "text" file`  | Shows matching line numbers              | `grep -n "ERROR" system.log`          |
| `grep -v "text" file`  | Shows lines that do not contain text     | `grep -v "INFO" system.log`           |
| `grep -r "text" .`     | Searches recursively                     | `grep -r "ERROR" .`                   |
| `grep -E "A\|B" file`  | Searches for multiple patterns           | `grep -E "ERROR\|WARNING" system.log` |
| `find . -name "*.log"` | Finds files by name pattern              | `find . -name "*.log"`                |
| `find . -type f`       | Finds files only                         | `find . -type f`                      |
| `find . -type d`       | Finds directories only                   | `find . -type d`                      |
| `wc -l file`           | Counts lines                             | `wc -l system.log`                    |
| `wc -w file`           | Counts words                             | `wc -w system.log`                    |
| `wc -c file`           | Counts bytes                             | `wc -c system.log`                    |
| `command1 \| command2` | Sends output from one command to another | `grep "ERROR" system.log \| wc -l`    |

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

The lab used a sample system log file:

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

The lab also used a sample users file:

```text
gourgen admin active
anna user active
aram user inactive
mariam manager active
testuser guest inactive
```

---

## Practical Commands Used

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-05-search-filtering
cd lesson-05-search-filtering
```

Create the sample log file:

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

Create the sample users file:

```bash
cat > users.txt <<'EOF'
gourgen admin active
anna user active
aram user inactive
mariam manager active
testuser guest inactive
EOF
```

Read the log file:

```bash
cat system.log
```

Read the users file:

```bash
cat users.txt
```

Find all `ERROR` lines:

```bash
grep "ERROR" system.log
```

Find all `ERROR` lines with line numbers:

```bash
grep -n "ERROR" system.log
```

Count how many `ERROR` lines exist:

```bash
grep "ERROR" system.log | wc -l
```

Find all `WARNING` lines:

```bash
grep "WARNING" system.log
```

Count how many `WARNING` lines exist:

```bash
grep "WARNING" system.log | wc -l
```

Find all `.log` files:

```bash
find . -name "*.log"
```

Find all files in the lesson directory:

```bash
find . -type f
```

Find active users correctly:

```bash
grep " active$" users.txt
```

Find both `ERROR` and `WARNING` lines:

```bash
grep -E "ERROR|WARNING" system.log
```

---

## `grep` Examples

`grep` is used to search for text inside files.

Basic search:

```bash
grep "ERROR" system.log
```

Search without case sensitivity:

```bash
grep -i "error" system.log
```

Show line numbers:

```bash
grep -n "ERROR" system.log
```

Show lines that do not contain `INFO`:

```bash
grep -v "INFO" system.log
```

Search recursively in the current directory:

```bash
grep -r "ERROR" .
```

Search for `ERROR` or `WARNING`:

```bash
grep -E "ERROR|WARNING" system.log
```

---

## `find` Examples

`find` is used to search for files and directories.

Find a file by name:

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

Find files modified in the last 24 hours:

```bash
find . -type f -mtime -1
```

---

## `wc` Examples

`wc` means word count.

It can count lines, words and bytes.

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

Show only the number of lines:

```bash
wc -l < system.log
```

---

## Pipes

The pipe symbol `|` sends the output of one command into another command.

Example:

```bash
grep "ERROR" system.log | wc -l
```

This command means:

1. Find all lines that contain `ERROR`
2. Send those lines to `wc -l`
3. Count the number of matching lines

Expected result:

```text
3
```

Another example:

```bash
grep "WARNING" system.log | wc -l
```

Expected result:

```text
2
```

---

## Important Search Detail

This command can give a wrong result:

```bash
grep "active" users.txt
```

The problem is that the word `inactive` also contains `active`.

Example:

```text
active
inactive
```

A better command is:

```bash
grep " active$" users.txt
```

The `$` symbol means end of line.

This command finds only users whose line ends with `active`.

Expected result:

```text
gourgen admin active
anna user active
mariam manager active
```

---

## Expected Lab Results

Find all `ERROR` lines:

```bash
grep "ERROR" system.log
```

Expected result:

```text
ERROR Failed to connect to database
ERROR Database connection timeout
ERROR Payment service unavailable
```

Find all `ERROR` lines with line numbers:

```bash
grep -n "ERROR" system.log
```

Expected result:

```text
4:ERROR Failed to connect to database
6:ERROR Database connection timeout
9:ERROR Payment service unavailable
```

Count `ERROR` lines:

```bash
grep "ERROR" system.log | wc -l
```

Expected result:

```text
3
```

Count `WARNING` lines:

```bash
grep "WARNING" system.log | wc -l
```

Expected result:

```text
2
```

Find all `.log` files:

```bash
find . -name "*.log"
```

Expected result:

```text
./system.log
```

Find all files:

```bash
find . -type f
```

Expected result:

```text
./notes.md
./system.log
./users.txt
```

---

## Why Search and Filtering Matter in DevOps

Search and filtering commands help answer important troubleshooting questions:

* Where is the configuration file?
* Which log file contains the error?
* How many errors happened?
* Are there warnings before the failure?
* Which files were recently changed?
* Which files are logs?
* Which users, services or entries match a condition?
* Is the issue repeated many times or only once?

In real DevOps work, these commands are commonly used when debugging:

* application logs
* deployment failures
* web server errors
* database connection issues
* authentication problems
* CI/CD pipeline logs
* system configuration files
* production incidents

---

## `grep` vs `find`

| Command | Best Used For                       |
| ------- | ----------------------------------- |
| `grep`  | Searching text inside files         |
| `find`  | Searching for files and directories |

Example:

```bash
grep "ERROR" system.log
```

This searches inside the file.

Example:

```bash
find . -name "*.log"
```

This searches for files.

---

## Common Mistakes

| Mistake                    | Problem                               | Correct Version             |
| -------------------------- | ------------------------------------- | --------------------------- |
| `grep "active" users.txt`  | Also matches `inactive`               | `grep " active$" users.txt` |
| `find . "*.log"`           | Incorrect `find` syntax               | `find . -name "*.log"`      |
| `wc system.log`            | Shows lines, words and bytes together | `wc -l system.log`          |
| Using `grep` to find files | `grep` searches inside files          | Use `find`                  |
| Forgetting quotes          | Search patterns may break             | `grep "ERROR" system.log`   |

---

## Quiz Review

| Question                                                     | Correct Answer                                                               |
| ------------------------------------------------------------ | ---------------------------------------------------------------------------- |
| What is the difference between `grep` and `find`?            | `grep` searches text inside files, `find` searches for files and directories |
| What is `wc -l` used for?                                    | It counts lines                                                              |
| What does pipe `\|` do?                                      | It sends output from one command to another                                  |
| How do I find all `.log` files?                              | `find . -name "*.log"`                                                       |
| How do I count how many `ERROR` lines exist in `system.log`? | `grep "ERROR" system.log \| wc -l`                                           |
| Why can `grep "active" users.txt` give a wrong result?       | Because it also matches `inactive`                                           |
| What does `grep -n` mean?                                    | It shows matching line numbers                                               |
| What does `grep -i` mean?                                    | It ignores uppercase and lowercase differences                               |
| What does `find . -type f` mean?                             | It finds all files                                                           |
| How do I find `ERROR` or `WARNING` lines?                    | `grep -E "ERROR\|WARNING" system.log`                                        |

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

Expected result:

* `system.log` exists
* `users.txt` exists
* `notes.md` exists
* `grep "ERROR" system.log` shows 3 error lines
* `grep -n "ERROR" system.log` shows line numbers 4, 6 and 9
* `grep "ERROR" system.log | wc -l` returns `3`
* `grep "WARNING" system.log | wc -l` returns `2`
* `find . -name "*.log"` returns `./system.log`
* `find . -type f` shows the lesson files
* `grep " active$" users.txt` returns only active users
* `grep -E "ERROR|WARNING" system.log` shows both warning and error lines

---

## Troubleshooting Notes

If `find . -name "*.log"` does not show `./system.log`, I should check my current directory:

```bash
pwd
ls
tree -a --charset=ascii
```

If `grep "ERROR" system.log` does not show results, I should check that the file exists and contains the expected text:

```bash
ls
cat system.log
```

If `grep "active" users.txt` shows inactive users too, I should use the more accurate pattern:

```bash
grep " active$" users.txt
```

If `wc -l` shows a filename and I only need the number, I can use input redirection:

```bash
wc -l < system.log
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

In this lesson, I learned how to search and filter data from the Linux terminal.

I learned that `grep` is used to search text inside files, while `find` is used to search for files and directories.

I also learned how to use `wc -l` to count lines and how to combine commands with pipes to build useful DevOps workflows.

These commands are essential for real DevOps work because logs, configuration files, errors and system outputs are often analyzed directly from the command line.

---

## Status

Lesson completed, committed and pushed to GitHub.
