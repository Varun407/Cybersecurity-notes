# SOC Metrics & Objectives

## Purpose of SOC Metrics

SOC metrics are used to measure:

* SOC effectiveness
* Detection capabilities
* Analyst performance
* Response efficiency
* Overall security posture

Metrics help identify weaknesses and areas for improvement.

---

# SOC Goals

The primary goal of a SOC is to protect:

```text id="c1f7zq"
Confidentiality
Integrity
Availability
```

This is achieved through:

* Monitoring
* Detection
* Alert triage
* Incident response

---

# Core SOC Metrics

## Alert Count (AC)

### Formula

```text id="yzc17m"
AC = Total Alerts Received
```

### Purpose

Measures analyst workload.

---

### Too Many Alerts

Problems:

* Alert fatigue
* Missed threats
* Analyst burnout

---

### Too Few Alerts

Potential issues:

* SIEM malfunction
* Logging issues
* Missing visibility
* Detection failures

---

### Target

```text id="6m67kp"
~30 alerts per analyst per day
```

---

# False Positive Rate (FPR)

## Formula

```text id="m1hvn6"
FPR = False Positives / Total Alerts
```

---

## Purpose

Measures alert noise.

---

### Example

```text id="ynwpk6"
50 Alerts
10 True Positives
40 False Positives
```

```text id="stxrt7"
FPR = 40 / 50 = 80%
```

---

### High FPR Consequences

* Alert fatigue
* Reduced vigilance
* Missed attacks
* Analyst burnout

---

### Acceptable Threshold

```text id="9nyyx6"
Below 80%
```

Anything above 80% requires improvement.

---

# Alert Escalation Rate (AER)

## Formula

```text id="oqv5kw"
AER = Escalated Alerts / Total Alerts
```

---

## Purpose

Measures L1 independence and experience.

---

### High AER

May indicate:

* Lack of confidence
* Inexperienced analysts
* Insufficient documentation

---

### Recommended Targets

```text id="aqny1p"
Below 50%
Ideal: Below 20%
```

---

# Threat Detection Rate (TDR)

## Formula

```text id="0ybqr0"
TDR = Detected Threats / Total Threats
```

---

## Purpose

Measures SOC detection effectiveness.

---

### Example

```text id="x11gzu"
4 Threats Detected
6 Threats Total
```

```text id="qk1r1t"
TDR = 67%
```

---

### Goal

```text id="zwicqb"
100%
```

Missed threats can result in:

* Data theft
* Ransomware
* Business disruption

---

# SLA (Service Level Agreement)

## Definition

Formal agreement defining SOC performance expectations.

Can exist between:

* SOC and Management
* MSSP and Customers

---

## Purpose

Ensures threats are handled within agreed timeframes.

---

# SOC Availability

Common models:

### 24/7

```text id="j0d3bx"
24 Hours
7 Days
```

Continuous coverage.

---

### 8/5

```text id="g0x1dw"
8 Hours
5 Working Days
```

No weekend coverage.

---

# MTTD

## Mean Time To Detect

### Measures

Time between:

```text id="2vvv4h"
Attack Starts
      ↓
Alert Generated
```

---

### Example

```text id="w8zjri"
Attack Started
↓
Alert Generated After 12 Minutes
```

```text id="jz8yjy"
MTTD = 12 Minutes
```

---

### Target

```text id="ixzwot"
≤ 5 Minutes
```

---

# MTTA

## Mean Time To Acknowledge

### Measures

Time between:

```text id="u4egje"
Alert Generated
      ↓
Analyst Starts Investigation
```

---

### Example

```text id="jtnp7o"
Alert Generated
↓
Analyst Takes Alert 10 Minutes Later
```

```text id="aqg6yb"
MTTA = 10 Minutes
```

---

### Target

```text id="2bdhlh"
≤ 10 Minutes
```

---

# MTTR

## Mean Time To Respond

### Measures

Time between:

```text id="6i1npg"
Alert Generated
      ↓
Threat Contained
```

---

### Example

```text id="ohtsnm"
10 min Acknowledgement
+
6 min Escalation
+
35 min Remediation
```

```text id="k0htm0"
MTTR = 51 Minutes
```

---

### Target

```text id="h4v4tp"
≤ 60 Minutes
```

---

# Improving SOC Metrics

## High False Positive Rate

### Causes

* Poor detection rules
* Excessive system noise
* Trusted activities triggering alerts

---

### Improvements

* Tune SIEM rules
* Exclude trusted activities
* SOAR automation
* False Positive remediation

---

# High MTTD

## Causes

* Slow rule execution
* Delayed log ingestion
* Detection gaps

---

### Improvements

* Optimize detection rules
* Increase rule execution frequency
* Ensure real-time log collection

---

# High MTTA

## Causes

* Poor alert visibility
* Uneven workload distribution
* Staffing issues

---

### Improvements

* Real-time notifications
* Better workload balancing
* Queue management

---

# High MTTR

## Causes

* Slow remediation
* Missing procedures
* Escalation delays

---

### Improvements

* Faster escalation
* Better documentation
* Incident response playbooks
* Investigation workbooks

---

# Team Responsibility

Improving metrics is not only the SOC Manager's job.

Everyone contributes:

### L1 Analysts

* Report issues
* Identify alert fatigue
* Escalate efficiently

---

### L2 Analysts

* Improve investigations
* Create workbooks

---

### SOC Engineers

* Tune detections
* Improve SIEM performance

---

### Managers

* Track metrics
* Allocate resources

---

# Common Metric Problems

## Analysts Closing Hundreds of Alerts Daily

Likely issue:

```text id="ehwjx6"
High False Positive Rate
```

---

## Alert Appears Long After Attack Starts

Likely issue:

```text id="1jiywv"
High MTTD
```

---

## Alert Seen Quickly But Response Is Slow

Likely issue:

```text id="jxtfh5"
High MTTR
```

---

## Analyst Takes Too Long To Pick Up Alert

Likely issue:

```text id="u7uwow"
High MTTA
```

---

# Quick Revision

## Alert Count

```text id="r8ecvp"
Measures Workload
```

---

## False Positive Rate

```text id="4a9j2t"
Measures Alert Noise
```

---

## Alert Escalation Rate

```text id="fut2l9"
Measures L1 Independence
```

---

## Threat Detection Rate

```text id="8pl6x8"
Measures Detection Effectiveness
```

---

## MTTD

```text id="pf8sx0"
Attack → Alert
```

---

## MTTA

```text id="n3m1t8"
Alert → Analyst Action
```

---

## MTTR

```text id="trqgwj"
Alert → Threat Contained
```

---

## Golden Rule

```text id="z5u5h4"
Low FPR
Low MTTD
Low MTTA
Low MTTR
High TDR
```

A healthy SOC detects threats quickly, investigates them quickly, responds quickly, and minimizes analyst fatigue.
