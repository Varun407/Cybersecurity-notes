# Network Discovery Detection — Complete Notes

# 1. Introduction to Network Discovery

## What is Network Discovery?

Network discovery is the process of identifying:
- Assets accessible on a network
- IP addresses
- Open ports
- Operating systems
- Running services
- Service versions
- Potential vulnerabilities

## Why Attackers Perform Network Discovery

**Goal:** Find an opening to exploit the network

**Information Sought:**
- What assets can be accessed?
- What IP addresses exist?
- What ports are open?
- What OS and services are running?
- What service versions are present?
- Are there any exploitable vulnerabilities?

## Why Defenders Perform Network Discovery

**Goals:**
- Inventory all organization assets
- Ensure all assets are documented
- Identify unnecessary IPs, ports, or services
- Ensure vulnerabilities are patched
- Reduce attack surface

**Key Insight:** Both attackers AND defenders perform discovery!

---

# 2. Network Discovery Overview

## The Challenge in Detection

Multiple entities perform discovery:
- Attackers (malicious)
- Defenders (legitimate)
- Research organizations
- Web crawlers
- Search engines

**SOC Challenge:** Differentiate between good and bad discovery

## Mitigation Techniques

| Technique | Description |
|-----------|-------------|
| **Allowlisting** | Known internal and external scanners excluded from alerts |
| **Threat Intelligence** | Flag scanning only from known malicious sources |
| **Severity Adjustment** | Use threat intelligence to raise alert severity rather than solely trigger alerts |
| **Generic Use Cases** | Alert on scanning behavior regardless of source |

---

# 3. External vs Internal Scanning

## External Scanning Activity

**Characteristics:**
- Source IP: External (outside organization)
- Destination IP: Organization's public-facing assets
- Stage: Reconnaissance (MITRE ATT&CK)

**MITRE Phase:** Reconnaissance

**Severity:** LOW

**Implication:** Attacker doesn't have foothold yet

**Response:**
- Block offending IPs on perimeter firewall
- Note: Attacker may return with masked IP

**Log Pattern:**
```
Source IP: External (203.0.113.25)
Destination IP: Organization asset (192.168.230.145)
```

## Internal Scanning Activity

**Characteristics:**
- Source IP: Internal (private IP)
- Destination IP: Internal (private IP)
- Stage: Discovery (MITRE ATT&CK)

**MITRE Phase:** Discovery

**Severity:** HIGH

**Implication:** Attacker already has foothold, preparing for lateral movement

**Response:**
- Escalate alert immediately
- Initiate Incident Response process
- Deeper investigation required
- Root cause analysis needed
- Blocking source IP insufficient

**Log Pattern:**
```
Source IP: Internal (10.0.0.50)
Destination IP: Internal (10.0.0.20)
```

## MITRE ATT&CK Mapping

| Phase | Description | Severity |
|-------|-------------|----------|
| **Reconnaissance** | External scanning, initial discovery | Low |
| **Discovery** | Internal scanning, lateral movement prep | High |

## Hands-On Log Analysis

**Location:** `/home/ubuntu/Downloads/logs/`

**Command to preview logs:**
```bash
head -n2 log-session-1.csv
```

**Log Structure:**
```
"@timestamp","source.ip","source.port","destination.ip","destination.port","rule.name","rule.category","rule.action","network.protocol",message,"event.dataset"
```

**Useful Commands:**
```bash
# Preview file
head -n5 filename.csv

# Extract specific column (adjust column numbers)
cut -d',' -f2 log-session-1.csv | head -10

# Count unique IPs
cut -d',' -f2 log-session-1.csv | sort | uniq -c

# Filter specific IP
grep "203.0.113.25" log-session-1.csv
```

---

# 4. Horizontal vs Vertical Scanning

## Horizontal Scanning

**Definition:** Scanning the same port across multiple destination IP addresses

**Purpose:** Identify which hosts expose a particular port

