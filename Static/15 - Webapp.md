# Route add

```bash
┌──(root💀kali)-[~/VPNs]
└─# route         
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         _gateway        0.0.0.0         UG    100    0        0 eth0
10.10.14.0      0.0.0.0         255.255.254.0   U     0      0        0 tun0
10.129.0.0      10.10.14.1      255.255.0.0     UG    0      0        0 tun0
172.17.0.0      172.30.0.1      255.255.255.0   UG    0      0        0 tun9
172.30.0.0      0.0.0.0         255.255.0.0     U     0      0        0 tun9
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 eth0
                                                                                                                                                                                                                                             
┌──(root💀kali)-[~/VPNs]
└─# route add -net 172.20.0.0/16 gw 172.30.0.1 dev tun9
                                                                                                                                                                                                                                             
┌──(root💀kali)-[~/VPNs]
└─# route                                              
Kernel IP routing table
Destination     Gateway         Genmask         Flags Metric Ref    Use Iface
default         _gateway        0.0.0.0         UG    100    0        0 eth0
10.10.14.0      0.0.0.0         255.255.254.0   U     0      0        0 tun0
10.129.0.0      10.10.14.1      255.255.0.0     UG    0      0        0 tun0
172.17.0.0      172.30.0.1      255.255.255.0   UG    0      0        0 tun9
172.20.0.0      172.30.0.1      255.255.0.0     UG    0      0        0 tun9
172.30.0.0      0.0.0.0         255.255.0.0     U     0      0        0 tun9
192.168.1.0     0.0.0.0         255.255.255.0   U     100    0        0 eth0
```

# Index directory Listing

![[Pasted image 20210620164611.png]]

# Looking at Info.php

xdebug is active and theres a Metasploit module for it

![[Pasted image 20210620180342.png]]