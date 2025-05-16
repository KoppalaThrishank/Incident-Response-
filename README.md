
# 🛡️ Incident Response Plan & Execution Process

This repository documents a hands-on **Incident Response Lifecycle**, covering key phases from **Detection** to **Recovery**, with real-world simulations using **Splunk**, **OSSIM**, and other tools.

---

## 🔁 1. Detection and Alert Trigger

**🔧 Tool:** SIEM (Splunk, OSSIM)

- Alerts are generated using correlation/directive rules.
- Common alert types include:
  - ⚠️ Suspicious logins
  - 🐛 Malware activities
  - 💉 SQLi & 🚨 XSS attacks
  - 📤 Data exfiltration attempts

---

## 🧪 2. Alert Validation

**👤 Role:** L1 SOC Analyst

- Determine if an alert is a **true positive** by:
  - Reviewing logs from 🔐 endpoints, 🔥 firewalls, 🖥️ servers
  - Correlating host & network data
  - Cross-checking with 🧠 threat intelligence feeds

---

## 🧾 3. Ticket Creation (OSSIM)

**🛠️ Tool:** OSSIM Ticketing System

- Create a ticket with:
  - 📝 Alert summary
  - 🖥️ Affected assets
  - 🔍 Initial investigation notes
  - 🟠 Severity level
- Assign to the Incident Response Team (IRT)

---

## 🧪 Lab 1: Ticket Creation Demo

- 🖥️ Setup: OSSIM, WinServer2012, Analyst machine
- 👤 Create IRT user in OSSIM
- 🛰️ Deploy HIDS agent to WinServer2012
- 🔄 Create correlation directive for Brute Force Detection
- 🔐 Simulate failed & successful logins
- 🚨 OSSIM triggers an alarm
- 🎫 Convert alarm into a ticket and assign to IRT

---

## 🔒 4. Containment Phase: Data Loss via FTP

**🎯 Objective:** Stop ongoing FTP-based data exfiltration

### 🧪 Lab Steps:

1. Configure Splunk UF on WinServer2012  
   - 📁 Edit `inputs.conf`, `props.conf`, `transforms.conf` for FTP logs

2. Simulate Unauthorized FTP Access  
   - 🧑‍💻 Use Kali Linux + Hydra for brute-force login

3. Simulate Data Theft  
   - 🗂️ Use FileZilla to download 4.22 GB `.ISO` file

4. Detect FTP Session in Splunk  
   - 🔍 Monitor FTP logs for abnormal transfers

5. Contain the Attack  
   - ⛔ On WinServer2012, kill `ftpsvc` via Task Manager

6. Confirm Block  
   - ❌ FileZilla errors
   - 📉 Splunk logs show partial transfer and `550` errors

---

## 💥 5. Eradication Phase: SQL Injection & XSS

**🎯 Objective:** Block root cause using web filters

### 🧪 Lab Steps:

1. 🛠️ Install UrlScan on WinServer2012  
2. 📁 Copy `UrlScan` folder to website directory  
3. ✍️ Add SQLi/XSS rules in `UrlScan.ini`  
4. 🔄 Apply ISAPI Filter to IIS (LuxuryTreats website)  
5. 🔁 Restart IIS  
6. ✅ Test legitimate user access  
7. ❌ Test SQLi (`ORD-001' or 1=1;--`) — blocked by UrlScan

---

## 🧷 6. Recovery Phase: Data Loss Recovery

**🎯 Objective:** Recover deleted files and resume business continuity

### 🧪 Lab Overview:

- 🧾 Enable PowerShell logging
- 👀 Detect file deletion by malicious insider
- 💾 Use forensic tools to recover deleted files (e.g., Recuva, FTK Imager)

---

## ✅ Conclusion

📌 Each phase of the Incident Response lifecycle is implemented using real-world tools and scenarios:

| 🌀 **Phase**   | 🛠️ **Tool(s)**                    | 🔍 **Key Activity**                    |
| -------------- | ---------------------------------- | -------------------------------------- |
| Detection      | OSSIM, Splunk                     | Alert generation                       |
| Validation     | Logs, Threat Intel                | Confirm true positive                  |
| Ticketing      | OSSIM Ticketing System            | Incident assignment                    |
| Containment    | Splunk, Task Manager              | Stop FTP data exfiltration             |
| Eradication    | IIS, UrlScan                      | Block SQLi/XSS via web filtering       |
| Recovery       | PowerShell Logs, Recovery Tools   | Restore deleted files                  |

---

## 🧰 Tools Used

- 🧠 OSSIM SIEM & Ticketing System  
- 📊 Splunk UF & dashboards  
- 🔐 Windows Server 2012  
- 🐍 Hydra (Brute force)  
- 🧳 FileZilla (FTP client)  
- 🔎 UrlScan for IIS  
- 🧰 Recuva / FTK Imager (Recovery)



