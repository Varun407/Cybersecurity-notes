# Windows Fundamentals — Part 2 (Notes)

> My revision notes from the TryHackMe "Windows Fundamentals 2" room. This one's all about the built-in tools: System Configuration, UAC settings, Computer Management, System Information, Resource Monitor, Command Prompt, and the Registry Editor.

---

## System Configuration (`msconfig`)

A utility for advanced troubleshooting — mainly used to diagnose **startup issues**. Requires local admin rights to open.

Five tabs:

| Tab | What it's for |
|---|---|
| **General** | Choose how Windows loads devices/services on boot — `Normal`, `Diagnostic`, or `Selective` |
| **Boot** | Configure boot options for the OS |
| **Services** | Lists every configured service, running or not (a **service** = a special app that runs in the background) |
| **Startup** | Shows startup programs *(only on desktop Windows — see note below)* |
| **Tools** | A list of built-in utilities you can launch straight from here, each with a short description and a pre-filled "Selected command" you can run via Run/CMD or the Launch button |

> ⚠️ **Startup tab quirk on servers:** Microsoft says to manage startup items via **Task Manager**, not msconfig — msconfig's Startup tab isn't a real startup manager. On **Windows Server** machines specifically, Task Manager doesn't even show a Startup tab at all (servers handle this differently than client Windows like 10/11). The reliable way to check user-level startup items on a server is the **Startup folder** itself:
> ```
> Win + R → shell:startup → Enter
> ```
> This opens the folder containing shortcuts/executables set to auto-run at next login.

---

## Change UAC Settings

