---
layout: post
title:  "Prepare Syslog Server"
date:   2020-09-21 07:00:00 +0200
categories: syslog
---
# Notes:
1. time zone in UTC so all times will be +00:00
2. log line config:

   ```
   template(name="FileFormat" type="list") {
   constant(value="{\"time\":\"")
   property(name="timestamp" dateFormat="rfc3339")
   constant(value="\",\"syslogtag\":\"")
   property(name="syslogtag")
   constant(value="\",\"msg\":\"")
   property(name="msg" spifno1stsp="on" )
   property(name="msg" droplastlf="on" )
   constant(value="\"}\n")
   ```

3. setup log rotate