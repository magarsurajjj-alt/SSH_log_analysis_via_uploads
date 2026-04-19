# 🔐 SSH Log Analysis using Splunk via uploads

## 📖 Overview
This project demonstrates how SSH authentication logs can be analyzed using **Splunk SIEM platform** to detect suspicious activities such as brute force attacks, unauthorized access attempts, and abnormal login behavior.

The project simulates a basic SOC (Security Operations Center) workflow including log ingestion, detection, visualization, and alerting.

---

## 🎯 Objectives
- Analyze SSH authentication logs
- Detect failed login attempts
- Identify brute force attacks
- Track successful logins
- Detect suspicious unauthenticated connections
- Build dashboards and alerts in Splunk

---

## 🛠️ Tools & Technologies
- Splunk (SIEM Platform)
- SSH Logs (auth.log / JSON dataset)
- Linux (Ubuntu/Kali optional)
- Windows (for Splunk UI access)

---

## 📂 Project Structure

```
SSH-Log-Analysis-Splunk/
├── README.md
├── data/
│   └── ssh_log.json
├── screenshots/
│   ├── data_ingestion/
│   ├── event_type/
│   ├── brute_force/
│   ├── failed_logins/
│   ├── alerts/
│   ├── successfull_login/
│   ├── connection_without_authentication/
│   └── dashboard_all_events/
├── queries/
│   ├── failed_logins.spl
│   ├── brute_force_detection.spl
│   ├── successful_logins.spl
│   └── suspicious_connections.spl
```


---

## 📥 Dataset
The dataset used in this project is `ssh_log.json`, which contains simulated SSH authentication events.

### Key Fields:
- `event_type` → Type of SSH event  
- `auth_success` → Success or failure status  
- `auth_attempts` → Number of attempts  
- `id.orig_h` → Source IP address  
- `id.resp_h` → Destination host  

---

## ⚙️ Data Ingestion Steps
1. Open Splunk Web  
2. Go to **Search & Reporting App**  
3. Click **Add Data → Upload**  
4. Upload `ssh_log.json`  
5. Set:
   - Sourcetype: `_json`  
   - Index: `ssh_logs`  
6. Start indexing and searching  

---

## 🔍 Key Splunk Queries

### 1. View All Events
```spl
index=ssh_logs

2. Failed SSH Login Attempts
index=ssh_logs event_type="Failed SSH Login"
| stats count by id.orig_h

3. Brute Force Detection
index=ssh_logs event_type="Multiple Failed Authentication Attempts"
| stats count by id.orig_h, id.resp_h

4. Successful SSH Logins
index=ssh_logs event_type="Successful SSH Login"
| stats count by id.orig_h, id.resp_h
<img width="1366" height="768" alt="08_Dashboard" src="https://github.com/user-attachments/assets/c63b85b1-03bf-46b8-910e-1438d2f1fd0b" />

5. Unauthenticated Connection Attempts
index=ssh_logs event_type="Connection Without Authentication"
| timechart count by id.orig_h
📊 Dashboards Created
Failed login attempts by IP
Successful login activity
Brute force detection panel
SSH connection trends over time
🚨 Detection Use Cases
Brute Force Attack → Multiple failed login attempts
Account Compromise → Failed attempts followed by success
Port Scanning / Reconnaissance → Repeated unauthenticated connections
📸 Screenshots



Dashboard overview
Failed login visualization
Alert configuration
Query outputs
🚨 Alerts (Optional Enhancement)

Configured Splunk alert:

Trigger when an IP has more than 5 failed login attempts in 10 minutes
Used for detecting brute force attacks
📈 Learning Outcome

By completing this project, I gain hands-on experience in:

Log ingestion in Splunk
Writing SPL queries
Detecting security threats
Creating dashboards
SOC analyst workflow understanding
👨‍💻 Author

Your Name

📌 Future Improvements
Real-time log monitoring using forwarders
Integration with threat intelligence feeds
MITRE ATT&CK mapping
Advanced alerting and incident response workflow
⭐ Conclusion

This project demonstrates practical SOC skills using Splunk for SSH log monitoring and security threat detection, simulating real-world cybersecurity operations.
