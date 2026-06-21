# Intro to Log Analysis 

# 1. Log Operations

## What is Log Configuration?

Log configuration determines:
- What data will be collected
- How logs are stored
- How long logs are retained
- How logs are analyzed
- Who can access logs

Proper configuration improves:
- Security monitoring
- Troubleshooting efficiency
- Compliance adherence
- Performance monitoring
- Incident response capabilities

## Logging Purposes

### Security Logging
**Focus:**
- Threat detection
- Incident response
- Unauthorized access detection

**Examples:**
- Login attempts (successful and failed)
- Privilege escalation events
- Firewall activities
- IDS/IPS alerts

**Main Goals:**
- Detect anomalies
- Verify authentication
- Protect data confidentiality
- Identify compromised accounts

### Operational Logging
**Focus:**
- System health monitoring
- Reliability tracking
- Performance optimization

**Examples:**
- Service crashes
- Resource utilization spikes
- Hardware failures
- Application errors

**Main Goals:**
- Troubleshooting
- Capacity planning
- Service continuity
- Performance optimization

### Legal & Compliance Logging
**Focus:**
- Regulatory requirements
- Audit trails
- Legal investigations

**Examples:**
- PCI DSS (Payment Card Industry)
- GDPR (General Data Protection Regulation)
- HIPAA (Health Insurance Portability)
- ISO 27001
- COBIT
- FISMA

**Common Requirements:**
- Centralized logging
- Defined retention periods (e.g., 12 months)
- Searchable archives (e.g., last 3 months accessible)
- Audit trails
- Security checks
- Yearly audits

### Debug Logging
**Focus:**
- Software development
- Application testing
- Bug identification

**Examples:**
- Function execution
- Variable values
- Application traces
- Error stack traces

**Main Goals:**
- Find bugs faster
- Improve software reliability
- Speed development process

## Planning Log Configuration

### Questions to Ask Before Implementation

| Category | Questions |
|----------|-----------|
| **Scope** | What will be logged? Why are we logging it? |
| **Requirements** | Any compliance obligations? Additional infrastructure needed? |
| **Detail Level** | How much detail is required? What data is actually useful? |
| **Collection** | How will logs be gathered? |
| **Storage** | Where will logs be stored? |
| **Protection** | How will logs be secured? |
| **Analysis** | How will logs be searched and investigated? |
| **Resources** | Budget? Staff? Infrastructure? |

## Configuration Dilemma

### The Balance

| Base Requirements (Reactive) | Aspirations (Proactive) |
|------------------------------|-------------------------|
| What happened? | More details |
| When did it happen? | Better context |
| Where did it happen? | Additional insights |
| Who caused it? | Future prediction |
| From which log source? | Threat hunting capability |

**Reactive Approach:**
- Answers: What? When? Where? Who?
- Good for: Incident detection and response
- Foundation for security operations

**Proactive Approach:**
- Answers: What next? What else is affected? How confident are we?
- Good for: Threat hunting, Advanced threat detection
- Requires more resources

### Finding the Balance
- Meet specific operational and security requirements (non-negotiable)
- Consider feasibility of improving capability
- Implement additional data and insights when possible
- Conduct comprehensive risk assessment
- Prioritize security, compliance, and legal needs

## Logging Principles

### Collection
| Do's | Don'ts |
|------|--------|
| Define logging purpose | Collect everything |
| Collect useful data | Create unnecessary noise |
| Avoid irrelevant data | |

### Format
| Do's | Don'ts |
|------|--------|
| Use consistent formats | Use inconsistent formats |
| Log at correct detail level | Log incorrect detail level |
| Synchronize timestamps | Have unsynchronized timestamps |

### Archiving and Accessibility
| Do's | Don'ts |
|------|--------|
| Create retention policies | Ignore retention requirements |
| Store logs securely | Store logs insecurely |
| Keep backups | Not back up logs |
| Make important data searchable | Not index logs |

### Monitoring and Alerting
| Do's | Don'ts |
|------|--------|
| Create actionable alerts | Create non-actionable alerts |
| Reduce alert fatigue | Ignore alert fatigue |
| Focus on meaningful events | Focus on noise |

