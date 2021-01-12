blocklist-ipset
===============

A script to update ipsets for IPv4 and IPv6 from the
all.txt list of blocklists.de.

Configuration
=============

There's none.

Installation
=============

Create the following ipsets and make sure they exist before you run this script:

```
ipset create blocklists-de-permanent_v4 hash:ip family inet hashsize 1024 maxelem 65535 comment
ipset create blocklists-de-permanent_v6 hash:ip family inet6 hashsize 1024 maxelem 65535 comment
```

Install as systemd service
```
cp blocklists_ipset.timer  /etc/systemd/system/
cp blocklists_ipset.service  /etc/systemd/system/

systemctl daemon-reload
systemctl enable blocklists.timer
systemctl enable blocklists.service
```

How to use
============

The script will create the following two sets and load the IPs from the blocklist
into the corresponding IPsec by restoring from two temporary ipset's.

Afterwards, the temporary sets and the permanent sets are swapped.
Then the temporary sets are destroyed and the temporary files deleted.

Errors are written to stderr.
