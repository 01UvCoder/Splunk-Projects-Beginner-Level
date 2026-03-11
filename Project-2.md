![Build Status](https://img.shields.io/badge/build-passing-brightgreen)
![Security Project](https://img.shields.io/badge/domain-SIEM%20Analysis-blue)
![Platform](https://img.shields.io/badge/platform-Splunk-orange)
![License](https://img.shields.io/badge/license-MIT-green)
![Maintained](https://img.shields.io/badge/maintained-yes-success)

# HTTP Log Analysis Using Splunk SIEM

This project demonstrates how HTTP web server logs can be ingested, analyzed, and monitored using **Splunk SIEM**. The objective of this lab is to simulate a real-world **Security Operations Center (SOC)** workflow where security analysts investigate web traffic, monitor activity patterns, and identify potential threats within HTTP logs.

The project was implemented in a **local cybersecurity lab environment** where **Splunk Enterprise was installed on a Windows 11 virtual machine running inside Oracle VirtualBox**. Using this setup, HTTP log files were uploaded into Splunk and analyzed using **SPL (Search Processing Language)** to extract insights about web server activity.

This project helps demonstrate fundamental SIEM skills such as **log ingestion, traffic analysis, anomaly detection, and investigation of suspicious events**.

---

# 🚀 Features

- Upload HTTP log files into Splunk SIEM
- Parse and analyze raw log data
- Extract key fields from HTTP logs
- Analyze web traffic behavior
- Identify frequently accessed endpoints
- Monitor HTTP response codes
- Detect abnormal activity patterns
- Investigate suspicious IP addresses
- Perform basic user behavior analysis

---

# 🛠️ Tech Stack

| Technology | Purpose |
|------------|--------|
| Splunk Enterprise | SIEM platform used for log analysis |
| Windows 11 | Operating system inside the lab VM |
| Oracle VirtualBox | Virtualization environment |
| HTTP Log Files | Web server activity data |
| SPL (Search Processing Language) | Query language used in Splunk |
| Regular Expressions (Regex) | Field extraction from log data |

---

# 🧪 Lab Environment

This project was built inside a controlled **local lab environment** to simulate a real SOC monitoring setup.

Environment configuration:

| Component | Configuration |
|----------|---------------|
| Host Machine | Local Computer |
| Virtualization Platform | Oracle VirtualBox |
| Guest OS | Windows 11 |
| SIEM Platform | Splunk Enterprise |
| Data Source | Sample HTTP Access Logs |

Architecture Overview

```
Local Machine
     │
     ▼
Oracle VirtualBox
     │
     ▼
Windows 11 Virtual Machine
     │
     ▼
Splunk Enterprise
     │
     ▼
HTTP Log File Ingestion & Analysis
```
---

# ⚙️ Installation

Follow the steps below to recreate the same lab environment.

## 1. Install Oracle VirtualBox

Download and install VirtualBox from the official website.

https://www.virtualbox.org

---

## 2. Create a Windows 11 Virtual Machine

Create a new virtual machine in VirtualBox and install Windows 11.

Recommended configuration:

- RAM: 8 GB
- CPU: 2 Cores
- Storage: 60 GB

---

## 3. Install Splunk Enterprise

Download Splunk Enterprise from the official website.

https://www.splunk.com

Install Splunk inside the Windows 11 virtual machine.

Once installed, start the Splunk service and open the Splunk web interface:

http://localhost:8000

Login using the administrator credentials created during the installation process.

---

# ▶️ Usage

After Splunk is installed and running, HTTP logs can be uploaded and analyzed.

---

# Upload HTTP Log Files to Splunk

### Step 1 – Prepare HTTP Log Files

Prepare sample HTTP access logs containing information such as:

- Timestamp
- Source IP Address
- HTTP Request Method
- Requested URL
- Response Status Code
- User Agent

Example log entry:

```
192.168.1.25 - - [10/Oct/2025:13:55:36] "GET /index.html HTTP/1.1" 200 1024
```

---

### Step 2 – Upload Logs to Splunk

Open the Splunk Web Interface and navigate to:

Settings → Add Data

Select:

Upload

---

### Step 3 – Select Log File

Choose the prepared HTTP log file from your system.

---

### Step 4 – Configure Source Type

Set the appropriate source type for the log file.

Example:

```
access_combined
```

---

### Step 5 – Configure Index

Create or select a Splunk index where the log data will be stored.

Example:

```
http_logs
```

---

### Step 6 – Review and Submit

Verify the configuration settings:

- Host
- Index
- Sourcetype

Click **Review** and then **Submit**.

Splunk will now ingest the HTTP logs.

---

# 📊 Log Analysis Using Splunk

Once the logs are indexed, various queries can be used to analyze the HTTP activity.

---

# Search HTTP Events

Retrieve all HTTP log events.

```spl
index=http_logs sourcetype=access_combined
```

---

# Analyze HTTP Request Methods

Determine how frequently different request methods are used.

```spl
index=http_logs sourcetype=access_combined
| stats count by method
```

This helps identify traffic patterns such as GET and POST requests.

---

# Identify Most Accessed URLs

```spl
index=http_logs sourcetype=access_combined
| top limit=10 uri
```

This query highlights the most frequently accessed endpoints.

---

# Monitor HTTP Response Codes

```spl
index=http_logs sourcetype=access_combined
| stats count by status
```

Common response codes include:

| Code | Meaning |
|-----|--------|
| 200 | Successful request |
| 404 | Resource not found |
| 500 | Internal server error |

Monitoring response codes helps identify application issues or attack attempts.

---

# Traffic Trend Analysis

```spl
index=http_logs sourcetype=access_combined
| timechart span=1h count
```

This visualization helps detect:

- Traffic spikes
- Suspicious activity
- Possible denial-of-service attempts

---

# Detect Suspicious IP Activity

```spl
index=http_logs sourcetype=access_combined
| search src_ip="SUSPICIOUS_IP"
```

This query can be used during investigations to track activity from suspicious hosts.

---

# User Behavior Analysis

Example query to detect failed login attempts.

```spl
index=http_logs sourcetype=access_combined
| search action="login" status="failed"
| stats count by user
```

This helps identify potential brute-force attacks or unauthorized access attempts.

---

# 📊 Example Output

Example results produced in Splunk include:

- Web traffic volume charts
- Top accessed endpoints
- HTTP status code distribution
- Suspicious IP investigation results

Screenshots of these outputs can be added to the **screenshots** directory for visualization.

---

# 🔐 Security Considerations

When analyzing HTTP logs, analysts should monitor for indicators such as:

- Repeated failed authentication attempts
- High volumes of 404 errors
- Large numbers of 500 server errors
- Requests from suspicious IP addresses
- Unusual spikes in traffic

These indicators may signal threats such as:

- Brute-force attacks
- Automated web scanning
- Enumeration attempts
- Bot activity

Proper log monitoring enables early detection of these security risks.

---

# 📌 Future Improvements

Future enhancements for this project may include:

- Creating interactive Splunk dashboards
- Implementing automated alerts
- Integrating threat intelligence feeds
- Simulating real attack scenarios
- Adding additional log sources for correlation

---

# 🤝 Contributing

Contributions are welcome.

To contribute to this project:

1. Fork the repository
2. Create a new branch

```
git checkout -b feature-improvement
```

3. Commit your changes

```
git commit -m "Improved Splunk queries"
```

4. Push the branch

```
git push origin feature-improvement
```

5. Open a Pull Request

---

# 📜 License

This project is licensed under the **MIT License**.

You are free to use and modify the project for learning and research purposes.

---

# 👨‍💻 Author

Umang Vataliya

Cybersecurity Enthusiast  
SOC Analyst Learner  
Splunk Practitioner

GitHub:  
https://github.com/YOUR_GITHUB_USERNAME

---

⭐ If you found this project useful, consider giving the repository a star.
