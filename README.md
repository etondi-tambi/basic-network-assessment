basic-network-assessment

Local vulnerability and network security assessment of an isolated Linux target using Kali Linux and Nmap.
Basic Network Security Assessment & Vulnerability Analysis

Executive Summary

This project demonstrates a local network security assessment conducted within an isolated virtual environment. Using Kali Linux as the attacking/scanning host and an intentionally vulnerable Ubuntu-based target (Metasploitable 2), the objective was to perform host discovery, port scanning, service enumeration, and vulnerability identification to determine the target's overall security posture.

---

 Lab Architecture & Infrastructure
 Hypervisor: VMware Workstation
 Attacker Node: Kali Linux 2024.x (NAT Network)
 Target Node: Metasploitable 2 / Ubuntu Linux (NAT Network)
 Networking Mode: Isolated NAT (Ensuring zero exposure to external or host networks)
 Firmware Configuration: Legacy BIOS / MBR Partitioning

---

 Methodology & Assessment Execution

 Phase 1: Host Discovery & Network Mapping
Identified live hosts within the isolated subnet range using ARP and ping sweeps.
bash
 Host discovery sweep
sudo nmap -sn 192.168.x.0/24
Target identified: 192.168.42.134
Phase 2: Port & Service Enumeration
Executed a full TCP port scan and service version detection to identify exposed entry points.

Bash
 Service version detection and default script scan
sudo nmap -sC -sV -p- -T4 192.168.x.xxx
Key Findings:
FTP (Port 21): Running vsftpd 2.3.4 (Known backdoor vulnerability).

SSH (Port 22): Open service running OpenSSH 4.7p1.

HTTP (Port 80): Running Apache httpd 2.2.8 with PHP 5.2.4.

SMB (Ports 139/445): Samba 3.X service active.

Phase 3: OS & Vulnerability Fingerprinting
Utilized OS stack fingerprinting and Nmap Scripting Engine (NSE) to verify the underlying operating system and unpatched vulnerabilities.

Bash
 OS Fingerprinting and Vulnerability Scripting
sudo nmap -O --script vuln 192.168.x.xxx
OS Confirmed: Linux 2.6.x (Ubuntu Hardy Heron 8.04).

Risk Severity: High / Critical due to outdated software packages and legacy network protocols.

Remediation & Defensive Recommendations
Patching & Upgrades: Upgrade legacy operating systems and service packages (e.g., updating Apache, OpenSSH, and vsftpd to supported versions).

Network Segmentation: Implement firewall filtering rules to restrict unnecessary exposed ports (e.g., closing unencrypted services like Telnet and FTP).

Access Controls: Disable root SSH logins and enforce key-based authentication.

Key Skills Demonstrated
Network Reconnaissance & Port Scanning (Nmap)

Vulnerability Identification & NSE Scripting

Linux System Fingerprinting & Banner Grabbing

Virtual Network Isolation & Hypervisor Management (VMware Workstation)
