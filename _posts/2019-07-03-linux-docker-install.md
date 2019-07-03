---
layout: post
title: Raspberry Pi 3b+ Docker 설치하기
excerpt: ""
categories: [Linux]
comments: true
---

## Raspberry Pi 3b+ Docker 설치하기

라즈베리파이의 메모리는 1G 밖에 안된다.  
이런 환경에서 Docker가 돌아갈까?  
타 블로그에서는 충분히 가능하다고 하는데...  
직접 경험해 보지 않고선 모르는거 아니겠나!!  

<br/>

pi로 접속해서 아래 명령어를 입력하여 docker를 다운로드 받는다.
>sudo curl -fsSL https://get.docker.com/ | sudo sh

```bash
pi@raspberrypi:/ $ sudo curl -fsSL https://get.docker.com/ | sudo sh
# Executing docker install script, commit: 2f4ae48
+ sh -c apt-get update -qq >/dev/null
+ sh -c apt-get install -y -qq apt-transport-https ca-certificates curl >/dev/null
+ sh -c curl -fsSL "https://download.docker.com/linux/raspbian/gpg" | apt-key add -qq - >/dev/null
Warning: apt-key output should not be parsed (stdout is not a terminal)
+ sh -c echo "deb [arch=armhf] https://download.docker.com/linux/raspbian stretch stable" > /etc/apt/sources.list.d/docker.list
+ sh -c apt-get update -qq >/dev/null
+ [ -n  ]
+ sh -c apt-get install -y -qq --no-install-recommends docker-ce >/dev/null
+ sh -c docker version
Client:
 Version:           18.09.0
 API version:       1.39
 Go version:        go1.10.4
 Git commit:        4d60db4
 Built:             Wed Nov  7 00:57:21 2018
 OS/Arch:           linux/arm
 Experimental:      false

Server: Docker Engine - Community
 Engine:
  Version:          18.09.0
  API version:      1.39 (minimum version 1.12)
  Go version:       go1.10.4
  Git commit:       4d60db4
  Built:            Wed Nov  7 00:17:57 2018
  OS/Arch:          linux/arm
  Experimental:     false

```