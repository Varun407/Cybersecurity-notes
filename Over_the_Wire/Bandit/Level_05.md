# Bandit Level 5 → Level 6

## Level Goal
The password for the next level is stored in a file somewhere under the `inhere` directory and has all of the following properties:
- human-readable
- 1033 bytes in size
- not executable

## Commands You May Need
`ls`, `cd`, `cat`, `file`, `du`, `find`

---

## What You Need to Know

### The `find` Command with Multiple Criteria
- `find` can search with multiple conditions using logical operators
- `-type f` - search for files only (not directories)
- `-size 1033c` - search for files exactly 1033 **bytes** (the `c` means bytes)
- `-executable` or `! -executable` - check executable permission
- Combine conditions: `find . -type f -size 1033c ! -executable`

### File Size Units in `find`
| Unit | Meaning | Example |
|------|---------|---------|
| `c` | bytes | `-size 1033c` |
| `k` | kibibytes (1024 bytes) | `-size 1k` |
| `M` | mebibytes | `-size 1M` |
| `G` | gibibytes | `-size 1G` |
| no letter | 512-byte blocks | `-size 2` |

### Directory Structure
- The `inhere` directory contains **multiple subdirectories**
- Each subdirectory contains **multiple files**
- You need to search recursively through all of them

---

## Useful Commands

```
find . -type f -size 1033c ! -executable -exec file {} \;
   - Find files, check size, exclude executable, and show file type

find . -type f -size 1033c ! -executable
   - Find files matching all criteria (human-readable check later)

find . -type f -size 1033c ! -executable -exec cat {} \;
   - Find and read matching files

ls -la
   - Show detailed file information (permissions, size)
```

---

## Solution Approaches

### Approach 1: Direct `find` with All Criteria
- Navigate to the `inhere` directory
- Use `find` with all three conditions
- The output will be the exact file path
- Read it with `cat`

**The Command:**
```bash
find . -type f -size 1033c ! -executable
```

### Approach 2: `find` with `file` Verification
- First find files matching size and permission criteria
- Pipe to `file` command to verify human-readable
- Then read the matching file

**Two-Step:**
```bash
# Find candidate files
find . -type f -size 1033c ! -executable

# Check if it's human-readable
file ./maybehere00/path/to/file

# Read it
cat ./maybehere00/path/to/file
```

### Approach 3: One-Liner with `-exec`
- Combine `find`, size check, permission check, and file type check
- Only display files that are ASCII text

```bash
find . -type f -size 1033c ! -executable -exec file {} \; | grep "ASCII text"
```

### Approach 4: Manual Exploration
- `cd` into each subdirectory
- Use `ls -la` to check file sizes and permissions
- Look for files exactly 1033 bytes that are not executable
- Read the one that contains readable text

### Approach 5: Use `find` with `-readable`
- Check if file is readable by the user
- Combine with size and permission checks

```bash
find . -type f -size 1033c ! -executable -readable
```

---

## Common Mistakes

❌ `-size 1033` (without `c`) - searches for 1033 **blocks** (512 bytes each)
❌ `-executable` instead of `! -executable` - finds executable files (wrong)
❌ Forgetting the `c` suffix and wondering why nothing is found
❌ Not specifying `-type f` and getting directories in results
❌ Using `-size 1033c` but forgetting files might be in subdirectories (use `find .`)

✅ Always use `c` for bytes: `-size 1033c`
✅ Use `! -executable` to exclude executables
✅ Start search from `.` to check all subdirectories

---

## Quick Steps

```bash
# Step 1: Enter the directory
cd inhere

# Step 2: Find the file with all properties
find . -type f -size 1033c ! -executable

# Step 3: Verify it's human-readable (optional)
find . -type f -size 1033c ! -executable -exec file {} \;

# Step 4: Read the file
cat ./maybehere07/.file2
```

---

## Understanding the Path
- The file is nested: `./maybehereXX/subdir/file`
- The exact subdirectory varies but `find` will show the path
- Copy the full path when reading with `cat`

---

**Key Lesson:** The `find` command with multiple criteria is a powerful tool for locating files with specific properties. Understanding file size units (`c` for bytes) is crucial for precise searching. The `!` operator negates conditions (`! -executable` means "not executable").
