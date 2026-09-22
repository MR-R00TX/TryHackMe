![[Pasted image 20260622235034.png]]

![[Pasted image 20260622235112.png]]

```
exiftool pepper_1611998632625.jpg 
ExifTool Version Number         : 13.50
File Name                       : pepper_1611998632625.jpg
Directory                       : .
File Size                       : 390 kB
File Modification Date/Time     : 2026:06:22 13:46:32-04:00
File Access Date/Time           : 2026:06:22 13:47:12-04:00
File Inode Change Date/Time     : 2026:06:22 13:48:11-04:00
File Permissions                : -rwxrwx---
File Type                       : JPEG
File Type Extension             : jpg
MIME Type                       : image/jpeg
XMP Toolkit                     : Image::ExifTool 12.16
Subject                         : https://gchq.github.io/CyberChef/#recipe=To_Hex('None',0)To_Base85('!-u',false)
Image Width                     : 2551
Image Height                    : 1913
Encoding Process                : Baseline DCT, Huffman coding
Bits Per Sample                 : 8
Color Components                : 3
Y Cb Cr Sub Sampling            : YCbCr4:2:0 (2 2)
Image Size                      : 2551x1913
Megapixels                      : 4.9

```


```
steghide extract -sf pepper_1611998632625.jpg 
Enter passphrase: 
steghide: could not extract any data with that passphrase!
  
```

```
apt install stegcracker
Installing:                     
  stegcracker
   
Summary:
  Upgrading: 0, Installing: 1, Removing: 0, Not Upgrading: 1385
  Download size: 12.0 kB
  Space needed: 51.2 kB / 35.5 GB available

Get:1 http://kali.download/kali kali-rolling/main amd64 stegcracker all 2.1.0-5 [12.0 kB]
Fetched 12.0 kB in 23s (528 B/s)        
Selecting previously unselected package stegcracker.
(Reading database… 478564 files and directories currently installed.)
Preparing to unpack …/stegcracker_2.1.0-5_all.deb…
Unpacking stegcracker (2.1.0-5)…
Setting up stegcracker (2.1.0-5)…
Processing triggers for man-db (2.13.1-1)…
Processing triggers for kali-menu (2026.2.2)…

```

```
stegcracker pepper_1611998632625.jpg /usr/share/wordlists/rockyou.txt
StegCracker 2.1.0 - (https://github.com/Paradoxis/StegCracker)
Copyright (c) 2026 - Luke Paris (Paradoxis)

StegCracker has been retired following the release of StegSeek, which 
will blast through the rockyou.txt wordlist within 1.9 second as opposed 
to StegCracker which takes ~5 hours.

StegSeek can be found at: https://github.com/RickdeJager/stegseek

Counting lines in wordlist..
Attacking file 'pepper_1611998632625.jpg' with wordlist '/usr/share/wordlists/rockyou.txt'..
Successfully cracked file with password: pepper
Tried 1009 passwords
Your file has been written to: pepper_1611998632625.jpg.out
pepper

```

```
steghide extract -sf pepper_1611998632625.jpg                        
Enter passphrase: 
wrote extracted data to "lone".
```

