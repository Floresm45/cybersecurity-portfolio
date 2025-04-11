# ☁️ AWS EC2 Cloud Security Hardening Lab

This hands-on project focuses on securing a publicly deployed Ubuntu EC2 instance in AWS using real-world security tools and practices. The goal was to lock down SSH access, enforce firewall policies, audit user behavior, and validate improvements using Lynis.

---

## 🧠 Objectives

- Launch a public EC2 instance running Ubuntu 24.04 LTS
- Configure SSH securely using key authentication and non-default ports
- Set up UFW firewall rules
- Enable intrusion detection with Fail2Ban
- Configure auditing with Auditd
- Perform post-hardening audit using Lynis

---

## 🛠️ Tools Used

| Tool       | Purpose                                |
|------------|----------------------------------------|
| AWS EC2    | Cloud-hosted Ubuntu server             |
| SSH        | Secure shell remote access             |
| UFW        | Host-based firewall                    |
| Fail2Ban   | Intrusion prevention system            |
| Auditd     | System auditing                        |
| Lynis      | Security auditing and compliance scan  |

---

## 🔐 Key Hardening Steps

### 🔹 SSH Configuration
- Disabled root login (`PermitRootLogin no`)
- Changed SSH port from 22 to 2222
- Reduced `MaxAuthTries` to 3

### 🔹 Firewall Configuration (UFW)
```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow 2222/tcp
sudo ufw enable
```

### 🔹 Intrusion Prevention (Fail2Ban)
- Created a jail for SSH with:
  - Max retries: 3
  - Ban time: 10 minutes

### 🔹 Auditing (Auditd)
- Enabled Auditd service
- Added custom rule to monitor `/etc/passwd` for changes
```bash
auditctl -w /etc/passwd -p wa -k passwd_watch
```

---

## 📊 Lynis Post-Hardening Audit

| Metric             | Value   |
|--------------------|---------|
| Hardening Index    | 66/100  |
| Warnings           | 0       |
| Suggestions        | ✔️ Present |

---

## 📸 Screenshots (in `/screenshots/` folder)

- SSH login via key
- UFW status
- Fail2Ban jail status
- Audit rule log search
- Lynis final score output

---

## ✅ Outcome

By following this lab, I implemented layered security controls on a publicly accessible cloud server. This exercise reflects foundational DevSecOps practices and showcases my ability to secure cloud infrastructure using free, open-source tools.

---

## 📁 Repository Structure

```
cloud-security-hardening/
├── README.md
├── screenshots/
│   ├── ssh-login.png
│   ├── ufw-status.png
│   ├── fail2ban-status.png
│   ├── auditd-output.png
│   └── lynis-summary.png
└── lynis-report.txt
```

---

## 📎 Related Projects

Return to the full portfolio: [Main README](../README.md)
