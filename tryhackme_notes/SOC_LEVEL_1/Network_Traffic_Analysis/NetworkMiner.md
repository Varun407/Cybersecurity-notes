# NetworkMiner

## Task 1: Introduction
### What is NetworkMiner?

* Open-source **Network Forensic Analysis Tool (NFAT)**.
* Used to analyze **PCAP files** and captured traffic.
* Works passively (does not generate network traffic).
* Can extract:

  * Hosts
  * Sessions
  * Files
  * Credentials
  * Certificates
  * OS information

### NetworkMiner vs Snort

| NetworkMiner                | Snort                 |
| --------------------------- | --------------------- |
| Passive analysis            | Real-time detection   |
| Post-incident investigation | Active monitoring     |
| PCAP analysis               | Live traffic analysis |
| File extraction             | Signature matching    |
| Network forensics           | IDS/IPS               |

---

## Task 2: Network Forensics

### What is Network Forensics?

* Investigation of network traffic to identify attacks and suspicious activity.
* Helps reconstruct events from captured packets.

### Five Questions of Network Forensics

* **Who?** → Source IP
* **What?** → Data transferred
* **Where?** → Destination IP
* **When?** → Timestamp
* **Why?** → Cause of incident

### Common Use Cases

* Network discovery
* Packet reconstruction
* Data leakage detection
* Threat hunting
* Compliance monitoring

### Advantages

* No additional network noise.
* Network evidence is difficult to erase.
* Can detect fileless/memory-based attacks.
* Provides historical evidence.

### Challenges

* Large storage requirements.
* Encrypted traffic visibility issues.
* Privacy and compliance concerns.
* Log tampering.
* Time-zone correlation problems.

### Evidence Sources

* Firewalls
* Routers
* Switches
* IDS/IPS
* DHCP Servers
* Authentication Servers
* Packet Captures (PCAP)

---

## Task 3: NetworkMiner Features

### Main Capabilities

* PCAP parsing
* Traffic sniffing
* OS fingerprinting
* File extraction
* Credential extraction
* Cleartext keyword discovery

### Pros

* Fast traffic overview.
* Easy file extraction.
* Good OS fingerprinting.
* Finds credentials automatically.

### Cons

* Limited filtering.
* Weak protocol analysis.
* Poor for huge PCAP files.
* Not ideal for live monitoring.

### NetworkMiner vs Wireshark

| Feature              | NetworkMiner | Wireshark |
| -------------------- | ------------ | --------- |
| Quick overview       | ✅            | ❌         |
| OS fingerprinting    | ✅            | ❌         |
| File extraction      | ✅            | ✅         |
| Deep packet analysis | ❌            | ✅         |
| Advanced filters     | ❌            | ✅         |
| Protocol decoding    | Limited      | Excellent |

### Remember

* **NetworkMiner = Quick overview & artifact extraction**
* **Wireshark = Deep packet investigation**
