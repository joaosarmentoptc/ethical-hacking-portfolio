# Create Account

|User|Email|Pass|
|---|---|---|
|jsarmz|jsarmz@mail.htb|Password|


## Flask App
* Flask App * due to Flask cookie available containing authenticated email

```bash
flask-unsign -d -c 'eyJlbWFpbCI6ImpzYXJtekBtYWlsLmh0YiJ9.YMzdIg.keKQRpRUfUdQlQ8-dkwYzAgcXbc'                                                                                     
{'email': 'jsarmz@mail.htb'}
```


## Gunicorn/20.0.0 - HTTP Smuggling Request

https://gist.github.com/ndavison/4c69a2c164b2125cd6685b7d5a3c135b

![[Pasted image 20210618204627.png]]


## Cookie from Admin

```bash
flask-unsign -d -c 'eyJlbWFpbCI6ImFkbWluQHNpbmsuaHRiIn0.YMzahw.ntyVeoP537iyzvnVMdFwFwZ9NC0'                                                                                       
{'email': 'admin@sink.htb'}
```


## Creds @ Admin Notes

[[00 - Creds]]

![[Pasted image 20210618205136.png]]