**Use Case:** Attacker wants to exploit a specific port/service

**Example:** WannaCry ransomware scanning for port 445 (SMBv1)

**Detection Pattern:**
```
Same source IP
Same destination port
Multiple destination IP addresses
```

**Visual:**
```
Attacker (10.0.0.100) -> 192.168.1.10:445
Attacker (10.0.0.100) -> 192.168.1.11:445
Attacker (10.0.0.100) -> 192.168.1.12:445
Attacker (10.0.0.100) -> 192.168.1.13:445
```

## Vertical Scanning

**Definition:** Scanning a single host across multiple ports

**Purpose:** Footprint a host and identify exposed services

**Use Case:** Attacker focused on high-value target

**Example:** Scanning a single internet-facing server

**Detection Pattern:**
```
Same source IP
Same destination IP
Multiple destination ports
```

**Visual:**
```
Attacker (10.0.0.100) -> 192.168.1.10:21
Attacker (10.0.0.100) -> 192.168.1.10:22
Attacker (10.0.0.100) -> 192.168.1.10:23
Attacker (10.0.0.100) -> 192.168.1.10:25
```

## Mixed Scanning

Combines horizontal and vertical scanning techniques

**Example:**
```
Attacker -> 192.168.1.10:21
Attacker -> 192.168.1.11:21
Attacker -> 192.168.1.10:22
Attacker -> 192.168.1.11:22
```

## Detection Commands

**Detect Horizontal Scan:**
```bash
cat logs.csv | cut -d',' -f2,5,6 | sort | uniq -c | grep "port"
```

**Detect Vertical Scan:**
```bash
cat logs.csv | cut -d',' -f2,5,6 | sort | uniq -c | grep "IP"
```

---

# 5. Mechanics of Scanning

## Ping Sweep

**Purpose:** Identify online hosts on network

**Method:**
1. Send ICMP packet to host
2. If host online → Replies with ICMP packet
3. If host offline → No response

**Limitation:** Often blocked by security controls

**Detection:**
- Look for multiple ICMP requests from single source
- Unusual ICMP traffic volume

```
Source -> Destination: ICMP Echo Request
Destination -> Source: ICMP Echo Reply
```

## TCP SYN Scan

**Purpose:** Identify online hosts and open ports

**Method:**
1. Send SYN request to recipient
2. If SYN-ACK received → Host online, port open
3. If RST received → Host online, port closed
4. If no response → Host offline or filtered

**Why It's Stealthy:**
- Blends with normal network traffic
- Doesn't complete full TCP handshake
- Harder to detect

**TCP Three-Way Handshake:**
```
Client -> Server: SYN
Server -> Client: SYN-ACK
Client -> Server: ACK (Connection established)
```

**SYN Scan (Half-Open):**
```
Client -> Server: SYN
Server -> Client: SYN-ACK
Client -> Server: RST (Connection reset)
```

**Detection:**
- Look for SYN packets without completed handshakes
- High volume of SYN packets from single source
- SYN packets to multiple ports on same host

## UDP Scan

**Purpose:** Identify online hosts and open UDP ports

**Method:**
1. Send empty UDP packet to port
2. If port closed → ICMP port unreachable reply
3. If no response until timeout → Mark port as open (unreliable)
4. If UDP response received → Port is open (rare)

**Characteristics:**
- Unreliable
- Slow (timeout-based)
- Less common

**Detection:**
- Look for UDP packets to multiple ports
- ICMP port unreachable responses
- Timeout patterns

## Comparison Table

| Scan Type | Protocol | Speed | Reliability | Stealth |
|-----------|----------|-------|-------------|---------|
| Ping Sweep | ICMP | Fast | High | Low |
| TCP SYN | TCP | Fast | High | High |
| UDP Scan | UDP | Slow | Low | Medium |

## Common Ports Scanned

