# Bandit Level 1 → Level 2

## Level Goal

The password for the next level is stored in a file called `-` located in the home directory.

---

# Learning Objectives

In this level, we learn:

* How Linux commands interpret arguments
* Why special filenames can cause problems
* How to reference files explicitly using paths
* The importance of understanding command behavior

---

# Concepts Learned

## Special Filenames

In Linux, files can have unusual names, including:

```text
-
--
...
file with spaces.txt
$file
*file*
```

Just because a filename exists does not mean commands will interpret it as a normal file.

---

## Why is '-' Special?

Many Linux programs treat a single hyphen (`-`) as:

```text
Standard Input (stdin)
```

instead of a filename.

Example:

```bash
cat -
```

This tells `cat`:

> "Read input from the keyboard."

not:

> "Open the file named '-'"

This is why the challenge cannot be solved using a simple:

```bash
cat -
```

---

# Walkthrough

## Step 1: Login

```bash
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```

---

## Step 2: Enumerate Files

List files in the current directory.

```bash
ls
```

Output:

```text
-
```

A file named `-` exists.

---

## Step 3: Attempt to Read the File

Many beginners try:

```bash
cat -
```

The command waits for keyboard input because `cat` interprets `-` as stdin.

---

## Step 4: Reference the File Explicitly

Use a relative path:

```bash
cat ./-
```

### Breakdown

| Component | Meaning           |
| --------- | ----------------- |
| .         | Current directory |
| /         | Path separator    |
| -         | Actual filename   |

By using:

```bash
./-
```

we tell Linux:

> "This is a file located in the current directory."

instead of:

> "Treat '-' as stdin."

---

## Step 5: Save the Password

The output contains the password for the next level.

Store it securely for future levels.

---

# Alternative Solutions

Using an absolute path:

```bash
cat /home/bandit1/-
```

Using input redirection:

```bash
cat < ./
-
```

(less common)

Using another viewer:

```bash
more ./-
```

```bash
less ./-
```

---

# How Linux Parses Commands

Consider:

```bash
cat -
```

Linux sees:

```text
Command: cat
Argument: -
```

`cat` has built-in logic that interprets:

```text
-
```

as stdin.

---

Now consider:

```bash
cat ./-
```

Linux sees:

```text
Command: cat
Argument: ./-
```

Since `./-` is a valid path, `cat` treats it as a file.

---

# Real-World Cybersecurity Relevance

Attackers sometimes create files with unusual names to:

* Confuse administrators
* Break scripts
* Hide malicious files
* Exploit improper input handling

Examples:

```text
-
--help
--version
*.log
$file
```

A SOC analyst or incident responder must understand how command-line tools interpret such names.

---

# Challenge-Specific Trick

The file is named:

```text
-
```

Many Linux commands interpret a lone hyphen as:

```text
stdin (standard input)
```

rather than a filename.

The solution is to specify the file path explicitly:

```bash
cat ./-
```

This forces the command to treat it as a file.

---

# Commands Learned

```bash
ls
cat
cat ./-
pwd
```

---

# Key Takeaways

* Linux filenames can contain unusual characters.
* A single hyphen (`-`) often has special meaning.
* Commands may interpret arguments differently than expected.
* Explicit paths help avoid ambiguity.
* Understanding command parsing is an important Linux skill.

---

# Skills Gained

* Linux file enumeration
* Handling special filenames
* Understanding stdin
* Working with relative paths
* Basic command-line troubleshooting
* Cybersecurity investigation mindset
