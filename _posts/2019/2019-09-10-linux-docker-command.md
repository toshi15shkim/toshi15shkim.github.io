---
layout: post
title: Docker의 기본적인 명령어 모음
excerpt: "CentOS 7.6"
categories: [Linux]
comments: true
---

## Docker의 기본적인 명령어 모음

#### 이미지 관련 명령어
```bash
#CentOS 이미지 다운로드
docker pull centos
```

```bash
#이미지 목록 확인
docker images
```

```bash
#이미지 삭제
docker rmi <이미지ID>
```

<br/>

#### 컨테이너 관련 명령어
```bash
#현재 실행중인 컨테이너 확인
docker ps
```

```bash
#정지된 컨테이너까지 확인
docker ps -a
```

```bash
#컨테이너 실행 (--rm 옵션을 사용하면 프로세스 종료시 컨테이너를 자동 삭제한다.)
docker run --rm -it <이미지ID> /bin/bash

#컨테이너명, 포트연결까지 하는 옵션
docker run -it --name <컨테이너명> -p 8081:80 <이미지ID> bash

#컨테이너 접속 (exit로 빠져나와도 컨테이너가 종료되지 않음)
docker exec -it <컨테이너명 또는 컨테이너ID> bash

#만들어진 컨테이너 실행
docker start <컨테이너명 또는 컨테이너ID>
```

<br/>

#### 도커에 파일 복사
```bash
#로컬에서 컨테이너로 파일 복사
docker cp <원본파일> <컨테이너명>:/<복사할위치>
ex) docker cp /home/paas/nginx.tar.gz paas:/home
```

<br/>

#### 이미지 추출 / Load
```bash
#이미지 추출하기
docker save -o <파일명.tar> <이미지ID>
```

```bash
#이미지 로드하기
docker load -i <파일명.tar>
```

