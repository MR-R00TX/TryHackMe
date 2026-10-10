


Markdown

````
---
tags:
  - tryhackme
  - owasp-top-10
  - juice-shop
  - walkthrough
  - web-security
difficulty: Easy/Medium
platform: TryHackMe
date_completed: 2026-06-06
---

# TryHackMe: OWASP Juice Shop Walkthrough

> [!info] **Room Description**
> This room utilizes the **OWASP Juice Shop** vulnerable web application to learn how to identify and exploit common web application vulnerabilities aligned with the OWASP Top 10.

---

## 📋 Task 1: Open for business!

- [x] Deploy the VM attached to the task.
- [x] Access the machine via browser or OpenVPN using the target IP.

---

## 🔍 Task 2: Let’s go on an adventure!

### Q1: What’s the Administrator’s email address?
- **Method:** Navigate to the homepage, click on the **Apple Juice (1000ml)** product, and view the review/details section to find the admin's email.
- **Answer:** `admin@juice-sh.op`

### Q2: What parameter is used for searching?
- **Method:** Click on the magnifying glass icon in the top right to open the search bar. Input test data and look at the updated URL: `http://<IP>/#/search?q=a`. The parameter after the query string is `q`.
- **Answer:** `q`

### Q3: What show does Jim reference in his review?
- **Method:** Look at Jim's product review on the **Green Smoothie**. He mentions a "replicator," which is a direct reference to **Star Trek**.
- **Answer:** `Star Trek`

---

## 💉 Task 3: Inject the juice

> [!key] **Vulnerability Concepts**
> - **SQL Injection (SQLi):** Malicious inputs alter database queries to retrieve or tamper with hidden data.
> - **Command Injection:** Exploiting user inputs to execute arbitrary OS commands on the host server.
> - **Email Injection:** Injecting extra headers into mail server forms to bypass authorization.

### Q1: Bruteforce the Administrator account’s password!
- **Method:** Open Burp Suite and intercept the login request. Replace the email field with a classic SQLi authentication bypass payload:
```sql
  ' or 1=1 --
````


- **Answer (Flag):** `690fa3247a99d651e0b26f947baf0b79b4f404a9`
    

### Q2: Log into the Bender account!

- **Method:** Similar to the admin bypass, capture the login request and target Bender's specific email string by appending the comment payload:
    

SQL

```
  bender@juice-sh.op' --
```

- **Answer (Flag):** `5ff5052e879e6fef64124e64c82c84ebc809c6c4`
    

## 🔓 Task 4: Who broke my lock?!

### Q1: Bruteforce the Administrator account’s password!

- **Method:**
    
    1. Send the standard login request to **Burp Intruder**.
        
    2. Clear all positions, select the password field value, and add payload markers (`§password§`).
        
    3. Load the wordlist from Seclists: `/usr/share/wordlists/SecLists/Passwords/Common-Credentials/best1050.txt`.
        
    4. Launch the attack. Filter by HTTP Status code; look for a `200 OK` response instead of `401 Unauthorized`.
        
- **Password Found:** `admin123`
    
- **Answer (Flag):** `ff4aebffe31b0ffdea9bdd0207a16a3c01ac6c56`
    

### Q2: Reset Jim’s password!

- **Method:** Navigate to the _Forgot Password_ page. Jim's security question asks: _"Your eldest sibling's middle name?"_. Based on OSINT/recon, his brother's middle name is **Samuel**. Submit this answer to successfully change the password.
    
- **Answer (Flag):** `3c3e2d6ef99b733b947e92f8e2a9ed08bf57ea63`
    

## 📁 Task 5: AH! Don’t look!

### Q1: Access the Confidential Document!

- **Method:** Browse the `/ftp/` directory manually. Locate and download the sensitive legal/acquisition file (`acquisitions.md`). Navigate back to the homepage to trigger the flag.
    
- **Answer (Flag):** `8d2072c6b0a455608ca1a293dc0c9579883fc6a5`
    

### Q2: Log into MC SafeSearch’s account!

- **Method:** Analyze the target's video/song lyrics. The artist mentions his password is "Mr. Noodles" but specifies that he replaces vowels with zeros.
    
- **Password:** `Mr. N00dles`
    
- **Answer (Flag):** `bb105418e73708ceccf1a7b2491f434b8f5230e4`
    

### Q3: Download the Backup file!

- **Method:** To access restricted extensions like `.json` or `.bak` inside `/ftp/`, bypass the application's extension filter using a **Poison Null Byte** sequence (`%00` encoded or double-encoded as `%2500`) followed by an allowed extension (`.md`).
    
- **URL Payload:**
    

HTTP

```
  http://<IP>/ftp/package.json.bak%2500.md
