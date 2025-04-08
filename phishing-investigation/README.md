```markdown
[Jump to Queries & Visuals](#splunk-queries--visualizations)
# Phishing Incident Investigation

## Project Overview
Simulated a phishing attack and used Splunk to identify indicators of compromise (IoCs), trace attack behavior, and recommend mitigations.

## Tools Used
- Splunk (free cloud trial)
- Sample phishing logs
- Regex, dashboards, log analysis

## Investigation Process
1. **Ingested Logs** – Uploaded email server logs into Splunk
2. **Identified Suspicious Activity** – Used queries to detect phishing URLs, attachments, and user activity
3. **Mapped the Attack Chain** – Traced timeline from phishing email to user click
4. **Recommendations** – Proposed 2FA, improved email filtering, security awareness training

## Screenshots
- [ ] Splunk query with results
- [ ] Dashboard with visualized threats

## Key Metrics
- Response time improved by ~40% using automation
- Reduced false positives by refining search filters

## 🔍 Splunk Queries & Visualizations

### Attachments by Sender
spl
index=main attachment!="-" 
| stats count by sender, attachment 
| sort -count

### URLs Sent by Sender
index=main url!="-" 
| stats count by sender, url 
| sort -count

### Most Targeted Recipients
index=main 
| top recipient

### Top Subject Lines
index=main 
| top subject

### Email Volume Over Time
index=main 
| timechart span=1h count by sender

