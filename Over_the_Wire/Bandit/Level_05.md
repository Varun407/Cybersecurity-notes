# Bandit Level 4 → Level 5

## Level Goal
The password for the next level is stored in the **only human-readable file** in the `inhere` directory. Tip: if your terminal is messed up, try the `reset` command.

## Commands You May Need
`ls`, `cd`, `cat`, `file`, `du`, `find`

---

## What You Need to Know

### "Human-Readable" Files
- Not all files are meant to be read by humans 
- Binary files, encrypted files, or data files appear as gibberish when viewed with `cat`
- Human-readable files typically contain plain text (ASCII or UTF-8 characters)
- **The `file` command** identifies file types and tells you which ones are readable 

### The `file` Command
- Determines the type of a file (ASCII text, data, executable, etc.) 
- `file ./*` checks all files in the current directory
- Look for output containing **"ASCII text"** - that's your human-readable file 

### The Filename Problem
- Files are named `-file00` to `-file09` 
- Filenames starting with `-` can be misinterpreted as command options 
- **Solution**: Use `./-filename` to specify the path explicitly 

---

## Useful Commands

```
file ./*          - Show file types for ALL files in current directory
file ./-file0*    - Show types for files starting with -file0
cat ./-file07     - Read a file starting with - (include the path)
cat ./{-file00..-file09}  - Read all files using brace expansion
cat ./*           - Display ALL files at once (risky, messy output)
```

---

## Solution Approaches

### Approach 1: Using the `file` Command (Best)
- Navigate to the `inhere` directory
- Run `file ./*` to identify file types
- Among the output, look for the file that says **"ASCII text"** 
- Read that specific file using `cat ./-fileXX` (with the path included)

**Expected Output Pattern:**
```
./-file00: data
./-file01: data
...
./-file07: ASCII text
...
```

### Approach 2: Trial and Error
- Navigate to `inhere` directory
- Use `cat ./-file00`, `cat ./-file01`, etc.
- When you get readable text instead of gibberish, you've found it 
- Time-consuming but works

### Approach 3: Using `grep` (Pattern Matching)
- Use `grep` to filter for password-like patterns 
- Example: `grep -rE "^[0-9a-zA-Z]+$" ./inhere/`
- Finds files containing only alphanumeric characters (password format)

### Approach 4: Read All Files at Once
- `cat ./*` - displays all files
- Scan through the output for readable text among the gibberish 
- Harder to read but works with only 10 files

---

## Common Mistakes

❌ `cat -file07` → `-f` interpreted as an option flag 
❌ Using `cat` on every file without checking types first
❌ Forgetting to `cd` into `inhere` first
❌ Running `ls` without `-la` and missing the files

✅ `cat ./-file07` → explicit path solves the `-` issue 
✅ `file ./*` → quickly identifies the right file
✅ Always check file types before reading

---

## Quick Steps

```bash
# Step 1: Enter the directory
cd inhere

# Step 2: Check file types
file ./*

# Step 3: Identify the ASCII text file (e.g., -file07)
# Step 4: Read it with the path included
cat ./-file07

---

**Key Lesson:** The `file` command is essential for identifying file types before attempting to read them. This saves time and prevents terminal corruption from binary data.
