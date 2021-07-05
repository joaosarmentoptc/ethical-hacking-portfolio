# Nmap
```bash
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-03 15:30 EDT
Nmap scan report for 10.129.177.125
Host is up (0.042s latency).
Not shown: 988 filtered ports
PORT     STATE SERVICE       VERSION
53/tcp   open  domain        Simple DNS Plus
80/tcp   open  http          Microsoft IIS httpd 10.0
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
|_http-title: Intelligence
88/tcp   open  kerberos-sec  Microsoft Windows Kerberos (server time: 2021-07-04 02:31:10Z)
135/tcp  open  msrpc         Microsoft Windows RPC
139/tcp  open  netbios-ssn   Microsoft Windows netbios-ssn
389/tcp  open  ldap          Microsoft Windows Active Directory LDAP (Domain: intelligence.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=dc.intelligence.htb
| Subject Alternative Name: othername:<unsupported>, DNS:dc.intelligence.htb
| Not valid before: 2021-04-19T00:43:16
|_Not valid after:  2022-04-19T00:43:16
|_ssl-date: 2021-07-04T02:32:31+00:00; +7h00m01s from scanner time.
445/tcp  open  microsoft-ds?
464/tcp  open  kpasswd5?
593/tcp  open  ncacn_http    Microsoft Windows RPC over HTTP 1.0
636/tcp  open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: intelligence.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=dc.intelligence.htb
| Subject Alternative Name: othername:<unsupported>, DNS:dc.intelligence.htb
| Not valid before: 2021-04-19T00:43:16
|_Not valid after:  2022-04-19T00:43:16
|_ssl-date: 2021-07-04T02:32:31+00:00; +7h00m01s from scanner time.
3268/tcp open  ldap          Microsoft Windows Active Directory LDAP (Domain: intelligence.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=dc.intelligence.htb
| Subject Alternative Name: othername:<unsupported>, DNS:dc.intelligence.htb
| Not valid before: 2021-04-19T00:43:16
|_Not valid after:  2022-04-19T00:43:16
|_ssl-date: 2021-07-04T02:32:31+00:00; +7h00m01s from scanner time.
3269/tcp open  ssl/ldap      Microsoft Windows Active Directory LDAP (Domain: intelligence.htb0., Site: Default-First-Site-Name)
| ssl-cert: Subject: commonName=dc.intelligence.htb
| Subject Alternative Name: othername:<unsupported>, DNS:dc.intelligence.htb
| Not valid before: 2021-04-19T00:43:16
|_Not valid after:  2022-04-19T00:43:16
|_ssl-date: 2021-07-04T02:32:31+00:00; +7h00m01s from scanner time.
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
|_clock-skew: mean: 7h00m00s, deviation: 0s, median: 7h00m00s
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled and required
| smb2-time: 
|   date: 2021-07-04T02:31:51
|_  start_date: N/A

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 92.14 seconds

```


# Document Listing

### Generate a file with dates

```python
from datetime import date, timedelta

start_date = date(2020, 1, 1)
end_date = date(2020, 12, 31)
delta = timedelta(days=1)
f = open("dates.txt","a")
while start_date <= end_date:
    print(start_date.strftime("%Y-%m-%d"))
    f.write(start_date.strftime("%Y-%m-%d")+"\n")
    start_date += delta

f.close()
```

### Iterate to get all the documents

```bash
#!/bin/bash

for date in $(cat dates.txt); do
        wget "http://intelligence.htb/documents/"$date"-upload.pdf"
done
```

### Interesting documents

### 2020-06-04-upload

```
New Account Guide
Welcome to Intelligence Corp!
Please login using your username and the default password of:
NewIntelligenceCorpUser9876
After logging in please change your password as soon as possible.
```


### 2020-12-30-upload

```
Internal IT Update
There has recently been some outages on our web servers. Ted has gotten a
script in place to help notify us if this happens again.
Also, after discussion following our recent security audit we are in the process
of locking down our service accounts.
``` 

![[Pasted image 20210703215714.png]]


# Usernames



```bash
$strings *.pdf | grep /Creator | grep -v "/Creator (TeX)" | cut -d " " -f 2 | sed 's/[)(]//g'  > ../usernames

William.Lee
Scott.Scott
Jason.Wright
Veronica.Patel
Jennifer.Thomas
Danny.Matthews
David.Reed
Stephanie.Young
Daniel.Shelton
Jose.Williams
John.Coleman
Jason.Wright
Jose.Williams
Daniel.Shelton
Brian.Morris
Jennifer.Thomas
Thomas.Valenzuela
Travis.Evans
Samuel.Richardson
Richard.Williams
David.Mcbride
Jose.Williams
John.Coleman
William.Lee
Anita.Roberts
Brian.Baker
Jose.Williams
David.Mcbride
Kelly.Long
John.Coleman
Jose.Williams
Nicole.Brock
Thomas.Valenzuela
David.Reed
Kaitlyn.Zimmerman
Jason.Patterson
Thomas.Valenzuela
David.Mcbride
Darryl.Harris
William.Lee
Stephanie.Young
David.Reed
Nicole.Brock
David.Mcbride
William.Lee
Stephanie.Young
John.Coleman
David.Wilson
Scott.Scott
Teresa.Williamson
John.Coleman
Veronica.Patel
John.Coleman
Samuel.Richardson
Ian.Duncan
Nicole.Brock
William.Lee
Jason.Wright
Travis.Evans
David.Mcbride
Jessica.Moody
Ian.Duncan
Jason.Wright
Richard.Williams
Tiffany.Molina
Jose.Williams
Jessica.Moody
Brian.Baker
Anita.Roberts
Teresa.Williamson
Kaitlyn.Zimmerman
Jose.Williams
Stephanie.Young
Samuel.Richardson
Tiffany.Molina
Ian.Duncan
Kelly.Long
Travis.Evans
Ian.Duncan
Jose.Williams
David.Wilson
Thomas.Hall
Ian.Duncan
Jason.Patterson
```