### Security
| Do's | Don'ts |
|------|--------|
| Restrict access | Allow open access |
| Encrypt logs when necessary | Not encrypt sensitive logs |
| Use dedicated logging platform | Use insecure storage |

### Continuous Change
| Do's | Don'ts |
|------|--------|
| Update configurations | Set and forget |
| Train analysts | Ignore training |
| Adapt to new threats | Stick to old methods |

## Logging Challenges

### Data Volume and Noise
- Massive log generation
- Too much irrelevant data
- Different log volumes from different applications
- Some applications generate insufficient logs

### System Performance
- Logging affects system performance
- Legacy systems may not support logging
- Deployment and optimization challenges
- Version update synchronization

### Processing and Storage
- Multiple data formats
- Parsing difficulties
- Balancing retention requirements
- Compliance with regulations

### Security
- Protecting stored logs
- Ensuring data security
- Access control implementation

### Analysis
- Correlation complexity
- False positives
- False negatives
- Real-time analysis challenges
- Combining multiple sources

### Organizational Issues
- Lack of planning
- Lack of budget
- Lack of skills
- Lack of implementation scenarios
- Focusing on collection over analysis
- Ignoring human factors

## Common Mistakes & Best Practices

### Mistakes (Don'ts)
```
❌ Logging sensitive information (passwords, credit cards)
❌ Creating custom logging scripts
❌ Leaving logs uncollected
❌ Collecting everything but not analyzing
❌ No proper planning and configuration
❌ Systems lacking planned log configuration
❌ Skipping scale and functionality testing
❌ Focusing on edges, skipping internal systems
❌ "Searching for what you want to find"
❌ "Not investigating what you see"
❌ Forgetting about planning, management, and analysis
```

### Best Practices (Dos)
```
✅ Create suitable log configuration plan
✅ Implement testing on scale and functionality
✅ Exclude logging sensitive information
✅ Secure logs with access controls
✅ Create meaningful alerts and notifications
✅ Focus on actionable and impactful insights
✅ Train analysts and enhance skills
✅ Update and maintain operation plans
✅ Adapt components as needed
✅ Follow industry best practices
```

---

# 2. Log Analysis Basics

## What is Log Analysis?

Log analysis is the process of:
- Collecting logs
- Parsing logs
- Processing logs
- Correlating events
- Extracting actionable information

**Purpose:**
- Detect security incidents
- Troubleshoot systems
- Perform threat hunting
- Meet compliance requirements
- Improve operational visibility

## What Are Logs?

A log is a time-sequenced record of events generated by:
- Systems
- Applications
- Devices
- Security tools

### Log Structure

**Example:**
```
Jul 28 17:45:02 10.10.0.4 FW-1: %WARNING% general: 
Unusual network activity detected from IP 10.10.0.15 
to IP 203.0.113.25
```

**Key Components:**

| Component | Example | Description |
|-----------|---------|-------------|
| Timestamp | Jul 28 17:45:02 | When event occurred |
| Source | 10.10.0.4 | System that generated log |
| Severity | %WARNING% | Event importance level |
| Action | Action: Alert | System response |
| Message | Unusual network activity... | Event details |

### Severity Levels

| Level | Description |
|-------|-------------|
| Informational | Routine events, normal operations |
| Warning | Potential issues, not critical yet |
| Error | Issues requiring attention |
| Critical | Serious problems, immediate response needed |

## Why Logs Are Important

| Purpose | Description | Examples |
|---------|-------------|----------|
| **System Troubleshooting** | Identify and fix system issues | Crashes, errors, service failures |
| **Security Incident Response** | Detect and respond to threats | Unauthorized access, malware, data breaches |
| **Threat Hunting** | Proactively find hidden threats | IOCs, anomalies, advanced attacks |
| **Compliance** | Meet regulatory requirements | GDPR, HIPAA, PCI DSS, ISO 27001 |

## Types of Logs

