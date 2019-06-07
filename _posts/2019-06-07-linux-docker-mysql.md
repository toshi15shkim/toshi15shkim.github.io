---
layout: post
title: Docker로 Mysql DB 이중화(Replication) 방법
excerpt: "Mysql"
categories: [Linux]
comments: true
---

## Docker로 Mysql DB 이중화(Replication) 방법
DB를 이중화해야 하지만 개발형편상 서버 추가는 어려운 상황이였다.  
그래서 기존 서버는 그대로 두고 docker로 Mysql을 추가 설치해서 이중화 하기로 결정했다.

> - Master DB는 설치된 그대로 유지
> - Docker로 Slave DB를 설치하여 이중화

<br/>

우선 Docker부터 설치하고 mysql을 검색한다.
```bash
$ yum install -y docker
$ docker search mysql
```

 ![Image](/img/190607/1_docker_search_mysql.jpg)

수 많은 mysql 이미지 중 docker.io/mysql을 받는다.
```bash
$ docker pull docker.io/mysql
```
![Image](/img/190607/2_docker_pull_mysql.jpg)

<br/>

도커 이미지를 확인하고 run을 해준다.
```bash
$ docker images
$ docker run -d -p 13306:3306 -e MYSQL_ROOT_PASSWORD=패스워드 --name mysql-slave mysql
# 외부에서 접속은 13306포트 // 내부는 3306으로 연결
```

```bash
#slave 도커 접속
$ docker exec -it mysql-slave bash

#위에서 설정한 비빌번호 입력해서 mysql 접속
$ mysql -u root -p

#디비생성
$ create database TSCPDB4;
$ exit #빠져나옴
```

<br/>

Master가 되는 기존 디비를 덤프 뜬다
```bash
$ mysqldump -u neighbor -p TSCPDB4 > TSCPDB4_dump.sql  

#slave 도커에 Copy
$ docker cp /DATA/TSCPDB4_dump.sql mysql-slave:.

#slave 도커 접속
$ docker exec -it mysql-slave bash 접속

#덤프 뜬 디비 옮기기
$ mysql -u root -p TSCPDB4 < TSCPDB4_dump.sql

#slave에 계정 생성
$ create user '아이디'@'%' identified with mysql_native_password by '비밀번호';

#권한설정
$ grant all privileges on TSCPDB4.* to '아이디'@'%';
```

<br/>

Master mysql에 접속해서 Replication slave 권한 설정

```bash
$ grant replication slave on *.* to '아이디'@'%'  
```

<br/>

Master /etc/my.cnf 파일에 아래내용 입력
> log-bin=mysql-bin  
> server-id=1  (숫자 입력해야 함)

Mysql 재시작
> systemctl restart mysqld

<br/>

Master mysql에서 show master status; 입력

![Image](/img/190607/5_show_master_status.jpg)

위의 내용을 slave에 넣어야 하므로 slave 접속  

> slave에서 vi안되는 현상 발견 (툴이 거의 없다고 봐야 됨)  
> apt-get update  
> apt-get install vim 설치

<br/>

Slave /etc/mysql/my.cnf 파일에 아래내용 입력
> server-id=2  
> replicate-do-db='TSCPDB4'

Mysql 접속해서 Master에 대한 정보 입력
```bash
mysql> change master to
    -> master_host='마스터아이피',
    -> master_user='아이디',
    -> master_password='비밀번호!',
    -> master_log_file='mysql-bin.000001',
    -> master_log_pos=6274;
```

<br/>

```bash
#빠져나와서 docker restart mysql-slave 실행
$ docker restart mysql-slave

#slave 들어가서 slave 상태 확인
$ mysql> show slave status\G;
```
![Image](/img/190607/6_complete.jpg)

>Last_Errno : 0  
>Last_IO_Errno : 0 이 찍혀야 함

### MySQL 이중화 완성~!