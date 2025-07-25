# Task 2 – Security Alert Monitoring & Incident Response    
 **Track Code**: FUTURE_CS_02  
 **SOC Analyst**: Vaibhav Malhotra  
 
---

This Repo contains all work related to Task2 of Cyber Security Internship by Future Interns.  
The task simulates the responsibilities of a SOC (Security Operations Center) analyst:  
Monitoring logs, analyzing security alerts, and drafting a professional incident response report using Splunk.  

---

## 📌 Deliverables:
1. Incident Response Report (PDF or Doc)  
2. Screenshots of analyzed alerts and SIEM dashboard
3. Alert classification log or spreadsheet  
4. Remediation Suggested Steps  
5. StakeHolder Communication  
6. Failed Login Attempts Screenshot  
7. Tools.txt  

---

## 🔧 Tools Used:
- Splunk Cloud Platform (Free Trial)  
- SPL (Search Processing Language)
- Git & GitHub

---

## 🔍 SPL Queries Used
1. Show Logs: source="imp-log.txt" host="name of the machine" sourcetype="implogs"  
2. Malware Alerts: index=main source="imp-log.txt" action="malware detected"  
3. Failed Logins: index=main source="imp-log.txt" user login failed
4.Severity classification: index=main source="imp-log.txt" action="malware detected"
| rex "user=(?<user>\w+)"
| rex "ip=(?<ip>\d+\.\d+\.\d+\.\d+)"
| rex "action=(?<action>[^|]+)"
| rex "threat=(?<threat>.+)"
| eval severity=case(
    match(threat, "Rootkit"), "Critical",
    match(threat, "Ransomware"), "Critical",
    match(threat, "Worm"), "High",
    match(threat, "Trojan"), "High",
    match(threat, "Spyware"), "Medium",
    1==1, "Low"
)
| table _time user ip threat severity
| sort -_time
---
   
   
