# Linux Fundamentals — Part 2 (Notes)

> My revision notes from the TryHackMe "Linux Fundamentals Part 2" room. This part moves from the in-browser terminal to actually SSH-ing into a remote machine, plus flags, file management, and permissions.

---

## SSH — Connecting to a Remote Machine

**SSH (Secure Shell)** lets you log into and control a remote Linux machine over an encrypted connection — no more in-browser terminal, this is the real deal.

Syntax:
```bash
ssh username@IP_address
```

Example:
```bash
ssh tryhackme@MACHINE_IP
```
Enter the password when prompted (it won't show any characters as you type — totally normal, not frozen).

Once you're in, every command you run executes on the **remote machine**, not your own.

---

## Flags & Switches

Most commands accept extra arguments called **flags/switches** — written with a `-` followed by a letter/keyword. They change a command's default behavior.

Example — `ls` normally hides dotfiles (hidden files), but:
```bash
ls -a
```
`-a` (all) shows hidden files/folders too (anything starting with `.`).

Other useful ones:
- `--help` — most commands support this, gives you a quick list of accepted options.
- `-h` — human-readable output (e.g. `ls -lh` shows file sizes as KB/MB instead of raw bytes).

### man pages
For the full documentation on any command:
```bash
man ls
```
- Navigate down with the **down arrow** (or `f`/`b` for bigger jumps).
- Quit with `q`.

---

## Creating, Copying, Moving & Deleting

| Command | What it does |
|---|---|
| `touch` | Creates a new (empty) file |
| `mkdir` | Creates a new directory |
| `cp` | Copies a file or folder |
| `mv` | Moves (or renames) a file or folder |
| `rm` | Deletes a file or folder |
| `file` | Tells you the type of a file |

**Create a file:**
```bash
touch newnote
```

**Create a folder:**
```bash
mkdir myfolder
```

**Copy a file** (takes two arguments — source, then destination name):
```bash
cp oldfile newfile
```

**Move / rename a file** (same two-argument pattern, but this one moves/merges instead of duplicating):
```bash
mv myfile myfolder
```
Same command works for renaming — `mv oldname newname`.

**Delete a file:**
```bash
rm somefile
```
Delete a folder — needs the recursive flag:
```bash
rm -R somefolder
```

**Check a file's type:**
```bash
file note
# note: ASCII text
```

---

## Permissions 101

List permissions for everything in a folder:
```bash
ls -lh
```
```
-rw-r--r-- 1 cmnatic cmnatic 0 Feb 19 10:37 file1
```

Breaking that permission string down — it's split into 4 parts:

1. **File type** — `-` = regular file, `d` = directory
2. **Owner** permissions — `rw-`
3. **Group** permissions — `r--`
4. **Other** (everyone else) permissions — `r--`

Each set of 3 = **r**ead, **w**rite, **e**xecute (in that order — a `-` means that permission is missing).

So `-rw-r--r--` means: it's a file, the owner can read+write, and everyone else (group + other) can only read.

### Switching users — `su`

```bash
su username
```
You'll need to know the target user's password (unless you're root/using sudo).

Useful flag: `-l` (or `--login`) — starts a full login shell as that user, so you inherit their environment variables etc., basically like actually logging in as them.

```bash
su -l username
```

---

## Common Directories to Know

| Directory | What lives there |
|---|---|
| `/etc` | System config files — includes `sudoers` (who can run sudo), and `passwd`/`shadow` (where user passwords are stored, hashed with SHA-512) |
| `/var` | Variable/frequently-changing data — logs live in `/var/log`, plus things like databases |
| `/root` | Home directory of the **root** user (not `/home/root` like you'd guess) |
| `/tmp` | Temporary storage — anyone can write here by default, and it's wiped on reboot. Handy for pentesting (dropping scripts) since it doesn't need special permissions |

---

## Quick Recap
- `ssh user@IP` — connect to a remote Linux box.
- Flags/switches (`-a`, `-h`, `--help`) extend default command behavior; `man <command>` for full docs.
- `touch` / `mkdir` — create files/folders. `cp` / `mv` — copy/move/rename. `rm` (`-R` for folders) — delete. `file` — check file type.
- Permissions: `-rwxrwxrwx` → type, owner, group, other. `su` (or `su -l`) to switch users.
- Key directories: `/etc` (configs), `/var` (logs/data), `/root` (root's home), `/tmp` (scratch space, wiped on reboot).

**Series done!** On to applying this stuff in actual boxes.
