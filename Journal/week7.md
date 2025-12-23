# Week 7: Security Audit and System Evaluation

**Phase 7** | [← Week 6](week6.md) | [Back to Index](index.md)

---

## Overview

This final week focuses on conducting a comprehensive security audit and evaluating the overall system configuration. The audit includes security scanning with Lynis, network security assessment with nmap, access control verification, service audit, and final system configuration review.

---

## 1. Security Audit Report

### Audit Overview

**Audit Date:** [Date]  
**Auditor:** [Your name]  
**System:** [Server details]  
**Audit Scope:** Complete security assessment of Linux server infrastructure

**Audit Components:**
1. Infrastructure security assessment
2. Lynis security scan (before and after remediation)
3. Network security testing with nmap
4. SSH security verification
5. Service inventory and justification
6. Remaining risk assessment

---

## 2. Infrastructure Security Assessment

### System Hardening Status

**Security Controls Implemented:**

| Control Category | Status | Implementation Details |
|------------------|--------|------------------------|
| SSH Hardening | ✅ Complete | Key-based auth, root login disabled, password auth disabled |
| Firewall Configuration | ✅ Complete | UFW enabled, default deny, SSH restricted to workstation |
| User Management | ✅ Complete | Non-root admin user, sudo configured, least privilege |
| Automatic Updates | ✅ Complete | Unattended-upgrades configured for security patches |
| Intrusion Detection | ✅ Complete | Fail2ban active, SSH jail enabled |
| Access Control | ✅ Complete | [SELinux/AppArmor] enabled and configured |
| Service Hardening | ✅ Complete | Unnecessary services disabled |
| File Permissions | ✅ Complete | Proper ownership and permissions set |

### Security Baseline Verification

**Running Security Baseline Script:**
```bash
adminuser@server:~$ sudo ./security-baseline.sh
======================================
  Security Baseline Verification
======================================
Generated: [timestamp]

=== SSH Security Checks ===
Checking SSH Root Login Disabled... PASS
Checking SSH Password Auth Disabled... PASS
Checking SSH Public Key Auth Enabled... PASS
Checking SSH Service Running... PASS

=== Firewall Security Checks ===
Checking UFW Enabled... PASS
Checking UFW Default Deny Incoming... PASS
Checking SSH Rule Exists... PASS

=== User Management Checks ===
Checking Admin User Exists... PASS
Checking Admin User in Sudo Group... PASS

=== Automatic Updates Checks ===
Checking Unattended Upgrades Installed... PASS
Checking Automatic Updates Enabled... PASS

=== Fail2ban Checks ===
Checking Fail2ban Installed... PASS
Checking Fail2ban Service Running... PASS
Checking Fail2ban SSH Jail Enabled... PASS

=== Mandatory Access Control Checks ===
Checking [MAC System] Loaded... PASS

======================================
  Summary
======================================
Passed: [number]
Failed: 0
Warnings: 0

✓ All security baseline checks passed!
```

**Screenshot:**
![Security Baseline Results](assets/week7/security-baseline-results.png)

---

## 3. Lynis Security Scan

### Pre-Hardening Scan (Baseline)

**Initial Lynis Scan:**
```bash
adminuser@server:~$ sudo lynis audit system

[+] Initializing program
------------------------------------
  - Detecting OS...                                           [ DONE ]
  - Checking profiles...                                      [ DONE ]

[+] System Tools
------------------------------------
  - Scanning available tools...
  - Checking system binaries...

[+] Boot and services
------------------------------------
  - Checking boot loaders...                                  [ DONE ]
  - Checking services...                                      [ DONE ]

[... full scan output ...]

  ---------------------------------------------------
  Program version:           [version]
  Operating system:          Linux
  Operating system name:     Ubuntu
  Operating system version:  [version]
  Kernel version:            [version]
  Hardware platform:         x86_64
  Hostname:                  [hostname]
  ---------------------------------------------------
  Hardening index : [XX] [############    ]
  ---------------------------------------------------
```

**Initial Hardening Index:** [XX]/100

**Key Findings (Before Hardening):**
- [Finding 1]
- [Finding 2]
- [Finding 3]
- [Finding 4]
- [Finding 5]

**Warnings Count:** [number]  
**Suggestions Count:** [number]

---

### Post-Hardening Scan (After Remediation)

**Final Lynis Scan:**
```bash
adminuser@server:~$ sudo lynis audit system

[... scan output ...]

  ---------------------------------------------------
  Hardening index : [YY] [##################  ]
  ---------------------------------------------------
```

