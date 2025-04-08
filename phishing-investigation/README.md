
# 🕵️ Phishing Incident Investigation

## 📋 Project Overview
Simulated a phishing attack and used Splunk to identify indicators of compromise (IoCs), trace attack behavior, and recommend mitigations.

---

## 🛠️ Tools Used
- Splunk (free cloud trial)
- Sample phishing logs
- Regex, dashboards, log analysis

---

## 🔍 Investigation Process
1. **Ingested Logs** – Uploaded email server logs into Splunk
2. **Identified Suspicious Activity** – Used queries to detect phishing URLs, attachments, and user activity
3. **Mapped the Attack Chain** – Traced timeline from phishing email to user click
4. **Recommendations** – Proposed 2FA, improved email filtering, security awareness training

---

## 📸 Screenshots
- [x] Splunk query with results
- [x] Dashboard with visualized threats

---

## 📊 Key Metrics
- Top senders and recipients
- Most common phishing URLs and subjects
- Frequency of email attachments
- Email volume trends

---

## 🔍 Splunk Queries & Visualizations

### 🔗 URLs Sent by Sender
```spl
index=main url!="-" 
| stats count by sender, url 
| sort -count
```
![URLs Sent by Sender](https://github.com/user-attachments/assets/93d8051a-ff96-4421-bd0d-a94a2d8a01a9)

---

### 🎯 Most Targeted Recipients
```spl
index=main 
| top recipient
```
![Most Targeted Recipients](https://github.com/user-attachments/assets/453cb61e-8ab7-4b7b-a66a-a332714a4bf4)

---

### 📬 Total Emails by Sender
```spl
index=main 
| stats count by sender 
| sort -count
```
![Top Senders (Potential Spammers)](https://github.com/user-attachments/assets/78fc2a63-f62e-43bd-bad6-a8c8fa2af129)

---

### 📈 Email Volume Over Time
```spl
index=main 
| timechart span=1h count by sender
```
![Email Volume Over Time](https://github.com/user-attachments/assets/7911962c-4764-433e-a298-5f78b3b1b3a9)

---

## ✅ Key Findings
- Majority of phishing attempts targeted `employee@company.com`
- High-risk attachments like `invoice.pdf` and fake URLs were present
- Attackers often used `Update` and `Alert` in subject lines

---

## 📌 Recommendations
- Improve phishing training and reporting protocol
- Flag senders with repeat high-risk activity
- Block known malicious domains and file types

---

## 📸 Dashboard Preview
> Here’s a snapshot of the full Splunk dashboard.

![Dashboard Overview](./screenshots/dashboard_full.png)
Restored full README with dashboard and queries
