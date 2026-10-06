# Day 5 — Processes & System Basics

Today we'll learn how Linux manages running programs, processes, CPU, memory, disk space, and jobs.

This is an important day for your DevOps goal because when a server is having problems, you'll often need to answer questions like:

```text
What is running?
What is using CPU?
What is using memory?
Is my application running?
Which process is causing the problem?
How much disk space is left?
```

## Today's roadmap

```text
Process
   ↓
ps
   ↓
top
   ↓
kill
   ↓
jobs
   ↓
bg / fg
   ↓
df
   ↓
du
   ↓
free
```

## What is a process?

When you start a program:

```bash
node server.js
```

Linux creates a process.

PID means: Process ID

You can think of it as the unique ID of a running program.

## ps — See running processes

```bash
ps
```

You might see:

```text
    PID TTY          TIME CMD
   4210 pts/0    00:00:00 bash
   4382 pts/0    00:00:00 ps
```

The important columns:

```text
PID → Process ID
TTY → Terminal
TIME → CPU time
CMD → Command
```

## ps aux

The simple ps only shows processes associated with your current terminal.

A much more useful command is:

```bash
ps aux
```

This shows processes from the system.

## Find a process

Let's say you want to know whether Bash is running.

```bash
ps aux | grep bash
```

## top — Live process monitoring

```bash
top
```

It continuously updates.

### Exit top

Press: q

### What should you look for in top?

When troubleshooting a server, pay attention to:

```text
%CPU
%MEM
```

For example:

```text
PID    %CPU    %MEM    COMMAND
1234   95.0    2.0     node
```

This means the Node.js process is consuming a lot of CPU.

Another example:

```text
PID    %CPU    %MEM    COMMAND
5678   2.0     70.0    java
```

The Java process is consuming a lot of memory.

This is the beginning of real server troubleshooting.

## Start a process yourself

Let's create a simple long-running process.

```bash
sleep 1000
```

Your terminal will appear to "hang." That's because sleep is running for 1000 seconds.
Don't worry—it's not broken.

### What is Ctrl + C?

When you press:

```text
Ctrl + C
```

you're normally sending an interrupt signal to the foreground process.

## Background processes

```bash
sleep 1000 &
```

Notice the & at the end.
means: Run this command in the background.

You'll get something like:

```text
[1] 5234
```

Here:

```text
[1]  → job number
5234 → PID
```

Your terminal is immediately available again.

## jobs

```bash
jobs
```

You might see:

```text
[1]+  Running    sleep 1000 &
```

This shows background jobs associated with your current shell.

### ps vs jobs

```text
jobs = Shows jobs managed by your current shell.
ps = Shows processes.
ps aux = Shows processes across the system.
```

### Bring a job to the foreground

We have:

```bash
sleep 1000 &
```

Run:

```bash
jobs
```

You should see job number 1.

Bring it back:

```bash
fg %1
```

Now the process is in the foreground.

Press:

```text
Ctrl + C
```

to stop it.

## Suspend a process

```bash
sleep 1000
```

While it is running, press:

```text
Ctrl + Z
```

This doesn't terminate it. It pauses/suspends the process.

## Continue it in the background

```bash
bg %1
```

Now:

```bash
jobs
```

You should see:

```text
[1]+  Running  sleep 1000 &
```

You've moved the suspended process into the background. Eventually it will finish.

## kill — Stop a process

```bash
sleep 1000 &
```

Run:

```bash
jobs
```

You might get:

```text
[2]+ Running sleep 1000 &
```

Get the PID:

```bash
ps
```

or:

```bash
jobs -l
```

You might see:

```text
[2]+  6001 Running sleep 1000 &
```

Here: 6001 is the PID.

Now:

```bash
kill 6001
```

Check:

```bash
jobs
```

The process should be gone or marked terminated.

### Important: kill doesn't always mean "force kill"

When you run:

```bash
kill 6001
```

Linux normally sends a signal to the process.

The default signal is:

```text
SIGTERM
```