**Final Hardening Index:** [YY]/100

**Improvements Made:**
- [Improvement 1]
- [Improvement 2]
- [Improvement 3]
- [Improvement 4]
- [Improvement 5]

**Remaining Warnings:** [number]  
**Remaining Suggestions:** [number]

---

### Lynis Score Comparison

| Category | Before | After | Improvement |
|----------|--------|-------|-------------|
| Overall Hardening Index | [XX]/100 | [YY]/100 | +[ZZ] points |
| Boot and Services | [score] | [score] | [change] |
| Kernel | [score] | [score] | [change] |
| Memory and Processes | [score] | [score] | [change] |
| Users and Authentication | [score] | [score] | [change] |
| File Systems | [score] | [score] | [change] |
| Storage | [score] | [score] | [change] |
| Networking | [score] | [score] | [change] |
| Software | [score] | [score] | [change] |

**Visualization:**
![Lynis Score Comparison](assets/week7/lynis-comparison-chart.png)

---

### Remediation Actions Taken

**Action 1: [Description]**
```bash
adminuser@server:~$ [remediation command]
```
**Result:** [What was fixed]

**Action 2: [Description]**
```bash
adminuser@server:~$ [remediation command]
```
**Result:** [What was fixed]

**Action 3: [Description]**
```bash
adminuser@server:~$ [remediation command]
```
**Result:** [What was fixed]

---

## 4. Network Security Testing

### Nmap Security Assessment

**External Port Scan (from Workstation):**
```bash
workstation$ nmap -sS -sV -O [server-ip]
Starting Nmap [version]
Nmap scan report for [server-ip]
Host is up (0.00XX s latency).
Not shown: 999 filtered ports
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH [version] (Ubuntu Linux; protocol 2.0)
OS details: Linux [version]

Nmap done: 1 IP address (1 host up) scanned in [time] seconds
```

**Findings:**
- ✅ Only SSH port (22) is open
- ✅ All other ports are filtered by firewall
- ✅ SSH version is up-to-date
- ✅ No unnecessary services exposed

**Aggressive Scan:**
```bash
workstation$ nmap -A -T4 [server-ip]
Starting Nmap [version]
Nmap scan report for [server-ip]
Host is up (0.00XX s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH [version]
| ssh-hostkey: 
|   [key details]
|_  [key details]

Service detection performed. Please report any incorrect results.
Nmap done: 1 IP address (1 host up) scanned in [time] seconds
```

**UDP Scan:**
```bash
workstation$ sudo nmap -sU --top-ports 20 [server-ip]
Starting Nmap [version]
Nmap scan report for [server-ip]
All 20 scanned ports on [server-ip] are open|filtered

Nmap done: 1 IP address (1 host up) scanned in [time] seconds
```

**Vulnerability Scan:**
```bash
workstation$ nmap --script vuln [server-ip]
Starting Nmap [version]
Nmap scan report for [server-ip]
PORT   STATE SERVICE
22/tcp open  ssh

Nmap done: 1 IP address (1 host up) scanned in [time] seconds
```

**Results:** No known vulnerabilities detected

**Screenshots:**
![Nmap Scan Results](assets/week7/nmap-scan.png)

---

### Network Security Summary

| Test Type | Result | Risk Level | Notes |
|-----------|--------|------------|-------|
| Port Scan | Only SSH open | ✅ Low | Firewall working correctly |
| Service Version | Up-to-date | ✅ Low | No known vulnerabilities |
| Vulnerability Scan | No vulns found | ✅ Low | System properly patched |
| UDP Scan | Filtered | ✅ Low | Firewall blocking UDP |
| Firewall Test | Blocking unauthorized | ✅ Low | Only workstation can connect |

---

## 5. SSH Security Verification

### SSH Configuration Audit

**SSH Configuration Review:**
```bash
adminuser@server:~$ sudo sshd -T
port 22
permitrootlogin no
pubkeyauthentication yes
passwordauthentication no
challengeresponseauthentication no
usepam yes
x11forwarding no
maxauthtries 3
clientaliveinterval 300
clientalivecountmax 2
allowusers adminuser [username]
```

**Security Checks:**

| Security Control | Status | Evidence |
|------------------|--------|----------|
| Root login disabled | ✅ Pass | `PermitRootLogin no` |
| Password auth disabled | ✅ Pass | `PasswordAuthentication no` |
| Key-based auth only | ✅ Pass | `PubkeyAuthentication yes` |
| Limited auth attempts | ✅ Pass | `MaxAuthTries 3` |
| Client timeout configured | ✅ Pass | `ClientAliveInterval 300` |
| User whitelist active | ✅ Pass | `AllowUsers` configured |
| X11 forwarding disabled | ✅ Pass | `X11Forwarding no` |

