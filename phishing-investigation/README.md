
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

### 📎 Attachments by Sender
```spl
index=main attachment!="-" 
| stats count by sender, attachment 
| sort -count
```
![Attachments by Sender](./screenshots/attachments_by_sender.png)

---

### 🔗 URLs Sent by Sender
```spl
index=main url!="-" 
| stats count by sender, url 
| sort -count
```
![URLs by Sender](./screenshots/urls_by_sender.png)

---

### 🎯 Most Targeted Recipients
```spl
index=main 
| top recipient
```
![Top Recipients](./screenshots/top_recipients.png)

---

### 🧾 Top Subject Lines
```spl
index=main 
| top subject
```
![Top Subjects](./screenshots/top_subjects.png)

---

### 📬 Total Emails by Sender
```spl
index=main 
| stats count by sender 
| sort -count
```
![Total Emails by Sender](./screenshots/top_senders.png)

---

### 📈 Email Volume Over Time
```spl
index=main 
| timechart span=1h count by sender
```
![Email Volume Over Time](./screenshots/email_volume.png)

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
