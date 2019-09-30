---
layout: post
title: 리눅스(Centos 7.6) FFMPEG 설치하기
excerpt: ""
categories: [ETC]
comments: true
---

## 리눅스(Centos 7.6) FFMPEG 설치하는 명령어 (yum)

<br/>


```bash
yum -y install epel-release

rpm --import http://li.nux.ro/download/nux/RPM-GPG-KEY-nux.ro

rpm -Uvh http://li.nux.ro/download/nux/dextop/el7/x86_64/nux-dextop-release-0-5.el7.nux.noarch.rpm

yum install ffmpeg
```