# Day 2 — Files & Directories

Today we'll learn how to create, copy, move, rename, delete, and find files.

By the end, you'll be able to manage a project directory entirely from Bash.

## Remember these commands

| Command    | Purpose                   |
| ---------- | ------------------------- |
| `mkdir`    | Create directory          |
| `mkdir -p` | Create nested directories |
| `cp`       | Copy                      |
| `cp -r`    | Copy directory            |
| `mv`       | Move                      |
| `mv`       | Rename                    |
| `rmdir`    | Remove empty directory    |
| `rm`       | Remove file               |
| `rm -r`    | Remove directory          |
| `find`     | Find files/directories    |
| `*`        | Any number of characters  |
| `?`        | One character             |

### mkdir — Create directories

Create three directories:

```bash
mkdir projects backups logs
```

Create nested directories, You can create multiple levels with -p:

```bash
mkdir -p projects/backend/src
```

NB. The -p option creates parent directories when necessary.

### cp — Copy files

Syntax:

```text
cp SOURCE DESTINATION
```

Example:

```bash
# Create a file
touch notes.txt

# Copy it
cp notes.txt notes-backup.txt
```

### Copy a file into a directory

Let's copy notes.txt into backups directory:

```bash
cp notes.txt backups/
```

### Copy an entire directory

```bash
cp -r projects projects-copy
```

NB. The -r means recursive. It's required when copying directories and their contents.

### mv — Move files

```bash
mv commands-new.txt backups/
```

### mv is also used for renaming

Syntax:

```text
mv old-name new-name
```

Example:

```bash
mv notes-backup.txt notes-old.txt
```

### Can move and rename a file at the same time using mv

```bash
mv old-file.txt /path/to/directory/new-file.txt
```

### Rename a directory

```bash
mv projects-copy old-projects
```

### Delete an empty directory

```bash
rmdir test-folder
```

NB. **rmdir** works only for empty directories.

### rm -r — Delete a directory with files

```bash
rm -r old-projects
```

Never casually run commands like:

```bash
rm -rf /
```

or,

```bash
rm -rf *
```

until you fully understand what they target.

### Wildcards

#### \* means "anything"

```bash
ls *.log
```

means: List all files in the current directory whose names end with .log

```bash
ls log*
```

means: List all files/directories whose names start with log.

#### ? represents one character

```bash
ls ca?.txt
```

means: Find .txt files whose name starts with ca, followed by exactly one character.

### find — Find files

Find all .txt files:

```bash
find . -name "*.txt"
```

This searches for files exactly named: **notes.txt**

```base
find . -name "notes.txt"
```

Explain:

find = The command

. = Start searching from the current directory

-name = Search based on filename

"\*.txt" = Filename pattern

#### Find directories

You can tell find that you only want directories:

```bash
find . -type d
```

#### Find file

You can tell find that you only want files:

```bash
find . -type f
```

A real-world example

```bash
find /var/www/app -type f -name "*.log"
```

## Homework

Now let's make this more realistic.

From:

```bash
cd ~/bash-course
```

Create this structure:

```text
bash-course/
└── day2/
    ├── projects/
    │   ├── backend/
    │   └── frontend/
    ├── backups/
    └── logs/
```

Then create these files:

```text
day2/
├── projects/
│   ├── backend/
│   │   └── app.js
│   └── frontend/
│       └── app.js
├── backups/
│   └── backup.txt
└── logs/
    ├── app.log
    └── error.log
```

**Then perform these operations:**

1. Copy app.js from backend to backups.

2. Rename the copied file to:

```text
backend-app.js
```

3. Move error.log into backups.

4. Find all .log files under day2.

5. Find all .js files under day2.

6. Create a copy of the entire backend directory called:

```text
backend-backup
```

Thank you.