UAC (covered in [Windows Fundamentals 1](https://tryhackme.com/room/windowsfundamentals1xbx)) has an adjustable slider with **4 security levels**:

| Level | Behavior |
|---|---|
| **Always notify** | Highest security — notifies for both app changes *and* your own changes; dims the desktop (Secure Desktop) |
| **Notify for apps** *(default)* | Notifies only when apps try to make changes, not when you change Windows settings yourself |
| **Notify without dimming** | Same as above, but the screen doesn't dim |
| **Never notify** | No notifications at all — not recommended |

You can find/change the current level in the **User Account Control settings** window (search for it from the Start Menu).

---

## Advanced System Settings

Search **"View advanced system settings"** to open the **System Properties** panel — controls performance behavior and system recovery.

### Page File
Windows uses a **page file** as extra virtual memory once physical RAM fills up, preventing slowdowns/crashes.

View/edit it: **Advanced tab → Performance → Settings → Advanced tab (in the new window)**. Shows:
- Which drive stores the page file
- Initial size (MB)
- Maximum size
- Whether Windows manages the size automatically

### Startup and Recovery (Crash Dumps)
Windows can generate a **crash dump** on a critical error (like a Blue Screen of Death) to help diagnose what went wrong.

View/edit: **Advanced tab → Startup and Recovery → Settings**. The **"Write debugging information"** dropdown controls how much gets saved:
- Automatic memory dump
- Kernel memory dump
- Small memory dump (256 KB)
- Complete memory dump
- None

---

## Computer Management (`compmgmt`)

Three main sections: **System Tools**, **Storage**, **Services and Applications**.

### System Tools

**Task Scheduler** — create/manage tasks the computer runs automatically (run an app, script, etc.) at login, logoff, or on a set schedule (e.g. every 5 minutes).
- **Task Scheduler Library** shows all scheduled tasks — click one to see its trigger and the program/command it runs.
- Some tasks are one-off rather than recurring (e.g. *"At 2:50 PM on 6/15/2025"*).
- Create a new one via **Create Basic Task** (Actions pane, right side).

**Event Viewer** — an audit trail of events on the computer, used to diagnose problems or investigate system activity. Three panes: a tree of event log providers (left), an overview of the selected provider's events (middle), and an actions pane (right). Five event types can be logged, and standard logs live under **Windows Logs**. *(More detail in the dedicated Windows Event Log room.)*

**Shared Folders** — lists all shares available for others to connect to, including Windows defaults like `C$` and remote-admin shares like `ADMIN$`. Right-click any folder to check its **Permissions**.
- **Sessions** — who's currently connected to the shares
- **Open Files** — which files/folders connected users currently have open

**Local Users and Groups** — same tool as `lusrmgr.msc` from Windows Fundamentals 1.

**Performance** — houses **Performance Monitor (`perfmon`)**, for viewing real-time or logged performance data; useful for troubleshooting local or remote performance issues.

**Device Manager** — view and configure attached hardware (including disabling a device).

### Storage

Includes **Windows Server Backup** and **Disk Management** *(this room only covers Disk Management)*.

> Note: since the lab machine is Windows Server, some of these utilities aren't present on a typical Windows 10 install.

**Disk Management** — handles advanced storage tasks:
- Set up a new drive
- Extend a partition
- Shrink a partition
- Assign/change a drive letter (e.g. `E:`)

### Services and Applications

**Services** — view every service and its current status. Right-click → **Properties** for more detail: the actual service name (can differ from the display name), path to its executable, startup type, etc.

**Startup type** options for a service:
- **Automatic** — starts on every boot
- **Manual** — only starts when triggered by a process/user
- **Disabled** — never starts

**WMI Control** — configures the **Windows Management Instrumentation (WMI)** service, which lets scripting languages (VBScript, PowerShell) manage Windows machines locally or remotely. The old CLI companion, **WMIC**, is deprecated as of Windows 10 21H1 — PowerShell has taken over that role.

---

## System Information (`msinfo32`)

Gathers a comprehensive view of hardware, system components, and the software environment — useful for diagnosing issues.

**System Summary** is split into three sections:
- **Hardware Resources** — low-level detail, not really for average users
- **Components** — specifics on installed hardware devices (some sections, like Display and Input, are more populated than others)
- **Software Environment** — installed/built-in software, plus **Environment Variables** and **Network Connections**

Environment variables store OS-related info — e.g. `%WINDIR%` points to the Windows installation directory, so programs can look it up rather than hardcoding a path. (Also viewable via **Control Panel → System and Security → System → Advanced system settings → Environment Variables**, or **Settings → System → About → Advanced system settings → Environment Variables**.)

There's also a **search bar** near the bottom of `msinfo32` — handy for quickly finding something like an IP address under Components instead of digging manually.

---

## Resource Monitor (`resmon`)

Shows **per-process and aggregate** CPU, memory, disk, and network usage, plus which processes are holding specific file handles/modules. Also useful for spotting **deadlocked processes or file-locking conflicts** without just force-closing an app and losing data.

Geared toward advanced troubleshooting. Four sections (with matching tabs across the top):
- **CPU**
- **Memory**
- **Disk**
- **Network**

There's also a live graphical pane on the far right showing real-time stats for each section.

---

## Command Prompt (`cmd`)

Before GUIs existed, the command line was the *only* way to interact with an OS. It's still there under the hood for direct interaction.

Basic identity commands:
```cmd
hostname    :: outputs the computer's name
whoami      :: outputs the currently logged-in user
```

Networking / troubleshooting commands:
```cmd
ipconfig    :: shows network address settings
```

Get help for (most) commands:
```cmd
ipconfig /?
```

Clear the screen:
```cmd
cls
```

**`netstat`** — displays protocol statistics and current TCP/IP connections. Supports parameters like `-a`, `-b`, `-e`, etc., each changing what gets shown.

**`net`** — manages network resources via sub-commands. Running `net` alone shows the available sub-commands. Unlike most commands, `/?` doesn't work for help here — instead use:
```cmd
net help
net help user       :: help for the "user" sub-command specifically
```
Same pattern works for other sub-commands like `localgroup`, `use`, `share`, `session`.

*(Full command reference: [ss64.com/nt](https://ss64.com/nt/))*

---

## Registry Editor (`regedit`)

The **Windows Registry** is a central hierarchical database storing configuration info for the system, users, applications, and hardware. It holds things like:
- Per-user profiles
- Installed applications and the document types each can create
- Property sheet settings for folders/icons
- Installed hardware
- Ports in use

⚠️ Advanced-user territory — bad edits here can break normal system operation. View/edit it via `regedit`.

---

## Quick Recap
- **msconfig** — General/Boot/Services/Startup/Tools tabs; on servers, check `shell:startup` instead of relying on the Startup tab.
- **UAC slider** — 4 levels from Always notify (safest) to Never notify (off).
- **Advanced System Settings** — page file config + crash dump (Startup and Recovery) settings.
- **Computer Management** — Task Scheduler, Event Viewer, Shared Folders, Local Users/Groups, Performance Monitor, Device Manager (System Tools); Disk Management (Storage); Services + WMI Control (Services and Applications).
- **msinfo32** — hardware/components/software overview, plus environment variables and a handy search bar.
- **resmon** — live CPU/memory/disk/network usage per process, good for deadlock/file-lock troubleshooting.
- **cmd** — `hostname`, `whoami`, `ipconfig`, `netstat`, `net` (+ `net help <subcommand>` since `/?` doesn't work for it), `cls` to clear.
- **regedit** — central config database; edit with caution.
