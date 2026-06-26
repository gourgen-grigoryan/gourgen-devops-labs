# Lesson 04 — Log Reading

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-log%20reading-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

This lesson covers basic Linux log reading commands used in daily DevOps work.

Logs are one of the first places to check when an application, service, server or deployment has a problem. A DevOps Engineer must be able to read logs quickly, find errors, inspect recent events and follow live log output during troubleshooting.

---

## Learning Objectives

By completing this lesson, I learned how to:

* read full file contents
* inspect large files safely
* view the beginning of a file
* view the end of a file
* follow log files live
* count lines in a file
* search inside files using `less`
* understand why logs are important in troubleshooting
* choose the right command for small and large files

---

## Commands Learned

| Command          | Purpose                                  | Example                  |
| ---------------- | ---------------------------------------- | ------------------------ |
| `cat file`       | Prints the full file content             | `cat logs/app.log`       |
| `less file`      | Opens a file for scrolling and searching | `less logs/app.log`      |
| `head file`      | Shows the beginning of a file            | `head logs/app.log`      |
| `head -n 5 file` | Shows the first 5 lines                  | `head -n 5 logs/app.log` |
| `tail file`      | Shows the end of a file                  | `tail logs/app.log`      |
| `tail -n 5 file` | Shows the last 5 lines                   | `tail -n 5 logs/app.log` |
| `tail -f file`   | Follows a file live                      | `tail -f logs/app.log`   |
| `wc -l file`     | Counts lines in a file                   | `wc -l logs/app.log`     |

---

## Lab Structure

In this lab, I created the following structure:

```text
lesson-04-log-reading/
|-- logs
|   `-- app.log
`-- notes.md
```

---

## Sample Log File

The lab used a sample application log file:

```text
2026-06-26 10:00:01 INFO Application starting
2026-06-26 10:00:02 INFO Loading configuration
2026-06-26 10:00:03 INFO Connecting to database
2026-06-26 10:00:04 WARN Database connection is slow
2026-06-26 10:00:05 INFO Server listening on port 3000
2026-06-26 10:00:06 ERROR Failed to send email notification
2026-06-26 10:00:07 INFO Request completed
```

---

## Practical Commands Used

Create the lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-04-log-reading
cd lesson-04-log-reading
```

Create the log directory and log file:

```bash
mkdir logs
touch logs/app.log
```

Append log lines to the file:

```bash
echo "2026-06-26 10:00:01 INFO Application starting" >> logs/app.log
echo "2026-06-26 10:00:02 INFO Loading configuration" >> logs/app.log
echo "2026-06-26 10:00:03 INFO Connecting to database" >> logs/app.log
echo "2026-06-26 10:00:04 WARN Database connection is slow" >> logs/app.log
echo "2026-06-26 10:00:05 INFO Server listening on port 3000" >> logs/app.log
echo "2026-06-26 10:00:06 ERROR Failed to send email notification" >> logs/app.log
echo "2026-06-26 10:00:07 INFO Request completed" >> logs/app.log
```

Read the full log file:

```bash
cat logs/app.log
```

Show the first 3 lines:

```bash
head -n 3 logs/app.log
```

Show the last 3 lines:

```bash
tail -n 3 logs/app.log
```

Count log lines:

```bash
wc -l logs/app.log
```

Open the log file with `less`:

```bash
less logs/app.log
```

Follow the log file live:

```bash
tail -f logs/app.log
```

Exit live follow mode:

```text
Ctrl + C
```

---

## Important `less` Keys

| Key     | Action             |
| ------- | ------------------ |
| `q`     | Exit `less`        |
| `/word` | Search for a word  |
| `Space` | Move forward       |
| `b`     | Move backward      |
| `Enter` | Move one line down |

Example search inside `less`:

```text
/ERROR
```

This searches for the word `ERROR` inside the opened file.

---

## Why Logs Matter in DevOps

Logs help answer important troubleshooting questions:

* Did the application start correctly?
* Did configuration loading fail?
* Did the application connect to the database?
* Are there warnings?
* Are there errors?
* What happened before the failure?
* Is the issue still happening live?

In real DevOps work, logs are commonly used when debugging:

* application failures
* deployment problems
* database connection issues
* web server errors
* authentication problems
* failed background jobs
* slow services
* production incidents

---

## `cat` vs `less` vs `head` vs `tail`

| Command   | Best Used For                             |
| --------- | ----------------------------------------- |
| `cat`     | Small files                               |
| `less`    | Large files that need scrolling/searching |
| `head`    | Checking the beginning of a file          |
| `tail`    | Checking the most recent lines            |
| `tail -f` | Watching logs live                        |

---

## Important Safety Note

For large log files, `cat` is usually not the best option because it prints the entire file into the terminal.

For large logs, better options are:

```bash
less logs/app.log
head -n 20 logs/app.log
tail -n 50 logs/app.log
tail -f logs/app.log
```

This helps avoid flooding the terminal with too much output.

---

## Validation

Commands used to validate this lab:

```bash
pwd
tree -a --charset=ascii
cat logs/app.log
head -n 3 logs/app.log
tail -n 3 logs/app.log
wc -l logs/app.log
less logs/app.log
tail -f logs/app.log
```

Expected result:

* `logs/app.log` exists
* the log file contains multiple log lines
* `head -n 3` shows the first 3 lines
* `tail -n 3` shows the last 3 lines
* `wc -l` counts the number of lines
* `less` opens the file for scrolling and searching
* `tail -f` follows the file live

---

## Troubleshooting Notes

If `less` opens and I cannot return to the terminal, I should press:

```text
q
```

If `tail -f` keeps running, I should stop it with:

```text
Ctrl + C
```

If a file does not exist, I should check my location and file structure:

```bash
pwd
ls
tree -a --charset=ascii
```

---

## Quiz Review

### 1. Why is `cat` not the best option for large log files?

`cat` prints the entire file directly into the terminal.

For large log files, this can flood the terminal with too much output and make troubleshooting harder.

Better options for large log files are:

```bash
less logs/app.log
head -n 20 logs/app.log
tail -n 50 logs/app.log
```

---

### 2. What does `tail -n 3` do?

The command:

```bash
tail -n 3 logs/app.log
```

shows the last 3 lines of the file.

This is useful when I want to quickly check the most recent log entries.

---

### 3. What is `tail -f` used for?

The command:

```bash
tail -f logs/app.log
```

follows a log file live.

If new lines are added to the file, they appear in the terminal immediately.

To stop `tail -f`, I use:

```text
Ctrl + C
```

---

### 4. How do I exit from `less`?

To exit from `less`, I press:

```text
q
```

---

### Quiz Result

```text
cat and large logs: Passed
tail -n usage: Passed
tail -f usage: Passed
less exit key: Passed
```

Lesson quiz passed successfully.

---

## Git Workflow

After completing the lab, I saved the work using Git:

```bash
cd ~/devops-labs
git status
git add .
git commit -m "Add Linux log reading notes"
git push
```

After improving the lesson documentation, I saved the updated notes using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-04-log-reading/notes.md
git commit -m "Add log reading quiz review"
git push
```

---

## What I Learned

In this lesson, I learned how to read and inspect log files using common Linux commands.

I learned that logs are one of the first places to check when troubleshooting application, service or server problems.

I also learned that `tail`, `tail -f`, `less`, `head` and `wc -l` are important tools for daily DevOps work.

---

## Status

Lesson completed, committed and pushed to GitHub.
