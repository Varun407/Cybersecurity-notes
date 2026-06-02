# Linux CLI Basics - Revision Notes

## CLI

* **CLI** = Command Line Interface
* Interact with the system using commands instead of a GUI.
* Essential for cybersecurity, Linux servers, and security tools.

---

## Important Commands

### pwd

```bash
pwd
```

* Shows current working directory.

### ls

```bash
ls
```

* Lists files and directories.

### ls -l

```bash
ls -l
```

* Detailed file information (permissions, owner, size, date).

### ls -al

```bash
ls -al
```

* Shows all files, including hidden files (`.`).

### cd

```bash
cd directory_name
```

* Change directory.

```bash
cd ..
```

* Move one directory back.

```bash
cd ~
```

* Go to home directory.

### find

```bash
find <path> -name <filename>
```

* Search for files and directories.

Example:

```bash
find ~ -name mission_brief.txt
```

### cat

```bash
cat filename.txt
```

* Display file contents.

Example:

```bash
cat mission_brief.txt
```

---

## Important Directory

### /etc

* Stores system configuration files.
* Common location for Linux settings and service configurations.

```bash
cd /etc
ls
```

---

## Cybersecurity Relevance

* Navigate Linux systems efficiently.
* Search for files during investigations.
* Read logs, reports, and configuration files.
* Perform system enumeration and basic forensics.

---

## Quick Revision Table

| Command  | Purpose                 |
| -------- | ----------------------- |
| `pwd`    | Show current directory  |
| `ls`     | List files/directories  |
| `ls -l`  | Detailed listing        |
| `ls -al` | Show hidden files       |
| `cd`     | Change directory        |
| `cd ..`  | Move back one directory |
| `find`   | Search for files        |
| `cat`    | View file contents      |

---

## Key Takeaways

* Linux is a core skill in cybersecurity.
* Learn navigation commands first (`pwd`, `ls`, `cd`).
* Use `find` to locate files quickly.
* Use `cat` to read file contents.
* Understand the purpose of the `/etc` directory.
* Comfort with the CLI is the foundation for advanced Linux and security topics.
