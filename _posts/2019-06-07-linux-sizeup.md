---
layout: post
title: 리눅스 (CentOS) home 용량 줄이고, root 용량 늘리기
excerpt: "CentOS 7.6"
categories: [Linux]
comments: true
---

## 리눅스(CentOS) home 용량 줄이고, root 용량 늘리기

### 환경 : CentOS 7.6 기준  
### /dev/mapper/centos-home을 삭제하고 /dev/mapper/centos-root만 활용

사내 개발서버를 점검하던 중 root에 50G만 할당되어 있고, home에 2TB가 할당되어 있는 현상을 발견했다.  
불필요한 /dev/mapper/centos-home을 삭제하는 방법에 대해 기술하였다.

<br/>

home 폴더를 압축하여 백업한다
> tar -zcf /home.tar.gz -C /home .  

<br/>

home 언마운트
> umount /dev/mapper/centos-home

<br/>

centos-home 삭제
> lvremove /dev/mapper/centos-home

<br/>

root에 남은 모든 용량 100%를 할당

> lvextend -r -l +100%FREE /dev/mapper/centos-root

<br/>

home 생성

> mkdir /home

<br/>

home 디렉토리 복구

> tar -zcf /home.tar.gz -C /home