```
cat lone          
H4sIAAAAAAAAA+3Vya6zyBUA4H/NU9w9ilxMBha9KObZDMY2bCIGG2MmMw9P39c3idRZtJJNK4rE
J6FT0imkoupQp2zq+9/z9NdfCXyjafoTMZoCf4wfBEnQvzASAJKkAX7EfgEMo2jw6wv8pav6p7Ef
ou7r69e7aVKQ/fm8/5T/P/W3D06UVevrZIuW5ylftqte4Fn80sXgJ4vEBFfGtbVFPNaFt2JIXyL8
4GRqiiv/MxTjih1DB/4L93mk+TNMtwTPhqRGrOdPav5++TPRESFJ1ZenOJwJutdri7sq+CXob/EL
MhPUmTsglUeXSeBo5bLs9C5nDNqMBNpIE+gmnwBsxHPDGMFz4ai7SgmsvsWNPJ4FOMqhM/otyliH
J1c9oim/K4aSFa7FdUDstCNASlyCiXA9voVmfuQzj019mi/O0WCK6fJMiw3I/sOG5UN1n4oyOJFT
O/Rcu0Mqv1RbZw8eZto9omonQ8A9mrUWj56ycWZo8w2S2n0JURnxiSsC0fAnQ9CdNCyvcQQK6WAn
eVvUhRC0eBUXvJsixOt6w/1qAdfBxmf+yXLOoV+Xsybc6mPFi31jqYeuMfSVw0a56g9vKecWD7Rp
HkJ4OvLruVhl5BnOMcbplf/ZeebprXXL+v37ODl/PImfg+CgI7yq9Cp6mP0Y5zYBUvAIL/mSjogp
rAzsFvqcpegIb+cGV4OQX0RxBDWXVfT0oM2AdvjMPb3mIVdEpSRfhQ06a8wiyjR5Mix5CvE6eiZQ
UQ7ZFtXIpL/z37shT47X1513C3xutuK2OL041IDGFV1wQxKaafXYq4SfbSd0GYa/MMhTFpM7xr35
VJj4VMZAZGZMR7CGP6NzVpC9HRoTICRjRHla2Pq1dtdUNq320miLeHacwWN6E3lzWHUJh85zbgy7
6q13d6y8i8LR0STiboWP0IsVNwKHGOoKkAR0MySzsO6PNlC9NQMvdMz6DlGVKxlFG1pcVUUyvDeu
FRDSjaGdzmok1dzki214/vdK59ARED4ubo92a7nXAEuk37Zu4EzGSKfb8wTl1xltpoJXqmO/rvm6
JJFNhRtBfZcbnYpKbKWkeNZEIT1Lgfu++TEL5NxHejl4a8G11qbyVnUqIbDtaZvaLKjR5WZFYcpe
UOo8q/b3B3P4ukhG7kji+IKR63f4NbDrkGh8hA+dE31v2nvmSBUl3YwVbCW4l7AQc6Hr3h7FW9xY
TzhL14ppSJytihxOYKYVB6ZwB55PAstBrlAWjTSHDpvT1sEzX1AL4AU34SuOtzc16oJvLTEBa4bq
/Kuu3PoSnoUnTkWxGoBIDhXDphaE/K7xvrJtY5HP7Q1j+epIDcXM5C/zCE0WXcmz9cJzQi6dzz0D
M0ewUPyYl8Kgq1VncxMKiwwZXr1uGABQrmEPugPLug0ermZji6HrG90kQTqWUVCBfm36AE0idYOX
xDqWtdRw3XYOcWKcV+TCgbB3jQObdOss1ewCRdab4vrILzIXOJfTcbnwb1TO1ZsTKu+A5s0Ll0Lr
eRC1Sn7w2iGT4xWpxoEeT9fqkWufNasiZKOCjSY6GOurUQvvY7j6j8iFTeLZy/BdLAz6OlZoNgf9
gE5MYmi4pyHp2IIh2+gtYmar8y0iu8FM2DLy0nO+bnhETmJPTKiy1hcp75op3VPVZhYa2KMhg7Gy
/YI7AMQDjunX2HEivcOjVrIwoHRB90ry6XZ3Kl67PrrooCnHXO+b0SU/Fz7PwRMYIa5OZeQn3r3j
EXAyC9NgCzmE9AgpXNFdNhQPHKm4rOPoFtmHaHayH7mTjHoQCd2jcvm7kabdoI5lG5BRdUlcpF6I
Efe4hdXN49hCfGaAX7ZazHCX1SS9PvEbJa3iNmGvC/VAa5mCMSPadgsky+62jtNsqgIISRSJkRp3
RpsO4vnx8xPyBEfFMjs6yj8idFSBg77Mzb/9hvy0N9ES/rz1/a/b82632+12u91ut9vtdrvdbrfb
7Xa73W632+12/5XfActiLj0AKAAA
     
```


```
 file lone
lone: ASCII text

```

```
 base64 -d lone > lone1 
```

```
tar -xvf lone1                                   
lone_id
```

