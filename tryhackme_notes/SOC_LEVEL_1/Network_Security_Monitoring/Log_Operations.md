# Log Operations

## 1. Introduction

### What is Log Operations?
- Managing, configuring, collecting, storing, and analysing logs.
- Helps security teams find threats faster.
- Prevents analysts from getting lost in huge amounts of log data.

### Objectives
- Understand log management logic.
- Learn log configuration approaches.
- Gain experience with logging operations.

---

# 2. Log Configuration

## Why Configure Logs?
Proper logging supports:

### Security
**Goal:** Detect attacks and unauthorized activities.

**Focus Areas**
- Threat detection
- User authentication tracking
- System integrity monitoring
- Data confidentiality

### Operational
**Goal:** Keep systems stable and reliable.

**Focus Areas**
- System monitoring
- Troubleshooting
- Capacity planning
- Service billing

### Legal / Compliance
**Goal:** Meet regulations and audit requirements.

**Examples**
- ISO 27001
- PCI DSS
- GDPR
- HIPAA
- COBIT
- FISMA

**Typical Requirements**
- Centralized logging
- Log retention policies
- Security audits
- Searchable historical logs

### Debugging
**Goal:** Help developers identify software issues.

**Focus Areas**
- Bug tracking
- Application visibility
- Faster development
- Performance improvement

---

# 3. Planning a Logging Strategy

## Key Questions

### Scope
- What will be logged?
- Why is it being logged?

### Requirements
- Are there compliance requirements?
- Are additional resources needed?

### Detail Level
- How much detail is necessary?
- How much data is useful?

### Collection
- How will logs be collected?

### Storage
- Where will logs be stored?

### Security
- How will logs be protected?

### Analysis
- How will logs be reviewed and analyzed?

### Resources
- Do we have enough staff?
- Do we have enough budget?

---

# 4. Configuration Dilemma

## Main Challenge

Finding a balance between:

- Requirements
- Scope
- Detail level
- Cost
- Resources

---

## Base Requirements (Reactive)

Focus on incident response.

Questions:
- What happened?
- When did it happen?
- Where did it happen?
- Who caused it?
- Was it successful?

---

## Aspirations (Proactive)

Focus on threat hunting.

Questions:
- Can we collect more context?
- What is affected?
- What happens next?
- What should be done?
- Are there hidden indicators?

### Comparison

| Reactive | Proactive |
|-----------|-----------|
| Incident Detection | Threat Hunting |
| Known Threats | Advanced Threats |
| Lower Cost | Higher Cost |
| Essential | Recommended |

---

# 5. Logging Principles

## Collection

### Best Practices
- Define logging purpose.
- Collect useful data only.
- Avoid irrelevant logs.
- Reduce log noise.

---

## Format

### Best Practices
- Use correct detail level.
- Maintain consistent format.
- Synchronize timestamps.

---

## Archiving & Accessibility

### Best Practices
- Define retention policies.
- Store logs securely.
- Keep important logs accessible.
- Maintain backups.

---

## Monitoring & Alerting

### Best Practices
- Create actionable alerts.
- Notify important events.
- Minimize alert fatigue.

---

## Security

### Best Practices
- Restrict log access.
- Encrypt when necessary.
- Use dedicated log management systems.

---

## Continuous Improvement

### Best Practices
- Adapt to changes.
- Update configurations.
- Train staff regularly.

---

# 6. Logging Challenges

## Data Volume & Noise

### Problems
- Too many log sources.
- Excessive log generation.
- Irrelevant events.
- Difficult investigations.

---

## System Performance & Collection

### Problems
- Logging impacts performance.
- Legacy systems are difficult to modify.
- Collection agent issues.
- Version synchronization challenges.

---

## Processing & Archiving

### Problems
- Multiple formats.
- Parsing complexity.
- Retention management difficulties.

---

## Security

### Problems
- Protecting logs from unauthorized access.
- Ensuring log integrity.

---

## Analysis

### Problems
- Correlation across sources.
- Real-time analysis difficulties.
- False positives.
- False negatives.

---

## Organizational Issues

### Problems
- Poor planning.
- Budget limitations.
- Lack of skills.
- Missing playbooks.
- Insufficient training.

---

# 7. Common Mistakes

## Mistakes ("Don'ts")

- Logging sensitive information.
- Creating custom logging scripts unnecessarily.
- Leaving logs uncollected.
- Collecting everything without analysis.
- Poor planning.
- Skipping testing.
- Ignoring internal systems.
- Investigating only expected findings.
- Ignoring maintenance.

---

# 8. Best Practices

## Do's

- Create proper logging plans.
- Test logging functionality.
- Exclude sensitive information.
- Secure stored logs.
- Create meaningful alerts.
- Focus on actionable insights.
- Train analysts.
- Regularly update configurations.

---

# Exam Notes

## Reactive Logging
- Incident detection.
- Answers: What, When, Where, Who.

## Proactive Logging
- Threat hunting.
- Looks beyond basic evidence.

## Important Principle
**Archiving and Accessibility**
- Retention policies.
- Log availability.
- Backups.

## Common Challenge
**System Performance and Collection**
- Log transfer failures.
- Collection agent problems.
- Synchronization issues.

## Common Mistake
**Creating logs by yourself**
- Custom scripts can miss events.
- Can lead to incomplete logging.