```

- **Answer (Flag):** `cfdeea14e8f01b4952722fd0e4a77f1928593c9a`
    

## 🕹️ Task 6: Who’s flying this thing?

> [!warning] **Broken Access Control Types**
> 
> - **Horizontal Privilege Escalation:** Accessing data/resources belonging to a user with the _same_ privilege tier.
>     
> - **Vertical Privilege Escalation:** Accessing functions or data belonging to a _higher_ privilege tier (e.g., User accessing Admin panel).
>     

### Q1: Access the administration page!

- **Method:** Analyze the client-side JavaScript bundle (`main-es2015.js`) via DevTools. Search for routing parameters to uncover the hidden admin path: `/#/administration`. Log into the Admin account first to gain access.
    
- **URL:** `http://<IP>/#/administration`
    
- **Answer (Flag):** `71aeb3b0bf01cc6e488f0207bb62f79b41454a87`
    

### Q2: View another user’s shopping basket!

- **Method:** Log into your account and open 'Your Basket'. Intercept the traffic with Burp Suite. Locate the following dynamic endpoint:
    

HTTP

```
  GET /rest/basket/1 HTTP/1.1
```

Change the basket ID parameter from `1` to `2` to view another user's cart (**Insecure Direct Object Reference - IDOR**).

- **Answer (Flag):** `e6982b34b6734ceadd28e5019b251f929a80b815`
    

### Q3: Remove all 5-star reviews!

- **Method:** While viewing the `/#/administration` dashboard as an admin, locate the user reviews table and click the delete (bin) icon next to the 5-star rating entry.
    
- **Answer (Flag):** `78231b75c0b2180b7e964dcbb1ab3c3f58639f2e`
    

## 💻 Task 7: Where did that come from?

> [!abstract] **Cross-Site Scripting (XSS) Breakdown**
> 
> 1. **DOM XSS:** Execution occurs purely client-side within the local browser environment.
>     
> 2. **Persistent (Stored) XSS:** Unsanitized payload is saved to the backend database and executes whenever a user loads the page.
>     
> 3. **Reflected XSS:** Payload is passed inside an HTTP request parameter and reflected immediately in the response page.
>     

### Q1: Perform a DOM XSS!

- **Method:** Input an HTML iframe injection payload with an inline JS alert directly into the main application search bar:
    

HTML

```
  <iframe src="javascript:alert(`xss`)">
```

- **Answer (Flag):** `4a31a4fe0954199566e360a873802bf64d0d0a84`
    

### Q2: Perform a persistent XSS!

- **Method:** Log into the Admin account, navigate to the **Last Login IP** section, and trigger a logout. Intercept the request in Burp Suite and inject a malicious header payload to poison the stored IP logging mechanism:
    

HTTP

```
  True-Client-IP: <iframe src="javascript:alert(`xss`)">
```


- **Answer (Flag):** `c37da14686b69a220fd9febd09bb9593e7d0539f`
    

### Q3: Perform a reflected XSS!

- **Method:** Navigate to **Order History** under the Admin panel. Click on the "Truck" tracking icon to load the tracking results page. Inject your XSS payload directly into the dynamic Order/Tracking ID parameter reflected on the page template.
    
- **Answer (Flag):** `305021787d3e9cd9cebc057a021c2504550bb3b6`
    

## 🏆 Task 8: Exploration!

- **Method:** To access the hidden gamified scoreboard tracking your overall challenge completion status, manually navigate to: `http://<IP>/#/score-board/`
    
- **Answer (Flag):** `2614339936e8282e2f820f023d4d998a1f95e02a`