# Data Exfiltration Detection — Complete Notes

# 1. Introduction to Data Exfiltration

## What is Data Exfiltration?

Data exfiltration is the **unauthorized transfer of sensitive data** from a computer or other device to an external destination controlled by an adversary.

**Key Point:** It's a primary objective for attackers who have breached a network.

## Why Adversaries Perform Data Exfiltration

| Reason | Description |
|--------|-------------|
| **Financial Gain** | Stolen data (credit cards, personal records) sold on dark web or used for fraud |
| **Espionage** | Nation-states target intellectual property, trade secrets, classified data |
| **Ransomware & Extortion** | Steal data, threaten to leak unless ransom paid |
| **Disruption & Sabotage** | Damage reputations or operations by leaking internal data |
| **Persistence & Reconnaissance** | Exfiltrated data helps understand environment for future attacks |

## Threat Actors & Exfiltration Techniques

| Threat Actor | Exfiltration Method |
|--------------|-------------------|
| APT Groups | Custom malware, DNS tunneling, encrypted channels |
| Ransomware Gangs | HTTP/HTTPS uploads, cloud storage, FTP |
| Insider Threats | USB drives, email, cloud sync |
| Hacktivists | Public leaks, social media, paste sites |

## Common Exfiltration Phases

```
Discovery/Collection
       ↓
Staging/Compression
       ↓
Exfiltration Transport
       ↓
C2 Coordination
```

**Detailed Breakdown:**

| Phase | Description | Examples |
|-------|-------------|----------|
| **Discovery/Collection** | Locate sensitive files | File enumeration, data mining |
| **Staging/Compression** | Aggregate, compress, encrypt | ZIP, RAR, 7z, tar, base64, steganography |
| **Exfiltration Transport** | Transfer over network | HTTP, DNS, FTP, ICMP, cloud, removable media |
| **C2 Coordination** | Orchestrate transfer | Beaconing, confirmation receipts |

---

# 2. Data Exfiltration Overview

## Techniques and Indicators

### Host-Level Indicators
- Unusually large or frequent outbound uploads
- Suspicious process command-lines
- Network connections from unexpected processes
- Sysmon/EDR alerts

### Network-Level Indicators
- Unusually large HTTP POST requests
- High-entropy DNS queries
- Long DNS subdomain labels
- Persistent ICMP sessions
- FTP transfers to suspicious IPs

### Cloud-Level Indicators
- Cloud storage API activity
- Unusual cloud sync patterns
- Unauthorized access to cloud resources

## Effective Triage Questions for SOC L1

| Question | Purpose |
|----------|---------|
| Who is the source host/user? | Identify compromised system |
| What is the destination? | Identify where data is going |
| How much data was transferred? | Assess impact |
| What process initiated the transfer? | Identify malware/attack tool |
| What supporting evidence exists? | Correlate across logs |

## Key Concept

> Data exfiltration detection depends less on single-point alerts and more on **rapid correlation** across host, network, and cloud telemetry.

---

# 3. Detection: DNS Tunneling

## What is DNS Tunneling?

DNS exfiltration abuses the **Domain Name System** to smuggle data out of a network.

**Why DNS is Attractive:**
- DNS is normally allowed through firewalls
- DNS queries are routine and ubiquitous
- DNS uses UDP port 53 (often unfiltered)
- Data can be encoded into subdomain labels

## How DNS Tunneling Works

```
Compromised Host → External DNS Server
Query: subdomain.attacker.com
Where "subdomain" contains encoded data
```

**Data Encoding:**
- Base32 (common in DNS)
- Base64
- Hexadecimal

## Indicators of Attack (IoAs)

| Indicator | Description |
|-----------|-------------|
| **Many DNS queries** | High count to single external domain |
| **Long subdomain labels** | > 60-100 characters |
| **High entropy patterns** | Base32/Base64-like characters |
| **Rare record types** | TXT, NULL, MX queries |
| **Unusual responses** | Frequent NXDOMAIN, TCP/large fragments |
| **Regular intervals** | Beaconing behavior |

## Detection: Wireshark

**File Location:** `/data_exfil/dns_exfil/dns_exfil.pcap`

### Step 1: Filter DNS Traffic
```
dns
```

### Step 2: Filter DNS Queries (No Response)
```
dns.flags.response == 0
```

### Step 3: Find Long Queries
```
dns && frame.len > 70
```

