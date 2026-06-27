# Դաս 04 — Log Reading

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-log%20reading-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը ծածկում է Linux log reading-ի հիմնական commands-ը, որոնք օգտագործվում են DevOps-ի ամենօրյա աշխատանքում։

Logs-ը առաջին տեղերից մեկն է, որտեղ պետք է նայել, երբ application, service, server կամ deployment ունի խնդիր։ DevOps Engineer-ը պետք է կարողանա արագ կարդալ logs, գտնել errors, տեսնել վերջին events-ը և հետևել live log output-ին troubleshooting-ի ժամանակ։

---

## Learning Objectives

Այս դասը ավարտելուց հետո ես սովորեցի՝

* կարդալ ամբողջ file content-ը
* inspect անել large files safely
* տեսնել file-ի սկիզբը
* տեսնել file-ի վերջը
* հետևել log file-ին live
* հաշվել file-ի տողերը
* search անել file-ի ներսում `less`-ով
* հասկանալ logs-ի կարևորությունը troubleshooting-ում
* ընտրել ճիշտ command small և large files-ի համար

---

## Commands Learned

| Command | Purpose | Example |
| ------- | ------- | ------- |
| `cat file` | Prints full file content | `cat logs/app.log` |
| `less file` | Opens file for scrolling/searching | `less logs/app.log` |
| `head file` | Shows beginning of file | `head logs/app.log` |
| `head -n 5 file` | Shows first 5 lines | `head -n 5 logs/app.log` |
| `tail file` | Shows end of file | `tail logs/app.log` |
| `tail -n 5 file` | Shows last 5 lines | `tail -n 5 logs/app.log` |
| `tail -f file` | Follows file live | `tail -f logs/app.log` |
| `wc -l file` | Counts file lines | `wc -l logs/app.log` |

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

