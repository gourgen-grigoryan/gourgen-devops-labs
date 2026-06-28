# Lesson 11 — Environment Variables

![Status](https://img.shields.io/badge/status-completed-brightgreen)
![Focus](https://img.shields.io/badge/focus-environment%20variables-blue)
![Level](https://img.shields.io/badge/level-foundation-lightgrey)

---

## Overview

Այս դասը բացատրում է Linux environment variables-ը, shell variables-ը, `$PATH`-ը, `export`, `unset`, `.bashrc`, `source` և safe secret handling-ը։

Environment variable-ը key/value արժեք է, որը օգտագործվում է shell-ի, commands-ի, scripts-ի և applications-ի կողմից։ Դրանք հաճախ օգտագործվում են application mode, ports, paths, API URLs և credentials փոխանցելու համար։

DevOps-ում environment variables-ը շատ կարևոր են, որովհետև դրանց միջոցով configuration-ը փոխանցվում է application-ին կամ automation tools-ին՝ առանց արժեքները hardcode անելու scripts-ի կամ source code-ի մեջ։

Այս դասում ես սովորեցի տեսնել environment variables-ը, ստուգել built-in variables-ը, հասկանալ `$PATH`-ը, ստեղծել shell variable, export անել environment variable, փորձարկել child shell behavior-ը, ջնջել variable և գրել safe secret handling note։

---

## Learning Objectives

Այս դասից հետո ես սովորեցի՝

* ինչ են environment variables-ը
* ինչ տարբերություն կա shell variable-ի և environment variable-ի միջև
* ինչպես list անել environment variables-ը `printenv` հրամանով
* ինչպես ստուգել common variables՝ `HOME`, `USER`, `SHELL` և `PATH`
* ինչպես `$PATH`-ը օգնում է Linux-ին գտնել commands
* ինչպես ստեղծել temporary shell variable
* ինչպես օգտագործել `export`, որ variable-ը հասանելի լինի child processes-ին
* ինչպես ստուգել variable visibility-ն child shell-ում
* ինչպես ջնջել variable-ը `unset` հրամանով
* ինչ տարբերություն կա temporary և permanent variables-ի միջև
* ինչի համար է `.bashrc` ֆայլը
* ինչպես `source ~/.bashrc`-ը reload է անում shell configuration-ը
* ինչ է safe secret handling-ը DevOps-ում
* ինչու secrets-ը պետք չէ commit անել GitHub

---

## Key Concepts

| Concept | Բացատրություն |
| ------- | ------------- |
| Variable | Անուն ունեցող արժեք, որը օգտագործվում է shell-ի կամ program-ի կողմից |
| Shell variable | Variable, որը հասանելի է միայն current shell-ում |
| Environment variable | Export արված variable, որը հասանելի է նաև child processes-ին |
| `printenv` | Command, որը list է անում environment variables-ը |
| `export` | Command, որը shell variable-ը հասանելի է դարձնում child processes-ին |
| `unset` | Command, որը ջնջում է variable-ը current shell-ից |
| `$PATH` | Folder-ների list, որտեղ Linux-ը փնտրում է executable commands |
| `.bashrc` | Interactive Bash sessions-ի startup configuration file |
| `source` | Command, որը reload է անում shell configuration-ը current shell-ում |
| Secret | Sensitive value, օրինակ՝ password, token, API key կամ private key |

---

## Commands Learned

| Command | Նպատակ | Օրինակ |
| ------- | ------ | ------ |
| `printenv` | Ցույց է տալիս environment variables-ը | `printenv` |
| `echo $VARIABLE` | Տպում է variable-ի արժեքը | `echo $HOME` |
| `echo $PATH` | Ցույց է տալիս command search path-ը | `echo $PATH` |
| `which COMMAND` | Ցույց է տալիս command-ի location-ը | `which ls` |
| `VARIABLE=value` | Ստեղծում է shell variable | `MY_LESSON="Environment Variables"` |
| `export VARIABLE=value` | Ստեղծում է environment variable | `export APP_ENV="dev"` |
| `bash -c 'COMMAND'` | Command է աշխատացնում child shell-ում | `bash -c 'echo $MY_LESSON'` |
| `unset VARIABLE` | Ջնջում է variable-ը current shell-ից | `unset MY_LESSON` |
| `source ~/.bashrc` | Reload է անում Bash configuration-ը | `source ~/.bashrc` |
| `cat FILE` | Ցույց է տալիս file-ի content-ը | `cat safe-secrets-note.txt` |
| `tee FILE` | Output-ը ցույց է տալիս և գրում է file-ի մեջ | `echo "$PATH" | tee path.txt` |

---

## Lab Structure

Այս lab-ում ստեղծվում է հետևյալ structure-ը՝

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

Ստեղծել lesson directory՝

```bash
cd ~/devops-labs/01-linux-basics
mkdir -p lesson-11-environment-variables
cd lesson-11-environment-variables
```

Ստեղծել lab files՝

```bash
touch env-list.txt path.txt home-user-shell.txt shell-variable.txt env-variable.txt child-shell-before-export.txt child-shell-after-export.txt unset-variable.txt bashrc-note.txt path-explanation.txt safe-secrets-note.txt
```

List անել environment variables-ը՝

```bash
printenv
```

Պահել առաջին environment variables-ը՝

```bash
printenv | head -n 30 | tee env-list.txt
```

Ստուգել common environment variables-ը՝

```bash
echo $HOME
echo $USER
echo $SHELL
```

Պահել common variables-ը՝

```bash
{
  echo "HOME=$HOME"
  echo "USER=$USER"
  echo "SHELL=$SHELL"
} | tee home-user-shell.txt
```

Ստուգել `$PATH`-ը՝

```bash
echo $PATH
```

Պահել `$PATH`-ը՝

```bash
echo "$PATH" | tee path.txt
```

Ստուգել՝ common commands-ը որտեղ են գտնվում՝

```bash
which ls
which bash
which systemctl
```

Պահել path explanation-ը՝

```bash
{
  echo "PATH is a list of directories where Linux searches for executable commands."
  echo "Example command paths:"
  which ls
  which bash
  which systemctl 2>/dev/null || echo "systemctl not found in PATH"
} | tee path-explanation.txt
```

Ստեղծել shell variable՝

```bash
MY_LESSON="Environment Variables"
echo $MY_LESSON
```

Պահել shell variable output-ը՝

```bash
{
  MY_LESSON="Environment Variables"
  echo "MY_LESSON=$MY_LESSON"
} | tee shell-variable.txt
```

Ստուգել child shell-ը մինչև export՝

```bash
MY_LESSON="Environment Variables"
bash -c 'echo "Child shell before export sees MY_LESSON=$MY_LESSON"' | tee child-shell-before-export.txt
```

Export անել variable-ը՝

```bash
export MY_LESSON="Environment Variables"
echo $MY_LESSON
```

Պահել exported variable output-ը՝

```bash
export MY_LESSON="Environment Variables"
echo "MY_LESSON=$MY_LESSON" | tee env-variable.txt
```

Ստուգել child shell-ը export-ից հետո՝

```bash
bash -c 'echo "Child shell after export sees MY_LESSON=$MY_LESSON"' | tee child-shell-after-export.txt
```

Ջնջել variable-ը՝

```bash
unset MY_LESSON
echo $MY_LESSON
```

Պահել unset output-ը՝

```bash
unset MY_LESSON
echo "After unset, MY_LESSON=$MY_LESSON" | tee unset-variable.txt
```

Ստեղծել `.bashrc` note՝

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

Ստեղծել safe secrets note՝

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

## Environment Variables Explanation

Environment variable-ը named key/value արժեք է, որը հասանելի է shell process-ին և դրա child processes-ին։

Օրինակ՝

```bash
HOME=/home/gourgen
USER=gourgen
PATH=/usr/local/bin:/usr/bin:/bin
```

Environment variables-ը հաճախ օգտագործվում են application-ներին և tools-ին configuration փոխանցելու համար՝ առանց source code-ում hardcode անելու։

DevOps-ում common examples՝

* application environment
* application port
* database URL
* API URL
* log level
* tokens
* deployment settings

---

## Shell Variables Explanation

Shell variable-ը հասանելի է միայն current shell-ում, եթե այն export արված չէ։

Օրինակ՝

```bash
MY_LESSON="Environment Variables"
echo $MY_LESSON
```

Այս variable-ը գոյություն ունի current shell-ում, բայց child process-ը այն automatically չի ստանում։

---

## Shell Variable vs Environment Variable

| Type | Visibility |
| ---- | ---------- |
| Shell variable | Հասանելի է միայն current shell-ում |
| Environment variable | Հասանելի է current shell-ում և child processes-ում |

Տարբերությունը պարզ երևում է child shell-ով՝

```bash
MY_LESSON="Environment Variables"
bash -c 'echo "$MY_LESSON"'
```

Մինչև export-ը child shell-ը արժեքը չի ստանում։

Export-ից հետո՝

```bash
export MY_LESSON="Environment Variables"
bash -c 'echo "$MY_LESSON"'
```

child shell-ը արդեն տեսնում է variable-ը։

---

## `printenv` Explanation

`printenv` command-ը list է անում environment variables-ը։

```bash
printenv
```

Output-ը սահմանափակելու համար՝

```bash
printenv | head -n 30
```

Սա օգտակար է current shell configuration-ը ստուգելու համար։

---

## Common Variables Explanation

Common environment variables՝

| Variable | Meaning |
| -------- | ------- |
| `HOME` | Current user-ի home directory |
| `USER` | Current username |
| `SHELL` | Current user-ի default shell |
| `PATH` | Directories, որտեղ Linux-ը փնտրում է commands |
| `PWD` | Current working directory |

Օրինակներ՝

```bash
echo $HOME
echo $USER
echo $SHELL
echo $PATH
```

---

## PATH Explanation

`PATH`-ը folder-ների list է, որտեղ Linux-ը փնտրում է executable commands։

Երբ command ես գրում, Linux-ը ստուգում է `$PATH`-ում նշված directories-ը։

Օրինակ՝

```bash
echo $PATH
```

Ստուգել command-ի location-ը՝

```bash
which ls
```

Օրինակ output՝

```text
/usr/bin/ls
```

Սա նշանակում է, որ `ls` executable-ը գտնվում է `/usr/bin` path-ում։

---

## export Explanation

`export` command-ը variable-ը հասանելի է դարձնում child processes-ին։

Օրինակ՝

```bash
export APP_ENV="dev"
```

Export-ից հետո current shell-ից start եղած scripts-ը կամ child shell-ը կարող են կարդալ այդ variable-ը։

Օրինակ՝

```bash
bash -c 'echo "$APP_ENV"'
```

---

## unset Explanation

`unset` command-ը ջնջում է variable-ը current shell-ից։

Օրինակ՝

```bash
unset APP_ENV
```

Unset-ից հետո variable-ի արժեքը այլևս հասանելի չէ current shell-ում։

---

## Temporary vs Permanent Variables

Terminal-ում direct ստեղծված variables-ը սովորաբար temporary են։

Օրինակ՝

```bash
export APP_ENV="dev"
```

Այս արժեքը գործում է միայն current terminal session-ում։

Եթե terminal-ը փակես և նորից բացես, variable-ը սովորաբար կկորի։

Bash sessions-ի համար variable-ը permanent դարձնելու համար այն կարող է ավելացվել `~/.bashrc` ֆայլում։

---

## `.bashrc` Explanation

`.bashrc`-ը shell configuration file է, որը load է լինում interactive Bash sessions-ի ժամանակ։

Permanent variable կարելի է ավելացնել այսպես՝

```bash
export APP_ENV="dev"
```

`.bashrc` edit անելուց հետո reload անել՝

```bash
source ~/.bashrc
```

Կարևոր է․ `.bashrc`-ը պետք է edit անել ուշադիր, հատկապես երբ փոխում ենք `PATH`։

---

## source Explanation

`source` command-ը script կամ config file է run անում current shell-ի մեջ։

Օրինակ՝

```bash
source ~/.bashrc
```

Սա reload է անում `.bashrc`-ը առանց terminal-ը փակելու և նորից բացելու։

---

## Safe Secret Handling

Secrets-ը sensitive values են, որոնք պետք չէ commit անել GitHub։

Secrets-ի օրինակներ՝

* API keys
* tokens
* passwords
* credentials պարունակող database URLs
* private keys

Վատ practice՝

```bash
export DATABASE_URL="postgres://user:password@host:5432/db"
git add .
git commit -m "Add config"
```

Լավ practice՝

* օգտագործել environment variables
* local-ի համար օգտագործել `.env` files
* ավելացնել `.env`-ը `.gitignore`-ի մեջ
* CI/CD-ի համար օգտագործել GitHub Actions Secrets
* production-ում օգտագործել cloud secret managers
* երբեք չcommit անել real passwords կամ tokens

---

## DevOps Examples

Environment variables-ը հաճախ օգտագործվում են applications configure անելու համար՝

```bash
export APP_ENV="production"
export APP_PORT="3000"
export LOG_LEVEL="info"
export DATABASE_URL="postgres://user:pass@host:5432/db"
```

Local `.env` օրինակ՝

```env
APP_ENV=development
APP_PORT=3000
DATABASE_URL=postgres://localhost:5432/app
```

`.gitignore`-ում պետք է լինի՝

```gitignore
.env
.env.local
```

---

## Why Environment Variables Matter in DevOps

Environment variables-ը կարևոր են, որովհետև դրանք առանձնացնում են configuration-ը application code-ից։

Դրանք օգտագործվում են՝

* local development-ում
* deployment scripts-ում
* CI/CD pipelines-ում
* Docker containers-ում
* systemd services-ում
* cloud deployments-ում
* application configuration-ում
* secret management-ում

DevOps Engineer-ը պետք է հասկանա՝ ինչպես են variables-ը փոխանցվում processes-ին և ինչպես խուսափել secrets leak-ից։

---

## Important Safety Notes

Environment variables-ը կարող են պարունակել sensitive information։

Կարևոր safety rules՝

* secrets չcommit անել GitHub
* real secrets չդնել public documentation-ում
* secrets unnecessary ձևով չտպել logs-ի մեջ
* local `.env` files-ի համար օգտագործել `.gitignore`
* pipelines-ի համար օգտագործել CI/CD secret storage
* production-ի համար օգտագործել cloud secret managers
* զգույշ լինել `PATH` edit անելիս

---

## Common Mistakes

| Սխալ | Խնդիր | Ճիշտ մոտեցում |
| ---- | ----- | ------------- |
| Շփոթել shell variable-ը և environment variable-ը | Child processes-ը կարող են չտեսնել արժեքը | Օգտագործել `export`, եթե child process-ին պետք է variable-ը |
| Մոռանալ reload անել `.bashrc`-ը | Նոր variables-ը կարող են անմիջապես չաշխատել | Օգտագործել `source ~/.bashrc` |
| Սխալ edit անել `PATH`-ը | Commands-ը կարող են չաշխատել | Edit անել ուշադիր և backup պահել |
| Commit անել `.env` files | Secrets-ը կարող են leak լինել public | Ավելացնել `.env`-ը `.gitignore` |
| Secrets տպել logs-ի մեջ | Sensitive values-ը կարող են երևալ | Չտպել real secrets |
| Hardcode անել configuration-ը | App-ը դառնում է պակաս portable և պակաս secure | Օգտագործել environment variables |

---

## Environment Variables Quick Reference

| Task | Command |
| ---- | ------- |
| List անել environment variables | `printenv` |
| Ցույց տալ variable | `echo $VARIABLE` |
| Ցույց տալ home directory | `echo $HOME` |
| Ցույց տալ current user | `echo $USER` |
| Ցույց տալ shell | `echo $SHELL` |
| Ցույց տալ command search path | `echo $PATH` |
| Գտնել command path | `which COMMAND` |
| Ստեղծել shell variable | `VARIABLE=value` |
| Export անել variable | `export VARIABLE=value` |
| Ջնջել variable | `unset VARIABLE` |
| Run անել child shell command | `bash -c 'COMMAND'` |
| Reload անել `.bashrc` | `source ~/.bashrc` |

---

## Validation

Այս lab-ը ստուգելու համար օգտագործվում են՝

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

Expected result՝

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
* environment variables-ը list է արվել
* common variables-ը ստուգվել են
* `$PATH`-ը ստուգվել է
* shell variable behavior-ը փորձարկվել է
* exported environment variable behavior-ը փորձարկվել է
* variable removal-ը practiced է
* safe secret handling-ը documented է

---

## Quiz Review

| Question | Correct Answer | Status |
| -------- | -------------- | ------ |
| What is an environment variable? | Key/value արժեք, որը հասանելի է shell-ին կամ processes-ին։ | Passed |
| What is the difference between a shell variable and an environment variable? | Shell variable-ը հասանելի է միայն current shell-ում, իսկ environment variable-ը հասանելի է current shell-ին և child processes-ին։ | Passed |
| What does `export` do? | Այն variable-ը հասանելի է դարձնում child processes-ին։ | Passed |
| What does `$PATH` do? | Այն folder-ների list է, որտեղ Linux-ը փնտրում է executable commands։ | Passed |
| What does `unset` do? | Այն ջնջում է variable-ը current shell-ից։ | Passed |
| Why should secrets not be committed to GitHub? | Secrets-ը GitHub-ում չպետք է commit անել անվտանգության պատճառով, որպեսզի passwords, tokens կամ API keys չհայտնվեն ուրիշների ձեռքում։ | Passed |

### Quiz Result

```text
Lesson quiz: Passed
```

Lesson quiz passed successfully.

---

## Troubleshooting Notes

Եթե variable-ը դատարկ է, ստուգիր՝ այն ստեղծվել է current shell-ում, թե ոչ՝

```bash
echo $VARIABLE
```

Եթե child shell-ը չի տեսնում variable-ը, նախ export արա՝

```bash
export VARIABLE=value
```

Եթե `.bashrc` փոփոխությունը անմիջապես չի աշխատում, reload արա՝

```bash
source ~/.bashrc
```

Եթե command-ը չի գտնվել, ստուգիր `$PATH`-ը՝

```bash
echo $PATH
which COMMAND
```

Եթե secrets-ը պատահաբար ավելացվել են ֆայլի մեջ, մի commit արա այդ ֆայլը։ Նախ ջնջիր secret-ը և ստուգիր Git status-ը՝

```bash
git status
```

Եթե `.env` file կա, համոզվիր, որ `.gitignore`-ում կա՝

```gitignore
.env
.env.local
```

---

## Git Workflow

Lesson-ը ավարտելուց և quiz-ը անցնելուց հետո աշխատանքը պահվելու է Git-ով՝

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

Այս դասում ես սովորեցի, թե ինչպես են environment variables-ը աշխատում Linux-ում։

Ես սովորեցի shell variables-ի և environment variables-ի տարբերությունը, ինչպես օգտագործել `printenv`, `export`, `unset`, `$PATH`, `.bashrc` և `source`։

Ես նաև սովորեցի, թե ինչու environment variables-ը կարևոր են DevOps-ում և ինչու secrets-ը երբեք պետք չէ commit անել GitHub։

---

## Status

Lesson completed, quiz passed, ready to commit and push.
