# Windows CLI Basics - Revision Notes

## Windows Command Line (CMD)

* **CMD** = Command Prompt
* Text-based interface used to interact with Windows.
* Useful for system administration, troubleshooting, and cybersecurity investigations.
* Faster and more precise than navigating through GUI menus.

---

## Essential Commands

### cd

```cmd
cd
```

* Display current directory.

```cmd
cd folder_name
```

* Change directory.

```cmd
cd ..
```

* Move one directory back.

---

### dir

```cmd
dir
```

* List files and folders in the current directory.

```cmd
dir /a
```

* Show all files, including hidden files and folders.

```cmd
dir /s filename.txt
```

* Search for a file recursively from the current directory.

Example:

```cmd
dir /s task_brief.txt
```

---

### type

```cmd
type filename.txt
```

* Display the contents of a text file.

Example:

```cmd
type task_brief.txt
```

---

## System Information Commands

### whoami

```cmd
whoami
```

* Shows the currently logged-in user.

---

### hostname

```cmd
hostname
```

* Displays the computer name.

---

### systeminfo

```cmd
systeminfo
```

* Displays detailed system information.

Important fields:

* OS Name
* OS Version
* System Type

---

### ipconfig

```cmd
ipconfig
```

* Displays network configuration.

Important fields:

* IPv4 Address
* Default Gateway

---

## Cybersecurity Relevance

* Identify the current user.
* Gather system information during investigations.
* Find files quickly.
* Read reports, notes, and logs.
* Check network configuration.
* Enumerate Windows systems efficiently.

---

## Quick Revision Table

| Command       | Purpose                     |
| ------------- | --------------------------- |
| `cd`          | Show/change directory       |
| `cd ..`       | Move back one directory     |
| `dir`         | List files and folders      |
| `dir /a`      | Show hidden files           |
| `dir /s file` | Search for a file           |
| `type`        | View file contents          |
| `whoami`      | Show current user           |
| `hostname`    | Show computer name          |
| `systeminfo`  | Display system details      |
| `ipconfig`    | Display network information |

---

## Key Takeaways

* CMD is the Windows Command Line Interface.
* `cd` and `dir` are the primary navigation commands.
* `dir /s` helps locate files when their location is unknown.
* `type` is used to read text files.
* `whoami`, `hostname`, and `systeminfo` are basic enumeration commands.
* `ipconfig` provides network information useful during investigations.
* Windows CLI skills are essential for SOC, DFIR, and system administration tasks.