It basically means: Please terminate gracefully. This gives an application a chance to clean up.

### kill -9

You may eventually encounter:

```bash
kill -9 6001
```

-9 sends:

```text
SIGKILL
```

This is much more forceful.

Think:

```text
kill PID
    ↓
"Please stop."

kill -9 PID
    ↓
"Stop immediately."
```

Don't use kill -9 as your first choice.

Usually:

```text
kill PID
```

should be tried first.

## Find a process by name

You can use:

```bash
pgrep bash
```

This returns the PID(s) of matching processes.

For example: 4210

You can then inspect it:

```bash
ps -p 4210
```

This is often cleaner than:

```bash
ps aux | grep bash
```

## Disk space — df

```bash
df -h
```

You'll see something like:

```text
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1       100G   45G   55G  45% /
```

df means: Disk filesystem usage.

-h means: Human-readable.

So instead of: 104857600

you get: 100G

Much easier to understand.

### Why df -h matters

Imagine your production server suddenly stops writing logs.

You check:

```bash
df -h
```

and see:

```text
/dev/sda1    100G    100G    0G    100% /
```

**The disk is full**.

That could explain why your application is failing. This is a very common production problem.

## du — Directory size

df tells you about filesystem usage.

du tells you how much space files/directories are using.

```bash
du -h
```

You can also check a specific directory:

```bash
du -h ~/bash-course
```

For a summary:

```bash
du -sh ~/bash-course
```

-s means summary.

So:

```bash
du -sh ~/bash-course
```

might return:

```text
20K    /home/jayanta/bash-course
```

## free — Memory usage

```bash
free -h
```

You might see:

```test
               total   used   free
Mem:            16Gi    6Gi    4Gi
Swap:            2Gi    0Gi    2Gi
```

The important part is memory: **Mem**

and swap: **Swap**

-h makes the output easier to read.

## uptime

```bash
uptime
```

You might get:

```bash
10:45:22 up 3 days, 4:20, 2 users, load average: 0.20, 0.30, 0.25
```

This tells you:

```text
Current time
How long the machine has been running
Number of users
Load average
```

Don't worry too much about load average yet. We'll revisit it when we get into DevOps monitoring.

## A real server troubleshooting workflow

Imagine your Node.js API is slow. You might start with:

```bash
top
```

Look for high CPU/memory processes.

Then:

```bash
free -h
```

Check memory.

Then:

```bash
df -h
```

Check disk.

Then:

```bash
ps aux
```

Inspect processes.

Then perhaps:

```bash
ps aux | grep node
```

Look for your Node.js application.

This is the beginning of a useful Linux troubleshooting workflow.

## Cheat Sheet

Processes

```text
ps
ps aux
pgrep <name>
top
```

Stop processes

```text
kill PID
kill -9 PID
```

Shell jobs

```bash
jobs
bg
fg
```

Disk

```text
df -h
du -sh directory
```

Memory

```bash
free -h
```

System

```text
uptime
```

Day 5 Goal

You should now understand this basic picture:

```text
                  Linux System
                       │
       ┌───────────────┼───────────────┐
       ↓               ↓               ↓
    Processes         RAM            Disk
       │               │               │
    ps/top          free -h          df -h
       │
    PID
       │
    kill
```

## Homework

Challenge 1 — Start a background process

Run:

```bash
sleep 500 &
```

Then:

```bash
jobs
```

Find its PID with:

```bash
jobs -l
```

Challenge 2 — Find it with ps

Use its PID:

```bash
ps -p PID
```

Replace PID with the actual number.

Challenge 3 — Terminate it

Run:

```bash
kill PID
```

Then verify:

```bash
jobs
```

Challenge 4 — System inspection

Run these:

```bash
free -h
df -h
uptime
```

Try to understand what each section means.

Challenge 5 — Process investigation

Run:

```bash
sleep 500 &
```

Then find the process using:

```bash
pgrep sleep
```

Now terminate it using the PID returned by pgrep.

Thank you
