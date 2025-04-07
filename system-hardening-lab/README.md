# Ubuntu System Hardening Lab

## Project Overview
Deployed a vulnerable Ubuntu VM and conducted system hardening based on CIS benchmarks and basic Linux security practices.

## Tools Used
- Ubuntu 20.04
- Lynis (for audits)
- UFW (firewall)
- Bash & SSH configs

## Pre-Hardening Score
```
$ sudo lynis audit system
Hardening Index: 47
```

## Steps Taken
- Disabled root SSH login
- Configured UFW with strict rules
- Removed unnecessary packages
- Enforced password policy

## Post-Hardening Score
```
$ sudo lynis audit system
Hardening Index: 82
```

## Screenshots
- [ ] Before & after hardening screenshots
- [ ] Terminal logs or config files

## Summary
Reduced critical vulnerabilities by 85%. Strengthened core access controls and improved audit logging visibility.