| Log Type | Description | Examples |
|----------|-------------|----------|
| **Application Logs** | Application events | Errors, warnings, status messages |
| **Audit Logs** | Track actions and changes | User activity, configuration changes |
| **Security Logs** | Security-related events | Logins, permissions, firewall activity |
| **Server Logs** | Server operations | Access logs, error logs, event logs |
| **System Logs** | OS and kernel events | Boot sequences, system errors, hardware status |
| **Network Logs** | Network communications | Connections, data transfers |
| **Database Logs** | Database activities | Queries, updates, operations |
| **Web Server Logs** | HTTP requests | URLs, response codes, user-agents |

---

# 3. Investigation Theory

## Timeline

A timeline is a chronological representation of logged events.

**Purpose:**
- Understand sequence of events
- Reconstruct security incidents
- Identify initial compromise point
- Trace attacker's TTPs (Tactics, Techniques, Procedures)

**Questions timelines answer:**
- What happened?
- When did it happen?
- Where did it happen?
- Who is responsible?
- Was the action successful?
- What was the result?

## Timestamps

### Challenges
- Different time zones
- Different formats
- Potential for inconsistency

### Best Practices
- Convert all timestamps to consistent time zone
- Use UNIX time for standardization
- Implement NTP (Network Time Protocol) for synchronization
- Let SIEM solutions handle timezone conversion

### NTP Example
```bash
ntpdate pool.ntp.org
date
```

## Super Timeline

A consolidated timeline combining logs from multiple sources:
- System logs
- Application logs
- Network logs
- Firewall logs
- Security logs

**Benefits:**
- Comprehensive view
- Correlate events across systems
- Understand attack progression
- Holistic investigation

### Plaso (Log2Timeline)
Open-source tool that:
- Automates timeline creation
- Parses multiple log sources
- Creates unified chronological timeline
- Used for digital forensics

## Data Visualization

**Tools:**
- Splunk
- Kibana (Elastic Stack)

**Benefits:**
- Convert raw logs to visual insights
- Spot patterns and anomalies
- Create interactive dashboards
- Single pane of glass view

**Example:**
Line chart showing failed login attempts over time

## Monitoring and Alerting

### What to Alert On
- Multiple failed login attempts
- Privilege escalation
- Sensitive file access
- Malware indicators
- Unusual network connections
- Anomalous user behavior

### Best Practices
- Create clear escalation procedures
- Define roles and responsibilities
- Ensure actionable alerts
- Reduce false positives
- Prompt notification

## Threat Intelligence

**What is Threat Intelligence?**
Information attributed to malicious actors:
- IP Addresses
- Domains
- File Hashes

**Usage in Log Analysis:**
```bash
grep "54.36.149.64" logfile.txt
```

**Benefits:**
- Identify known bad actors
- Correlate with logs
- Enrich investigations
- Proactive detection

---

# 4. Detection Engineering

## Common Log Locations

### Web Servers
| Server | Log Type | Location |
|--------|----------|----------|
| Apache | Access | `/var/log/apache2/access.log` |
| Apache | Error | `/var/log/apache2/error.log` |
| Nginx | Access | `/var/log/nginx/access.log` |
| Nginx | Error | `/var/log/nginx/error.log` |

### Databases
| Database | Log Type | Location |
|----------|----------|----------|
| MySQL | Error | `/var/log/mysql/error.log` |
| PostgreSQL | Activity | `/var/log/postgresql/postgresql-{version}-main.log` |

### Operating Systems
| OS | Log Type | Location |
|----|----------|----------|
| Linux | General | `/var/log/syslog` |
| Linux | Authentication | `/var/log/auth.log` |

### Firewalls & IDS/IPS
| Tool | Log Type | Location |
|------|----------|----------|
| iptables | Firewall | `/var/log/iptables.log` |
| Snort | IDS | `/var/log/snort/` |

### Web Applications
| Language | Log Type | Location |
|----------|----------|----------|
| PHP | Error | `/var/log/php/error.log` |

## Abnormal User Behavior

### Indicators to Monitor

