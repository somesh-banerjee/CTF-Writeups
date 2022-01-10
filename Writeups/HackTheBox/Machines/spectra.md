# [Spectra]()
Other OS, 20 Points, Easy

ip=10.10.10.229

## User solution
The first thing is to do the nmap scan.
```
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.1 (protocol 2.0)
| ssh-hostkey:
|_  4096 52:47:de:5c:37:4f:29:0e:8e:1d:88:6e:f9:23:4d:5a (RSA)
80/tcp   open  http    nginx 1.17.4
|_http-server-header: nginx/1.17.4
|_http-title: Site doesn't have a title (text/html).
3306/tcp open  mysql   MySQL (unauthorized)
|_ssl-cert: ERROR: Script execution failed (use -d to debug)
|_ssl-date: ERROR: Script execution failed (use -d to debug)
|_sslv2: ERROR: Script execution failed (use -d to debug)
|_tls-alpn: ERROR: Script execution failed (use -d to debug)
|_tls-nextprotoneg: ERROR: Script execution failed (use -d to debug)
5555/tcp open  http    SimpleHTTPServer 0.6 (Python 3.8.2)
|_http-server-header: SimpleHTTP/0.6 Python/3.8.2
|_http-title: Directory listing for /
8080/tcp open  http    SimpleHTTPServer 0.6 (Python 3.8.2)
|_http-server-header: SimpleHTTP/0.6 Python/3.8.2
|_http-title: Directory listing for /
```
