---
layout: post
title:  "Miklop Notes (src / GIT / container)"
date:   2020-09-22 14:30:00 +0200
categories: miklop
---
# Miklop Notes (src / GIT / container)

## Source Code
Ubuntu on WSL2
```
/home/mikusk/miklop
\\wsl$\Ubuntu-20.04\home\mikusk\miklop
```

## GIT
Remote already added: git remote add miklop <https://github.com/mikusk1104/miklop>
```
cd /home/mikusk/miklop
git status
git add .
git commit -m „message“
git push miklop master
```

## Container
Source folder: /home/pi/miklop-image<br/>
Prepare src folder: git clone <https://github.com/mikusk1104/miklop/>

**DockerFile**
```
FROM python:3.8

WORKDIR /code

RUN pip install pytz
RUN pip install tzlocal
RUN pip install influxdb

COPY miklop/src_new/ .

ENTRYPOINT ["python", "miklop_starter.py"]
```

**Build image:**
```
docker build -t miklop .
```

**Volumes:**
```
miklop_data - /var/lib/docker/volumes/miklop_data/_data
miklop_logs - /var/lib/docker/volumes/miklop_logs/_data
```

**Start Container:**
```
docker run -d --restart unless-stopped --name=miklop -v miklop_logs:/logs -v miklop_data:/data miklop
```

