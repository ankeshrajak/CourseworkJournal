# Week 2: Security Planning and Testing Methodology

**Phase 2** | [← Week 1](week1.md) | [Back to Index](index.md) | [Week 3 →](week3.md)

---

## Overview

This week focuses on designing a comprehensive security baseline and establishing a robust performance testing methodology for the Linux server system.

---

## 1. Performance Testing Plan

### Testing Objectives
- Establish baseline performance metrics
- Evaluate system behavior under different workloads
- Identify performance bottlenecks
- Measure optimization improvements

### Remote Monitoring Methodology

**Monitoring Approach:**
- All monitoring performed via SSH from workstation
- Automated data collection using custom scripts
- Real-time and historical performance tracking

**Key Metrics to Monitor:**
1. **CPU Usage** - Processor utilization and load averages
2. **Memory Usage** - RAM consumption and swap usage
3. **Disk I/O** - Read/write operations and throughput
4. **Network Performance** - Bandwidth, latency, and packet loss
5. **System Latency** - Response times for various operations
6. **Service Response Times** - Application-specific performance

**Monitoring Tools:**
```bash
# CPU monitoring
top, htop, mpstat, uptime

# Memory monitoring
free, vmstat, /proc/meminfo

# Disk I/O monitoring
iostat, iotop, df, du

# Network monitoring
iftop, nethogs, ss, netstat, ping

# System monitoring
dmesg, journalctl, systemctl status
```

### Testing Schedule

| Week | Testing Phase | Focus |
|------|---------------|-------|
| 3 | Baseline | Initial system performance |
| 4 | Post-Security | Impact of security controls |
| 5 | Advanced Security | Impact of additional hardening |
| 6 | Application Load | Performance under workloads |
| 6 | Optimization | Post-optimization improvements |

---

## 2. Security Configuration Checklist

### SSH Hardening
- [ ] Disable root login via SSH
- [ ] Implement key-based authentication
- [ ] Disable password authentication
- [ ] Change default SSH port (optional)
- [ ] Configure SSH timeout settings
- [ ] Limit SSH access to specific users
- [ ] Enable SSH protocol 2 only
- [ ] Configure fail2ban for SSH protection

**Configuration File:** `/etc/ssh/sshd_config`

**Key Settings:**
```bash
PermitRootLogin no
PubkeyAuthentication yes
PasswordAuthentication no
ChallengeResponseAuthentication no
UsePAM yes
X11Forwarding no
MaxAuthTries 3
ClientAliveInterval 300
ClientAliveCountMax 2
```

---

### Firewall Configuration
- [ ] Install and enable UFW/iptables
- [ ] Default deny all incoming traffic
- [ ] Allow SSH from workstation IP only
- [ ] Configure rate limiting for SSH
- [ ] Document all firewall rules
- [ ] Test firewall effectiveness

**Firewall Rules:**
```bash
# Default policies
ufw default deny incoming
ufw default allow outgoing

# Allow SSH from workstation only
ufw allow from [workstation-ip] to any port 22

# Enable firewall
ufw enable
```

---

### Mandatory Access Control
- [ ] Choose MAC system (SELinux or AppArmor)
- [ ] Enable and configure MAC
- [ ] Create custom policies if needed
- [ ] Monitor MAC denials
- [ ] Document MAC configuration

**Selected MAC System:** [SELinux / AppArmor]

**Justification:** [Your reasoning]

---

### Automatic Updates
- [ ] Configure unattended-upgrades
- [ ] Enable automatic security updates
- [ ] Configure update notifications
- [ ] Set update schedule
- [ ] Test update mechanism

**Configuration File:** `/etc/apt/apt.conf.d/50unattended-upgrades`

---

### User Privilege Management
- [ ] Create non-root administrative user
- [ ] Configure sudo access
- [ ] Implement principle of least privilege
- [ ] Disable unnecessary user accounts
- [ ] Set strong password policies
- [ ] Configure account lockout policies

**Sudo Configuration:**
```bash
# /etc/sudoers.d/admin-user
[username] ALL=(ALL:ALL) ALL
```

---

### Network Security
- [ ] Disable IPv6 if not needed
- [ ] Configure TCP wrappers
- [ ] Disable unnecessary network services
- [ ] Configure network time synchronization
- [ ] Enable SYN flood protection
- [ ] Configure ICMP settings

