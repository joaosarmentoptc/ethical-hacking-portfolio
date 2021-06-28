# Nmap

```bash
nmap -A -T4 -p- -oA nmap/unobtainium 10.10.10.235                                                                                                                    1 ⨯
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-27 17:29 EDT
Warning: 10.10.10.235 giving up on port because retransmission cap hit (6).
Nmap scan report for 10.10.10.235
Host is up (0.043s latency).
Not shown: 65507 closed ports
PORT      STATE    SERVICE          VERSION
22/tcp    open     ssh              OpenSSH 8.2p1 Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 e4:bf:68:42:e5:74:4b:06:58:78:bd:ed:1e:6a:df:66 (RSA)
|   256 bd:88:a1:d9:19:a0:12:35:ca:d3:fa:63:76:48:dc:65 (ECDSA)
|_  256 cf:c4:19:25:19:fa:6e:2e:b7:a4:aa:7d:c3:f1:3d:9b (ED25519)
80/tcp    open     http             Apache httpd 2.4.41 ((Ubuntu))
|_http-server-header: Apache/2.4.41 (Ubuntu)
|_http-title: Unobtainium
122/tcp   filtered smakynet
575/tcp   filtered vemmi
2379/tcp  open     ssl/etcd-client?
| ssl-cert: Subject: commonName=unobtainium
| Subject Alternative Name: DNS:localhost, DNS:unobtainium, IP Address:10.10.10.3, IP Address:127.0.0.1, IP Address:0:0:0:0:0:0:0:1
| Not valid before: 2021-01-17T07:10:30
|_Not valid after:  2022-01-17T07:10:30
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  h2
| tls-nextprotoneg: 
|_  h2
2380/tcp  open     ssl/etcd-server?
| ssl-cert: Subject: commonName=unobtainium
| Subject Alternative Name: DNS:localhost, DNS:unobtainium, IP Address:10.10.10.3, IP Address:127.0.0.1, IP Address:0:0:0:0:0:0:0:1
| Not valid before: 2021-01-17T07:10:30
|_Not valid after:  2022-01-17T07:10:30
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|_  h2
| tls-nextprotoneg: 
|_  h2
6931/tcp  filtered unknown
8299/tcp  filtered unknown
8443/tcp  open     ssl/https-alt
| fingerprint-strings: 
|   FourOhFourRequest: 
|     HTTP/1.0 403 Forbidden
|     Cache-Control: no-cache, private
|     Content-Type: application/json
|     X-Content-Type-Options: nosniff
|     X-Kubernetes-Pf-Flowschema-Uid: 3082aa7f-e4b1-444a-a726-829587cd9e39
|     X-Kubernetes-Pf-Prioritylevel-Uid: c4131e14-5fda-4a46-8349-09ccbed9efdd
|     Date: Sun, 27 Jun 2021 21:38:33 GMT
|     Content-Length: 212
|     {"kind":"Status","apiVersion":"v1","metadata":{},"status":"Failure","message":"forbidden: User "system:anonymous" cannot get path "/nice ports,/Trinity.txt.bak"","reason":"Forbidden","details":{},"code":403}
|   GenericLines: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest: 
|     HTTP/1.0 403 Forbidden
|     Cache-Control: no-cache, private
|     Content-Type: application/json
|     X-Content-Type-Options: nosniff
|     X-Kubernetes-Pf-Flowschema-Uid: 3082aa7f-e4b1-444a-a726-829587cd9e39
|     X-Kubernetes-Pf-Prioritylevel-Uid: c4131e14-5fda-4a46-8349-09ccbed9efdd
|     Date: Sun, 27 Jun 2021 21:38:32 GMT
|     Content-Length: 185
|     {"kind":"Status","apiVersion":"v1","metadata":{},"status":"Failure","message":"forbidden: User "system:anonymous" cannot get path "/"","reason":"Forbidden","details":{},"code":403}
|   HTTPOptions: 
|     HTTP/1.0 403 Forbidden
|     Cache-Control: no-cache, private
|     Content-Type: application/json
|     X-Content-Type-Options: nosniff
|     X-Kubernetes-Pf-Flowschema-Uid: 3082aa7f-e4b1-444a-a726-829587cd9e39
|     X-Kubernetes-Pf-Prioritylevel-Uid: c4131e14-5fda-4a46-8349-09ccbed9efdd
|     Date: Sun, 27 Jun 2021 21:38:32 GMT
|     Content-Length: 189
|_    {"kind":"Status","apiVersion":"v1","metadata":{},"status":"Failure","message":"forbidden: User "system:anonymous" cannot options path "/"","reason":"Forbidden","details":{},"code":403}
|_http-title: Site doesn't have a title (application/json).
| ssl-cert: Subject: commonName=minikube/organizationName=system:masters
| Subject Alternative Name: DNS:minikubeCA, DNS:control-plane.minikube.internal, DNS:kubernetes.default.svc.cluster.local, DNS:kubernetes.default.svc, DNS:kubernetes.default, DNS:kubernetes, DNS:localhost, IP Address:10.10.10.235, IP Address:10.96.0.1, IP Address:127.0.0.1, IP Address:10.0.0.1
| Not valid before: 2021-06-26T21:28:45
|_Not valid after:  2022-06-27T21:28:45
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|   h2
|_  http/1.1
8458/tcp  filtered unknown
10250/tcp open     ssl/http         Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
|_http-title: Site doesn't have a title (text/plain; charset=utf-8).
| ssl-cert: Subject: commonName=unobtainium@1610865428
| Subject Alternative Name: DNS:unobtainium
| Not valid before: 2021-01-17T05:37:08
|_Not valid after:  2022-01-17T05:37:08
|_ssl-date: TLS randomness does not represent time
| tls-alpn: 
|   h2
|_  http/1.1
10256/tcp open     http             Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
|_http-title: Site doesn't have a title (text/plain; charset=utf-8).
14366/tcp filtered unknown
17091/tcp filtered unknown
19022/tcp filtered unknown
21511/tcp filtered unknown
22455/tcp filtered unknown
24163/tcp filtered unknown
26955/tcp filtered unknown
35662/tcp filtered unknown
37139/tcp filtered unknown
41731/tcp filtered unknown
41841/tcp filtered unknown
42539/tcp filtered unknown
49680/tcp filtered unknown
52418/tcp filtered unknown
55349/tcp filtered unknown
62890/tcp filtered unknown
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port8443-TCP:V=7.91%T=SSL%I=7%D=6/27%Time=60D8EFD8%P=x86_64-pc-linux-gn
SF:u%r(GetRequest,1FF,"HTTP/1\.0\x20403\x20Forbidden\r\nCache-Control:\x20
SF:no-cache,\x20private\r\nContent-Type:\x20application/json\r\nX-Content-
SF:Type-Options:\x20nosniff\r\nX-Kubernetes-Pf-Flowschema-Uid:\x203082aa7f
SF:-e4b1-444a-a726-829587cd9e39\r\nX-Kubernetes-Pf-Prioritylevel-Uid:\x20c
SF:4131e14-5fda-4a46-8349-09ccbed9efdd\r\nDate:\x20Sun,\x2027\x20Jun\x2020
SF:21\x2021:38:32\x20GMT\r\nContent-Length:\x20185\r\n\r\n{\"kind\":\"Stat
SF:us\",\"apiVersion\":\"v1\",\"metadata\":{},\"status\":\"Failure\",\"mes
SF:sage\":\"forbidden:\x20User\x20\\\"system:anonymous\\\"\x20cannot\x20ge
SF:t\x20path\x20\\\"/\\\"\",\"reason\":\"Forbidden\",\"details\":{},\"code
SF:\":403}\n")%r(HTTPOptions,203,"HTTP/1\.0\x20403\x20Forbidden\r\nCache-C
SF:ontrol:\x20no-cache,\x20private\r\nContent-Type:\x20application/json\r\
SF:nX-Content-Type-Options:\x20nosniff\r\nX-Kubernetes-Pf-Flowschema-Uid:\
SF:x203082aa7f-e4b1-444a-a726-829587cd9e39\r\nX-Kubernetes-Pf-Priorityleve
SF:l-Uid:\x20c4131e14-5fda-4a46-8349-09ccbed9efdd\r\nDate:\x20Sun,\x2027\x
SF:20Jun\x202021\x2021:38:32\x20GMT\r\nContent-Length:\x20189\r\n\r\n{\"ki
SF:nd\":\"Status\",\"apiVersion\":\"v1\",\"metadata\":{},\"status\":\"Fail
SF:ure\",\"message\":\"forbidden:\x20User\x20\\\"system:anonymous\\\"\x20c
SF:annot\x20options\x20path\x20\\\"/\\\"\",\"reason\":\"Forbidden\",\"deta
SF:ils\":{},\"code\":403}\n")%r(FourOhFourRequest,21A,"HTTP/1\.0\x20403\x2
SF:0Forbidden\r\nCache-Control:\x20no-cache,\x20private\r\nContent-Type:\x
SF:20application/json\r\nX-Content-Type-Options:\x20nosniff\r\nX-Kubernete
SF:s-Pf-Flowschema-Uid:\x203082aa7f-e4b1-444a-a726-829587cd9e39\r\nX-Kuber
SF:netes-Pf-Prioritylevel-Uid:\x20c4131e14-5fda-4a46-8349-09ccbed9efdd\r\n
SF:Date:\x20Sun,\x2027\x20Jun\x202021\x2021:38:33\x20GMT\r\nContent-Length
SF::\x20212\r\n\r\n{\"kind\":\"Status\",\"apiVersion\":\"v1\",\"metadata\"
SF::{},\"status\":\"Failure\",\"message\":\"forbidden:\x20User\x20\\\"syst
SF:em:anonymous\\\"\x20cannot\x20get\x20path\x20\\\"/nice\x20ports,/Trinit
SF:y\.txt\.bak\\\"\",\"reason\":\"Forbidden\",\"details\":{},\"code\":403}
SF:\n")%r(GenericLines,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-T
SF:ype:\x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400
SF:\x20Bad\x20Request");
No exact OS matches for host (If you know what OS is running on it, see https://nmap.org/submit/ ).
TCP/IP fingerprint:
OS:SCAN(V=7.91%E=4%D=6/27%OT=22%CT=1%CU=30473%PV=Y%DS=2%DC=T%G=Y%TM=60D8F03
OS:C%P=x86_64-pc-linux-gnu)SEQ(SP=104%GCD=1%ISR=10C%TI=Z%CI=Z%II=I%TS=A)OPS
OS:(O1=M54DST11NW7%O2=M54DST11NW7%O3=M54DNNT11NW7%O4=M54DST11NW7%O5=M54DST1
OS:1NW7%O6=M54DST11)WIN(W1=FE88%W2=FE88%W3=FE88%W4=FE88%W5=FE88%W6=FE88)ECN
OS:(R=Y%DF=Y%T=40%W=FAF0%O=M54DNNSNW7%CC=Y%Q=)T1(R=Y%DF=Y%T=40%S=O%A=S+%F=A
OS:S%RD=0%Q=)T2(R=N)T3(R=N)T4(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F=R%O=%RD=0%Q=)T5(R
OS:=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)T6(R=Y%DF=Y%T=40%W=0%S=A%A=Z%F
OS:=R%O=%RD=0%Q=)T7(R=Y%DF=Y%T=40%W=0%S=Z%A=S+%F=AR%O=%RD=0%Q=)U1(R=Y%DF=N%
OS:T=40%IPL=164%UN=0%RIPL=G%RID=G%RIPCK=G%RUCK=G%RUD=G)IE(R=Y%DFI=N%T=40%CD
OS:=S)

Network Distance: 2 hops
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

TRACEROUTE (using port 23/tcp)
HOP RTT      ADDRESS
1   43.52 ms 10.10.14.1
2   43.63 ms 10.10.10.235

OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 654.99 seconds

```


# Usernames:

```json
[{"icon":"__","text":"","id":1,"timestamp":1624830043697,"userName":"felamos"}]
```