### Step 4: Isolate Suspicious Domain
```
dns && dns.qry.name contains <suspicious_domain>
```

**Example Results:**
```
tunnelcorp.net identified as suspicious domain
Multiple internal hosts compromised
Data sent in chunks via DNS tunneling
```

## Detection: Splunk

**Search Query:**
```
index="data_exfil" sourcetype="DNS_logs"
```

### Step 1: View All DNS Logs
```
index="data_exfil" sourcetype="DNS_logs"
```

### Step 2: Count by Source IP
```
index="data_exfil" sourcetype="DNS_logs" | stats count by src_ip
```

### Step 3: Count by Query
```
index="data_exfil" sourcetype="dns_logs" | stats count by query | sort -count
```

### Step 4: Filter Long Queries
```
index="data_exfil" sourcetype="DNS_logs" | where len(query) > 30
```

### Step 5: Identify Source with Max Requests
```
index="data_exfil" sourcetype="DNS_logs" | where len(query) > 30 | stats count by src_ip | sort -count
```

## Key Findings from DNS Tunneling

| Question | Answer |
|----------|--------|
| Suspicious Domain | **tunnelcorp.net** |
| Number of Suspicious Logs | **315** |
| Source IP with Max Requests | **192.168.1.103** |

## Exfiltration Through HTTP

**Technique Classification:** Network-based

---

# 4. Detection: FTP Exfiltration

## What is FTP Exfiltration?

FTP (File Transfer Protocol) is used to move large amounts of data off a network using:
- Compromised credentials
- Misconfigured servers
- Ephemeral accounts

## How Attackers Use FTP

| Method | Description |
|--------|-------------|
| **Legitimate FTP Servers** | Public or misconfigured internal servers |
| **Compromised Credentials** | Service accounts, user credentials |
| **Non-Standard Ports** | Tunneling to blend with other traffic |
| **PASV Mode** | Data channel on ephemeral ports |

## Indicators of Attack

| Indicator | Description |
|-----------|-------------|
| **USER/PASS commands** | Cleartext credentials |
| **STOR command** | Uploads (exfiltration) |
| **RETR command** | Downloads (collection) |
| **Large transfers** | Unusual volume to external IPs |
| **Data channel openings** | Large payloads on ephemeral ports |

## Detection: Wireshark

**File Location:** `/data_exfil/ftp_exfil/ftp-lab.pcap`

### Step 1: Isolate FTP Traffic
```
ftp || ftp-data
```

### Step 2: Look for Credentials
```
ftp.request.command == "USER" || ftp.request.command == "PASS"
```

### Step 3: Look for Uploads
```
ftp contains "STOR"
```

### Step 4: Look for Suspicious Files
```
ftp contains "csv"
ftp contains "pdf"
ftp contains "xlsx"
```

### Step 5: Analyze TCP Stream
```
Right-click packet → Follow → TCP Stream
```

### Step 6: Check Large Payloads
```
ftp && frame.len > 90
```

## Detection: Key Findings

| Question | Answer |
|----------|--------|
| Connections from guest account | **5** |
| Customer file exfiltrated from root | **customer_data.xlsx** |
| Internal IP with largest payload | **192.168.1.105** |
| Flag in CSV transfer stream | **THM{ftp_exfil_hidden_flag}** |

---

# 5. Detection: HTTP Exfiltration

## What is HTTP Exfiltration?

Data exfiltration using HTTP as the transport protocol.

**Why HTTP is Attractive:**
- Blends with normal web traffic
- Traverses firewalls and proxies
- Can be obfuscated (encoding, encryption)
- HTTPS provides encryption

## How Attackers Use HTTP

| Method | Description |
|--------|-------------|
| **POST uploads** | Bulk data in POST request bodies |
| **GET with encoded data** | Small chunks in query strings |
| **Common services/CDN** | Disguised as cloud service uploads |
| **Custom headers** | Data in `X-Data:` headers |
| **Chunked transfer** | Large payloads split across requests |
| **HTTPS tunneling** | Encrypted channel hides payload |
| **Cloud staging** | Upload to Dropbox/GitHub then fetch externally |

## Indicators of Attack

| Indicator | Description |
|-----------|-------------|
| **Unusually large POST** | Large request body to external host |
| **Low reputation domains** | Rarely seen in baseline traffic |
| **Frequent small requests** | Beaconing followed by large uploads |
| **Chunked/multipart transfers** | Multiple requests composing larger file |

