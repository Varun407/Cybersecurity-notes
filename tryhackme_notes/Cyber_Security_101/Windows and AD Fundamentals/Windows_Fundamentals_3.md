# Windows Fundamentals — Part 3 (Notes)

> My revision notes from the TryHackMe "Windows Fundamentals 3" room — the final part of the series, focused on Windows' built-in security tools: Updates, Windows Security dashboard, Defender, Firewall, App & Browser Control, Device Security, BitLocker, and VSS.

---

## Windows Updates

Microsoft ships updates on **"Patch Tuesday"** — the 2nd Tuesday of every month. Urgent/critical fixes don't wait for that schedule though — they can roll out immediately.

The **Windows Update** utility (Settings or Start Menu search) lets you:
- Check for updates
- Schedule them
- View update history

If you keep dismissing updates for too long, Windows will eventually force a restart to install them.

To check update history: **Settings → Windows Update → View update history** — categorized (e.g. "Definition Updates" for Defender's virus definitions).

---

## Windows Security (Dashboard)

A central dashboard for reviewing your system's overall security status, using **green/yellow/red** color-coding to flag how urgent an issue is.

From here you can jump into:
- Virus & threat protection
- Firewall & network protection
- App & browser control
- Device security
- And more

Whichever area is flagged (yellow/red) on the dashboard is the one that needs your attention first.

---

## Virus & Threat Protection

Windows' built-in antivirus is **Microsoft Defender**, managed through this section.

**Current threats** area shows:
- Results of the most recent scan
- Any unresolved threats
- Scan options: **Quick**, **Full**, **Custom**, **Offline**
  - *Quick scan* — good starting point; tells you if a full scan is actually needed
  - *Offline scan* — useful if you suspect a stubborn infection that's hard to catch while Windows is fully running

**Manage Settings** holds the key toggles:
- **Real-time protection** — actively blocks malware from executing; only works while it's switched on (if the dashboard flags Virus & Threat Protection, this is very often the setting that's off)
- **Cloud-delivered protection** — lets Microsoft check suspicious code against a cloud database for faster, more robust detection

---

## Firewall & Network Protection

Windows' built-in firewall runs on **three network profiles**:

| Profile | Typical use case |
|---|---|
| **Domain** | Corporate/managed network |
| **Private network** | Trusted home/office network |
| **Public network** | Untrusted networks — e.g. airport or coffee-shop Wi-Fi |

Each profile can independently have its firewall turned on/off, block all incoming connections, or allow specific traffic through custom rules. Connecting to something like open airport Wi-Fi would put you on the **Public network** profile — the most locked-down of the three by default.

---

## App & Browser Control

Works alongside Defender to add another protection layer. Two main pieces:

- **Check apps and files** (reputation-based protection) — powered by **Microsoft Defender SmartScreen**, which flags unrecognized apps/files and warns you before you run or download something potentially malicious.
- **Exploit protection** — defends against a number of specific exploit techniques, adding extra hardening beyond standard antivirus detection.

---

## Device Security

A smaller, rarely-touched section focused on hardware-level protections.

- **Core isolation** — isolates critical processes from the rest of the OS. The main setting here is **memory integrity**, which uses **Hyper-V virtualization** to run isolated processes inside a protected VM-like memory space, shielding them from attacks.
- **Security processor / TPM (Trusted Platform Module)** — a dedicated chip that handles cryptographic operations. If your system has one, its details show up here.

---

## BitLocker

Protects data on lost/stolen devices by encrypting the drive. Works best paired with a **TPM**.

- With a TPM (version 1.2 or later) — BitLocker can unlock automatically and transparently at boot.
- **Without** a TPM — you need to insert a **USB startup key** at boot or when resuming from hibernation, since there's no chip to handle the unlock automatically.

---

## Volume Shadow Copy Service (VSS)

**VSS** coordinates backup/restore operations between the backup application, the app being backed up, and the underlying storage — so backups can happen **without taking the application offline**. Introduced with Windows Server 2003.

Malware authors are often aware of VSS and specifically try to bypass or destroy shadow copies (a common ransomware move) — which is exactly why **offline backups** still matter, even with VSS in place.

---

## Quick Recap
- **Windows Update** — Patch Tuesday (2nd Tuesday monthly), urgent patches can arrive off-schedule; check via "View update history."
- **Windows Security dashboard** — green/yellow/red status across all security categories.
- **Virus & Threat Protection (Defender)** — Quick/Full/Custom/Offline scans; Real-time protection + Cloud-delivered protection are the key toggles.
- **Firewall** — three profiles: Domain, Private, Public (public Wi-Fi = Public profile, most restrictive).
- **App & Browser Control** — SmartScreen (reputation checks) + Exploit protection.
- **Device Security** — Core isolation/memory integrity (Hyper-V based) + TPM info.
- **BitLocker** — drive encryption; TPM enables automatic unlock, otherwise a USB startup key is required.
- **VSS** — enables live backups without taking apps offline; still worth keeping offline backups since malware can target VSS directly.
