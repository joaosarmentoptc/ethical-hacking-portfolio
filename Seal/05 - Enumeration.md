# Nmap

```bash
Starting Nmap 7.91 ( https://nmap.org ) at 2021-07-12 11:30 EDT
Nmap scan report for 10.129.182.5
Host is up (0.058s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE    VERSION
22/tcp   open  ssh        OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 4b:89:47:39:67:3d:07:31:5e:3f:4c:27:41:1f:f9:67 (RSA)
|   256 04:a7:4f:39:95:65:c5:b0:8d:d5:49:2e:d8:44:00:36 (ECDSA)
|_  256 b4:5e:83:93:c5:42:49:de:71:25:92:71:23:b1:85:54 (ED25519)
443/tcp  open  ssl/http   nginx 1.18.0 (Ubuntu)
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-title: Seal Market
| ssl-cert: Subject: commonName=seal.htb/organizationName=Seal Pvt Ltd/stateOrProvinceName=London/countryName=UK
| Not valid before: 2021-05-05T10:24:03
|_Not valid after:  2022-05-05T10:24:03
| tls-alpn: 
|_  http/1.1
| tls-nextprotoneg: 
|_  http/1.1
8080/tcp open  http-proxy
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.1 401 Unauthorized
|     Date: Mon, 12 Jul 2021 15:30:52 GMT
|     Set-Cookie: JSESSIONID=node019nigjinulta81ghlvyd3om9uk2.node0; Path=/; HttpOnly
|     Expires: Thu, 01 Jan 1970 00:00:00 GMT
|     Content-Type: text/html;charset=utf-8
|     Content-Length: 0
|   GetRequest: 
|     HTTP/1.1 401 Unauthorized
|     Date: Mon, 12 Jul 2021 15:30:51 GMT
|     Set-Cookie: JSESSIONID=node01sx71s3eg9jtlf28rss13w4pt0.node0; Path=/; HttpOnly
|     Expires: Thu, 01 Jan 1970 00:00:00 GMT
|     Content-Type: text/html;charset=utf-8
|     Content-Length: 0
|   HTTPOptions: 
|     HTTP/1.1 200 OK
|     Date: Mon, 12 Jul 2021 15:30:52 GMT
|     Set-Cookie: JSESSIONID=node0gmhwi6pua95v7sopzg6nhnns1.node0; Path=/; HttpOnly
|     Expires: Thu, 01 Jan 1970 00:00:00 GMT
|     Content-Type: text/html;charset=utf-8
|     Allow: GET,HEAD,POST,OPTIONS
|     Content-Length: 0
|   RPCCheck: 
|     HTTP/1.1 400 Illegal character OTEXT=0x80
|     Content-Type: text/html;charset=iso-8859-1
|     Content-Length: 71
|     Connection: close
|     <h1>Bad Message 400</h1><pre>reason: Illegal character OTEXT=0x80</pre>
|   RTSPRequest: 
|     HTTP/1.1 505 Unknown Version
|     Content-Type: text/html;charset=iso-8859-1
|     Content-Length: 58
|     Connection: close
|     <h1>Bad Message 505</h1><pre>reason: Unknown Version</pre>
|   Socks4: 
|     HTTP/1.1 400 Illegal character CNTL=0x4
|     Content-Type: text/html;charset=iso-8859-1
|     Content-Length: 69
|     Connection: close
|     <h1>Bad Message 400</h1><pre>reason: Illegal character CNTL=0x4</pre>
|   Socks5: 
|     HTTP/1.1 400 Illegal character CNTL=0x5
|     Content-Type: text/html;charset=iso-8859-1
|     Content-Length: 69
|     Connection: close
|_    <h1>Bad Message 400</h1><pre>reason: Illegal character CNTL=0x5</pre>
| http-auth: 
| HTTP/1.1 401 Unauthorized\x0D
|_  Server returned status 401 but no WWW-Authenticate header.
|_http-title: Site doesn't have a title (text/html;charset=utf-8).
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8080-TCP:V=7.91%I=7%D=7/12%Time=60EC6031%P=x86_64-pc-linux-gnu%r(Ge
SF:tRequest,F4,"HTTP/1\.1\x20401\x20Unauthorized\r\nDate:\x20Mon,\x2012\x2
SF:0Jul\x202021\x2015:30:51\x20GMT\r\nSet-Cookie:\x20JSESSIONID=node01sx71
SF:s3eg9jtlf28rss13w4pt0\.node0;\x20Path=/;\x20HttpOnly\r\nExpires:\x20Thu
SF:,\x2001\x20Jan\x201970\x2000:00:00\x20GMT\r\nContent-Type:\x20text/html
SF:;charset=utf-8\r\nContent-Length:\x200\r\n\r\n")%r(HTTPOptions,107,"HTT
SF:P/1\.1\x20200\x20OK\r\nDate:\x20Mon,\x2012\x20Jul\x202021\x2015:30:52\x
SF:20GMT\r\nSet-Cookie:\x20JSESSIONID=node0gmhwi6pua95v7sopzg6nhnns1\.node
SF:0;\x20Path=/;\x20HttpOnly\r\nExpires:\x20Thu,\x2001\x20Jan\x201970\x200
SF:0:00:00\x20GMT\r\nContent-Type:\x20text/html;charset=utf-8\r\nAllow:\x2
SF:0GET,HEAD,POST,OPTIONS\r\nContent-Length:\x200\r\n\r\n")%r(RTSPRequest,
SF:AD,"HTTP/1\.1\x20505\x20Unknown\x20Version\r\nContent-Type:\x20text/htm
SF:l;charset=iso-8859-1\r\nContent-Length:\x2058\r\nConnection:\x20close\r
SF:\n\r\n<h1>Bad\x20Message\x20505</h1><pre>reason:\x20Unknown\x20Version<
SF:/pre>")%r(FourOhFourRequest,F5,"HTTP/1\.1\x20401\x20Unauthorized\r\nDat
SF:e:\x20Mon,\x2012\x20Jul\x202021\x2015:30:52\x20GMT\r\nSet-Cookie:\x20JS
SF:ESSIONID=node019nigjinulta81ghlvyd3om9uk2\.node0;\x20Path=/;\x20HttpOnl
SF:y\r\nExpires:\x20Thu,\x2001\x20Jan\x201970\x2000:00:00\x20GMT\r\nConten
SF:t-Type:\x20text/html;charset=utf-8\r\nContent-Length:\x200\r\n\r\n")%r(
SF:Socks5,C3,"HTTP/1\.1\x20400\x20Illegal\x20character\x20CNTL=0x5\r\nCont
SF:ent-Type:\x20text/html;charset=iso-8859-1\r\nContent-Length:\x2069\r\nC
SF:onnection:\x20close\r\n\r\n<h1>Bad\x20Message\x20400</h1><pre>reason:\x
SF:20Illegal\x20character\x20CNTL=0x5</pre>")%r(Socks4,C3,"HTTP/1\.1\x2040
SF:0\x20Illegal\x20character\x20CNTL=0x4\r\nContent-Type:\x20text/html;cha
SF:rset=iso-8859-1\r\nContent-Length:\x2069\r\nConnection:\x20close\r\n\r\
SF:n<h1>Bad\x20Message\x20400</h1><pre>reason:\x20Illegal\x20character\x20
SF:CNTL=0x4</pre>")%r(RPCCheck,C7,"HTTP/1\.1\x20400\x20Illegal\x20characte
SF:r\x20OTEXT=0x80\r\nContent-Type:\x20text/html;charset=iso-8859-1\r\nCon
SF:tent-Length:\x2071\r\nConnection:\x20close\r\n\r\n<h1>Bad\x20Message\x2
SF:0400</h1><pre>reason:\x20Illegal\x20character\x20OTEXT=0x80</pre>");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 21.25 seconds
```


# GitBucket

## Firewall / Proxy

![[Pasted image 20210712175611.png]]

## Creds

http://seal.htb:8080/root/seal_market/commit/ac210325afd2f6ae17cce84a8aa42805ce5fd010

![[Pasted image 20210712175637.png]]