| Pattern | Description | Risk |
|---------|-------------|------|
| **Multiple failed logins** | Unusually high failures | Brute force attack |
| **Unusual login times** | Outside normal hours | Compromised account |
| **Geographic anomalies** | Impossible travel | Account compromise |
| **Simultaneous logins** | Different locations | Account sharing/compromise |
| **Frequent password changes** | Rapid changes | Account takeover |
| **Suspicious user-agents** | Nmap, Hydra, etc. | Automated attacks |

### User-Agent Examples
```
Hydra: (Hydra)
Nmap: Nmap Scripting Engine
```

## Common Attack Signatures

### SQL Injection
**Indicators:**
```
'
--
#
UNION
SELECT
WAITFOR DELAY
SLEEP()
```

**Example:**
```
GET /products.php?q=books' UNION SELECT null, null, username, password, null FROM users-- HTTP/1.1
```

**Detection:**
- Look for unusual/malformed SQL queries
- Check for escape characters
- Detect URL encoding attempts

### Cross-Site Scripting (XSS)
**Indicators:**
```
<script>
alert()
onerror=
onclick=
onmouseover=
```

**Example:**
```
GET /products.php?search=<script>alert(1);</script> HTTP/1.1
```

**Detection:**
- Look for script tags
- Check for event handlers
- Detect encoded payloads

### Path Traversal
**Indicators:**
```
../
../../
../../../
/etc/passwd
/etc/shadow
```

**URL Encoded:**
```
%2E = . (dot)
%2F = / (slash)
```

**Example:**
```
GET /../../../../../etc/passwd HTTP/1.1
```

**Detection:**
- Look for traversal sequences
- Check for sensitive file paths
- Detect encoded attempts

---

# 5. Automated vs Manual Analysis

## Automated Analysis

**Tools:**
- Splunk
- XPLG
- SolarWinds Loggly
- SIEM solutions

### Advantages
✅ Saves time
✅ Processes large data volumes
✅ Uses AI/Machine Learning for pattern recognition
✅ Scales effectively

### Disadvantages
❌ Expensive (usually commercial)
❌ False positives possible
❌ May miss novel attacks
❌ Model limitations

## Manual Analysis

**Tools:**
- grep
- awk
- cat
- less
- tail
- head
- cut
- sort
- uniq
- sed

### Advantages
✅ No expensive tooling required
✅ Allows thorough investigation
✅ Reduces overfitting/false positives
✅ Contextual understanding
✅ Human judgment

### Disadvantages
❌ Time-consuming
❌ Human error possible
❌ May miss events
❌ Less scalable

---

# 6. Command Line Log Analysis

## Viewing Logs

### cat
Displays entire file content.
```bash
cat apache.log
```
**Use Case:** Small files
**Limitation:** Too much output for large files

### less
Displays content page by page.
```bash
less apache.log
```
**Navigation:**
- `Space` - Next page
- `b` - Previous page
- `/` - Search
- `q` - Quit
- `↑/↓` - Scroll

**Use Case:** Large files
**Advantage:** Can scroll and search

### tail
Shows the end of the file.
```bash
# Last 10 lines (default)
tail apache.log

# Last 5 lines
tail -n 5 apache.log

# Follow in real-time
tail -f apache.log

# Follow last 5 lines
tail -f -n 5 apache.log
```
**Use Case:** Monitoring live logs

### head
Shows the beginning of the file.
```bash
# First 10 lines (default)
head apache.log

# First 5 lines
head -n 5 apache.log
```

## File Statistics

### wc (Word Count)
```bash
wc apache.log
# Output: lines words characters filename
70 1562 14305 apache.log
```
**Options:**
- `-l` : Lines only
- `-w` : Words only
- `-c` : Characters only

## Extracting Data

### cut
Extracts specific columns/fields.
```bash
# Extract IP addresses (first field)
cut -d ' ' -f 1 apache.log

# Extract URLs (7th field)
cut -d ' ' -f 7 apache.log

# Extract status codes (9th field)
cut -d ' ' -f 9 apache.log
```
**Options:**
- `-d` : Delimiter
- `-f` : Field number(s)

## Sorting Data

