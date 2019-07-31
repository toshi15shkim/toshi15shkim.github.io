---
layout: post
title: Docker의 모든 컨테이너 / 이미지 삭제하는 명령어
excerpt: "CentOS 7.6"
categories: [Linux]
comments: true
---

## Docker의 모든 컨테이너 / 이미지 삭제하는 명령어

```bash
#모든 도커 컨테이너 Stop
docker stop $(docker ps -a -q)

#모든 도커 컨테이너 Remove
docker rm $(docker ps -a -q)

#모든 도커 이미지 Remove
docker rmi $(docker images -q)
```