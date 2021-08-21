# Nmap

```bash
nmap -sC -sV -oA nmap/anubis 10.10.11.102
Starting Nmap 7.91 ( https://nmap.org ) at 2021-08-19 08:42 EDT
Nmap scan report for 10.10.11.102
Host is up (0.051s latency).
Not shown: 996 filtered ports
PORT    STATE SERVICE       VERSION
135/tcp open  msrpc         Microsoft Windows RPC
443/tcp open  ssl/http      Microsoft HTTPAPI httpd 2.0 (SSDP/UPnP)
|_http-server-header: Microsoft-HTTPAPI/2.0
|_http-title: Not Found
| ssl-cert: Subject: commonName=www.windcorp.htb
| Subject Alternative Name: DNS:www.windcorp.htb
| Not valid before: 2021-05-24T19:44:56
|_Not valid after:  2031-05-24T19:54:56
|_ssl-date: 2021-08-19T12:43:32+00:00; 0s from scanner time.
| tls-alpn: 
|_  http/1.1
445/tcp open  microsoft-ds?
593/tcp open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2021-08-19T12:42:54
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 66.43 seconds
```

# /etc/hosts
* Add www.windcorp.htb 