### sort
Arranges data in order.
```bash
# Sort alphabetically
cut -d ' ' -f 1 apache.log | sort

# Sort numerically
cut -d ' ' -f 1 apache.log | sort -n

# Sort reverse
cut -d ' ' -f 1 apache.log | sort -n -r
```
**Options:**
- `-n` : Numeric sort
- `-r` : Reverse order

## Removing Duplicates

### uniq
Removes adjacent duplicate lines.
```bash
# Remove duplicates
cut -d ' ' -f 1 apache.log | sort | uniq

# Count occurrences
cut -d ' ' -f 1 apache.log | sort | uniq -c

# Show unique lines only
cut -d ' ' -f 1 apache.log | sort | uniq -u
```

## Manipulating Data

### sed
Stream editor for text manipulation.
```bash
# Replace text
sed 's/old/new/g' file.log

# Replace in file (in-place)
sed -i 's/old/new/g' file.log

# Example: Change date format
sed 's/31/Jul/2023/July 31, 2023/g' apache.log
```

### awk
Powerful text processing.
```bash
# Filter by field value
awk '$9 >= 400' apache.log

# Print specific fields
awk '{print $1, $9}' apache.log

# Conditional processing
awk '$9 == 404 {print $1}' apache.log
```
**Fields:** `$1, $2, $3, ...` (like cut)

## Searching Logs

### grep
Powerful text search.
```bash
# Basic search
grep "keyword" apache.log

# Case-insensitive
grep -i "keyword" apache.log

# Count matches
grep -c "keyword" apache.log

# Show line numbers
grep -n "keyword" apache.log

# Inverse match (exclude)
grep -v "keyword" apache.log

# Regular expression
grep -E 'pattern' apache.log

# Multiple patterns
grep -E 'pattern1|pattern2' apache.log
```

**Common Flags:**

| Flag | Description |
|------|-------------|
| `-E` | Extended regex |
| `-i` | Case insensitive |
| `-c` | Count matches |
| `-n` | Show line numbers |
| `-v` | Invert match |
| `-r` | Recursive search |

### Pipeline Examples

```bash
# Find top attacking IPs
cut -d ' ' -f 1 apache.log | sort | uniq -c | sort -nr | head -10

# Find all 404 errors
grep "404" apache.log

# Find failed logins from a specific IP
grep "Failed" auth.log | grep "192.168.1.100"

# Exclude a specific page
grep -v "/index.php" apache.log | grep "203.64.78.90"

# Count attacks by IP
grep "Failed password" auth.log | awk '{print $11}' | sort | uniq -c | sort -nr
```

---

# 7. Regular Expressions (Regex)

## What is Regex?

Regular expressions are patterns for:
- Searching
- Matching
- Extracting
- Manipulating text data

**Usage in Log Analysis:**
- Extract relevant information
- Filter data
- Identify patterns
- Process logs before SIEM ingestion

## Common Regex Patterns

### Basic Patterns

| Pattern | Meaning | Example |
|---------|---------|---------|
| `.` | Any character | `a.c` matches "abc" |
| `*` | Zero or more | `ab*` matches "a", "ab", "abb" |
| `+` | One or more | `ab+` matches "ab", "abb" |
| `?` | Zero or one | `ab?` matches "a", "ab" |
| `{n}` | Exactly n | `a{3}` matches "aaa" |
| `{n,}` | n or more | `a{3,}` matches "aaa", "aaaa" |
| `{n,m}` | Between n and m | `a{2,4}` matches "aa", "aaa", "aaaa" |
| `[]` | Character class | `[0-9]` matches any digit |
| `[^]` | Negated class | `[^0-9]` matches non-digit |
| `\d` | Digit | `[0-9]` |
| `\w` | Word character | `[a-zA-Z0-9_]` |
| `\s` | Whitespace | Space, tab, newline |
| `^` | Start of line | `^Error` |
| `$` | End of line | `done$` |
| `\b` | Word boundary | `\bword\b` |
| `|` | OR | `cat|dog` |
| `()` | Grouping | `(ab)+` |

### IP Address Regex
```regex
\b([0-9]{1,3}\.){3}[0-9]{1,3}\b
```

