# Day 3 — Reading & Editing Files

Today we'll learn how to read, create, edit, search, and inspect text files from Bash.

This is especially important because, later, you'll spend a lot of time working with logs, configuration files, .env files, JSON, YAML, and application output.

## Today's roadmap

## Remember these commands

```text
cat
 ↓
less
 ↓
head / tail
 ↓
nano
 ↓
echo
 ↓
>
>>
 ↓
file contents
```

## > — Write to a file

```bash
echo "Hello Bash" > notes.txt
```

means: Write/redirect output into a file. If the file doesn't exist, Bash creates it. If it already exists, its previous contents are replaced.

NB. Remember this. > can overwrite files.

## >> — Append to a file

```bash
echo "First line" > notes.txt
echo "Second line" >> notes.txt
echo "Third line" >> notes.txt

cat notes.txt
```

The difference is:

```text
> → overwrite
>> → append
```

This is one of the most useful concepts in Bash.

## cat — Read a file

It displays the entire file.

```bash
cat notes.txt
```

You can also combine multiple files:

```bash
cat file1.txt file2.txt
```

## less — Read large files

This lets you read the file page by page.

```bash
less application.log
```

Useful keys inside less:

```text
Space      → next page
b          → previous page
↑ / ↓      → move
/word      → search
q          → quit
```

## head — First lines

```bash
head numbers.txt
```

By default, head shows the first 10 lines.

Specify number of lines (show the first 5 lines)

```bash
head -n 5 numbers.txt
```

## tail — Last lines

```bash
tail numbers.txt
```

It shows the last 10 lines.

Specify number of lines (show the last 5 lines)

```bash
tail -n 5 numbers.txt
```

## Homework

Let's make this more practical.

Go to:

```text
cd ~/bash-course/day3
```

Challenge 1 — Create a configuration file

Create:

```text
config.txt
```

with Nano.

Put:

```text
APP_NAME=MyBashApp
APP_ENV=development
APP_PORT=3000
DATABASE=postgres
```

Then save it.

Verify:

```text
cat config.txt
Challenge 2 — Create a log
```

Create **server.log** using **echo** and **>>**.

It should contain:

```text
Server starting
Database connecting
Database connected
Server listening
Request received
Request completed
```

Then verify with:

```bash
cat server.log
```

Challenge 3 — Inspect the log

Run:

```bash
head -n 3 server.log
```

Then:

```bash
tail -n 3 server.log
```

Observe the difference.

Challenge 4 — Count

Run:

```bash
wc -l server.log
```

You should get:

```text
6 server.log
```

Challenge 5 — Live log monitoring

Run:

```bash
tail -f server.log
```

Keep it running.

Open another terminal and execute:

```bash
cd ~/bash-course/day3
echo "New request received" >> server.log
echo "Request completed" >> server.log
```

Watch the first terminal.

Then press:

```text
Ctrl + C
```

to stop **tail -f**.

Thank you