| Port | Service | Commonly Exploited |
|------|---------|-------------------|
| 21 | FTP | Yes |
| 22 | SSH | Yes |
| 23 | Telnet | Yes |
| 25 | SMTP | Yes |
| 53 | DNS | Yes |
| 80 | HTTP | Yes |
| 443 | HTTPS | Yes |
| 445 | SMB | Yes |
| 3389 | RDP | Yes |

## Using Kibana for Analysis

**Access:** `http://MACHINE_IP:5601`

**Credentials:**
- Username: `elastic`
- Password: `changeme`

**Steps:**
1. Navigate to hamburger menu → Discover
2. Select "All logs" data view
3. Select "Search entire time range"
4. Click "+" to add fields as columns
5. Use controls to filter values

**Useful Fields to Add:**
- `source.ip`
- `destination.ip`
- `destination.port`
- `network.protocol`
- `rule.action`

**Kibana Filter Example:**
```
source.ip: "10.0.0.100" AND destination.port: 445
```

---

# 6. Detection Techniques

## Understanding Normal vs Abnormal Scanning

**Normal Activity:**
- Authorized vulnerability scans
- Asset discovery tools
- Compliance scanning
- Monitoring tools

**Abnormal Activity:**
- Scanning from unknown IPs
- Scanning outside business hours
- Scanning internal assets from unexpected sources
- High volume scanning

## Detection Use Cases

### External Scanning Detection
```yaml
Rule Name: External Port Scan Detection
Description: Alert when external IP scans multiple internal hosts
Detection Logic:
  - Source IP: External
  - Multiple destination IPs
  - Multiple ports
  - Time window: 5 minutes
Severity: Low
Action: Block IP on firewall
```

### Internal Scanning Detection
```yaml
Rule Name: Internal Network Discovery
Description: Alert when internal host performs reconnaissance
Detection Logic:
  - Source IP: Internal
  - Multiple destination IPs
  - Multiple ports
  - Time window: 5 minutes
Severity: High
Action: Initiate Incident Response
```

### Horizontal Scan Detection
```yaml
Rule Name: Horizontal Port Scan
Description: Alert when same port scanned across many hosts
Detection Logic:
  - Same source IP
  - Same destination port
  - Multiple destination IPs
  - Count > threshold
Severity: Medium
```

### Vertical Scan Detection
```yaml
Rule Name: Vertical Host Scan
Description: Alert when host scanned across many ports
Detection Logic:
  - Same source IP
  - Same destination IP
  - Multiple destination ports
  - Count > threshold
Severity: Medium
```

## Response Procedures

**External Scanning:**
1. Verify alert
2. Block source IP on firewall
3. Document activity
4. Monitor for recurrence

**Internal Scanning:**
1. Verify alert
2. Escalate to incident response
3. Investigate compromised host
4. Contain affected systems
5. Perform root cause analysis

## Best Practices for SOC Analysts

**Documentation:**
- Maintain list of authorized scanners
- Document scanning schedules
- Record scanning types and IPs

**Allowlisting:**
- Add authorized scanners to allowlist
- Exclude from detection use cases
- Monitor for changes

**Threat Intelligence:**
- Integrate threat feeds
- Flag known malicious IPs
- Adjust severity based on reputation

**Continuous Improvement:**
- Review detection rules regularly
- Update allowlists
- Learn from incidents

---

# 7. Quick Revision

## Key Terms

| Term | Definition |
|------|------------|
| **Network Discovery** | Identifying assets on a network |
| **Horizontal Scan** | Same port, multiple IPs |
| **Vertical Scan** | Multiple ports, same IP |
| **Ping Sweep** | ICMP-based host discovery |
| **TCP SYN Scan** | Half-open TCP scan |
| **UDP Scan** | Unreliable UDP port discovery |

## MITRE ATT&CK Mapping

| Technique | MITRE Phase | Severity |
|-----------|-------------|----------|
| External Scanning | Reconnaissance | Low |
| Internal Scanning | Discovery | High |

