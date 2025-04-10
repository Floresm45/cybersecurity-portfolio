# 🛡️ System Hardening Lab (Ubuntu)

## 📋 Overview

This lab simulates a real-world system hardening process on an Ubuntu 22.04 virtual machine (VM). The goal was to identify and remediate security weaknesses using open-source tools and industry best practices, all documented step-by-step.

---

## 🧰 Tools Used

- Ubuntu 22.04 LTS (VirtualBox VM)
- VirtualBox (Hypervisor)
- Lynis (Security auditing tool)
- UFW (Uncomplicated Firewall)
- OpenSSH (with secure config)
- Auditd & Fail2Ban (Logging & intrusion protection)

---

## 🔐 Hardening Process

### 1️⃣ Pre-Hardening Audit (Baseline)

- Installed **Lynis**:

  ```bash
  sudo apt install lynis
  sudo lynis audit system
  ```
![Lynis warnings and suggestions](https://github.com/user-attachments/assets/1f6b3446-ea38-42d2-bd2c-f0bf21be227e)
![Lynis audit score](https://github.com/user-attachments/assets/ba31d417-f72a-4cc8-9f36-f0c737773f4a)
- 📸 *Screenshot: Lynis initial scan results* 

- 🔍 Findings: Weak SSH config, no firewall, poor password policies, missing auditing

---

### 2️⃣ SSH Security Configuration

- Opened SSH config file:

  ```bash
  sudo nano /etc/ssh/sshd_config
  ```

- 🔧 Changed settings:
  - Changed port to `2222`
  - Disabled root login (`PermitRootLogin no`)
  - Enforced key-based auth (optional)

- Applied changes:

  ```bash
  sudo systemctl restart ssh
  ```
![Changing SSH permissions](https://github.com/user-attachments/assets/5d50e330-084d-4206-b578-2c56f9f0a501)

📸 *Screenshot: Edited sshd_config file (highlighted changes)*



![SSH running after config](https://github.com/user-attachments/assets/63a97362-9e7b-4d36-9ea0-302283916438)

📸 *Screenshot: Terminal confirming SSH restart*

---

### 3️⃣ UFW Firewall Setup

- Installed & enabled UFW:

  ```bash
  sudo apt install ufw
  sudo ufw allow 2222/tcp
  sudo ufw allow 80/tcp    # (optional)
  sudo ufw allow 443/tcp   # (optional)
  sudo ufw enable
  sudo ufw status verbose
  ```

- 🔒 Allowed only essential ports

![UFW status update](https://github.com/user-attachments/assets/e3741dcf-e1e5-4f7e-9b90-58463a24f009)
- 📸 *Screenshot: Terminal output from enabling UFW and status check*

---

### 4️⃣ System Auditing with auditd

- Installed auditd and verified logging was working:

  ```bash
  sudo apt install auditd audispd-plugins -y
  sudo systemctl enable auditd
  sudo systemctl start auditd
  sudo systemctl status auditd
  ```

- Bonus check:
  ```bash
  sudo ausearch -m USER_LOGIN
  sudo aureport -au
  ```
![Auditd status](https://github.com/user-attachments/assets/ee95f86c-aac9-47c6-a7ef-1950356498aa)
- 📸 *Screenshot: `auditd` running + sample audit logs*

---

### 5️⃣ Brute-force Protection with Fail2Ban

- Installed and enabled Fail2Ban:

  ```bash
  sudo apt install fail2ban -y
  sudo systemctl enable fail2ban
  sudo systemctl start fail2ban
  ```

- Verified active SSH protection:
  ```bash
  sudo fail2ban-client status
  sudo fail2ban-client status sshd
  ```

![Fail2ban client status   (jail)](https://github.com/user-attachments/assets/cd12f300-b4e3-4380-95e4-73889d4dba83)
- 📸 *Screenshot: `fail2ban` service active + SSH jail active*

---

### 🧪 Final Audit Summary (Lynis)

- Re-ran Lynis after completing all hardening tasks

  ```bash
  sudo lynis audit system
  ```

![Lynis audit score post config](https://github.com/user-attachments/assets/e8958a93-fd39-47f7-8c3a-c942635a4123)
- 📸 *Screenshot: Final hardening index*

| Phase          | Lynis Hardening Index |
|----------------|------------------------|
| Pre-Hardening  | 65/100                 |
| Post-Hardening | 67/100                 |

**Key Improvements:**
- Disabled root login and changed SSH port
- Enabled UFW and restricted open ports
- Installed and verified audit logging
- Implemented fail2ban to block brute-force attempts

📝 While the score improvement was modest, high-impact remediations were made and are reflected in fewer critical warnings.

---

## 📸 Screenshots (Located in `/screenshots` folder)

- Lynis before/after audit output
- SSH config changes
- Firewall rule confirmation
- auditd and fail2ban service status

---

## 🧠 Takeaways

- Learned to interpret and apply Lynis recommendations
- Hardened a live Ubuntu VM using real CLI tools
- Implemented layered defenses that reflect real-world blue team practices

---

## 🔗 References

- https://cisofy.com/lynis/
- https://wiki.ubuntu.com/UncomplicatedFirewall
- https://github.com/fail2ban/fail2ban
- https://linux.die.net/man/5/sshd_config
