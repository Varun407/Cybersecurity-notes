# Introduction to Endpoint Detection and Response (EDR)

## Overview

Endpoint Detection and Response (EDR) is an endpoint security solution designed to continuously monitor, detect, investigate, and respond to threats on endpoint devices such as Windows, Linux, and macOS systems.

Unlike traditional Antivirus (AV), EDR provides deep visibility into endpoint activities and enables security teams to investigate and respond to advanced threats.

---

## Why EDR is Important

With the rise of remote work and cloud-connected devices, endpoints often operate outside traditional network security boundaries. EDR ensures continuous protection regardless of the endpoint's location.

### Common EDR Solutions

* CrowdStrike Falcon
* SentinelOne ActiveEDR
* Microsoft Defender for Endpoint
* OpenEDR
* Symantec EDR

---

## Core Pillars of EDR

### 1. Visibility

Provides detailed endpoint telemetry and complete attack context.

Monitored activities include:

* Process executions and terminations
* Registry modifications
* File and folder changes
* User activities
* Network connections
* Command-line executions

Benefits:

* Process tree visualization
* Historical endpoint activity
* Attack timeline reconstruction
* Threat hunting support

### 2. Detection

Uses multiple detection methods:

* Signature-based detection
* Behavioral analysis
* IOC matching
* Anomaly detection
* Machine Learning models

Examples:

* Word document spawning PowerShell
* Obfuscated PowerShell execution
* Process injection attacks
* Fileless malware activity

### 3. Response

Allows analysts to respond directly from the EDR console.

Common response actions:

* Isolate host
* Terminate process
* Quarantine files
* Remote shell access
* Collect forensic artefacts

---

## EDR vs Traditional Antivirus

| Antivirus (AV)             | EDR                                  |
| -------------------------- | ------------------------------------ |
| Primarily signature-based  | Signature + behavioral detection     |
| Focuses on known threats   | Detects advanced and unknown threats |
| Limited visibility         | Full endpoint visibility             |
| Minimal investigation data | Complete attack context              |
| Limited response actions   | Extensive response capabilities      |

### Example Attack Chain

1. User opens malicious Word document.
2. Macro executes.
3. PowerShell is spawned.
4. Payload is downloaded.
5. Payload injects into `svchost.exe`.
6. Attacker gains remote access.

AV may miss several stages if no known signatures exist.

EDR can:

* Detect unusual parent-child processes
* Detect obfuscated commands
* Detect process injection
* Detect suspicious network activity
* Present the complete attack chain

---

## EDR Architecture

### EDR Agent (Sensor)

Installed on endpoints.

Responsibilities:

* Collect telemetry
* Monitor endpoint activity
* Perform basic detections
* Send data to EDR console

### EDR Console

Centralized management platform.

Responsibilities:

* Analyze telemetry
* Correlate events
* Apply threat intelligence
* Generate alerts
* Enable response actions

---

## Endpoint Telemetry Collected by EDR

### Process Activity

* Process creation
* Process termination
* Parent-child relationships

### Network Connections

* Outbound connections
* Inbound connections
* C2 communication detection
* Data exfiltration monitoring

### Command-Line Activity

* CMD commands
* PowerShell commands
* Script execution monitoring

### File & Folder Activity

* File creation
* File modification
* File deletion

### Registry Activity

* Registry key creation
* Registry modification
* Persistence mechanisms

---

## Detection Techniques

### Behavioral Detection

Detects suspicious behavior patterns.

Example:

* `winword.exe` spawning `powershell.exe`

### Anomaly Detection

Flags activities that deviate from normal baseline behavior.

### IOC Matching

Matches activity against known Indicators of Compromise.

Examples:

* Malicious hashes
* Domains
* IP addresses

### MITRE ATT&CK Mapping

Maps detections to:

* Tactics
* Techniques

Example:

* Persistence → Scheduled Task/Job

### Machine Learning Detection

Identifies complex attack chains and fileless malware.

---

## Response Capabilities

### Host Isolation

Disconnects an infected endpoint from the network.

### Process Termination

Stops malicious processes.

### File Quarantine

Moves malicious files to a safe isolated location.

### Remote Response

Provides remote shell access for investigation and remediation.

### Artefact Collection

Useful for forensic investigations.

Common artefacts:

* Memory dumps
* Event logs
* Registry hives
* Specific folder contents

---

## Key Takeaways

* EDR provides Visibility, Detection, and Response capabilities.
* EDR offers deeper visibility than traditional Antivirus.
* EDR agents collect telemetry from endpoints.
* Telemetry enables advanced threat detection and investigation.
* EDR supports both automated and manual response actions.
* EDR is a critical tool for SOC analysts during detection, investigation, and incident response.
