# Operating Systems Coursework - Technical Journal

**Student ID:** [Your Student ID]  
**Module:** CMPN202 - Operating Systems  
**Academic Year:** 2025/2026

---

## Project Overview

This technical journal documents my journey through a comprehensive Linux server administration project spanning 7 weeks. The coursework focuses on configuring, securing, and evaluating the performance of a Linux operating system in a dual-system architecture where a headless server is administered remotely via SSH from a workstation.

### Learning Objectives

- Deploy and manage Linux server infrastructure
- Implement security controls and hardening measures
- Develop command-line proficiency for system administration
- Analyze operating system performance under different workloads
- Create automation scripts for monitoring and security verification

### System Architecture

This project implements a dual-system architecture:
- **Server System:** Headless Linux server (Ubuntu Server) accessible only via SSH
- **Workstation System:** Administrative access point with SSH client
- **Network:** Isolated VirtualBox network with firewall-controlled access

---

## Weekly Progress

### [Week 1: System Planning and Distribution Selection](week1.md)
**Phase 1** - Planning the operating system deployment and justifying technical decisions.

**Key Deliverables:**
- System architecture diagram
- Distribution selection justification
- Network configuration documentation
- CLI system specifications

---

### [Week 2: Security Planning and Testing Methodology](week2.md)
**Phase 2** - Designing security baseline and performance testing methodology.

**Key Deliverables:**
- Performance testing plan
- Security configuration checklist
- Threat model with mitigation strategies

---

### [Week 3: Application Selection for Performance Testing](week3.md)
**Phase 3** - Selecting applications representing different workload types for performance evaluation.

**Key Deliverables:**
- Application selection matrix
- Installation documentation
- Expected resource profiles
- Monitoring strategy

---

### [Week 4: Initial System Configuration & Security Implementation](week4.md)
**Phase 4** - Deploying the server and implementing foundational security controls.

**Key Deliverables:**
- SSH key-based authentication configuration
- Firewall configuration
- User and privilege management
- Configuration file comparisons

---

### [Week 5: Advanced Security and Monitoring Infrastructure](week5.md)
**Phase 5** - Implementing advanced security controls and developing monitoring capabilities.

**Key Deliverables:**
- Access control implementation (SELinux/AppArmor)
- Automatic security updates
- Fail2ban configuration
- Security baseline verification script
- Remote monitoring script

---

### [Week 6: Performance Evaluation and Analysis](week6.md)
**Phase 6** - Executing detailed performance testing and analyzing OS behavior under different workloads.

**Key Deliverables:**
- Performance testing approach
- Performance data tables and visualizations
- Network performance analysis
- Optimization results

---

### [Week 7: Security Audit and System Evaluation](week7.md)
**Phase 7** - Conducting comprehensive security audit and evaluating overall system configuration.

**Key Deliverables:**
- Security audit report
- Lynis security scores
- Network security testing results
- Service inventory and risk assessment

---

## Key Technologies and Tools

- **Operating System:** Ubuntu Server (headless)
- **Virtualization:** VirtualBox
- **Security Tools:** SSH, UFW/iptables, SELinux/AppArmor, fail2ban, Lynis, nmap
- **Monitoring Tools:** htop, vmstat, iostat, iftop, custom bash scripts
- **Version Control:** Git and GitHub Pages

---

## Project Timeline

| Week | Phase | Focus Area |
|------|-------|------------|
| 1 | Planning | System architecture and distribution selection |
| 2 | Planning | Security and testing methodology |
| 3 | Planning | Application selection for testing |
| 4 | Implementation | Initial security configuration |
| 5 | Implementation | Advanced security and monitoring |
| 6 | Testing | Performance evaluation and analysis |
| 7 | Audit | Security audit and system evaluation |

---

## References

All references follow IEEE citation style and are documented at the end of each weekly page.

---

**Last Updated:** [Date]
