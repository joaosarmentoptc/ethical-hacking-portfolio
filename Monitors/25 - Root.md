# Notes

```bash
marcus@monitors:~$ cat note.txt 
TODO:

Disable phpinfo in php.ini              - DONE
Update docker image for production use  - 
```

```bash
root       1579  0.0  0.3 975760 14252 ?        Ssl  14:36   0:04 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock
root       2060  0.0  0.0 553112  1396 ?        Sl   14:36   0:00  _ /usr/bin/docker-proxy -proto tcp -host-ip 127.0.0.1 -host-port 8443 -container-ip 172.17.0.2 -container-port 8443

``` 

# OFBiz

![[Pasted image 20210606232330.png]]


https://www.rapid7.com/db/modules/exploit/linux/http/apache_ofbiz_deserialiation/

**use SET ForceExploit true** to make it work

```bash
root@db786d0b671d:/#  capsh --print
 capsh --print

Current: = cap_chown,cap_dac_override,cap_fowner,cap_fsetid,cap_kill,cap_setgid,cap_setuid,cap_setpcap,cap_net_bind_service,cap_net_raw,cap_sys_module,cap_sys_chroot,cap_mknod,cap_audit_write,cap_setfcap+eip
Bounding set =cap_chown,cap_dac_override,cap_fowner,cap_fsetid,cap_kill,cap_setgid,cap_setuid,cap_setpcap,cap_net_bind_service,cap_net_raw,cap_sys_module,cap_sys_chroot,cap_mknod,cap_audit_write,cap_setfcapSecurebits: 00/0x0/1'b0
 secure-noroot: no (unlocked)
 secure-no-suid-fixup: no (unlocked)
 secure-keep-caps: no (unlocked)
uid=0(root)
gid=0(root)
groups=
```

# Abusing cap_sys_module

https://blog.pentesteracademy.com/abusing-sys-module-capability-to-perform-docker-container-breakout-cf5c29956edd

