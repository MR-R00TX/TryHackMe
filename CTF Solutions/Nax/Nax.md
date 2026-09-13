
```
nmap -sV -sC -A 10.48.164.172                       
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-10 08:29 -0400
Nmap scan report for 10.48.164.172
Host is up (0.076s latency).
Not shown: 995 closed tcp ports (reset)
PORT    STATE SERVICE  VERSION
22/tcp  open  ssh      OpenSSH 7.2p2 Ubuntu 4ubuntu2.8 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 62:1d:d9:88:01:77:0a:52:bb:59:f9:da:c1:a6:e3:cd (RSA)
|   256 af:67:7d:24:e5:95:f4:44:72:d1:0c:39:8d:cc:21:15 (ECDSA)
|_  256 20:28:15:ef:13:c8:9f:b8:a7:0f:50:e6:2f:3b:1e:57 (ED25519)
25/tcp  open  smtp     Postfix smtpd
|_smtp-commands: ubuntu.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, STARTTLS, ENHANCEDSTATUSCODES, 8BITMIME, DSN
| ssl-cert: Subject: commonName=ubuntu
| Not valid before: 2020-03-23T23:42:04
|_Not valid after:  2030-03-21T23:42:04
|_ssl-date: TLS randomness does not represent time
80/tcp  open  http     Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
389/tcp open  ldap     OpenLDAP 2.2.X - 2.3.X
443/tcp open  ssl/http Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
| tls-alpn: 
|_  http/1.1
|_ssl-date: TLS randomness does not represent time
|_http-title: Site doesn't have a title (text/html).
| ssl-cert: Subject: commonName=192.168.85.153/organizationName=Nagios Enterprises/stateOrProvinceName=Minnesota/countryName=US
| Not valid before: 2020-03-24T00:14:58
|_Not valid after:  2030-03-22T00:14:58
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.99%E=4%D=7/10%OT=22%CT=1%CU=31194%PV=Y%DS=3%DC=T%G=Y%TM=6A50E5D
OS:4%P=x86_64-pc-linux-gnu)SEQ(SP=101%GCD=1%ISR=10E%TI=Z%CI=I%II=I%TS=8)SEQ
OS:(SP=102%GCD=1%ISR=10D%TI=Z%CI=I%II=I%TS=8)SEQ(SP=103%GCD=1%ISR=10A%TI=Z%
OS:CI=I%II=I%TS=8)SEQ(SP=104%GCD=1%ISR=105%TI=Z%CI=I%II=I%TS=8)SEQ(SP=108%G
OS:CD=1%ISR=109%TI=Z%CI=I%II=I%TS=8)OPS(O1=M4E8ST11NW7%O2=M4E8ST11NW7%O3=M4
OS:E8NNT11NW7%O4=M4E8ST11NW7%O5=M4E8ST11NW7%O6=M4E8ST11)WIN(W1=68DF%W2=68DF
OS:%W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W=6903%O=M4E8NNSNW7%C
OS:C=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%
OS:T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD
OS:=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S
OS:=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK
OS:=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 3 hops
Service Info: Host:  ubuntu.localdomain; OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 53/tcp)
HOP RTT      ADDRESS
1   74.70 ms 192.168.128.1
2   ...
3   76.23 ms 10.48.164.172

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 42.16 seconds

   
```


```

 dirsearch -u http://10.48.164.172    
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3                                                                                                                              
 (_||| _) (/_(_|| (_| )                                                                                                                                       
                                                                                                                                                              
Extensions: php, aspx, jsp, html, js | HTTP method: GET | Threads: 25 | Wordlist size: 11460

Output File: /home/kali/Desktop/Tryhackme/reports/http_10.48.164.172/_26-07-10_08-33-50.txt

Target: http://10.48.164.172/

[08:33:50] Starting:                                                                                                                                          
[08:33:57] 403 -  278B  - /.ht_wsr.txt                                      
[08:33:57] 403 -  278B  - /.htaccess.bak1                                   
[08:33:57] 403 -  278B  - /.htaccess.orig                                   
[08:33:57] 403 -  278B  - /.htaccess.sample                                 
[08:33:57] 403 -  278B  - /.htaccess.save                                   
[08:33:57] 403 -  278B  - /.htaccess_extra
[08:33:57] 403 -  278B  - /.htaccess_orig
[08:33:57] 403 -  278B  - /.htaccess_sc
[08:33:57] 403 -  278B  - /.htaccessOLD2
[08:33:57] 403 -  278B  - /.htaccessOLD
[08:33:57] 403 -  278B  - /.htaccessBAK
[08:33:57] 403 -  278B  - /.htm                                             
[08:33:57] 403 -  278B  - /.html
[08:33:57] 403 -  278B  - /.htpasswd_test                                   
[08:33:57] 403 -  278B  - /.httr-oauth
[08:33:57] 403 -  278B  - /.htpasswds                                       
[08:33:58] 403 -  278B  - /.php                                             
[08:33:58] 403 -  278B  - /.php3                                            
[08:34:13] 403 -  278B  - /cgi-bin/                                         
[08:34:23] 200 -    1KB - /index.php                                        
[08:34:23] 200 -    1KB - /index.php/login/                                 
[08:34:24] 301 -  319B  - /javascript  ->  http://10.48.164.172/javascript/ 
[08:34:29] 401 -  460B  - /nagios                                           
[08:34:29] 401 -  460B  - /nagios/                                          
[08:34:39] 403 -  278B  - /server-status                                    
[08:34:39] 403 -  278B  - /server-status/

Task Completed                                    

```




![[Pasted image 20260710211911.png]]




```
gobuster dir -u http://10.48.160.124/ -w /usr/share/wordlists/dirb/common.txt 
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.48.160.124/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
.htpasswd            (Status: 403) [Size: 278]
.hta                 (Status: 403) [Size: 278]
.htaccess            (Status: 403) [Size: 278]
cgi-bin/             (Status: 403) [Size: 278]
index.html           (Status: 200) [Size: 1332]
index.php            (Status: 200) [Size: 2968]
javascript           (Status: 301) [Size: 319] [--> http://10.48.160.124/javascript/]
nagios               (Status: 401) [Size: 460]
server-status        (Status: 403) [Size: 278]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished

```

