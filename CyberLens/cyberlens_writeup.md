# 🔐 Penetration Testing Report: LupinOne

**Client:** LupinOne  
**Target IP:** 192.168.0.105  
**Test Type:** Internal Network Penetration Test  
**Date:** October 2026  
**Tester:** MR-R00TX  
**Classification:** CONFIDENTIAL

---

## 📋 Executive Summary

A comprehensive penetration test was conducted against the LupinOne system (192.168.0.105). The assessment successfully identified and exploited multiple critical vulnerabilities, resulting in full system compromise (root access). The attack chain leveraged exposed SSH keys, weak credential security, misconfigured file permissions, and excessive sudo privileges.

**Overall Risk Rating:** 🔴 **CRITICAL**  
**Recommended Action:** Immediate remediation required.

---

## 🔍 1. Reconnaissance & Enumeration

### 1.1 Nmap Full Port Scan

```bash
nmap -sV -sC -p- 192.168.0.105
