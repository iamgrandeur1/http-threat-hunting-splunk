# HTTP Threat Hunting & Web Attack Detection Using Splunk

##  Overview

This project focuses on analyzing Zeek HTTP logs within Splunk to identify suspicious web activity, exploitation attempts, and indicators of web-based attacks.

The investigation involved parsing HTTP traffic, reviewing request behavior, and identifying malicious URI patterns commonly associated with reconnaissance and exploitation attempts.

---

##  Objective

To perform HTTP threat hunting using Splunk and identify suspicious web requests indicative of attacker behavior.

---

##  Lab Setup

- **Log Source:** Zeek (`http.log`)
- **SIEM:** Splunk
- **Environment:** Virtual Lab (Kali Linux + VirtualBox)

---

##  Dataset

The HTTP logs contained:

- Client IP addresses
- Destination web servers
- HTTP methods
- Requested URIs
- User-Agent strings
- HTTP status codes

---

##  Detection Methodology

### 1. HTTP Log Ingestion

- Uploaded HTTP logs into Splunk
- Assigned custom sourcetype: `zeek_http`
- Verified successful event parsing

---

### 2. Suspicious Request Hunting

Used Splunk SPL to identify suspicious URI patterns and potential exploitation attempts.

```spl
index=main sourcetype=zeek_http
| search _raw="*passwd*" OR _raw="*phpmyadmin*" OR _raw="*../*"
| table _time id.orig_h id.resp_h method uri user_agent status_code
```

---

##  Analysis & Findings

### Observed Suspicious Activity

The investigation identified multiple suspicious web requests, including:
m
- Directory traversal attempts
- Requests targeting `/etc/passwd`
- phpMyAdmin enumeration attempts
- Suspicious JSP and PHP requests
- Web reconnaissance behavior

---

### Example Indicators

Suspicious URI examples observed:

```text
../../../../../../../../etc/passwd
```

```text
/phpmyadmin/admin/general.php
```

These requests are commonly associated with:

- Web exploitation attempts
- Vulnerability scanning
- Unauthorized access attempts
- Reconnaissance activity

---

##  SOC Insight

HTTP traffic analysis is critical for identifying early-stage attack activity.

Indicators such as directory traversal attempts and administrative page targeting can reveal:

- automated scanners
- exploitation frameworks
- attacker reconnaissance
- vulnerable application probing

Proper log visibility enables analysts to detect suspicious behavior before compromise escalation.

---

##  Key Takeaway

Threat hunting is not limited to malware detection.

Analyzing web traffic and suspicious HTTP requests provides valuable visibility into attacker behavior and infrastructure targeting.

---

##  Next Steps

- Correlate HTTP activity with DNS requests
- Identify suspicious User-Agent behavior
- Build HTTP anomaly dashboards
- Develop Splunk alerts for exploitation indicators
- Expand detection coverage for web attacks

---

##  Sample Output

Add screenshots here showing:

- suspicious HTTP requests
- `/etc/passwd` targeting
- phpMyAdmin requests
- Splunk threat hunting queries

Example:

```markdown
![HTTP Threat Hunting](http-threat-hunting.png)
```

---

##  Skills Demonstrated

- Splunk SPL
- Threat Hunting
- HTTP Traffic Analysis
- Detection Engineering
- Log Parsing
- Web Attack Detection
- SOC Investigation
- Zeek Log Analysis
- Cybersecurity Monitoring
