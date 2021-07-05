# User Fuzzing

```bash
└─# crackmapexec smb intelligence.htb -u usernames -p 'NewIntelligenceCorpUser9876'   

SMB         10.129.177.125  445    DC               [+] intelligence.htb\Tiffany.Molina:NewIntelligenceCorpUser9876 

```


# Mount the shares
```bash
┌──(root💀kali)-[~/HTB/Intelligence/smb]
└─# mount -t cifs -o 'user=Tiffany.Molina,password=NewIntelligenceCorpUser9876' //intelligence.htb/Users Users 
                                                                                                                                                                                                                                             
┌──(root💀kali)-[~/HTB/Intelligence/smb]
└─# mount -t cifs -o 'user=Tiffany.Molina,password=NewIntelligenceCorpUser9876' //intelligence.htb/IT IT  
```


# IT Queries LDAP

downdetector.ps1
```powershell
# Check web server status. Scheduled to run every 5min
Import-Module ActiveDirectory 
foreach($record in Get-ChildItem "AD:DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb" | Where-Object Name -like "web*")  {
try {
$request = Invoke-WebRequest -Uri "http://$($record.Name)" -UseDefaultCredentials
if(.StatusCode -ne 200) {
Send-MailMessage -From 'Ted Graves <Ted.Graves@intelligence.htb>' -To 'Ted Graves <Ted.Graves@intelligence.htb>' -Subject "Host: $($record.Name) is down"
}
} catch {}
}
```



