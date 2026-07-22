# Windows Fundamentals — Part 1 (Notes)

> My revision notes from the TryHackMe "Windows Fundamentals 1" room. Covers Windows editions, the desktop/GUI, NTFS, System32, user accounts, UAC, Settings vs Control Panel, and Task Manager.

---

## A Quick History of Windows Editions

Windows has been around since 1985 and is the most widely used OS in both home and corporate environments — which also makes it the biggest target for hackers/malware.

Quick timeline of what mattered:
- **Windows XP** — long-running, hugely popular.
- **Windows Vista** — a full overhaul, poorly received, phased out fast.
- **Windows 7** — the "safe" replacement everyone scrambled to adopt once XP's end-of-life was announced; vendors had to rush to make sure their products worked with it.
- **Windows 8.x** — short-lived, like Vista.
- **Windows 10 → Windows 11** — Windows 11 is the current desktop OS, available in **Home** and **Pro** editions.
- On the server side, the current version is **Windows Server 2025**.

Deployed VM for this room runs **Windows Server 2019 Standard** (checkable via System Information).

---

## The Desktop (GUI)

After the login screen (username + password), you land on the **Desktop** — the graphical user interface (GUI).

Main components:
- **Desktop** — shortcuts/icons for quick access; right-click for a context menu to arrange icons, create new items, or jump into **Display settings** (resolution, orientation, multi-monitor) and **Personalize** (wallpaper, themes, fonts). *Note: some display settings are disabled during a Remote Desktop session.*
- **Start Menu** — click the Windows logo to open it. Split into sections:
  1. **Account shortcuts** — account settings, lock screen, sign out, Documents/Pictures folders, Settings (gear icon), and power options (disconnect RDP session, shut down, restart).
  2. **App list** — recently added apps at the top, then all installed apps alphabetically (click a letter heading to jump straight to that section of a long list).
  3. **Tiles** — pinned app icons on the right; right-click a tile to resize, unpin, or view properties. Pin any app via right-click → **Pin to Start**.
- **Search Box (Cortana)** — search the system.
- **Task View** — see/manage open windows.
- **Taskbar** — shows currently open apps/files/folders; hover for a preview thumbnail + tooltip (handy for picking the right window when you have several instances of the same app open). Closed items vanish from the taskbar unless pinned. Right-click the taskbar for a context menu to toggle components like the Toolbar.
- **Notification Area** — bottom right; shows date/time, volume, network icons, etc. Which icons appear here is configurable in Taskbar settings.

---

## The File System — NTFS

Modern Windows uses **NTFS** (New Technology File System). Before it: **FAT16/FAT32** and **HPFS**. FAT still shows up today on USB drives and microSD cards, but not typically on Windows PCs/servers anymore.

NTFS is a **journaling file system** — if something fails, it can self-repair using a log file. FAT can't do this.

What NTFS added over older file systems:
- Support for files larger than 4GB
- Specific permissions on files/folders
- File/folder compression
- Encryption (**EFS** — Encrypted File System)

### NTFS Permissions
Available permission levels:
- Full control
- Modify
- Read & Execute
- List folder contents
- Read
- Write

To check permissions on a file/folder: **right-click → Properties → Security tab**, then select a user/group under "Group or user names" to see their specific permissions.

### Alternate Data Streams (ADS)
Every file has at least one data stream (`$DATA`), but NTFS allows a file to hold **more than one stream** — this is ADS.
- File Explorer doesn't show ADS by default — you'd need third-party tools or PowerShell to view it.
- Malware writers sometimes abuse ADS to hide data.
- Not all uses are malicious — e.g. Windows tags downloaded files with an ADS identifier noting they came from the internet.

---

## The Windows / System32 Folder

`C:\Windows` is the traditional home of the Windows OS itself — though it doesn't *have* to live on the C drive (this is where the `%windir%` environment variable comes in, since environment variables track things like OS path info, processor count, and temp folder locations).

Inside it, **`System32`** holds files critical to the OS running properly.

⚠️ Be careful in here — deleting the wrong file/folder can make Windows unbootable. A lot of the tools covered elsewhere in this series live inside System32.

---

## User Accounts, Profiles & Permissions

Two typical local account types:
- **Administrator** — can add/remove users, modify groups, change system settings, install software, etc.
- **Standard User** — limited to their own files/folders, can't make system-level changes (e.g. can't install programs).

Check existing accounts via **Start Menu → "Other User"** (Administrators see an "Add someone else to this PC" option; Standard Users don't). Clicking an account gives you **Change account type** or **Remove**.

### Profiles
A user's profile is created on their **first login**, stored at `C:\Users\<username>`. You'll briefly see a "User Profile Service" message on the login screen while this happens.

Every profile gets the same set of default folders: Desktop, Documents, Downloads, Music, Pictures.

### Local Users and Groups (`lusrmgr.msc`)
Open via **Run dialog (right-click Start → Run) → `lusrmgr.msc`**. Shows two folders:
- **Users**
- **Groups** — each group has its own permission set and description; users get added to groups by an Admin, and inherit that group's permissions. A user can belong to multiple groups.

---

## User Account Control (UAC)

Most home users run as local admins day-to-day — convenient, but risky, since malware then runs with the same elevated privileges as the logged-in user.

**UAC**, introduced in Windows Vista, fixes this: even an admin's session doesn't run with elevated permissions by default. When an action needs higher privileges, UAC pops up asking for confirmation (and a password, if prompted).

- UAC does **not** apply to the *built-in* local administrator account by default.
- Programs needing elevation show a **shield icon** overlay — a visual cue that UAC will trigger.
- If no password is entered in time, the UAC prompt disappears and the action is cancelled.

This significantly cuts down the chance of malware silently gaining elevated access.

---

## Settings vs. Control Panel

Two places to change system configuration:
- **Control Panel** — the traditional, more "advanced" location (adding printers, uninstalling programs, etc.)
- **Settings** — introduced in Windows 8 (built for touchscreens), now the primary go-to for most users.

They overlap — sometimes changing something in Settings drops you into a Control Panel window instead (e.g. Settings → Network & Internet → Change adapter options opens a Control Panel window).

To check installed applications: **Control Panel → Programs → Programs and Features** — lists all installed software with name, publisher, and version. Useful for auditing what's on a machine.

Tip: if you're not sure where a setting lives, just search for it from the Start Menu — it'll point you to the right place (Settings or Control Panel).

---

## Task Manager

Shows currently running applications and processes, plus performance stats (CPU/RAM usage under the **Performance** tab).

Access it by **right-clicking the taskbar**. It opens in a simplified view by default — click **"More details"** to unlock the full view (processes, performance, app history, startup, users, details, services).

---

## Quick Recap
- Windows history: XP → Vista (rough) → 7 → 8.x (short-lived) → 10 → 11 (current). Server side: Windows Server 2025.
- Desktop GUI = Desktop + Start Menu + Search + Task View + Taskbar + Toolbars + Notification Area.
- **NTFS** — journaling file system, supports big files, permissions, compression, encryption (EFS), and Alternate Data Streams (ADS).
- `C:\Windows` (aka `%windir%`) houses the OS; **System32** is critical — don't touch carelessly.
- Accounts: **Administrator** vs **Standard User**; profiles live in `C:\Users\<name>`; manage locally via `lusrmgr.msc`.
- **UAC** — stops admin sessions from silently running with elevated privileges; shield icon = elevation required.
- **Settings** (modern, primary) vs **Control Panel** (legacy, more advanced) — often interlinked.
- **Task Manager** — running apps/processes + performance stats; right-click taskbar → More details for the full view.