```
cat lone_id                              
-----BEGIN OPENSSH PRIVATE KEY-----
b3BlbnNzaC1rZXktdjEAAAAABG5vbmUAAAAEbm9uZQAAAAAAAAABAAABFwAAAAdzc2gtcn
NhAAAAAwEAAQAAAQEA45nVhEtT37sKnNBWH2VYsXbjA8vAK8e04HfrgF06NiGGQsRBLtJw
YJu73+zGO0AoETo8LYhxB5eI5D9KzboGuTDAuGZQuUq+8N/hBmfavieHLHgkRNBr0ErJ60
l2FAcDW6pDowfiwC1vsdixQ6L8kvVhdkz0GUfPAlfIRhHHtQaQnQ7wnRtdGjIPK9/S1MPs
IJOLD2S79NxS7vguw87Mp0cnRjDalaCcRE0ELUvLDKQdZlWba0kF/PciqknkDYq2mbkCRd
3jWX2Umx0WtP2wCh9BQ/syxTJDXn6mCEsoNI/roLKyB1uGms/pFiBxS0qdiZAAO6CyTkyG
hZwb1BKmUwAAA8hSynq9Usp6vQAAAAdzc2gtcnNhAAABAQDjmdWES1Pfuwqc0FYfZVixdu
MDy8Arx7Tgd+uAXTo2IYZCxEEu0nBgm7vf7MY7QCgROjwtiHEHl4jkP0rNuga5MMC4ZlC5
Sr7w3+EGZ9q+J4cseCRE0GvQSsnrSXYUBwNbqkOjB+LALW+x2LFDovyS9WF2TPQZR88CV8
hGEce1BpCdDvCdG10aMg8r39LUw+wgk4sPZLv03FLu+C7DzsynRydGMNqVoJxETQQtS8sM
pB1mVZtrSQX89yKqSeQNiraZuQJF3eNZfZSbHRa0/bAKH0FD+zLFMkNefqYISyg0j+ugsr
IHW4aaz+kWIHFLSp2JkAA7oLJOTIaFnBvUEqZTAAAAAwEAAQAAAQB+u03U2EzfqzqBjtAl
szzrtBM8LdvXhOAGjT+ovkCHm6syyiyxcaP5Zz35tdG7dEHbNd4ETJEDdTFYRpXUb90GiU
sGYpJYWnJvlXmrI3D9qOzvqgYn+xXNaZd9V+5TwIPyKqB2yxFLiQFEujAaRUr2WYPnZ3oU
CZQO7eoqegQFm5FXLy0zl0elAkEiDrrpS5CNBunv297nHMLFBPIEB231MNbYMDe0SU40NQ
WAGELdiAQ9i7N/SMjAJYAV2MAjbbzp5uKDUNxb3An85rUWKHXslATDh25abIY0aGZHLP5x
4B1usmPPLxGTqX19Cm65tkw8ijM6AM9+y4TNj2i3GlQBAAAAgQDN+26ilDtKImrPBv+Akg
tjsKLL005RLPtKQAlnqYfRJP1xLKKz7ocYdulaYm0syosY+caIzAVcN6lnFoBrzTZ23uwy
VB0ZsRL/9crywFn9xAE9Svbn6CxGBYQVO6xVCp+GiIXQZHpY7CMVBdANh/EJmGfCJ/gGby
mut7uOWmfiJAAAAIEA9ak9av7YunWLnDp6ZyUfaRAocSPxt2Ez8+j6m+gwYst+v8cLJ2SJ
duq0tgz7za8wNrUN3gXAgDzg4VsBUKLS3i41h1DmgqUE5SWgHrhIJw9AL1fo4YumPUkB/0
S0QMUn16v4S/fnHgZY5KDKSl4hRre5byrsaVK0oluiKsouR4EAAACBAO0uA2IvlaUcSerC
0OMkML9kGZA7uA52HKR9ZE/B4HR9QQKN4sZ+gOPfiQcuKYaDrfmRCeLddrtIulqY4amVcR
nx3u2SBx9KM6uqA2w80UlqJb8BVyM4SscUoHdmbqc9Wx5f+nG5Ab8EPPq0FNPrzrBJP5m0
43kcLdLe8Jv/ETfTAAAAC3B5bG9uQHB5bG9uAQIDBAUGBw==
-----END OPENSSH PRIVATE KEY-----

```


```
rustscan -a 10.48.189.2  
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
😵 https://admin.tryhackme.com

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.48.189.2:22
Open 10.48.189.2:222
[~] Starting Script(s)
[~] Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-22 14:05 -0400
Initiating Ping Scan at 14:05
Scanning 10.48.189.2 [4 ports]
Completed Ping Scan at 14:05, 0.11s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 14:05
Completed Parallel DNS resolution of 1 host. at 14:05, 0.50s elapsed
DNS resolution of 1 IPs took 0.50s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 14:05
Scanning 10.48.189.2 [2 ports]
Discovered open port 22/tcp on 10.48.189.2
Discovered open port 222/tcp on 10.48.189.2
Completed SYN Stealth Scan at 14:05, 1.13s elapsed (2 total ports)
Nmap scan report for 10.48.189.2
Host is up, received echo-reply ttl 62 (0.20s latency).
Scanned at 2026-06-22 14:05:55 EDT for 1s

PORT    STATE SERVICE REASON
22/tcp  open  ssh     syn-ack ttl 62
222/tcp open  rsh-spx syn-ack ttl 61

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 1.96 seconds
      Raw packets sent: 6 (240B) | Rcvd: 13 (516B)


```

```
nmap -sV -sS -p 22,222 10.48.189.2 
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-22 14:07 -0400
Nmap scan report for 10.48.189.2
Host is up (0.074s latency).

PORT    STATE SERVICE VERSION
22/tcp  open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
222/tcp open  ssh     OpenSSH 8.4 (protocol 2.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 3.37 seconds
    
```

```
               
                  /               
      __         /       __    __
    /   ) /   / /      /   ) /   )
   /___/ (___/ /____/ (___/ /   /
  /         /                     
 /      (_ /  pyLon Password Manager
                   by LeonM

  
        [1] Decrypt a password.
        [2] Create new password.
        [3] Delete a password.
        [4] Search passwords.
        

Select an option [Q] to Quit: 
```

use 4 & use 1 ,2

```
                  /               
      __         /       __    __
    /   ) /   / /      /   ) /   )
   /___/ (___/ /____/ (___/ /   /
  /         /                     
 /      (_ /  pyLon Password Manager
                   by LeonM

    Password for pylon.thm

        Username = lone
        Password = +2BRkRuE!w7>ozQ4            

Press ENTER to continue.

```

```
ssh lone@10.48.189.2
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
lone@10.48.189.2's password: 
Welcome to
                   /
       __         /       __    __
     /   ) /   / /      /   ) /   )
    /___/ (___/ /____/ (___/ /   /
   /         /
  /      (_ /       by LeonM

lone@pylon:~$ 

```



