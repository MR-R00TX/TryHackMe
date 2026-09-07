# TryHackMe
My solutions and write-ups for TryHackMe CTF challenges

<div align="center">

# 🦇 TryHackMe : CTF Solutions & Write-ups 🦇

<p align="center">
  <img src="https://img.shields.io/badge/Platform-TryHackMe-B91C1C?style=for-the-badge&logo=tryhackme&logoColor=white">
  <img src="https://img.shields.io/badge/OS-Kali_Linux-268BEE?style=for-the-badge&logo=kali-linux&logoColor=white">
  <img src="https://img.shields.io/badge/Focus-Cybersecurity-000000?style=for-the-badge&logo=security&logoColor=white">
</p>

*Detailed write-ups, methodologies, and complete attack chains for TryHackMe rooms.*

---
</div>

## 📜 [ 0x01 ] System Log & Overview
> **Boot Sequence:** Initiated... Connection Established... 🟢

Welcome to my TryHackMe laboratory. This repository is a structured archive of my penetration testing methodologies, CTF solutions, and exploit development notes. It demonstrates practical skills in vulnerability assessment, web exploitation, and privilege escalation across various THM environments.

---

## 🎯 [ 0x02 ] Attack Vectors & Capabilities

| Domain | Technical Focus |
| :--- | :--- |
| 🌐 **Web Exploitation** | OWASP Top 10, API testing, SQLi, LFI/RFI, and Command Injection. |
| 🖥️ **Network Security** | Port scanning, pivoting, packet analysis, and service enumeration. |
| 🔑 **Active Directory** | Kerberoasting, AS-REP Roasting, BloodHound mapping, and lateral movement. |
| 🔓 **Privilege Escalation** | Linux/Windows internal enumeration, kernel exploits, and misconfigurations. |

---

## ⚔️ [ 0x03 ] The Arsenal

```bash
root@munna:~# cat /opt/toolkit.txt

[+] Recon & Enum        : Nmap, Rustscan, Amass, Subfinder, Dirb/Gobuster
[+] Web Exploitation    : Burp Suite, Httpx, Naabu, Nuclei, SQLmap
[+] Exploitation        : Metasploit, Searchsploit, Netcat
[+] Password Cracking   : Hashcat, John The Ripper, Hydra


- [ WARNING: AUTHORIZED PERSONNEL ONLY ] -
- All methodologies, scripts, and write-ups documented here are strictly for educational purposes and authorized security research on the TryHackMe platform.
- Do not utilize these techniques on systems without explicit, mutual consent.
