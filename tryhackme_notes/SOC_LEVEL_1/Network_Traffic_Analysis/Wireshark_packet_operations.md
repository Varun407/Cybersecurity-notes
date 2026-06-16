# Wireshark Packet Operations

## What is Packet Operations?

Packet Operations refers to analyzing captured network traffic beyond simply viewing packets. The goal is to understand communication patterns, identify anomalies, and extract evidence from large packet captures.

A SOC analyst rarely investigates packets one by one. Instead, they use statistics, conversations, endpoints, and filters to narrow the investigation and quickly identify suspicious activity.

---

# Why Packet Operations Matter

Modern PCAP files can contain thousands or even millions of packets. Manually reviewing every packet is impossible.

Packet operations help analysts:

* Identify the most active hosts.
* Understand communication relationships.
* Detect suspicious protocols.
* Investigate malware traffic.
* Find command-and-control (C2) communications.
* Locate evidence of data exfiltration.

Without packet operations, investigations become slow and inefficient.

---

# Typical Investigation Workflow

```text id="jqhd9h"
Open PCAP
    ↓
Review Statistics
    ↓
Identify Interesting Hosts
    ↓
Review Conversations
    ↓
Apply Filters
    ↓
Analyze Protocols
    ↓
Investigate Suspicious Traffic
```

This workflow allows analysts to move from a broad overview to packet-level evidence.

---

# Resolved Addresses

Resolved Addresses displays IP addresses, hostnames, and MAC addresses discovered in the capture.

Instead of seeing:

```text id="nbk7nf"
142.250.190.46
```

You may see:

```text id="o25hnv"
google.com
```

This makes investigations significantly easier because analysts can immediately understand which systems are being contacted.

### SOC Relevance

Resolved addresses help analysts:

* Identify external services.
* Detect malicious domains.
* Investigate suspicious destinations.
* Map network activity to real systems.

---

# Protocol Hierarchy

Protocol Hierarchy provides a breakdown of every protocol observed in the capture.

Example:

```text id="w37u17"
Ethernet
 └── IPv4
      └── TCP
           └── HTTP
```

Wireshark also displays the percentage of traffic each protocol represents.

### Why Analysts Use It

Protocol hierarchy quickly answers questions such as:

* Is most traffic HTTP or HTTPS?
* Is DNS activity unusually high?
* Is SMB traffic present where it shouldn't be?
* Are uncommon protocols being used?

### Threat Hunting Value

Unexpected protocols often indicate suspicious activity.

Examples:

* Excessive ICMP traffic.
* Unusual SMB communications.
* DNS tunneling activity.
* Unexpected remote administration protocols.

---

# Conversations

Conversations show communications occurring between two endpoints.

Instead of looking at individual packets, analysts can view an entire communication relationship.

Information displayed includes:

* Source host.
* Destination host.
* Packet count.
* Bytes transferred.
* Duration.

### Why Conversations Matter

Conversations help identify:

* Beaconing malware.
* Long-running sessions.
* Large file transfers.
* Suspicious external connections.

### Example

```text id="lx4go4"
Workstation
      ↔
Unknown Internet Host
```

If thousands of packets are exchanged over long periods, the connection may require investigation.

---

# Endpoints

Endpoints provide a list of all unique hosts present in the capture.

Displayed information includes:

* IP address.
* MAC address.
* Vendor information.
* Packet counts.
* Traffic volume.

### SOC Use Cases

Endpoints help analysts identify:

* Most active devices.
* Unknown systems.
* External infrastructure.
* Suspicious hosts generating unusual traffic.

Instead of searching through packets, analysts can immediately locate the systems responsible for activity.

---

# Name Resolution

Name Resolution converts technical identifiers into readable values.

Examples include:

```text id="tq0uyg"
8.8.8.8      → dns.google
443          → HTTPS
00:50:56     → VMware
```

### Why It Matters

Investigations become much easier when analysts can see meaningful names rather than raw numerical values.

---

# GeoIP Mapping

GeoIP Mapping associates IP addresses with geographic locations.

Information may include:

* Country
* Region
* City
* ISP

### Threat Hunting Use

Analysts frequently investigate:

* Connections to unusual countries.
* Unexpected foreign infrastructure.
* Traffic to regions not normally contacted by the organization.

GeoIP alone does not prove malicious activity, but it often provides valuable investigative context.

---

# IPv4 Statistics

IPv4 statistics provide visibility into:

* Source addresses.
* Destination addresses.
* Packet counts.
* Port usage.

### Why It Matters

Analysts can quickly determine:

* Most active hosts.
* Most contacted destinations.
* Potential scanning activity.
* Network hotspots.

### Detection Opportunities

Look for:

* One host communicating with many systems.
* High-volume traffic spikes.
* Unexpected external communications.

---

# DNS Statistics

DNS statistics provide insight into name resolution activity.

Information includes:

* Query types.
* Response codes.
* Request counts.
* Response times.

### Common DNS Record Types

#### A Record

Maps a hostname to an IPv4 address.

Example:

```text id="xq7ukr"
google.com → 142.250.x.x
```

#### AAAA Record

Maps a hostname to an IPv6 address.

#### MX Record

Specifies mail servers.

#### TXT Record

Stores arbitrary text data.

TXT records are commonly abused in DNS tunneling and malware communications.

---

# Why DNS Analysis Matters

Attackers frequently use DNS because it is trusted and rarely blocked.

### Detection Opportunities

Look for:

* Excessive DNS requests.
* Long domain names.
* Repeated failed lookups.
* Suspicious TXT records.
* Algorithmically generated domains (DGAs).

