# Nmap

```bash
nmap -sC -sV -oA nmap/writer 10.129.8.225     
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-31 15:47 EDT
Nmap scan report for 10.129.8.225
Host is up (0.043s latency).
Not shown: 996 closed ports
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 98:20:b9:d0:52:1f:4e:10:3a:4a:93:7e:50:bc:b8:7d (RSA)
|   256 10:04:79:7a:29:74:db:28:f9:ff:af:68:df:f1:3f:34 (ECDSA)
|_  256 77:c4:86:9a:9f:33:4f:da:71:20:2c:e1:51:10:7e:8d (ED25519)
80/tcp  open  http        Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Story Bank | Writer.HTB
139/tcp open  netbios-ssn Samba smbd 4.6.2
445/tcp open  netbios-ssn Samba smbd 4.6.2
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Host script results:
|_clock-skew: 1s
|_nbstat: NetBIOS name: WRITER, NetBIOS user: <unknown>, NetBIOS MAC: <unknown> (unknown)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2021-07-31T19:47:28
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.81 seconds
```


# SMB

![[Pasted image 20210801204122.png]]


# Gobuster

```bash
gobuster dir -u "http://writer.htb" -w /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt -x php             
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://writer.htb
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/seclists/Discovery/Web-Content/raft-small-words.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php
[+] Timeout:                 10s
===============================================================
2021/07/31 15:53:19 Starting gobuster in directory enumeration mode
===============================================================
/contact              (Status: 200) [Size: 4905]
/logout               (Status: 302) [Size: 208] [--> http://writer.htb/]
/about                (Status: 200) [Size: 3522]                        
/static               (Status: 301) [Size: 309] [--> http://writer.htb/static/]
/.                    (Status: 200) [Size: 11971]                              
/dashboard            (Status: 302) [Size: 208] [--> http://writer.htb/]       
/server-status        (Status: 403) [Size: 275]                                
/administrative       (Status: 200) [Size: 1443]                               
                                                                               
===============================================================
2021/07/31 16:00:29 Finished
===============================================================
```


# Administrative

![[Pasted image 20210731211510.png]]