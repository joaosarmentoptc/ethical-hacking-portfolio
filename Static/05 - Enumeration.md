# Nmap

```bash
nmap -sC -sV -oA nmap/static 10.129.162.67
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-20 07:43 EDT
Nmap scan report for 10.129.162.67
Host is up (0.046s latency).
Not shown: 997 filtered ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 7.9p1 Debian 10+deb10u2 (protocol 2.0)
| ssh-hostkey: 
|   2048 16:bb:a0:a1:20:b7:82:4d:d2:9f:35:52:f4:2e:6c:90 (RSA)
|   256 ca:ad:63:8f:30:ee:66:b1:37:9d:c5:eb:4d:44:d9:2b (ECDSA)
|_  256 2d:43:bc:4e:b3:33:c9:82:4e:de:b6:5e:10:ca:a7:c5 (ED25519)
2222/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 a9:a4:5c:e3:a9:05:54:b1:1c:ae:1b:b7:61:ac:76:d6 (RSA)
|   256 c9:58:53:93:b3:90:9e:a0:08:aa:48:be:5e:c4:0a:94 (ECDSA)
|_  256 c7:07:2b:07:43:4f:ab:c8:da:57:7f:ea:b5:50:21:bd (ED25519)
8080/tcp open  http    Apache httpd 2.4.38 ((Debian))
| http-robots.txt: 2 disallowed entries 
|_/vpn/ /.ftp_uploads/
|_http-server-header: Apache/2.4.38 (Debian)
|_http-title: Site doesn't have a title (text/html; charset=UTF-8).
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 35.40 seconds
```

# VPN Login Page

http://10.129.162.67:8080/vpn/login.php

admin:admin asks for 2FA Password
![[Pasted image 20210620130359.png]]

![[Pasted image 20210620130417.png]]


# FTP Uploads

http://10.129.162.67:8080/.ftp_uploads/warning.txt

```text
Binary files are being corrupted during transfer!!! Check if are recoverable.
```

It seems that the file transfers are using ASCII Mode instead of Binary Mode to the FTP, so the file is getting corrupted


# DB.sql

