---
layout: post
title:  "Miklop Notes (src / GIT / container)"
date:   2020-09-22 14:30:00 +0200
categories: syslog
---
# Miklop Notes (src / GIT / container)

## Source Code
Ubuntu on WSL2
```
/home/mikusk/miklop
\\wsl$\Ubuntu-20.04\home\mikusk\miklop
```

## GIT
Remote already added: git remote add miklop https://github.com/mikusk1104/miklop
```
cd /home/mikusk/miklop
git status
git add .
git commit -m „message“
git push miklop master
```

## Container
Source folder: /home/pi/miklop-image
prepare src folder: git clone https://github.com/mikusk1104/miklop/

**DockerFile**
```
FROM python:3.8

WORKDIR /code

RUN pip install pytz
RUN pip install tzlocal
RUN pip install influxdb

COPY miklop/src/ .

ENTRYPOINT ["python", "miklop.py", "-c", "/data/config.ini"]
```

**Build image:**
```
docker build -t miklop-2 .
```

**Volumes:**
```
miklop_data - /var/lib/docker/volumes/miklop_data/_data
miklop_logs - /var/lib/docker/volumes/miklop_logs/_data
```

**Start Container:**
```
docker run -d --rm --log-driver json-file --log-opt max-size=10m --name=miklop-2 -v miklop_logs:/logs -v miklop_data:/data miklop-2
```

**Check Logs:**
```
docker logs -f miklop-2
```

