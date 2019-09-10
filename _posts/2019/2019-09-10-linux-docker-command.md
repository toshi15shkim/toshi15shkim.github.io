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

