# Day 4 — Linux Permissions

Today we're going to understand one of the most important Linux concepts for DevOps:

```text
-rwxr-xr--
```

## Understanding -rw-r--r--

Look at:

```text
-rw-r--r--
```

There are 10 characters:

```text
- r w - r - - r - -
```

Think of them as:

```text
[TYPE][OWNER][GROUP][OTHERS]
```

More specifically:

```text
- | rw- | r-- | r--
  |     |     |
  |     |     └── Others
  |     └──────── Group
  └────────────── Owner
```

The first character tells us the file type.

```text
- → regular file
  d → directory
  l → symbolic link
```

## Read, Write, Execute

Each group represents:

```text
r = read
w = write
x = execute
```

So:

rw-

means:

```text
read    ✓
write   ✓
execute ✗
```

And:

r--

means:

```text
read    ✓
write   ✗
execute ✗
```

## Three permission categories

Linux has three main permission categories:

Owner
Group
Others

For example:

```text
-rwxr-xr--
```

means:

```text
       Owner  Group  Others
         ↓      ↓      ↓
       rwx    r-x     r--
```

Therefore:

### Owner

```text
rwx
```

Can:

```text
read
write
execute
```

### Group

```text
r-x
```

Can:

```text
read
execute
```

but cannot write.

### Others

```text
r--
```

Can only read.

## Who am I?

Which user am I currently logged in as?

```bash
whoami
```

## id

```bash
id
```

You might get:

```text
uid=1000(jayanta) gid=1000(jayanta) groups=1000(jayanta),27(sudo)
```

The important concepts are:

```text
uid → User ID
gid → Group ID
groups → Groups you're a member of
```

## groups

```bash
groups
```

You might see:

```text
jayanta sudo
```

This means your user belongs to those groups. Groups are important because Linux can give permissions to an entire group.

## File ownership

Look at:

```text
-rw-r--r-- 1 jayanta jayanta 0 Oct 4 script.sh
                  ↑       ↑
                owner   group
```

There are two important fields:

```text
owner
group
```

In this example:

```text
owner = jayanta
group = jayanta
```

## chmod — Change permissions

```bash
ls -l script.sh
```

You might have:

```text
-rw-r--r-- ... script.sh
```

Notice that the file isn't executable.

Try:

```bash
./script.sh
```

You may get:

```text
Permission denied
```

That's because it doesn't have execute permission.

### Add execute permission

```bash
chmod +x script.sh
```

Now:

```bash
ls -l script.sh
```

You should see something like:

```text
-rwxr-xr-x ... script.sh
```

Now the file is executable.

### What does +x mean?

This:

```bash
chmod +x script.sh
```

means: Add execute permission.

You can also remove it:

```bash
chmod -x script.sh
```

Then:

```bash
ls -l script.sh
```

Execute permission disappears.

## Owner/group/others with chmod

You can specify who receives the permission.

### Owner command

```bash
chmod u+x script.sh
```

u = user/owner.

### Group command

```bash
chmod g+x script.sh
```

g = group.

### Others command

```bash
chmod o+x script.sh
```

o = others.

### Everyone

```bash
chmod a+x script.sh
```

a = all.

So:

```text
u → user
g → group
o → others
a → all
```

## Remove permissions

```bash
chmod o-w data.txt
```

means: Remove write permission from others.

Or:

```bash
chmod g-w data.txt
```

means: Remove write permission from the group.

## Numeric permissions

This is extremely common in Linux.

Instead of:

```bash
chmod u+rwx,g+rx,o+r script.sh
```

you'll often see:

```bash
chmod 754 script.sh
```

But where do these numbers come from?

Here's the magic:

```text
Read     = 4
Write    = 2
Execute  = 1
```

Add them together.

Read only: 4
Write only: 2
Execute only: 1
Read + Write: 4 + 2 = 6
Read + Execute: 4 + 1 = 5
Read + Write + Execute: 4 + 2 + 1 = 7

### Understanding 755

Consider:

```bash
chmod 755 script.sh
```

Break it into: 7 5 5

**First number = owner:**

```text
7 = 4 + 2 + 1
  = r + w + x
```

**Second = group:**

```text
5 = 4 + 1
  = r + x
```

**Third = others:**

```text
5 = 4 + 1
  = r + x
```

Therefore:

| 7   | 5   | 5   |
| --- | --- | --- |
| rwx | r-x | r-x |

Which produces: -rwxr-xr-x

### Why 777 is dangerous

You may see people suggesting:

```bash
chmod 777 file
```

when something doesn't work. Don't blindly do this.

777 means:

```text
Owner  → rwx
Group  → rwx
Others → rwx
```

You're essentially saying:

**Everybody can read, modify, and execute this.**

That's usually far more permission than necessary.

In DevOps, we generally follow the principle:

**Give only the permissions that are actually required.**

## Directory permissions are slightly different

This is important.

For a file:

```text
r → read file
w → modify file
x → execute file
```

For a directory:

```text
r → list contents
w → create/delete entries
x → enter/traverse directory
```

For example:

```bash
chmod 700 app
```

means only the owner can properly access/traverse that directory. You'll encounter this frequently when securing application directories.

## chown — Change ownership

chown means: Change owner.

The syntax is:

```bash
chown USER file
```

For example:

```bash
sudo chown root data.txt
```

Now root owns the file.

You can also change both owner and group:

```bash
sudo chown root:root data.txt
```

Format:

```bash
chown USER:GROUP FILE
```

Using administrator privileges, make root the owner of data.txt and make root its group.

Changes only the owner.

```bash
sudo chown :root data.txt
```

## Cheat Sheet

Identity

```bash
whoami
id
groups
```

Inspect permissions

```bash
ls -l
```

Change permissions

```bash
chmod +x script.sh
chmod -x script.sh
chmod 755 script.sh
chmod 644 data.txt
chmod 600 secret.txt
```

Ownership

```bash
chown user file
chown user:group file
```

## Homework

Let's make this more practical.

Go to:

```bash
cd ~/bash-course/day4
```

Challenge 1

Create:

```text
script.sh
secret.txt
public.txt
```

Check their permissions:

```bash
ls -l
```

Challenge 2

Make script.sh executable:

```bash
chmod 755 script.sh
```

Verify:

```bash
ls -l script.sh
```

You should see:

```text
-rwxr-xr-x
```

Challenge 3

Make secret.txt private:

chmod 600 secret.txt

Verify:

```bash
ls -l secret.txt
```

You should see:

```text
-rw-------
```

Challenge 4

Set public.txt to: 644

Run:

```bash
chmod 644 public.txt
```

Then verify.

Challenge 5 — Think before running

What permissions does this create?

```bash
chmod 750 script.sh
```

Don't look it up. Calculate it:

```text
7 = ?
5 = ?
0 = ?
```

Then tell me what the resulting permission string should be.

Thank you