**Breakdown:**
| Component | Meaning |
|-----------|---------|
| `\b` | Word boundary |
| `[0-9]{1,3}` | 1-3 digits (0-999) |
| `\.` | Literal dot |
| `{3}` | Repeat 3 times |
| `[0-9]{1,3}` | Final octet |
| `\b` | Word boundary |

### Grep with Regex
```bash
# Find blog posts 10-19
grep -E 'post=1[0-9]' apache-ex2.log

# Find IP addresses
grep -E '\b([0-9]{1,3}\.){3}[0-9]{1,3}\b' logfile.log

# Find 404 errors
grep -E 'HTTP/1.1" 404' access.log

# Find SQL injection attempts
grep -E "('|--|UNION|SELECT)" application.log

# Find XSS attempts
grep -E "(<script>|alert\()" web.log
```

## Log Parsing with Regex

### Use Cases
1. **Extract IP addresses**
2. **Extract timestamps**
3. **Extract HTTP methods**
4. **Extract URLs**
5. **Extract user-agents**
6. **Identify attack patterns**

### Logstash & Grok
**Purpose:** Parse unstructured logs into structured data

**Syntax:**
```
%{SYNTAX:SEMANTIC}
```

**Example:**
```ruby
# Custom IP extraction
filter {
  grok {
    match => { 
      "message" => "(?<ipv4_address>\b([0-9]{1,3}\.){3}[0-9]{1,3}\b)" 
    }
  }
}
```

---

# 8. CyberChef

## What is CyberChef?

**Created by:** GCHQ (Government Communications Headquarters)

**Nickname:** "Cyber Swiss Army Knife"

**Features:**
- 300+ operations
- Encoding/Decoding
- Encryption/Hashing
- Data analysis
- Log parsing
- Regex extraction

## CyberChef Interface

| Component | Description |
|-----------|-------------|
| **Operations Tab** | Select operations to apply |
| **Recipe** | Collection of operations |
| **Input** | Data to analyze |
| **Output** | Result after operations |

## Key Features

### Magic
- Automatically identifies encodings
- Attempts to decode unknown formats
- Suggests useful operations

### Regex Extraction
**Example:** Extract all IPs from logs
```regex
\b([0-9]{1,3}\.){3}[0-9]{1,3}\b
```
**Output format:** "List matches"

### File Upload
- Upload log files directly
- Support for compressed files (.zip, .tar.gz)
- Process large files

### Common Use Cases
1. **Decode Base64** - "To Base64" operation
2. **Extract IPs** - Regex operation
3. **Parse JSON logs** - JSON parser
4. **Extract URLs** - Regex
5. **Timestamp conversion** - Convert timestamp formats
6. **Decode URL encoded** - URL decode

---

# 9. Sigma & YARA

## Sigma

**Purpose:** Create portable detection rules for log analysis

**Language:** YAML

**Use Cases:**
- Detect events in log files
- Create SIEM searches
- Identify threats
- Share detections

### Sigma Rule Structure

```yaml
title: Failed SSH Logins
description: Searches sshd logs for failed SSH login attempts
status: experimental
author: CMNatic
logsource:
    product: linux
    service: sshd
detection:
    selection:
        type: 'sshd'
        a0|contains: 'Failed'
        a1|contains: 'Illegal'
    condition: selection
falsepositives:
    - Users forgetting or mistyping their credentials
level: medium
```

### Key Fields

| Key | Description | Example |
|-----|-------------|---------|
| **title** | Rule purpose | Failed SSH Logins |
| **description** | Expanded explanation | Searches sshd logs... |
| **status** | Rule maturity | experimental, stable, deprecated |
| **author** | Creator | CMNatic |
| **logsource** | Log location | product: linux, service: sshd |
| **detection** | What to find | a0\|contains: 'Failed' |
| **condition** | Trigger logic | selection |
| **falsepositives** | Expected non-malicious matches | Users mistyping |
| **level** | Severity | low, medium, high |

**Answer:** Sigma uses **YAML** language.

