---
layout: post
title: PostgreSQL 명령어 모음
excerpt: ""
categories: [DB]
comments: true
---

## PostgreSQL 명령어 모음

<br/>

### 사용자 목록 조회 1 (유저 및 권한 요약)
```bash
postgres=$ \du


                                   List of roles
 Role name |                         Attributes                         | Member of
-----------+------------------------------------------------------------+-----------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS | {}

```

<br/>

### 사용자 목록 조회 2
```bash
postgres=$ select * from pg_user;


 usename  | usesysid | usecreatedb | usesuper | userepl | usebypassrls |  passwd  | valuntil | useconfig
----------+----------+-------------+----------+---------+--------------+----------+----------+-----------
 postgres |       10 | t           | t        | t       | t            | ******** |          |
(1 row)
```

<br/>

### 사용자 생성
```bash
create user <아이디> with encrypted password '<비밀번호>';
```

<br/>

### 사용자 비밀번호 변경
```bash
alter user <아이디> with password '<비밀번호>';
```

<br/>

### DB 생성 / 소유주 설정
```bash
create database <DB명>> owner <아이디>;
```

<br/>

### 테이블 목록 조회
```bash
postgres=$ \l


                             List of databases
   Name    |  Owner   | Encoding  | Collate | Ctype |   Access privileges
-----------+----------+-----------+---------+-------+-----------------------
 paasdb    | paas     | SQL_ASCII | C       | C     |
 postgres  | postgres | SQL_ASCII | C       | C     |
 template0 | postgres | SQL_ASCII | C       | C     | =c/postgres          +
           |          |           |         |       | postgres=CTc/postgres
 template1 | postgres | SQL_ASCII | C       | C     | =c/postgres          +
           |          |           |         |       | postgres=CTc/postgres
(4 rows)
```

<br/>

### DB 백업/복원
```bash
#백업
pg_dump 디비명 > 파일명
ex) pg_dump paasdb > /DATA/db.sql

#복원
psql -f 파일명 디비명
ex) psql -f /DATA/db.sql paasdb
```