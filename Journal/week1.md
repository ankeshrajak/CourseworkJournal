up# Week 1: System Planning and Distribution Selection

**Phase 1** | [← Back to Index](index.md) | [Week 2 →](week2.md)

---

## Overview

This week focuses on planning the operating system deployment and making informed technical decisions about the system architecture, distribution selection, and network configuration.

---

## 1. System Architecture Diagram

### Dual-System Architecture

![System Architecture Diagram](assets/week1/architecture-diagram.png)

**Architecture Description:**
- **Workstation VM:** A Linux Desktop environment acting as the administrative console. It hosts SSH clients, monitoring tools, and terminal emulators.
- **Server VM:** A headless Ubuntu Server handling the core workloads. It is secured with UFW and accessible only via SSH.
- **Connection:** A dedicated SSH tunnel connects the workstation to the server within the virtual network.

---

## 2. Distribution Selection Justification

### Chosen Server Distribution: [Distribution Name]

**Comparison Matrix:**

| Criteria | Ubuntu Server | Debian | CentOS Stream | Rocky Linux |
|----------|---------------|--------|---------------|-------------|
| Stability | ⭐⭐⭐⭐ | ⭐⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐⭐ |
| Documentation | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |
| Community Support | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |
| Package Management | APT | APT | DNF | DNF |
| LTS Support | 5 years | Varies | Rolling | 10 years |
| Ease of Use | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ | ⭐⭐⭐ |

**Justification:**
- **Industry Standard:** Ubuntu Server is widely deployed in enterprise environments, making it a relevant choice for gaining improved employability skills.
- **Documentation & Support:** The extensive community documentation and "Ask Ubuntu" forums provide excellent troubleshooting resources for learning.
- **Hardware Compatibility:** Excellent driver support ensures smooth operation within the VirtualBox environment without complex configuration.

**Key Features:**
- **Long Term Support (LTS):** The 24.04 LTS release guarantees 5 years of security updates, ensuring system stability throughout the coursework.
- **Package Management:** The APT ecosystem offers a vast repository of pre-compiled binaries, simplifying the installation of monitoring tools and services.
- **Security Integration:** Native support for AppArmor and UFW allows for immediate implementation of mandatory access controls and firewall rules.

---

## 3. Workstation Configuration Decision

### Selected Workstation Option: [Option A/B/C]

**Available Options:**
- **Option A:** Linux Desktop VM (separate virtual machine)
- **Option B:** Host machine with SSH client
- **Option C:** Hybrid approach

**My Choice:** Option A: Linux Desktop VM

**Justification:**
- **Realistic Network Simulation:** Simulating a separate workstation creates a realistic "air-gapped" administration scenario, mimicking enterprise jump-host architectures.
- **Tool Availability:** Using a full Linux Desktop (e.g., Ubuntu Desktop or Linux Mint) provides native access to GUI-based tools (like Wireshark or browser-based dashboards) that might be cumbersome to run on a headless server.
- **Isolation:** Keeps the administration environment separate from the host OS, preventing accidental changes to the host and allowing for easy snapshot recovery.

**Configuration Details:**
- Operating System: Ubuntu Desktop 24.04 LTS
- SSH Client: OpenSSH Client (Standard)
- Additional Tools: Wireshark, Remmina, VS Code

---

## 4. Network Configuration Documentation

### VirtualBox Network Settings

**Network Mode:** [NAT Network / Host-Only / Bridged]

**Network Configuration:**
```
Server VM:
- Network Adapter: [Adapter type]
- IP Address: [Static IP]
- Subnet Mask: [Mask]
- Gateway: [Gateway IP]

Workstation VM:
- Network Adapter: [Adapter type]
- IP Address: [Static IP]
- Subnet Mask: [Mask]
- Gateway: [Gateway IP]
```

**Network Diagram:**
![Network Configuration](assets/week1/network-diagram.png)

**Configuration Steps:**
1.  **Network Setup:** Configured VirtualBox "NAT Network" (10.0.2.0/24) to allow internal communication between the Server and Workstation while enabling internet access.
2.  **Server Installation:** Installed Ubuntu Server 24.04, selecting "No" for GUI and partitioning the disk with LVM for future flexibility.
3.  **SSH Enabling:** Installed `openssh-server` during the installation wizard and verified service status post-boot with `systemctl status ssh`.

**Connectivity Testing:**
```bash
# Ping test from workstation to server
ping [server-ip]

# SSH connectivity test
ssh [username]@[server-ip]
```

---

## 5. CLI System Specifications

### Server System Specifications

**Command: `uname -a`**
```bash
[username]@[hostname]:~$ uname -a
[Output here]
```

**Command: `lsb_release -a`**
```bash
[username]@[hostname]:~$ lsb_release -a
[Output here]
```

**Command: `free -h`**
```bash
[username]@[hostname]:~$ free -h
              total        used        free      shared  buff/cache   available
Mem:          [data]       [data]      [data]    [data]    [data]       [data]
Swap:         [data]       [data]      [data]
```

**Command: `df -h`**
```bash
[username]@[hostname]:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
[Output here]
```

**Command: `ip addr`**
```bash
[username]@[hostname]:~$ ip addr
[Output here]
```

**Screenshot:**
![CLI System Specifications](assets/week1/system-specs.png)

---

## Learning Reflections

### What I Learned This Week
- **Virtual Network Management:** Gained practical experience in configuring VirtualBox NAT Networks to create isolated subnets for secure inter-VM communication.
- **Headless Administration:** Developed comfort with managing a server solely through the command line (CLI) without relying on graphical interfaces.
- **SSH Key Management:** Understood the importance of generating and securing SSH keys for authentication instead of relying on password-based logins.

### Challenges Encountered
- **Permission Denied (publickey):** Encountered initial connection refusals when setting up keys. Addressed this by correcting file permissions on the private key (`chmod 600 id_rsa`).
- **Network Isolation Issues:** Initially, the VMs could not ping each other. Addressed this by ensuring both were attached to the exact same "NAT Network" adapter name in VirtualBox settings.

### Next Steps
- Prepare for Phase 2: Security Planning and Testing Methodology
- Begin researching security hardening techniques
- Plan performance testing approach

---

## References

[1] Canonical Ltd., "Ubuntu Server Documentation," ubuntu.com, 2025. [Online]. Available: https://ubuntu.com/server/docs. [Accessed: Dec. 2025].

[2] Oracle Corporation, "Oracle VM VirtualBox User Manual," virtualbox.org, 2025. [Online]. Available: https://www.virtualbox.org/manual/. [Accessed: Dec. 2025].

---

**Week 1 Completion Date:** [Date]  
**Time Spent:** [Hours]

[← Back to Index](index.md) | [Week 2 →](week2.md)
