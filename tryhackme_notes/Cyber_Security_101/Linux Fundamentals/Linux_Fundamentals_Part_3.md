# Linux Fundamentals — Part 3 (Notes)

> My revision notes from the TryHackMe "Linux Fundamentals Part 3" room — the final one in the series. Covers text editors, transferring files, processes, automation, package management, and logs.

---

## Terminal Text Editors

### Nano
Beginner-friendly, built for quick edits:
```bash
nano filename
```
- Navigate with the up/down arrows, `Enter` for a new line.
- Shortcuts use `Ctrl` (shown as `^` on screen) + a letter — e.g. `Ctrl + X` to exit.
- Also supports searching text, copy/paste, jumping to a line number, and checking your current line number.

### VIM
More advanced, steeper learning curve, but worth knowing exists:
- Fully customizable keybindings.
- Syntax highlighting — great if you're writing/reading code.
- Available on basically every Linux system, even where nano isn't installed.

---

## General Utilities — Downloading & Serving Files

### Downloading — `wget`
Grabs a file straight from a URL:
```bash
wget https://assets.tryhackme.com/additional/linux-fundamentals/part3/myfile.txt
```

### Secure Copy — `scp`
Like `cp`, but works over SSH between two machines (encrypted + authenticated):
- Push files from your machine → remote machine
- Pull files from remote machine → your machine

### Serving Files — Python's HTTPServer
Turn your current directory into a quick web server:
```bash
python3 -m http.server
```
By default it serves whatever folder you ran it in, on port `8000`. Other machines can then grab files from it using either `wget` or `curl`:
```bash
wget http://<ip>:8000/file
```
- Run it from the folder you actually want to share (e.g. a user's home directory) since it serves from wherever you launch it.
- Check `python3 -m http.server --help` / the man pages if you want to change the port or serving directory.
- Stop the server with `Ctrl + C`.

---

## Processes 101

Every running program is a **process**, and each gets a **PID** (Process ID) — these increment in the order processes start (so process #300 is followed by #301).

### Viewing processes
```bash
ps          # your session's processes
ps aux      # everyone's processes, including system/background ones
top         # live view of everything running
```
- `ps` shows things like the process's status code, which session is running it, CPU time used, and the actual command/program name.
- `ps aux` is the one to reach for when you want processes from *other* users too, or ones not tied to a session (system processes).
- `top` isn't a one-off snapshot like `ps` — it refreshes automatically (roughly every 10 seconds), and also refreshes when you scroll through rows with the arrow keys.

### Killing processes
```bash
kill 1337
```
Signals you can send along with it:
- **SIGTERM** — kill cleanly, let it clean up first *(the "proper" way to kill something)*
- **SIGKILL** — kill immediately, no cleanup
- **SIGSTOP** — pause/suspend it

```bash
kill -9 1337        # by number
kill -SIGTERM 1337  # by name
```
> Note: the TryHackMe material pairs SIGTERM with `9` and SIGKILL with `15` — worth double-checking against `man 7 signal` on a real system, since the conventional numbering is usually the other way round (SIGKILL = 9, SIGTERM = 15).

### How processes start
PID `0` is the very first process at boot — on Ubuntu that's usually **systemd**. Every other process you start afterward is a child of systemd.

### Starting services on boot — `systemctl`
Lets you talk to the systemd process/daemon directly:
```bash
systemctl [option] [service]
```
Four options worth knowing:
```bash
systemctl start apache2     # start it now
systemctl stop apache2      # stop it now
systemctl enable apache2    # start automatically on boot
systemctl disable apache2   # don't start automatically on boot
```

### Backgrounding / foregrounding
- Add `&` to a command to run it in the background right away (you get the PID back instead of the output).
- `Ctrl + Z` pauses/backgrounds a currently running process.
- `fg` brings a backgrounded process back to the foreground.

---

## Automation — Cron & Crontabs

**Cron** runs scheduled tasks automatically, defined in a **crontab**. Each line needs 6 fields:

| MIN | HOUR | DOM | MON | DOW | CMD |
|---|---|---|---|---|---|
| Minute | Hour | Day of month | Month | Day of week | Command to run |

Example — back up a folder every 12 hours:
```bash
0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/
```
`*` = wildcard, meaning "any/every" value for that field.

Edit your crontab with:
```bash
crontab -e
```
Special shortcut worth knowing: `@reboot` — runs the command every time the system boots up, instead of on a time schedule.

---

## Package Management (Overview)

Software gets installed from **repositories** (repos) — remote servers your system pulls packages/updates from. Developers submit their software to an apt repo, and once approved, it's available for anyone to install.

- On Debian/Ubuntu-based systems, the default repos are listed in `/etc/apt/sources.list` and under `/etc/apt/sources.list.d/`.
- OS vendors maintain their own official repos, but you can also add **community repos** to unlock extra software — e.g. some vendors host a repo closer to your geographic region for faster downloads.
- Add extra repos with:
  ```bash
  add-apt-repository <repo>
  ```

*(Kept light here — adding/removing repos gets fairly technical, worth a dedicated deep-dive later.)*

---

## Logs

Logs live in `/var/log` and record what's happening across your services and applications — great for monitoring system health and protecting it.

Web server logs are a good example: they record **every single request** made to the site, which lets developers/admins:
- Diagnose performance issues
- Investigate an intruder's activity after the fact

Example — Apache web server logs:
```bash
cat /var/log/apache2/access.log.1
```
Each line typically shows the visitor's IP and what resource they requested — handy for tracing exactly who accessed what.

---

## Quick Recap
- **nano** / **vim** — edit files directly in the terminal.
- **wget** / **scp** / `python3 -m http.server` — download, securely copy, and serve files.
- **ps** / **ps aux** / **top** — view processes. **kill** (with SIGTERM/SIGKILL/SIGSTOP) — manage them. **systemctl** — control services + boot behavior. `&`, `Ctrl+Z`, `fg` — background/foreground control.
- **cron** / **crontab -e** — schedule recurring tasks (6 fields: MIN HOUR DOM MON DOW CMD), `@reboot` for boot-time jobs.
- **Repositories** — where your packages come from, configured in `/etc/apt/`.
- **/var/log** — where to look when something breaks or looks suspicious.

**Series complete!** Natural next steps on TryHackMe:
- [The find command](https://tryhackme.com/room/thefindcommand)
- [Bash Scripting](https://tryhackme.com/room/bashscripting)
- [Regular Expressions](https://tryhackme.com/room/catregex)
