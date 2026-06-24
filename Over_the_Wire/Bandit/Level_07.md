# Bandit Level 6 → Level 7

## Level Goal
The password for the next level is stored **somewhere on the server** and has all of the following properties:
- owned by user **bandit7**
- owned by group **bandit6**
- **33 bytes** in size

## Commands You May Need
`ls`, `cd`, `cat`, `file`, `du`, `find`, `grep`

---

## What You Need to Know

### Searching the Entire Filesystem
- The file is **not** in the current directory or home folder
- It's located **somewhere** on the server
- You need to search from the root directory (`/`)
- **Permission Denied** errors will appear when searching restricted areas

### The `find` Command with User/Group Criteria
| Option | Meaning | Example |
|--------|---------|---------|
| `-user bandit7` | File owned by user bandit7 | `find / -user bandit7` |
| `-group bandit6` | File owned by group bandit6 | `find / -group bandit6` |
| `-size 33c` | File size exactly 33 bytes | `-size 33c` |
| `-type f` | Only files (not directories) | `-type f` |

### Handling Permission Errors
- Searching from `/` will generate many "Permission denied" errors
- These are **normal** and can be ignored
- **Redirect stderr** to hide them: `2>/dev/null`
- The file you're looking for is accessible to your user

---

## Useful Commands

```
find / -user bandit7 -group bandit6 -size 33c
   - Search entire filesystem for matching files

find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
   - Same but hide all "Permission denied" errors

find / -user bandit7 -group bandit6 -size 33c -type f 2>/dev/null
   - Ensure only files, not directories

cat /var/lib/path/to/file
   - Read the file once found
```

---

## Solution Approaches

### Approach 1: Direct `find` from Root
- Search from `/` with all three conditions
- Redirect stderr to `/dev/null` for cleaner output
- Read the found file

```bash
find / -user bandit7 -group bandit6 -size 33c -type f 2>/dev/null
```

### Approach 2: Without Hiding Errors
- Run `find` without `2>/dev/null`
- Look through the errors for the one file that's found
- **Expected**: Many "Permission denied" + one valid path

```bash
find / -user bandit7 -group bandit6 -size 33c
```

### Approach 3: Search Specific Directories
- Limit search to directories you can access
- Check `/var`, `/tmp`, `/home`, `/etc` for better performance

```bash
find /var /tmp /home /etc -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

### Approach 4: Use `-exec` to Verify
- Find the file and display its details
- Use `ls -la` or `file` to confirm properties

```bash
find / -user bandit7 -group bandit6 -size 33c -type f -exec ls -la {} \; 2>/dev/null
```

### Approach 5: Step-by-Step
- First check all files owned by bandit7
- Then filter by group bandit6
- Then filter by size 33c

```bash
# Step 1: Find files owned by bandit7
find / -user bandit7 2>/dev/null

# Step 2: Further filter (pipe to grep or use more conditions)
find / -user bandit7 -group bandit6 2>/dev/null

# Step 3: Add size
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

---

## Common Mistakes

❌ Searching from current directory (`.`) instead of root (`/`) - won't find it
❌ `-size 33` (without `c`) - that's 33 **blocks** (512 bytes each)
❌ Forgetting `-type f` and getting directories
❌ Not using `2>/dev/null` and getting overwhelmed by errors
❌ Assuming the file is in `/home` or `/etc` - could be anywhere
❌ Using `grep` incorrectly when you already have `find`

✅ Search from `/` - the file exists on the server
✅ Always use `c` for bytes: `-size 33c`
✅ Use `2>/dev/null` to hide permission errors
✅ The file will be accessible (no "Permission denied" for the actual file)

---

## Quick Steps

```bash
# Step 1: Search the entire filesystem
find / -user bandit7 -group bandit6 -size 33c -type f 2>/dev/null

# Step 2: Note the path (e.g., /var/lib/.../somefile)
# Step 3: Read the file
cat /path/to/found/file
```

---

## Understanding the Output

**Expected Result:**
```
/var/lib/dpkg/info/bandit7.password
```

The file is typically in `/var/lib/dpkg/info/` or `/etc/` or similar system directory.

---

## Performance Tip
- Searching from `/` can be slow
- Redirect errors (`2>/dev/null`) to speed up
- If too slow, try common directories first: `/var`, `/tmp`, `/home`, `/etc`

---

**Key Lesson:** When a file can be anywhere on a system, use `find` from the root directory (`/`). Understanding user/group ownership (`-user`, `-group`) is essential for system administration and security auditing. Always check your `find` conditions carefully - size units matter!