## Detection: Splunk

### Step 1: View HTTP Logs
```
index="data_exfil" sourcetype="http_logs"
```

### Step 2: Filter POST Requests
```
index="data_exfil" sourcetype="http_logs" method=POST
```

### Step 3: Analyze Data Volume by Domain
```
index="data_exfil" sourcetype="http_logs" method=POST | stats count avg(bytes_sent) max(bytes_sent) min(bytes_sent) by domain | sort - count
```

### Step 4: Isolate Large POSTs
```
index="data_exfil" sourcetype="http_logs" method=POST bytes_sent > 600 | table _time src_ip uri domain dst_ip bytes_sent | sort - bytes_sent
```

## Detection: Wireshark

**File Location:** `/data_exfil/http_exfil/http_lab.pcap`

### Step 1: Filter HTTP Traffic
```
http
```

### Step 2: Filter POST Requests
```
http.request.method == "POST"
```

### Step 3: Filter Large Payloads
```
http.request.method == "POST" and frame.len > 500
```

### Step 4: Increase Threshold
```
http.request.method == "POST" and frame.len > 750
```

### Step 5: Analyze HTTP Stream
```
Right-click packet → Follow → HTTP Stream
```

## Key Findings from HTTP Exfiltration

| Question | Answer |
|----------|--------|
| Internal compromised host | **192.168.1.103** |
| Flag hidden in exfiltrated data | **THM{http_raw_3xf1ltr4t10n_succ3ss}** |

---

# 6. Detection: ICMP Exfiltration

## What is ICMP Exfiltration?

ICMP (Internet Control Message Protocol) is used for diagnostics (ping). Attackers encode data into ICMP payloads to exfiltrate data.

**Why ICMP is Attractive:**
- Commonly allowed through firewalls
- Inspected less strictly than TCP/UDP
- ICMP payloads can carry data

## How Attackers Use ICMP

| Method | Description |
|--------|-------------|
| **ICMP echo (type 8) tunneling** | Data in echo request payloads |
| **ICMP reply (type 0) tunneling** | Data in echo reply payloads |
| **Custom ICMP types/codes** | Avoid signature-based detection |
| **Fragmentation/reassembly** | Large payloads split across packets |
| **Encryption/obfuscation** | Base64 encoding to look random |

## Indicators of Attack

| Indicator | Description |
|-----------|-------------|
| **Persistent ICMP sessions** | To external host not used for monitoring |
| **Unusually large payloads** | > typical ping size (64 bytes) |
| **High-entropy payloads** | Base64/hex patterns |
| **Bursts with no other traffic** | ICMP alone from same host |
| **Regular timing** | Evenly spaced packets |

## Detection: Wireshark

**File Location:** `/data_exfil/icmp_exfil/icmp_lab.pcap`

### Step 1: Filter ICMP Traffic
```
icmp
```

### Step 2: Isolate Echo Requests
```
icmp.type == 8
```

### Step 3: Check Large ICMP Packets
```
icmp.type == 8 and frame.len > 100
```

### Step 4: Analyze Payload
```
Click on packet → Expand ICMP payload → Look for encoded data
```

## ICMP Exfiltration Detection Tips

| Observation | Suspicion |
|-------------|-----------|
| Normal ping size | ~74 bytes total |
| Suspicious ping size | > 100 bytes total |
| Encoded data in payload | Base64, hex strings |
| Regular intervals | Beaconing behavior |

---

# 7. Detection Techniques Summary

## Comparison of Exfiltration Channels

| Channel | Protocol | Port | Stealth Level | Detection Difficulty |
|---------|----------|------|---------------|---------------------|
| DNS Tunneling | DNS | 53 | Very High | High |
| HTTP | HTTP/HTTPS | 80/443 | High | Medium |
| FTP | FTP | 21 | Low | Low |
| ICMP | ICMP | N/A | High | Medium |

## Detection Methods by Channel

| Channel | Wireshark Filters | Splunk Queries | Key Indicators |
|---------|-------------------|----------------|----------------|
| **DNS** | `dns`, `dns.flags.response == 0` | `len(query) > 30` | Long subdomains, high entropy |
| **FTP** | `ftp`, `ftp.request.command == "STOR"` | `method=STOR` | Large transfers, suspicious filenames |
| **HTTP** | `http.request.method == "POST"` | `method=POST bytes_sent > 600` | Large POST bodies |
| **ICMP** | `icmp.type == 8 and frame.len > 100` | N/A | Large payloads, persistent sessions |

