---
layout: post
title:  "Linux cheasheet"
date:   2017-01-10 22:18:00
categories: cheatsheet,linux
comments: true
---
## Pass result of `awk` into `kill` or another command

`docker ps -a | grep houston | awk '{print $1}' | xargs docker rm`

**Search replace `=enforcing` to `=permissive` in file**
```bash
sudo sed -i 's\=enforcing\=permissive\g' /etc/sysconfig/selinux
```

## Get public key for example to https://google.com

`$ openssl s_client -connect google.com:443 | openssl x509 -pubkey -noout`

## Timestamp to hours since start day

`awk '$3/3600000-int($3/86400000)*24+3<13 {print $3, $2, $4}'`

1. `/3600000` - unix time in hours units.
2. `/86400000` - unix time in days units.
3. `*24` - start of today in hours units.
4. `+3` - increase 3 hours to align to our timezone.

## TCPDUMP Textual

```bash
tcpdump -A -iany port 8080 -w scoring-conf-req.tcpdump
```

## Which process listens on port

```bash
lsof -n -i:4888 | grep LISTEN
```

`-n` causes it to run much faster (do not resolve host names)

** iptables **

`/etc/sysconfig/iptables` (iptables configuration)

allow remote connections to port 8140

`-A INPUT -m state --state NEW -m tcp -p tcp --dport 8140 -j ACCEPT`

* `-A`: We are appending a rule.
* `INPUT`: The rule applies to incoming packets.
* `-m tcp -p tcp --dport 8140`: The rule applies to `tcp` port 8140.
* `ACCEPT`: iptables should accept the packets.

reload iptables

`sudo service iptables restart `