---

## 3. Threat Model

### Threat 1: Unauthorized SSH Access

**Threat Description:**
Attackers attempting to gain unauthorized access to the server through SSH by exploiting weak authentication or brute-force attacks.

**Attack Vectors:**
- Brute-force password attacks
- Exploitation of weak passwords
- Stolen credentials
- Man-in-the-middle attacks

**Impact:**
- **Confidentiality:** High - Full system access
- **Integrity:** High - Ability to modify system
- **Availability:** High - Potential for system disruption

**Likelihood:** Medium-High (SSH is commonly targeted)

**Mitigation Strategies:**
1. **Key-based authentication only** - Eliminate password-based attacks
2. **Firewall restrictions** - Limit SSH access to workstation IP only
3. **Fail2ban implementation** - Automatic blocking of brute-force attempts
4. **SSH hardening** - Disable root login, limit authentication attempts
5. **Regular monitoring** - Monitor auth logs for suspicious activity

**Residual Risk:** Low (after mitigations)

---

### Threat 2: Privilege Escalation

**Threat Description:**
An attacker with limited access attempts to gain elevated privileges to compromise the entire system.

**Attack Vectors:**
- Exploitation of sudo misconfigurations
- Kernel vulnerabilities
- SUID/SGID binary exploitation
- Container escape (if using containers)

**Impact:**
- **Confidentiality:** Critical - Access to all system data
- **Integrity:** Critical - Complete system control
- **Availability:** Critical - Ability to disable system

**Likelihood:** Medium (depends on system configuration)

**Mitigation Strategies:**
1. **Principle of least privilege** - Minimal sudo permissions
2. **Automatic security updates** - Patch kernel vulnerabilities
3. **Mandatory Access Control** - SELinux/AppArmor policies
4. **Regular security audits** - Identify misconfigurations
5. **File permission monitoring** - Track SUID/SGID files

**Residual Risk:** Low-Medium (after mitigations)

---

### Threat 3: Denial of Service (DoS)

**Threat Description:**
Attackers attempting to overwhelm the server's resources, making it unavailable for legitimate use.

**Attack Vectors:**
- Network flooding (SYN flood, UDP flood)
- Resource exhaustion attacks
- Application-layer attacks
- Fork bomb or process exhaustion

**Impact:**
- **Confidentiality:** Low - No data breach
- **Integrity:** Low - No data modification
- **Availability:** Critical - System becomes unavailable

**Likelihood:** Medium (common attack type)

**Mitigation Strategies:**
1. **Firewall rate limiting** - Limit connection rates
2. **SYN flood protection** - Kernel-level protections
3. **Resource limits** - ulimit and cgroups configuration
4. **Fail2ban** - Block repeated connection attempts
5. **Network monitoring** - Detect unusual traffic patterns
6. **Service hardening** - Configure service-specific limits

**Residual Risk:** Medium (some DoS attacks are difficult to prevent)

---

## Testing Methodology Validation

### Security Testing Approach
1. **Baseline Security Scan** - Run Lynis before hardening
2. **Incremental Hardening** - Implement controls one at a time
3. **Validation Testing** - Verify each control works as expected
4. **Post-Hardening Scan** - Run Lynis after all controls implemented
5. **Penetration Testing** - Attempt to bypass controls from workstation

### Performance Impact Testing
1. **Baseline Performance** - Measure before security controls
2. **Post-Security Performance** - Measure after each security control
3. **Analysis** - Quantify performance impact of security measures
4. **Optimization** - Balance security and performance

---

## Learning Reflections

### What I Learned This Week
- [Key learning point 1]
- [Key learning point 2]
- [Key learning point 3]

### Challenges Encountered
- [Challenge 1 and solution]
- [Challenge 2 and solution]

### Security Insights
- [Insight about security trade-offs]
- [Insight about threat modeling]

### Next Steps
- Begin application selection for performance testing
- Research different workload types
- Prepare installation documentation

---

## References

[1] [Reference in IEEE format]

[2] [Reference in IEEE format]

[3] [Reference in IEEE format]

---

**Week 2 Completion Date:** [Date]  
**Time Spent:** [Hours]

[← Week 1](week1.md) | [Back to Index](index.md) | [Week 3 →](week3.md)
