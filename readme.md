# Day 1 — Bash Fundamentals

Today we'll start from absolute zero. By the end, you should understand what Bash is and be comfortable with the most basic terminal commands.

## What is Bash?

First, understand these three terms:

**Terminal:**

The Terminal is the application/window where you type commands.

For example:

```bash
ls
```

Your Ubuntu terminal receives that command.

**Shell:**

A shell is a program that interprets the commands you type and tells Linux what to do.

There are several shells:

```text
sh
bash
zsh
fish
```

**Bash:**

Bash = Bourne Again SHell.

It's one of the most common Linux shells.

So the relationship is roughly:

```text
You
 ↓
Terminal
 ↓
Bash
 ↓
Linux
 ↓
Hardware
```

NB. Bash is named the Bourne-Again SHell as a clever pun on the name of **Stephen Bourne**, who created the original Unix Bourne shell (sh) in 1979.

## Remember these commands

| Command   | Meaning                |
| --------- | ---------------------- |
| `pwd`     | Where am I?            |
| `ls`      | What's here?           |
| `cd`      | Move somewhere         |
| `cd ..`   | Go to parent directory |
| `cd ~`    | Go home                |
| `mkdir`   | Create directory       |
| `touch`   | Create file            |
| `rm`      | Remove file            |
| `clear`   | Clear terminal         |
| `history` | Show previous commands |

## Homework

Challenge 1:

- Go to your home directory
- Create a directory named 'bash-course'
- Inside it create a directory named 'day1'

Challenge 2

- Enter day1 directory
- Create these files: notes.txt, commands.txt & practice.txt

Challenge 3

- Show, where are you?
- Show, What's here?
- Now show detailed listing using **-l** option/flag

Thank you.
