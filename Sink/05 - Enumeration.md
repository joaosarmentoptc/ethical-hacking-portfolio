# Nmap

```bash
nmap -sC -sV -oA nmap/sink 10.10.10.225                                                                                                                                                                                            130 ⨯
Starting Nmap 7.91 ( https://nmap.org ) at 2021-06-18 13:41 EDT
Nmap scan report for 10.10.10.225
Host is up (0.046s latency).
Not shown: 997 closed ports
PORT     STATE SERVICE VERSION
22/tcp   open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.1 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   3072 48:ad:d5:b8:3a:9f:bc:be:f7:e8:20:1e:f6:bf:de:ae (RSA)
|   256 b7:89:6c:0b:20:ed:49:b2:c1:86:7c:29:92:74:1c:1f (ECDSA)
|_  256 18:cd:9d:08:a6:21:a8:b8:b6:f7:9f:8d:40:51:54:fb (ED25519)
3000/tcp open  ppp?
| fingerprint-strings: 
|   GenericLines, Help: 
|     HTTP/1.1 400 Bad Request
|     Content-Type: text/plain; charset=utf-8
|     Connection: close
|     Request
|   GetRequest: 
|     HTTP/1.0 200 OK
|     Content-Type: text/html; charset=UTF-8
|     Set-Cookie: lang=en-US; Path=/; Max-Age=2147483647
|     Set-Cookie: i_like_gitea=d491f10dc0b79f52; Path=/; HttpOnly
|     Set-Cookie: _csrf=5JhRrpagaAG9t-AZK8qvPigBlK06MTYyNDAzODEwNDYxNjcyMzYwMA; Path=/; Expires=Sat, 19 Jun 2021 17:41:44 GMT; HttpOnly
|     X-Frame-Options: SAMEORIGIN
|     Date: Fri, 18 Jun 2021 17:41:44 GMT
|     <!DOCTYPE html>
|     <html lang="en-US" class="theme-">
|     <head data-suburl="">
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <meta http-equiv="x-ua-compatible" content="ie=edge">
|     <title> Gitea: Git with a cup of tea </title>
|     <link rel="manifest" href="/manifest.json" crossorigin="use-credentials">
|     <meta name="theme-color" content="#6cc644">
|     <meta name="author" content="Gitea - Git with a cup of tea" />
|     <meta name="description" content="Gitea (Git with a cup of tea) is a painless
|   HTTPOptions: 
|     HTTP/1.0 404 Not Found
|     Content-Type: text/html; charset=UTF-8
|     Set-Cookie: lang=en-US; Path=/; Max-Age=2147483647
|     Set-Cookie: i_like_gitea=9426e3ce1d716998; Path=/; HttpOnly
|     Set-Cookie: _csrf=9a9zhnq91udEKHATA-mNBwrNC7I6MTYyNDAzODEwOTg4MTcxNzk4OQ; Path=/; Expires=Sat, 19 Jun 2021 17:41:49 GMT; HttpOnly
|     X-Frame-Options: SAMEORIGIN
|     Date: Fri, 18 Jun 2021 17:41:49 GMT
|     <!DOCTYPE html>
|     <html lang="en-US" class="theme-">
|     <head data-suburl="">
|     <meta charset="utf-8">
|     <meta name="viewport" content="width=device-width, initial-scale=1">
|     <meta http-equiv="x-ua-compatible" content="ie=edge">
|     <title>Page Not Found - Gitea: Git with a cup of tea </title>
|     <link rel="manifest" href="/manifest.json" crossorigin="use-credentials">
|     <meta name="theme-color" content="#6cc644">
|     <meta name="author" content="Gitea - Git with a cup of tea" />
|_    <meta name="description" content="Gitea (Git with a c
5000/tcp open  http    Gunicorn 20.0.0
|_http-server-header: gunicorn/20.0.0
|_http-title: Sink Devops
1 service unrecognized despite returning data. If you know the service/version, please submit the following fingerprint at https://nmap.org/cgi-bin/submit.cgi?new-service :
SF-Port3000-TCP:V=7.91%I=7%D=6/18%Time=60CCDAD8%P=x86_64-pc-linux-gnu%r(Ge
SF:nericLines,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\x20t
SF:ext/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20Bad\x
SF:20Request")%r(GetRequest,1000,"HTTP/1\.0\x20200\x20OK\r\nContent-Type:\
SF:x20text/html;\x20charset=UTF-8\r\nSet-Cookie:\x20lang=en-US;\x20Path=/;
SF:\x20Max-Age=2147483647\r\nSet-Cookie:\x20i_like_gitea=d491f10dc0b79f52;
SF:\x20Path=/;\x20HttpOnly\r\nSet-Cookie:\x20_csrf=5JhRrpagaAG9t-AZK8qvPig
SF:BlK06MTYyNDAzODEwNDYxNjcyMzYwMA;\x20Path=/;\x20Expires=Sat,\x2019\x20Ju
SF:n\x202021\x2017:41:44\x20GMT;\x20HttpOnly\r\nX-Frame-Options:\x20SAMEOR
SF:IGIN\r\nDate:\x20Fri,\x2018\x20Jun\x202021\x2017:41:44\x20GMT\r\n\r\n<!
SF:DOCTYPE\x20html>\n<html\x20lang=\"en-US\"\x20class=\"theme-\">\n<head\x
SF:20data-suburl=\"\">\n\t<meta\x20charset=\"utf-8\">\n\t<meta\x20name=\"v
SF:iewport\"\x20content=\"width=device-width,\x20initial-scale=1\">\n\t<me
SF:ta\x20http-equiv=\"x-ua-compatible\"\x20content=\"ie=edge\">\n\t<title>
SF:\x20Gitea:\x20Git\x20with\x20a\x20cup\x20of\x20tea\x20</title>\n\t<link
SF:\x20rel=\"manifest\"\x20href=\"/manifest\.json\"\x20crossorigin=\"use-c
SF:redentials\">\n\t<meta\x20name=\"theme-color\"\x20content=\"#6cc644\">\
SF:n\t<meta\x20name=\"author\"\x20content=\"Gitea\x20-\x20Git\x20with\x20a
SF:\x20cup\x20of\x20tea\"\x20/>\n\t<meta\x20name=\"description\"\x20conten
SF:t=\"Gitea\x20\(Git\x20with\x20a\x20cup\x20of\x20tea\)\x20is\x20a\x20pai
SF:nless")%r(Help,67,"HTTP/1\.1\x20400\x20Bad\x20Request\r\nContent-Type:\
SF:x20text/plain;\x20charset=utf-8\r\nConnection:\x20close\r\n\r\n400\x20B
SF:ad\x20Request")%r(HTTPOptions,1A82,"HTTP/1\.0\x20404\x20Not\x20Found\r\
SF:nContent-Type:\x20text/html;\x20charset=UTF-8\r\nSet-Cookie:\x20lang=en
SF:-US;\x20Path=/;\x20Max-Age=2147483647\r\nSet-Cookie:\x20i_like_gitea=94
SF:26e3ce1d716998;\x20Path=/;\x20HttpOnly\r\nSet-Cookie:\x20_csrf=9a9zhnq9
SF:1udEKHATA-mNBwrNC7I6MTYyNDAzODEwOTg4MTcxNzk4OQ;\x20Path=/;\x20Expires=S
SF:at,\x2019\x20Jun\x202021\x2017:41:49\x20GMT;\x20HttpOnly\r\nX-Frame-Opt
SF:ions:\x20SAMEORIGIN\r\nDate:\x20Fri,\x2018\x20Jun\x202021\x2017:41:49\x
SF:20GMT\r\n\r\n<!DOCTYPE\x20html>\n<html\x20lang=\"en-US\"\x20class=\"the
SF:me-\">\n<head\x20data-suburl=\"\">\n\t<meta\x20charset=\"utf-8\">\n\t<m
SF:eta\x20name=\"viewport\"\x20content=\"width=device-width,\x20initial-sc
SF:ale=1\">\n\t<meta\x20http-equiv=\"x-ua-compatible\"\x20content=\"ie=edg
SF:e\">\n\t<title>Page\x20Not\x20Found\x20-\x20\x20Gitea:\x20Git\x20with\x
SF:20a\x20cup\x20of\x20tea\x20</title>\n\t<link\x20rel=\"manifest\"\x20hre
SF:f=\"/manifest\.json\"\x20crossorigin=\"use-credentials\">\n\t<meta\x20n
SF:ame=\"theme-color\"\x20content=\"#6cc644\">\n\t<meta\x20name=\"author\"
SF:\x20content=\"Gitea\x20-\x20Git\x20with\x20a\x20cup\x20of\x20tea\"\x20/
SF:>\n\t<meta\x20name=\"description\"\x20content=\"Gitea\x20\(Git\x20with\
SF:x20a\x20c");
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 92.73 seconds

```