### SSH Key Security

**Key Algorithm Verification:**
```bash
adminuser@server:~$ ssh-keygen -lf ~/.ssh/authorized_keys
[key-size] SHA256:[fingerprint] [comment] (ED25519)
```

**Key Security:**
- ✅ Using ED25519 (modern, secure algorithm)
- ✅ Key size: [size] bits
- ✅ Proper file permissions (600)

### Fail2ban SSH Protection

**Fail2ban Status:**
```bash
adminuser@server:~$ sudo fail2ban-client status sshd
Status for the jail: sshd
|- Filter
|  |- Currently failed: [number]
|  |- Total failed:     [number]
|  `- File list:        /var/log/auth.log
`- Actions
   |- Currently banned: [number]
   |- Total banned:     [number]
   `- Banned IP list:   [IPs if any]
```

**Protection Status:**
- ✅ Fail2ban active and monitoring SSH
- ✅ Ban time: 3600 seconds (1 hour)
- ✅ Max retries: 3 attempts
- ✅ Find time: 600 seconds (10 minutes)

---

## 6. Service Inventory and Justification

### Running Services Audit

**List All Running Services:**
```bash
adminuser@server:~$ systemctl list-units --type=service --state=running
UNIT                               LOAD   ACTIVE SUB     DESCRIPTION
[service list]
```

### Service Justification Table

| Service Name | Purpose | Justification | Security Impact | Status |
|--------------|---------|---------------|-----------------|--------|
| sshd | Remote access | Required for administration | High - properly hardened | ✅ Keep |
| ufw | Firewall | Network security | Essential security control | ✅ Keep |
| fail2ban | Intrusion detection | Brute-force protection | Essential security control | ✅ Keep |
| unattended-upgrades | Auto updates | Security patch management | Reduces vulnerability window | ✅ Keep |
| [apparmor/selinux] | Access control | Mandatory access control | Essential security layer | ✅ Keep |
| cron | Task scheduler | Automated maintenance | Required for updates/monitoring | ✅ Keep |
| systemd-* | System services | Core OS functionality | Essential system services | ✅ Keep |
| [application 1] | [Purpose] | [Justification] | [Impact] | ✅ Keep |
| [application 2] | [Purpose] | [Justification] | [Impact] | ✅ Keep |

### Disabled/Removed Services

**Services Disabled for Security:**
```bash
adminuser@server:~$ systemctl list-unit-files --type=service --state=disabled
[List of disabled services]
```

| Service | Reason for Disabling | Security Benefit |
|---------|---------------------|------------------|
| [service 1] | [Reason] | [Benefit] |
| [service 2] | [Reason] | [Benefit] |
| [service 3] | [Reason] | [Benefit] |

---

## 7. Remaining Risk Assessment

### Identified Risks

**Risk 1: [Risk Name]**
- **Description:** [What is the risk]
- **Likelihood:** [Low/Medium/High]
- **Impact:** [Low/Medium/High]
- **Overall Risk Level:** [Low/Medium/High]
- **Mitigation Status:** [What has been done]
- **Residual Risk:** [What remains]
- **Acceptance Rationale:** [Why acceptable]

**Risk 2: [Risk Name]**
- **Description:** [What is the risk]
- **Likelihood:** [Low/Medium/High]
- **Impact:** [Low/Medium/High]
- **Overall Risk Level:** [Low/Medium/High]
- **Mitigation Status:** [What has been done]
- **Residual Risk:** [What remains]
- **Acceptance Rationale:** [Why acceptable]

**Risk 3: [Risk Name]**
- **Description:** [What is the risk]
- **Likelihood:** [Low/Medium/High]
- **Impact:** [Low/Medium/High]
- **Overall Risk Level:** [Low/Medium/High]
- **Mitigation Status:** [What has been done]
- **Residual Risk:** [What remains]
- **Acceptance Rationale:** [Why acceptable]

### Risk Matrix

| Risk | Likelihood | Impact | Risk Level | Mitigation | Residual Risk |
|------|------------|--------|------------|------------|---------------|
| [Risk 1] | [L/M/H] | [L/M/H] | [L/M/H] | [Status] | [L/M/H] |
| [Risk 2] | [L/M/H] | [L/M/H] | [L/M/H] | [Status] | [L/M/H] |
| [Risk 3] | [L/M/H] | [L/M/H] | [L/M/H] | [Status] | [L/M/H] |

---

## Final System Evaluation

### Security Posture Summary

**Overall Security Rating:** [Excellent/Good/Fair/Poor]

**Strengths:**
- ✅ [Strength 1]
- ✅ [Strength 2]
- ✅ [Strength 3]
- ✅ [Strength 4]
- ✅ [Strength 5]

**Areas for Improvement:**
- ⚠️ [Area 1]
- ⚠️ [Area 2]
- ⚠️ [Area 3]

### Performance vs Security Trade-offs

**Trade-off Analysis:**

1. **Firewall Restrictiveness**
   - Security benefit: Minimal attack surface
   - Performance impact: Negligible
   - Decision: Optimal balance achieved

2. **Mandatory Access Control**
   - Security benefit: Additional security layer
   - Performance impact: [X]% overhead
   - Decision: [Justification]

3. **Automatic Updates**
   - Security benefit: Timely patching
   - Performance impact: Potential unexpected reboots
   - Decision: Configured for security updates only, no auto-reboot

### System Configuration Summary

**Final Configuration:**
- Operating System: [Ubuntu Server version]
- Kernel: [version]
- Security Controls: 6 major controls implemented
- Lynis Score: [score]/100
- Open Ports: 1 (SSH only)
- Running Services: [number] (all justified)
- Uptime: [uptime]

---

## Compliance and Best Practices

### Industry Standards Alignment

**CIS Benchmark Compliance:**
- [X] Level 1 controls: [percentage]% implemented
- [X] Level 2 controls: [percentage]% implemented

**NIST Cybersecurity Framework:**
- ✅ Identify: Asset inventory complete
- ✅ Protect: Security controls implemented
- ✅ Detect: Monitoring and IDS active
- ✅ Respond: Incident response capability
- ✅ Recover: Backup and recovery plan

---

## Learning Reflections

### What I Learned This Week
- [Key learning about security auditing]
- [Key learning about risk assessment]
- [Key learning about compliance]

### Challenges Encountered
- [Challenge 1 and solution]
- [Challenge 2 and solution]

### Overall Coursework Insights
- [Major insight about Linux administration]
- [Major insight about security implementation]
- [Major insight about performance optimization]
- [Major insight about system design trade-offs]

### Skills Developed
1. **Command-Line Proficiency:** [Description]
2. **Security Implementation:** [Description]
3. **Performance Analysis:** [Description]
4. **Automation Scripting:** [Description]
5. **Technical Documentation:** [Description]

---

## Project Conclusion

### Achievements

**Technical Accomplishments:**
- ✅ Deployed and configured headless Linux server
- ✅ Implemented 6 major security controls
- ✅ Achieved Lynis score of [score]/100
- ✅ Created 2 automation scripts
- ✅ Conducted comprehensive performance testing
- ✅ Optimized system performance by [X]%
- ✅ Completed full security audit

**Learning Outcomes Met:**
- ✅ LO3: Security vulnerabilities and protection mechanisms
- ✅ LO4: Command-line proficiency for system management
- ✅ LO5: Critical evaluation of OS design trade-offs

**Employability Skills:**
- ✅ Linux server administration
- ✅ SSH and remote system management
- ✅ Security hardening and compliance
- ✅ Performance monitoring and optimization
- ✅ Bash scripting and automation
- ✅ Technical documentation

### Future Recommendations

**For Production Deployment:**
1. [Recommendation 1]
2. [Recommendation 2]
3. [Recommendation 3]

**For Further Learning:**
1. [Learning area 1]
2. [Learning area 2]
3. [Learning area 3]

---

## References

[1] [Reference in IEEE format]

[2] [Reference in IEEE format]

[3] [Reference in IEEE format]

[4] [Reference in IEEE format]

[5] [Reference in IEEE format]

---

## Appendices

### Appendix A: Complete Configuration Files
- [Link to SSH config]
- [Link to firewall rules]
- [Link to security scripts]

### Appendix B: Performance Data
- [Link to raw performance data]
- [Link to monitoring logs]

### Appendix C: Security Scan Reports
- [Link to full Lynis report]
- [Link to nmap scan results]

---

**Week 7 Completion Date:** [Date]  
**Time Spent:** [Hours]  
**Total Coursework Time:** [Total hours]

**Project Status:** ✅ **COMPLETE**

[← Week 6](week6.md) | [Back to Index](index.md)

---

**End of Technical Journal**