## Detection Patterns

| Pattern | Type |
|---------|------|
| Same IP → Different IPs, Same Port | Horizontal Scan |
| Same IP → Same IP, Different Ports | Vertical Scan |
| Multiple SYN Packets | TCP SYN Scan |
| Multiple ICMP Requests | Ping Sweep |

## Common Scanning Ports

| Port | Service |
|------|---------|
| 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 445 | SMB |
| 3389 | RDP |

## Key Commands

### Linux
```bash
# Preview logs
head -n5 logfile.csv

# Extract specific column
cut -d',' -f2 logfile.csv

# Count unique values
cut -d',' -f2 logfile.csv | sort | uniq -c

# Filter by value
grep "203.0.113.25" logfile.csv
```

### Kibana
```
# Add fields as columns
Click "+" next to field name

# Filter by value
Click filter icon on value

# Remove filter
Click "x" on filter badge

# Search entire time range
Select "Search entire time range"
```

## Quick Reference Table

| Scenario | Source IP | Dest IP | Dest Port | Action |
|----------|-----------|---------|-----------|--------|
| External Scan | External | Internal | Multiple | Block IP |
| Internal Scan | Internal | Internal | Multiple | IR Escalate |
| Horizontal Scan | Internal | Multiple | Same | Investigate |
| Vertical Scan | Internal | Same | Multiple | Investigate |

## Investigation Checklist

- [ ] Determine if scanning is external or internal
- [ ] Identify source IP address
- [ ] Determine scan type (horizontal/vertical)
- [ ] Count frequency and scope
- [ ] Check authorized scanner list
- [ ] Verify with threat intelligence
- [ ] Determine severity
- [ ] Take appropriate action
- [ ] Document findings

## Important Notes

1. **Both attackers AND defenders perform discovery**
2. **Context is crucial** - Internal scanning is HIGH severity
3. **Horizontal scanning** = same port, many IPs
4. **Vertical scanning** = many ports, same IP
5. **TCP SYN scans** are stealthy and common
6. **Ping sweeps** are basic but often blocked
7. **UDP scans** are unreliable and slow
8. **Always verify** before escalating

---

# Log Analysis Commands Reference

## Basic Navigation
```bash
# Navigate to logs
cd /home/ubuntu/Downloads/logs

# List files
ls -la

# Preview file
head -n10 filename.csv

# View entire file
cat filename.csv

# Search for pattern
grep "pattern" filename.csv
```

## Data Extraction
```bash
# Extract column (adjust delimiter)
cut -d',' -f2 filename.csv

# Extract multiple columns
cut -d',' -f2,5,6 filename.csv

# Extract and sort
cut -d',' -f2 filename.csv | sort

# Extract and count unique
cut -d',' -f2 filename.csv | sort | uniq -c
```

## Filtering
```bash
# Filter by IP
grep "203.0.113.25" filename.csv

# Filter and count
grep "203.0.113.25" filename.csv | wc -l

# Filter multiple patterns
grep -E "203.0.113.25|198.51.100.92" filename.csv
```

## Advanced Analysis
```bash
# Count connections per IP
cut -d',' -f2 filename.csv | sort | uniq -c | sort -nr

# Count connections per port
cut -d',' -f6 filename.csv | sort | uniq -c | sort -nr

# Find horizontal scans
cut -d',' -f2,5,6 filename.csv | sort | uniq -c | grep "port"

# Find vertical scans
cut -d',' -f2,5,6 filename.csv | sort | uniq -c | grep "IP"
```

---

## Tips

1. **Understand the difference** between external and internal scanning
2. **Know your ports** - common ports and their services
3. **Practice with Kibana** - learn to filter and visualize logs
4. **Remember the patterns** - horizontal vs vertical
5. **Context matters** - same activity can be normal or malicious
6. **Document everything** - keep notes for future reference
7. **Stay updated** - new scanning techniques emerge constantly