```bash
ldapsearch -LLL -x -H ldap://intelligence.htb -D "Tiffany.Molina@intelligence.htb" -w NewIntelligenceCorpUser9876 -b DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb                                 32 ⨯
dn: DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=h
 tb
objectClass: top
objectClass: dnsZone
cn: Zone
distinguishedName: DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=in
 telligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13051
uSNChanged: 13086
showInAdvancedViewOnly: TRUE
name: intelligence.htb
objectGUID:: NuM+g7/PakC7RkjlBiS9+g==
objectCategory: CN=Dns-Zone,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dNSProperty:: BAAAAAAAAAAAAAAAAQAAABIAAAAAAAAAAAAAAA==
dNSProperty:: AAAAAAAAAAAAAAAAAQAAAJIAAAAAAAAA
dNSProperty:: AAAAAAAAAAAAAAAAAQAAAJAAAAAAAAAA
dNSProperty:: BAAAAAAAAAAAAAAAAQAAABAAAACoAAAAAAAAAA==
dNSProperty:: BAAAAAAAAAAAAAAAAQAAAAEAAAABAAAAAAAAAA==
dNSProperty:: BAAAAAAAAAAAAAAAAQAAACAAAACoAAAAAAAAAA==
dNSProperty:: BAAAAAAAAAAAAAAAAQAAAEAAAAAAAAAAAAAAAA==
dNSProperty:: CAAAAAAAAAAAAAAAAQAAAAgAAAAAAAAAAAAAAAAAAAA=
dNSProperty:: AQAAAAAAAAAAAAAAAQAAAAIAAAACAAAAAA==
dSCorePropagationData: 20210419005130.0Z
dSCorePropagationData: 16010101000000.0Z
dc: intelligence.htb

dn: DC=_ldap._tcp.Default-First-Site-Name._sites.DomainDnsZones,DC=intelligenc
 e.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_ldap._tcp.Default-First-Site-Name._sites.DomainDnsZones
 ,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13118
uSNChanged: 13118
showInAdvancedViewOnly: TRUE
name: _ldap._tcp.Default-First-Site-Name._sites.DomainDnsZones
objectGUID:: AF4gmPGzSUOhcL5Vo36LnQ==
dnsRecord:: HQAhAAXwAAAQAAAAAAACWAAAAACQNzgAAAAAZAGFFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _ldap._tcp.Default-First-Site-Name._sites.DomainDnsZones

dn: DC=ForestDnsZones,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC
 =intelligence,DC=htb

dn: DC=_ldap._tcp.ForestDnsZones,DC=intelligence.htb,CN=MicrosoftDNS,DC=Domain
 DnsZones,DC=intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_ldap._tcp.ForestDnsZones,DC=intelligence.htb,CN=Microso
 ftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13120
uSNChanged: 13120
showInAdvancedViewOnly: TRUE
name: _ldap._tcp.ForestDnsZones
objectGUID:: QfkEU1fifUK3iP7bQwOdDw==
dnsRecord:: HQAhAAXwAAASAAAAAAACWAAAAACQNzgAAAAAZAGFFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _ldap._tcp.ForestDnsZones

dn: DC=_ldap._tcp.Default-First-Site-Name._sites.ForestDnsZones,DC=intelligenc
 e.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_ldap._tcp.Default-First-Site-Name._sites.ForestDnsZones
 ,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13121
uSNChanged: 13121
showInAdvancedViewOnly: TRUE
name: _ldap._tcp.Default-First-Site-Name._sites.ForestDnsZones
objectGUID:: Ie8P7RX1G0CI2LeU6Epp5A==
dnsRecord:: HQAhAAXwAAATAAAAAAACWAAAAACQNzgAAAAAZAGFFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _ldap._tcp.Default-First-Site-Name._sites.ForestDnsZones

dn: DC=web1,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intellige
 nce,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=web1,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZon
 es,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210630005218.0Z
whenChanged: 20210630010959.0Z
uSNCreated: 106733
uSNChanged: 106745
showInAdvancedViewOnly: TRUE
name: web1
objectGUID:: lgDIMYr6GkmUtbsrvMeJoA==
dnsRecord:: CAAAAAUAAABcAAAAAAAAAAAAAAAAAAAAv4FzpUxt1wE=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dNSTombstoned: TRUE
dc: web1

dn: DC=@,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence
 ,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=@,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,
 DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210704100407.0Z
uSNCreated: 13054
uSNChanged: 110681
showInAdvancedViewOnly: TRUE
name: @
objectGUID:: Re9mLspeKkWlV30zRT9a1A==
dnsRecord:: EAAcAAXwAABpAAAAAAACWAAAAAC5PjgA3q2+7wAAAACQGSVMzxAmGg==
dnsRecord:: SgAGAAXwAABpAAAAAAAOEAAAAAAAAAAAAAAAaAAAA4QAAAJYAAFRgAAADhAVAwJkYw
 xpbnRlbGxpZ2VuY2UDaHRiAB0DCmhvc3RtYXN0ZXIMaW50ZWxsaWdlbmNlA2h0YgA=
dnsRecord:: FwACAAXwAABpAAAAAAAOEAAAAAAAAAAAFQMCZGMMaW50ZWxsaWdlbmNlA2h0YgA=
dnsRecord:: BAABAAXwAABpAAAAAAACWAAAAAC5PjgACoEYHQ==
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dNSTombstoned: FALSE
dc: @

dn: DC=_gc._tcp,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intel
 ligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_gc._tcp,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDn
 sZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13055
uSNChanged: 13055
showInAdvancedViewOnly: TRUE
name: _gc._tcp
objectGUID:: fmuKDvgqOkaEHjVP0KlPCg==
dnsRecord:: HQAhAAXwAAAIAAAAAAACWAAAAACQNzgAAAAAZAzEFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _gc._tcp

dn: DC=_gc._tcp.Default-First-Site-Name._sites,DC=intelligence.htb,CN=Microsof
 tDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_gc._tcp.Default-First-Site-Name._sites,DC=intelligence.
 htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13056
uSNChanged: 13056
showInAdvancedViewOnly: TRUE
name: _gc._tcp.Default-First-Site-Name._sites
objectGUID:: td1/r0vfEkGkplTfDwl0hQ==
dnsRecord:: HQAhAAXwAAAJAAAAAAACWAAAAACQNzgAAAAAZAzEFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _gc._tcp.Default-First-Site-Name._sites

dn: DC=_kerberos._tcp,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC
 =intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_kerberos._tcp,DC=intelligence.htb,CN=MicrosoftDNS,DC=Do
 mainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13057
uSNChanged: 13057
showInAdvancedViewOnly: TRUE
name: _kerberos._tcp
objectGUID:: uj9kpb4FV06xye5BHaGB6A==
dnsRecord:: HQAhAAXwAAAGAAAAAAACWAAAAACQNzgAAAAAZABYFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _kerberos._tcp

dn: DC=_kerberos._tcp.Default-First-Site-Name._sites,DC=intelligence.htb,CN=Mi
 crosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_kerberos._tcp.Default-First-Site-Name._sites,DC=intelli
 gence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13058
uSNChanged: 13058
showInAdvancedViewOnly: TRUE
name: _kerberos._tcp.Default-First-Site-Name._sites
objectGUID:: 0CiCyh9iZkKoknLO2v6OSg==
dnsRecord:: HQAhAAXwAAAHAAAAAAACWAAAAACQNzgAAAAAZABYFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _kerberos._tcp.Default-First-Site-Name._sites

dn: DC=_kerberos._udp,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC
 =intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_kerberos._udp,DC=intelligence.htb,CN=MicrosoftDNS,DC=Do
 mainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13059
uSNChanged: 13059
showInAdvancedViewOnly: TRUE
name: _kerberos._udp
objectGUID:: RAPYGGjS8EWtRdRYcXOk+A==
dnsRecord:: HQAhAAXwAAAKAAAAAAACWAAAAACQNzgAAAAAZABYFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _kerberos._udp

dn: DC=_kpasswd._tcp,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=
 intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_kpasswd._tcp,DC=intelligence.htb,CN=MicrosoftDNS,DC=Dom
 ainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13060
uSNChanged: 13060
showInAdvancedViewOnly: TRUE
name: _kpasswd._tcp
objectGUID:: +RGKHg8uPESED6ylpYHu0w==
dnsRecord:: HQAhAAXwAAALAAAAAAACWAAAAACQNzgAAAAAZAHQFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _kpasswd._tcp

dn: DC=_kpasswd._udp,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=
 intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_kpasswd._udp,DC=intelligence.htb,CN=MicrosoftDNS,DC=Dom
 ainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13061
uSNChanged: 13061
showInAdvancedViewOnly: TRUE
name: _kpasswd._udp
objectGUID:: C/7FqBHhi0mJkqbZLVRnog==
dnsRecord:: HQAhAAXwAAAMAAAAAAACWAAAAACQNzgAAAAAZAHQFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _kpasswd._udp

dn: DC=_ldap._tcp,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=int
 elligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_ldap._tcp,DC=intelligence.htb,CN=MicrosoftDNS,DC=Domain
 DnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13062
uSNChanged: 13062
showInAdvancedViewOnly: TRUE
name: _ldap._tcp
objectGUID:: 1oGxxe7XvU2c7SVs4eVrrQ==
dnsRecord:: HQAhAAXwAAAEAAAAAAACWAAAAACQNzgAAAAAZAGFFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _ldap._tcp

dn: DC=_ldap._tcp.Default-First-Site-Name._sites,DC=intelligence.htb,CN=Micros
 oftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_ldap._tcp.Default-First-Site-Name._sites,DC=intelligenc
 e.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13063
uSNChanged: 13063
showInAdvancedViewOnly: TRUE
name: _ldap._tcp.Default-First-Site-Name._sites
objectGUID:: BiIm6vdfIEG5Gqz3pT70zA==
dnsRecord:: HQAhAAXwAAAFAAAAAAACWAAAAACQNzgAAAAAZAGFFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _ldap._tcp.Default-First-Site-Name._sites

dn: DC=_ldap._tcp.DomainDnsZones,DC=intelligence.htb,CN=MicrosoftDNS,DC=Domain
 DnsZones,DC=intelligence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_ldap._tcp.DomainDnsZones,DC=intelligence.htb,CN=Microso
 ftDNS,DC=DomainDnsZones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13064
uSNChanged: 13064
showInAdvancedViewOnly: TRUE
name: _ldap._tcp.DomainDnsZones
objectGUID:: OvQXo+AwhEKY1cKqrU/d1A==
dnsRecord:: HQAhAAXwAAAPAAAAAAACWAAAAACQNzgAAAAAZAGFFQMCZGMMaW50ZWxsaWdlbmNlA2
 h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _ldap._tcp.DomainDnsZones

dn: DC=_msdcs,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelli
 gence,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=_msdcs,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZ
 ones,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210419005130.0Z
uSNCreated: 13065
uSNChanged: 13065
showInAdvancedViewOnly: TRUE
name: _msdcs
objectGUID:: Jq57JC1QkkaoPUBqAjUIGw==
dnsRecord:: FwACAAWCAAADAAAAAAAOEAAAAAAAAAAAFQMCZGMMaW50ZWxsaWdlbmNlA2h0YgA=
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dc: _msdcs

dn: DC=dc,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC=intelligenc
 e,DC=htb
objectClass: top
objectClass: dnsNode
distinguishedName: DC=dc,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones
 ,DC=intelligence,DC=htb
instanceType: 4
whenCreated: 20210419005130.0Z
whenChanged: 20210704181911.0Z
uSNCreated: 13066
uSNChanged: 110876
showInAdvancedViewOnly: TRUE
name: dc
objectGUID:: NDrzTrQJtUOYxqbquzWBVw==
dnsRecord:: EAAcAAXwAACdAAAAAAAEsAAAAAAAAAAA3q2+7wAAAACQGSVMzxAmGg==
dnsRecord:: BAABAAXwAACdAAAAAAAEsAAAAAAAAAAACoEYHQ==
objectCategory: CN=Dns-Node,CN=Schema,CN=Configuration,DC=intelligence,DC=htb
dSCorePropagationData: 16010101000000.0Z
dNSTombstoned: FALSE
dc: dc

dn: DC=DomainDnsZones,DC=intelligence.htb,CN=MicrosoftDNS,DC=DomainDnsZones,DC
 =intelligence,DC=htb
```