# Bandit Level 3 → Level 4

## Level Goal
The password for the next level is stored in a hidden file in the **inhere** directory.

## Commands You May Need
`ls`, `cd`, `cat`, `file`, `du`, `find`

---

## What You Need to Know

### Hidden Files in Linux
- Files beginning with a dot (`.`) are hidden
- Examples: `.bashrc`, `.profile`, `.hiddenfile`
- Hidden files don't appear with a normal `ls` command
- **You need to use `ls -a` to see them** (the `-a` flag shows "all" files including hidden ones)

### Directory Navigation
- You start in your home directory (`~`)
- The `inhere` directory is inside your home directory
- You need to change into it with `cd inhere`

---

## Useful Commands

```
ls -a    - List ALL files including hidden ones (those starting with .)
ls -la   - List all files with detailed information (permissions, size, etc.)
cd       - Change directory
cat      - Display contents of a file
find .   - Find files/directories recursively from current directory
file     - Determine file type
du       - Estimate disk usage (helps find non-empty files)
```

---

## Solution Approach

### Step 1: Navigate to the Directory
- Move into the `inhere` directory from your home location
- Use `cd` with the directory name

### Step 2: List Files Properly
- Run `ls` and see what appears (it might look empty)
- **Now run `ls -a`** - notice the hidden file appears
- Hidden files always start with a dot (`.`)

### Step 3: Identify the Hidden File
- Look for any file that starts with `.`
- It could be named something like `.hidden` or `.something`
- Use `ls -la` to see file details - hidden files will be visible with `-a`

### Step 4: Read the Contents
- Use `cat` with the exact hidden filename (including the dot)
- The file contains the password for the next level

---

## Common Mistakes

❌ Staying in home directory and running `ls -a` (won't see files inside `inhere`)
❌ Running `ls` without `-a` (won't show hidden files)
❌ Guessing the filename without using `ls -a` first

✅ Change to the directory first: `cd inhere`
✅ Use `ls -a` to reveal hidden files
✅ Use `cat .hiddenfilename` to read (with the dot)

---

## Quick Steps

```bash
# Step 1: Enter the directory
cd inhere

# Step 2: List ALL files (including hidden)
ls -a

# Step 3: Identify the hidden file (e.g., .hidden)
# Step 4: Read it
cat .hiddenfilename
```

---

**Remember:** The dot at the beginning of a filename is what makes it hidden. You MUST use `-a` with `ls` to see it, and you MUST include the dot when reading it with `cat`.