**Answer:** The title keyword denotes the title of a Sigma rule.

## YARA

**Purpose:** Pattern matching engine

**Common Uses:**
- Malware detection
- IOC detection
- Log analysis

### YARA Rule Structure

```yaml
rule IPFinder {
    meta:
        author = "CMNatic"
    strings:
        $ip = /([0-9]{1,3}\.){3}[0-9]{1,3}/ wide ascii
    condition:
        $ip
}
```

### Key Fields

| Key | Description | Example |
|-----|-------------|---------|
| **rule** | Rule name | IPFinder |
| **meta** | Metadata | author = "CMNatic" |
| **strings** | Patterns to match | $ip = /regex/ |
| **condition** | Trigger logic | $ip |

### Pattern Matching
- Textual patterns (strings)
- Binary patterns (hexadecimal)
- Regular expressions
- Combinations

**Example Usage:**
```bash
yara ipfinder.yar apache2.txt
```

**Answer:** The **rule** keyword denotes the name of a rule in YARA.

---

# 10. Exam Quick Revision

## Logging Purposes

| Purpose | Focus |
|---------|-------|
| **Security** | Threat detection, incident response |
| **Operational** | System health, troubleshooting |
| **Legal** | Compliance, regulations |
| **Debug** | Development, testing |

## Important Log Types

| Log Type | Generated By |
|----------|--------------|
| Application | Applications |
| Audit | Systems/applications |
| Security | Security tools |
| Server | Servers |
| System | Operating system |
| Network | Network devices |
| Database | Database systems |
| Web Server | Web servers |

## Detection Patterns

| Pattern | Indicates |
|---------|-----------|
| Multiple failed logins | Brute force attack |
| Impossible travel | Compromised account |
| Suspicious user-agent | Automated attack |
| `' UNION SELECT` | SQL Injection |
| `<script>` | XSS |
| `../` | Path Traversal |

## Important Tools

| Tool | Purpose |
|------|---------|
| grep | Search logs |
| awk | Process logs |
| sed | Edit logs |
| cut | Extract fields |
| sort | Sort data |
| uniq | Remove duplicates |
| tail -f | Monitor logs |
| CyberChef | Data processing |
| Sigma | Detection rules |
| YARA | Pattern matching |
| Plaso | Super timelines |
| Splunk | SIEM |
| Kibana | Visualization |

## Regex Patterns

| Pattern | Matches |
|---------|---------|
| `\b([0-9]{1,3}\.){3}[0-9]{1,3}\b` | IPv4 Address |
| `\d{4}-\d{2}-\d{2}` | Date YYYY-MM-DD |
| `\d{2}:\d{2}:\d{2}` | Time HH:MM:SS |
| `error\|warning\|critical` | Error levels |

## Linux Log Locations

| Log | Location |
|-----|----------|
| Apache Access | `/var/log/apache2/access.log` |
| Apache Error | `/var/log/apache2/error.log` |
| Nginx Access | `/var/log/nginx/access.log` |
| Nginx Error | `/var/log/nginx/error.log` |
| System | `/var/log/syslog` |
| Authentication | `/var/log/auth.log` |
| MySQL Error | `/var/log/mysql/error.log` |
| iptables | `/var/log/iptables.log` |

## TryHackMe Answers

| Question | Answer |
|----------|--------|
| Based on the list of log types... what log type is used? | Web Server Log |
| Which logging principle would be implemented? | Archiving and Accessibility |
| What languages does Sigma use? | YAML |
| What keyword denotes the "title" of a Sigma rule? | title |
| What keyword denotes the "name" of a rule in YARA? | rule |

## Key Commands Quick Reference

```bash
# View log
cat logfile.log
less logfile.log
tail -f logfile.log

# Extract IPs
cut -d ' ' -f 1 logfile.log

# Count occurrences
cut -d ' ' -f 1 logfile.log | sort | uniq -c | sort -nr

# Search
grep "error" logfile.log
grep -E 'pattern' logfile.log

# Filter
awk '$9 >= 400' logfile.log

# Replace
sed 's/old/new/g' logfile.log
```

---