## Wireshark Quick Reference

| Channel | Filter | Purpose |
|---------|--------|---------|
| DNS | `dns` | All DNS traffic |
| DNS | `dns.flags.response == 0` | DNS queries |
| DNS | `dns && frame.len > 70` | Long DNS queries |
| FTP | `ftp || ftp-data` | All FTP traffic |
| FTP | `ftp.request.command == "STOR"` | File uploads |
| HTTP | `http` | All HTTP traffic |
| HTTP | `http.request.method == "POST"` | POST requests |
| HTTP | `http.request.method == "POST" and frame.len > 750` | Large POST |
| ICMP | `icmp` | All ICMP traffic |
| ICMP | `icmp.type == 8` | Echo requests |
| ICMP | `icmp.type == 8 and frame.len > 100` | Large echo requests |

## Splunk Quick Reference

| Channel | Query | Purpose |
|---------|-------|---------|
| DNS | `index="data_exfil" sourcetype="DNS_logs"` | View DNS logs |
| DNS | `\| stats count by query \| sort -count` | Find top queries |
| DNS | `\| where len(query) > 30` | Find long queries |
| HTTP | `sourcetype="http_logs" method=POST` | POST requests |
| HTTP | `\| stats count avg(bytes_sent) by domain` | Data volume analysis |
| HTTP | `bytes_sent > 600 \| table _time src_ip domain` | Large transfers |

---

# 8. Quick Revision

## Key Terms

| Term | Definition |
|------|------------|
| **Data Exfiltration** | Unauthorized transfer of data from a network |
| **DNS Tunneling** | Using DNS to exfiltrate data |
| **Covert Channel** | Hidden communication path |
| **C2 (Command & Control)** | Attacker controlling compromised hosts |
| **PASV Mode** | FTP passive mode (data on ephemeral ports) |

## Detection Checklist

- [ ] Identify source host/user
- [ ] Determine destination (external IP/domain)
- [ ] Calculate volume of data transferred
- [ ] Identify process involved
- [ ] Correlate across log sources
- [ ] Check for encoded/encrypted data
- [ ] Look for beaconing patterns

## Quick Command Reference

### Wireshark
```
# DNS
dns
dns.flags.response == 0
dns && frame.len > 70

# FTP
ftp || ftp-data
ftp.request.command == "STOR"
ftp contains "csv"

# HTTP
http
http.request.method == "POST"
http.request.method == "POST" and frame.len > 750

# ICMP
icmp
icmp.type == 8
icmp.type == 8 and frame.len > 100
```

### Splunk
```
# DNS
index="data_exfil" sourcetype="DNS_logs"
| stats count by query | sort -count
| where len(query) > 30

# HTTP
index="data_exfil" sourcetype="http_logs" method=POST
| stats count avg(bytes_sent) by domain
| table _time src_ip uri domain bytes_sent
```

## Common Exfiltration Indicators

| Indicator | What to Look For |
|-----------|------------------|
| **DNS** | Long subdomains, high count, base32 patterns |
| **FTP** | STOR commands, large transfers, guest accounts |
| **HTTP** | Large POST bodies, unusual domains, encoded data |
| **ICMP** | Large payloads, persistent sessions, regular timing |

## Exfiltration Phases

```
Discovery → Collection → Staging → Compression → Encryption → Transport
```

## MITRE ATT&CK Mapping

| Technique | MITRE ID | Description |
|-----------|----------|-------------|
| Data Exfiltration | T1048 | Transfer data to external location |
| Exfiltration Over DNS | T1048.001 | DNS tunneling |
| Exfiltration Over FTP | T1048.002 | FTP transfers |
| Exfiltration Over HTTP | T1048.003 | HTTP/S transfers |
| Exfiltration Over ICMP | T1048.004 | ICMP tunneling |

## Tips

1. **Know the protocols** - Understand how DNS, FTP, HTTP, and ICMP work
2. **Learn the indicators** - Recognize suspicious patterns
3. **Practice with Wireshark** - Filters are essential
4. **Master Splunk queries** - Correlate across logs
5. **Think like an attacker** - How would you exfiltrate data?
6. **Correlate across sources** - Single alert is never enough
7. **Document findings** - Build investigation skills
