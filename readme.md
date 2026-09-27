# Bash Learning Roadmap — 30 Days

30-day Bash learning roadmap, starting from zero and gradually moving toward scripting, automation, and DevOps tasks.

## Phase 1 — Linux & Bash Fundamentals (Days 1–5)

| Day   | Topics                                      | Practice                                        |
| ----- | ------------------------------------------- | ----------------------------------------------- |
| **1** | Terminal, Bash, shell vs terminal, commands | `pwd`, `ls`, `cd`, `clear`, `history`           |
| **2** | Files & directories                         | `touch`, `mkdir`, `cp`, `mv`, `rm`, `find`      |
| **3** | Reading & editing files                     | `cat`, `less`, `head`, `tail`, `nano`, `vim`    |
| **4** | Permissions                                 | `chmod`, `chown`, `whoami`, `id`, `groups`      |
| **5** | Processes & system basics                   | `ps`, `top`, `kill`, `jobs`, `df`, `du`, `free` |

**Goal:** Be comfortable working inside an Ubuntu terminal without a GUI.

---

## Phase 2 — Bash Command Power (Days 6–10)

| Day    | Topics                                    |
| ------ | ----------------------------------------- |
| **6**  | Pipes `\|`, redirection `>`, `>>`, `<`    |
| **7**  | `grep`, `sort`, `uniq`, `wc`, `cut`       |
| **8**  | `awk` basics                              |
| **9**  | `sed` basics                              |
| **10** | Combining commands into useful one-liners |

For example, you'll eventually understand commands like:

```bash
cat access.log | grep "500" | sort | uniq -c
```

And:

```bash
ps aux | grep node
```

**Goal:** Learn to manipulate Linux output instead of manually reading everything.

---

### Phase 3 — Your First Bash Scripts (Days 11–15)

| Day    | Topics                                           |
| ------ | ------------------------------------------------ |
| **11** | Creating `.sh` files, shebang, executing scripts |
| **12** | Variables                                        |
| **13** | User input and arguments                         |
| **14** | `if`, `else`, `elif`                             |
| **15** | `case`, exit codes, `$?`                         |

You'll create scripts such as:

```bash
#!/bin/bash

name="Jayanta"

echo "Hello $name"
```

Then move toward:

```bash
./backup.sh database.sql
```

**Goal:** Write basic Bash programs yourself.

---

### Phase 4 — Bash Programming (Days 16–20)

| Day    | Topics                       |
| ------ | ---------------------------- |
| **16** | Arrays                       |
| **17** | `for` loops                  |
| **18** | `while` / `until`            |
| **19** | Functions                    |
| **20** | String and number operations |

You'll build things like:

```bash
for file in *.log
do
  echo "$file"
done
```

And:

```bash
function backup() {
  echo "Starting backup..."
}
```

**Goal:** Think of Bash as a programming language rather than just a collection of commands.

---

### Phase 5 — Real Bash / Linux Automation (Days 21–25)

This is where Bash becomes especially useful for your DevOps work.

| Day    | Topics                          |
| ------ | ------------------------------- |
| **21** | Environment variables           |
| **22** | `.env`, configuration & secrets |
| **23** | Error handling                  |
| **24** | Logging & debugging             |
| **25** | Cron jobs & scheduled scripts   |

You'll create scripts such as:

```text
backup-database.sh
cleanup-logs.sh
restart-server.sh
health-check.sh
```

---

### Phase 6 — DevOps Bash (Days 26–30)

| Day    | Project                                 |
| ------ | --------------------------------------- |
| **26** | Server health-check script              |
| **27** | Automated backup script                 |
| **28** | Application deployment script           |
| **29** | Log monitoring script                   |
| **30** | Complete mini DevOps automation project |

For example, your final project could look like:

```text
devops-toolkit/
├── deploy.sh
├── backup.sh
├── health-check.sh
├── logs.sh
├── restart.sh
└── config.sh
```

And eventually you could run:

```bash
./deploy.sh
```

to automate a deployment.

---

## What You'll Know After 30 Days

You should be able to:

- Navigate Linux from the terminal
- Create/manage files and directories
- Understand Linux permissions
- Find and manipulate files
- Search logs with `grep`
- Process text with `awk` and `sed`
- Use pipes and redirection
- Write Bash scripts
- Use variables and arrays
- Use conditions and loops
- Create functions
- Handle script errors
- Work with environment variables
- Create cron jobs
- Automate backups
- Monitor servers
- Automate deployments
- Write useful DevOps scripts

And importantly, you'll understand commands you see in real production environments rather than just memorizing them.

## How I'll teach you

Since you're a beginner in Bash, I recommend this pattern for **every lesson**:

```text
1. Concept
   ↓
2. Simple explanation
   ↓
3. Command examples
   ↓
4. Real-world example
   ↓
5. Practice exercises
   ↓
6. Small challenge
   ↓
7. Review
```

I won't dump 20 commands on you at once. We'll learn a small number of commands, **you'll run them on your Ubuntu machine**, and then we'll build on them.

### Your starting environment

Since you're using Ubuntu, that's perfect. We'll use Bash directly from your terminal.

**Day 1 will start from absolute zero:**

```text
Terminal
   ↓
What is Bash?
   ↓
Shell vs Bash vs Terminal
   ↓
pwd
   ↓
ls
   ↓
cd
   ↓
mkdir
   ↓
touch
   ↓
Your first mini exercise
```

Thank you.
