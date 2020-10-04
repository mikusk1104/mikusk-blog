---
layout: post
title:  "Prepare Syslog Server"
date:   2020-09-21 07:00:00 +0200
categories: syslog
---
# RSYSLOG container (base image Linux ALPINE) - testing

## logrotate

config: /etc/logrotate.d/miklop

   ```
   /logs/miklop.log {
      rotate 4
      daily
      delaycompress
      compress
      copytruncate
   }
   ```
**test: logrotate -v -f /etc/logrotate.d/miklop**

## rsyslogd config

config: /etc/rsyslogd.config

```
$WorkDirectory /var/lib/rsyslog
$FileOwner root
$FileGroup adm
$FileCreateMode 0640
$DirCreateMode 0755
$Umask 0022
include(file="/etc/rsyslog.d/*.conf" mode="optional")
module(load="imudp")
input(
        type="imudp"
        port="514"
)

template(name="FileFormat" type="list") {
constant(value="{\"time\":\"")
property(name="timestamp" dateFormat="rfc3339")
constant(value="\",\"syslogtag\":\"")
property(name="syslogtag")
constant(value="\",\"msg\":\"")
property(name="msg" spifno1stsp="on" )
property(name="msg" droplastlf="on" )
constant(value="\"}\n")
}

action(type="omfile" file="/logs/miklop.log" template="FileFormat")
```
## Dockerfile
```
FROM alpine

RUN apk add --no-cache \
        rsyslog \
        logrotate

COPY rsyslog.conf /etc/
COPY miklop /etc/logrotate.d/
COPY start_syslog_cron /usr/local/bin/start_syslog_cron

RUN chmod +x /usr/local/bin/start_syslog_cron


EXPOSE 514/udp

CMD /usr/local/bin/start_syslog_cron

```
## start_syslog_cron
```
#!/bin/ash
crond
rsyslogd -n -f/etc/rsyslog.conf

```

## build image
```
git clone https://github.com/mikusk1104/miklop/
docker build -t mikusk/miklop_rsyslog .
```
## run image
```
docker run -d --restart unless-stopped --name=miklop_rsyslog -p 514:514/udp -v miklop_logs:/logs mikusk/miklop_rsyslog
docker exec -it rsyslog-1 ./bin/ash

```
## volume for logs
```
docker volume inspect logs
```
**/var/lib/docker/volumes/logs/_data**

