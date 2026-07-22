# Linux Fundamentals — Part 1 (Notes)

> My revision notes from the TryHackMe "Linux Fundamentals Part 1" room. Keeping this short and practical — just the commands, what they do, and how to use them.

---

## Why Linux?

Linux is everywhere, even if you don't notice it — websites, car dashboards, POS/checkout systems, traffic light controllers, smart devices. It's lightweight compared to Windows/Mac, but the tradeoff is most servers don't have a GUI. You interact through the **terminal** instead.

Ubuntu/Debian are common distros because they're flexible — same OS can run as a full desktop or a barebones server (Ubuntu Server can run on just 512MB RAM).

---

## First Commands

| Command | What it does |
|---|---|
| `echo` | Prints text back to the terminal |
| `whoami` | Shows which user you're logged in as |

```bash
echo Hello
# Hello

echo "Hello Friend!"
# Hello Friend!
```

Note: wrap text in quotes if there's a space in it, otherwise it's not needed.

```bash
whoami
# tryhackme
```

---

## Moving Around the Filesystem

| Command | Full name | What it does |
|---|---|---|
| `ls` | listing | Lists what's in the current directory |
| `cd` | change directory | Moves you into a directory |
| `cat` | concatenate | Prints the contents of a file |
| `pwd` | print working directory | Shows the full path of where you are |

**`ls`** — see what's around you:
```bash
ls
# 'Important Files' 'My Documents' Notes Pictures
```
Tip: you can `ls` a folder without moving into it — `ls Pictures`.

**`cd`** — move into a folder:
```bash
cd Pictures
ls
# dog_picture1.jpg dog_picture2.jpg ...
```

**`cat`** — read a file's contents:
```bash
cat todo.txt
# Here's something important for me to do later!
```
Tip: works without navigating there first — `cat /home/ubuntu/Documents/todo.txt`.
Useful for pulling out usernames, passwords, flags, config values sitting in plain text files.

**`pwd`** — find out exactly where you are:
```bash
pwd
# /home/ubuntu/Documents
```
Handy since you can then just `cd /home/ubuntu/Documents` to jump straight back later.

---

## Searching for Stuff — `find` and `grep`

Instead of manually `cd`-ing and `ls`-ing through every folder, these two commands search for you.

### `find` — locate files by name

Search by exact filename:
```bash
find -name passwords.txt
# ./folder1/passwords.txt
```

Search using a wildcard (`*`) for anything matching a pattern:
```bash
find -name *.txt
# ./folder1/passwords.txt
# ./Documents/todo.txt
```

### `grep` — search inside file contents

Where `find` locates files, `grep` looks *inside* them for a value.

```bash
wc -l access.log
# 244 access.log

grep "81.143.211.90" access.log
# 81.143.211.90 - - [25/Mar/2021:11:17 +0000] "GET / HTTP/1.1" 200 417 ...
```
Way faster than manually reading through hundreds of log lines.

**Recursive search** — search every file in a directory *and* its subfolders with `-R`:
```bash
grep -R "PRETTY_NAME" /etc/
# grep: /etc/sudoers: Permission denied
# /etc/os-release:PRETTY_NAME="Ubuntu"
```
The file path shows up before the match, so you know exactly where it was found.

---

## Shell Operators

| Operator | Description |
|---|---|
| `&` | Runs a command in the background |
| `&&` | Chains commands — second one only runs if the first succeeds |
| `>` | Redirects output to a file (overwrites) |
| `>>` | Redirects output to a file (appends, doesn't overwrite) |

**`&`** — free up the terminal while something long-running (like a big file copy) finishes.

**`&&`** — chain commands together:
```bash
command1 && command2
```
`command2` only fires if `command1` actually succeeded.

**`>`** — send command output into a file instead of the screen:
```bash
echo hey > welcome
cat welcome
# hey
```
⚠️ Overwrites the file completely if it already exists.

**`>>`** — same idea, but appends instead of wiping the file:
```bash
echo hello >> welcome
cat welcome
# hey
# hello
```

---

## Quick Recap
- Linux is lightweight, everywhere, and mostly driven through the terminal.
- `echo` / `whoami` — basic output + identity check.
- `ls` / `cd` / `cat` / `pwd` — navigate and read the filesystem.
- `find` — locate files by name/pattern. `grep` — search file contents (add `-R` for recursive).
- `&`, `&&`, `>`, `>>` — control how and where commands run/output.

**Next up:** [Linux Fundamentals Part 2](https://tryhackme.com/jr/linuxfundamentalspart2/)