Create lesson directory:

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-04-log-reading
cd lesson-04-log-reading
```

Create log directory and log file:

```bash
mkdir logs
touch logs/app.log
```

Append log lines:

```bash
echo "2026-06-26 10:00:01 INFO Application starting" >> logs/app.log
echo "2026-06-26 10:00:02 INFO Loading configuration" >> logs/app.log
echo "2026-06-26 10:00:03 INFO Connecting to database" >> logs/app.log
echo "2026-06-26 10:00:04 WARN Database connection is slow" >> logs/app.log
echo "2026-06-26 10:00:05 INFO Server listening on port 3000" >> logs/app.log
echo "2026-06-26 10:00:06 ERROR Failed to send email notification" >> logs/app.log
echo "2026-06-26 10:00:07 INFO Request completed" >> logs/app.log
```

Read full log:

```bash
cat logs/app.log
```

Show first 3 lines:

```bash
head -n 3 logs/app.log
```

Show last 3 lines:

```bash
tail -n 3 logs/app.log
```

Count log lines:

```bash
wc -l logs/app.log
```

Open with `less`:

```bash
less logs/app.log
```

Follow live:

```bash
tail -f logs/app.log
```

Stop live follow:

```text
Ctrl + C
```

---

## Important `less` Keys

| Key | Action |
| --- | ------ |
| `q` | Exit `less` |
| `/word` | Search for a word |
| `Space` | Move forward |
| `b` | Move backward |
| `Enter` | Move one line down |

Example search inside `less`:

```text
/ERROR
```

---

## Why Logs Matter in DevOps

Logs-ը օգնում է պատասխանել կարևոր troubleshooting հարցերի՝

* Application-ը ճիշտ start եղե՞լ է
* Configuration loading-ը fail եղե՞լ է
* Database connection կա՞
* Կա՞ն warnings
* Կա՞ն errors
* Ի՞նչ է եղել failure-ից առաջ
* Խնդիրը դեռ live շարունակվու՞մ է

DevOps-ում logs-ը օգտագործվում են՝ application failures, deployment problems, database issues, web server errors, authentication problems և production incidents debug անելու համար։

---

## `cat` vs `less` vs `head` vs `tail`

| Command | Best Used For |
| ------- | ------------- |
| `cat` | Small files |
| `less` | Large files that need scrolling/searching |
| `head` | Checking beginning of file |
| `tail` | Checking most recent lines |
| `tail -f` | Watching logs live |

---

## Important Safety Note

Large log files-ի համար `cat` command-ը սովորաբար լավ ընտրություն չէ, որովհետև ամբողջ file-ը տպում է terminal-ում։

Ավելի լավ տարբերակներ են՝

```bash
less logs/app.log
head -n 20 logs/app.log
tail -n 50 logs/app.log
tail -f logs/app.log
```

---

## Common Mistakes

| Mistake | Problem | Correct Practice |
| ------- | ------- | ---------------- |
| Large log կարդալ `cat`-ով | Terminal-ը կարող է լցվել output-ով | Օգտագործել `less`, `head`, `tail` |
| Մոռանալ դուրս գալ `less`-ից | Terminal-ը կարծես "կանգնել" է | Press `q` |
| Մոռանալ stop անել `tail -f` | Command-ը շարունակում է աշխատել | Press `Ctrl + C` |
| Միայն առաջին lines նայել | Կարող ես բաց թողնել վերջին error-ը | Օգտագործել `tail` |

---

## Log Reading Quick Reference

| Task | Command |
| ---- | ------- |
| Read small file | `cat logs/app.log` |
| Open large file | `less logs/app.log` |
| First 3 lines | `head -n 3 logs/app.log` |
| Last 3 lines | `tail -n 3 logs/app.log` |
| Follow live | `tail -f logs/app.log` |
| Count lines | `wc -l logs/app.log` |
| Search in less | `/ERROR` |
| Exit less | `q` |
| Stop live follow | `Ctrl + C` |

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

Expected result՝

* `logs/app.log` exists
* log file contains multiple lines
* `head -n 3` shows first 3 lines
* `tail -n 3` shows last 3 lines
* `wc -l` counts lines
* `less` opens file for scrolling/searching
* `tail -f` follows file live

---

## Quiz Review

| Question | Correct Answer | Status |
| --- | --- | --- |
| Why is `cat` not best for large logs? | It prints the entire file and can flood terminal output. | Passed |
| What is better than `cat` for large logs? | `less`, `head` and `tail`. | Passed |
| What does `head -n 3` do? | Shows first 3 lines. | Passed |
| What does `tail -n 3` do? | Shows last 3 lines. | Passed |
| What is `tail -f` used for? | Follows a file live. | Passed |
| How do I stop `tail -f`? | Press `Ctrl + C`. | Passed |
| How do I exit from `less`? | Press `q`. | Passed |
| Why are logs important in DevOps? | Logs help troubleshoot application, service and server problems. | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

Եթե `less` բացվել է և չես կարողանում վերադառնալ terminal՝

```text
q
```

Եթե `tail -f` շարունակում է աշխատել՝

```text
Ctrl + C
```

Եթե file-ը չկա՝

```bash
pwd
ls
tree -a --charset=ascii
```

---

## Git Workflow

After completing the lab, I saved the work using Git:

```bash
cd ~/devops-labs
git status
git add 01-linux-basics/lesson-04-log-reading
git commit -m "Add Linux log reading notes"
git push
```

---

## What I Learned

Այս դասում ես սովորեցի կարդալ և inspect անել log files Linux commands-ով։

Ես սովորեցի, որ logs-ը առաջին տեղերից մեկն է, որտեղ պետք է նայել troubleshooting-ի ժամանակ։

Ես նաև սովորեցի, որ `tail`, `tail -f`, `less`, `head` և `wc -l` կարևոր tools են DevOps-ի ամենօրյա աշխատանքի համար։

---

## Status

Lesson completed, quiz passed, committed and pushed to GitHub.
