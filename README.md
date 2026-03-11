# Project #1 — Analyzing DNS Logs Using Splunk SIEM

---

## 📌 Introduction

DNS (Domain Name System) logs provide valuable insight into network activity and can help security analysts detect suspicious or malicious behavior.

In this project, DNS log files are ingested into **Splunk SIEM** and analyzed using **Splunk Search Processing Language (SPL)** to identify patterns, anomalies, and potentially malicious domains.

This project simulates how a **SOC Analyst investigates DNS activity using a SIEM platform**.

---

## 🎯 Objectives

The goal of this project is to:

- Upload DNS log files into Splunk
- Search and analyze DNS events
- Identify abnormal DNS query patterns
- Investigate suspicious domains
- Understand how SIEM tools assist SOC analysts in threat detection

---

## 🧪 Lab Environment

This project was performed in a personal cybersecurity lab environment.

**Virtualization Platform**

Oracle VirtualBox

**Virtual Machine**

Windows 11

**Security Tool**

Splunk Enterprise SIEM

---

### Lab Architecture

```
Host Machine
    │
    ▼
Oracle VirtualBox
    │
    ▼
Windows 11 Virtual Machine
    │
    ▼
Splunk Enterprise Installed
    │
    ▼
DNS Log Analysis
```

---

# Step 1 — Prepare DNS Log Files

Before uploading logs to Splunk, prepare a DNS log file containing relevant fields.

Typical DNS log fields include:

- Source IP
- Destination IP
- Domain name
- Query type
- Response code
- Timestamp

Example DNS log format:

```
timestamp src_ip dest_ip fqdn query_type response_code
```

Save the DNS log file locally.

Example:

```
dns_sample.log
```

---

# Step 2 — Upload DNS Logs into Splunk

1. Log in to the **Splunk Web Interface**

2. Navigate to:

```
Settings → Add Data
```

3. Select the **Upload** option

4. Click **Select File**

5. Choose the DNS log file

Example:

```
dns_sample.log
```

---

# Step 3 — Configure Source Type

During upload, configure the **source type** for DNS logs.

Example:

```
sourcetype=dns_sample
```

Also verify:

- Index
- Host
- Source type

Once everything is configured, click **Submit**.

---

# Step 4 — Verify Log Ingestion

After uploading the logs, verify that the events are visible.

Run the following query in Splunk:

```
index=* sourcetype=dns_sample
```

If the logs appear, the ingestion process was successful.

---

# Step 5 — Analyze DNS Events

Now we begin analyzing DNS activity using Splunk queries.

---

## Retrieve DNS Events

```
index=* sourcetype=dns_sample
```

This query retrieves all DNS events stored in the index.

---

## Extract DNS Related Events

```
index=* sourcetype=dns_sample
| regex _raw="(?i)\b(dns|domain|query|response|port 53)\b"
```

This query searches for DNS-related keywords within raw events.

---

## Identify DNS Query Spikes

```
index=* sourcetype=dns_sample
| stats count by fqdn
```

This query shows how frequently each domain is queried.

Unusual spikes may indicate suspicious activity.

---

## Find Top DNS Sources

```
index=* sourcetype=dns_sample
| top fqdn, src_ip
```

This helps identify:

- Most queried domains
- Most active source IP addresses

---

## Investigate Suspicious Domains

If a suspicious domain is discovered, it can be investigated further.

Example query:

```
index=* sourcetype=dns_sample fqdn="maliciousdomain.com"
```

Threat intelligence platforms such as **VirusTotal** can be used to verify malicious domains.

---

# 📊 Analysis Results

During DNS investigation, analysts may identify:

- Frequently queried domains
- Suspicious DNS requests
- Abnormal traffic patterns
- Potential command-and-control domains

These findings help security teams detect early indicators of compromise.

---

# 🔐 Security Insights

DNS monitoring is extremely important because attackers often use DNS for:

- Malware communication
- Data exfiltration
- Command and control infrastructure
- DNS tunneling

Analyzing DNS traffic allows SOC teams to detect threats early.

---

# 📌 Conclusion

This project demonstrates how **Splunk SIEM can be used to analyze DNS logs and detect suspicious network activity**.

Through this investigation process, we learned how to:

- Upload logs into Splunk
- Search and analyze DNS events
- Identify abnormal query behavior
- Investigate suspicious domains

These skills are essential for **SOC Analysts and Cybersecurity Professionals** working with SIEM platforms.

---