---

# HTTP Statistics

HTTP statistics provide visibility into web traffic.

Analysts can review:

* Requests.
* Responses.
* Methods.
* Status codes.
* Hostnames.

### Common HTTP Methods

#### GET

Requests data from a server.

#### POST

Sends data to a server.

#### PUT

Uploads or replaces content.

#### DELETE

Removes content.

---

# Important HTTP Status Codes

### 200

Request succeeded.

### 301 / 302

Resource redirected.

### 403

Access denied.

### 404

Resource not found.

### 500

Server-side error.

---

# Threat Hunting Through HTTP

HTTP traffic often reveals:

* Malware downloads.
* Phishing activity.
* Suspicious file transfers.
* Data exfiltration.

A large number of HTTP POST requests may indicate data being sent outside the network.

---

# Display Filters

Display filters are the most powerful feature in Wireshark.

They allow analysts to focus only on relevant packets without modifying the original capture.

### Benefits

Display filters:

* Reduce noise.
* Accelerate investigations.
* Isolate malicious traffic.
* Improve visibility.

---

# IP Filters

IP filters operate at the network layer.

### Examples

Show all IP traffic:

```text id="5c8i9g"
ip
```

Show packets involving a host:

```text id="viy7sn"
ip.addr == 10.10.10.10
```

Show source traffic:

```text id="hjwz2m"
ip.src == 10.10.10.10
```

Show destination traffic:

```text id="mllvmb"
ip.dst == 10.10.10.10
```

### SOC Use

Useful for tracking:

* Compromised devices.
* Threat actor infrastructure.
* Lateral movement activity.

---

# TCP and UDP Filters

Transport-layer filters help analysts investigate services and communications.

### Examples

```text id="5ie5i1"
tcp.port == 80
udp.port == 53
```

### Why They Matter

Attackers often use specific ports for:

* Reverse shells.
* Command-and-control traffic.
* Unauthorized services.

Port filtering helps quickly isolate these communications.

---

# HTTP Filters

Examples:

```text id="oqzt6y"
http
```

```text id="r76g7i"
http.request.method == "GET"
```

```text id="w4mmyi"
http.response.code == 200
```

### Investigation Use Cases

* File downloads.
* Malware delivery.
* User browsing activity.
* Successful web requests.

---

# DNS Filters

Examples:

```text id="z0x6nk"
dns
```

```text id="14tbm2"
dns.flags.response == 0
```

```text id="jlwmx4"
dns.qry.type == 1
```

### Investigation Use Cases

* DNS tunneling.
* Malware lookups.
* Beaconing activity.
* DGA detection.

---

# Advanced Filtering

Advanced operators make investigations significantly more powerful.

---

## contains

Searches for a keyword within a field.

Example:

```text id="2g1uhw"
http.server contains "Apache"
```

Useful for locating:

* Server banners.
* File names.
* Keywords.
* User-agent strings.

---

## matches

Uses regular expressions.

Example:

```text id="bxr4wa"
http.host matches "\.(php|html)"
```

Useful for complex searches involving patterns.

---

## in

Searches multiple values simultaneously.

Example:

```text id="4gd33m"
tcp.port in {80 443 8080}
```

This simplifies multi-port investigations.

---

## string()

Converts numerical values into strings.

Example:

```text id="wxj2kz"
string(ip.ttl)
```

This enables advanced pattern matching on fields that are normally numeric.

---

# Checksum Analysis

Checksums validate packet integrity.

A valid checksum suggests the packet arrived correctly.

A bad checksum may indicate:

* Corrupted traffic.
* Capture artifacts.
* Malformed packets.
* Potential manipulation attempts.

### SOC Relevance

Large volumes of malformed traffic may indicate:

* Scanning activity.
* Exploitation attempts.
* Misconfigured systems.

---

# Profiles

Profiles store custom Wireshark configurations.

A profile can contain:

* Custom filters.
* Coloring rules.
* Display settings.
* Investigation preferences.

### Benefits

Profiles allow analysts to quickly switch between:

* DNS investigations.
* Malware analysis.
* HTTP analysis.
* Checksum investigations.

Without reconfiguring Wireshark each time.

---

# Detection Opportunities

### DNS

Watch for:

* Tunneling.
* DGA domains.
* Beaconing.

### HTTP

Watch for:

* Malware downloads.
* Suspicious uploads.
* Phishing activity.

### TCP

Watch for:

* Reverse shells.
* C2 communications.
* Unauthorized services.

### Infrastructure

Watch for:

* Unknown hosts.
* Foreign IP addresses.
* Suspicious ASN ownership.

---

# Quick Revision

### Resolved Addresses

Maps IPs and MACs to meaningful names.

### Protocol Hierarchy

Shows protocol distribution and traffic composition.

### Conversations

Shows communication between two endpoints.

### Endpoints

Lists all hosts involved in traffic.

### DNS Statistics

Analyzes name resolution activity.

### HTTP Statistics

Analyzes web communications.

### Display Filters

Focus investigations on relevant traffic.

### contains

Searches for keywords.

### matches

Uses regular expressions.

### in

Matches multiple values.

### Profiles

Stores customized investigation environments.

---

# Final Takeaway

Packet Operations transforms Wireshark from a packet viewer into a powerful investigation platform.

By combining statistics, conversations, endpoints, protocol analysis, and advanced filtering, SOC analysts can rapidly identify suspicious activity, hunt threats, investigate incidents, and uncover attacker behavior hidden within large network captures.
