
***Step1:Reconnaissance***

***Try  to  Nmap Scan***


```
nmap  -sS -p-  -sV 10.49.143.16
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-17 06:48 -0400
Nmap scan report for 10.49.143.16
Host is up (0.079s latency).
Not shown: 65534 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 208.43 seconds

```


And nmap scan to not find the terget

```
rustscan -a 10.49.143.16 -b 1000 -t 2000 -- -sV
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
0day was here ♥

[~] The config file is expected to be at "/root/.rustscan.toml"
[~] File limit higher than batch size. Can increase speed by increasing batch size '-b 924'.
Open 10.49.143.16:22
Open 10.49.143.16:7777
[~] Starting Script(s)
[>] Running script "nmap -vvv -p {{port}} -{{ipversion}} {{ip}} -sV" on ip 10.49.143.16
Depending on the complexity of the script, results may take some time to appear.
[~] Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-17 06:57 -0400
NSE: Loaded 48 scripts for scanning.
Initiating Ping Scan at 06:57
Scanning 10.49.143.16 [4 ports]
Completed Ping Scan at 06:57, 0.09s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 06:57
Completed Parallel DNS resolution of 1 host. at 06:57, 0.50s elapsed
DNS resolution of 1 IPs took 0.50s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 06:57
Scanning 10.49.143.16 [2 ports]
Discovered open port 22/tcp on 10.49.143.16
Discovered open port 7777/tcp on 10.49.143.16
Completed SYN Stealth Scan at 06:57, 0.09s elapsed (2 total ports)
Initiating Service scan at 06:57
Scanning 2 services on 10.49.143.16
Completed Service scan at 06:57, 16.73s elapsed (2 services on 1 host)
NSE: Script scanning 10.49.143.16.
NSE: Starting runlevel 1 (of 2) scan.
Initiating NSE at 06:57
Completed NSE at 06:57, 0.40s elapsed
NSE: Starting runlevel 2 (of 2) scan.
Initiating NSE at 06:57
Completed NSE at 06:57, 0.32s elapsed
Nmap scan report for 10.49.143.16
Host is up, received echo-reply ttl 62 (0.078s latency).
Scanned at 2026-06-17 06:57:19 EDT for 17s

PORT     STATE SERVICE REASON         VERSION
22/tcp   open  ssh     syn-ack ttl 62 OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
7777/tcp open  http    syn-ack ttl 61 Werkzeug httpd 2.3.4 (Python 3.11.0)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Read data files from: /usr/share/nmap
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 18.59 seconds      Raw packets sent: 6 (240B) | Rcvd: 7 (276B)


```


```
gobuster dir -u http://10.49.143.16:7777 -w /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt 
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.49.143.16:7777
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirbuster/wordlists/directory-list-lowercase-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
cloud                (Status: 200) [Size: 2991]
debug                (Status: 200) [Size: 1957]

```


![[Screenshot_2026-06-17_07-26-31.png|697]]




![[Screenshot_2026-06-17_07-28-18.png]]


![[Screenshot_2026-06-17_07-47-08.png]]

![[Screenshot_2026-06-17_07-46-48.png]]

![[Screenshot 2026-06-17 174759.png]]


