---
layout: post
title: Mysql Log 설정 정리
excerpt: "Mysql"
categories: [DB]
comments: true
---

## Mysql Log 설정 정리
Web/WAS 로그도 중요하지만, DB로그도 운영에 있어서 소홀히 할 수 없다.  
그래서 Mysql 쿼리 로그를 설정했던 경험을 기록해보기로 했다.

<br/>

#### general_log
Mysql에서 실행되는 모든 쿼리를 저장  
default는 OFF로 설정되어 있음  
ON으로 설정해야 로그를 기록함  

```bash
#general_log 확인
mysql> show variables like 'general%';
+------------------+------------------------------+
| Variable_name    | Value                        |
+------------------+------------------------------+
| general_log      | OFF                          |
| general_log_file | /var/lib/mysql/localhost.log |
+------------------+------------------------------+
2 rows in set (0.00 sec)
```

<br/>

```bash
#사용여부 ON
mysql> set global general_log = ON;
Query OK, 0 rows affected (0.00 sec)

#로그 위치변경
mysql> set global general_log_file = '/var/log/mysql/general_mysql.log';
Query OK, 0 rows affected (0.00 sec)
```
데이터가 굉장히 빨리 쌓이므로 용량관리에 주의해야 함

<br/>

#### slow_query_log
설정된 시간보다 오래걸리는 쿼리를 저장  
얼마나 오래 걸리는지에 대해서는 long_query_time 에서 설정하기 나름
```bash
#long_query_time 확인
mysql> show variables like 'long_query%';
+-----------------+-----------+
| Variable_name   | Value     |
+-----------------+-----------+
| long_query_time | 10.000000 |
+-----------------+-----------+
1 row in set (0.00 sec)
```

```bash
#slow_query_log 확인
mysql> show variables like 'slow%';
+---------------------+-----------------------------------+
| Variable_name       | Value                             |
+---------------------+-----------------------------------+
| slow_launch_time    | 2                                 |
| slow_query_log      | OFF                               |
| slow_query_log_file | /var/lib/mysql/localhost-slow.log |
+---------------------+-----------------------------------+
3 rows in set (0.00 sec)
```

<br/>

```bash
#사용여부 ON
mysql> set global slow_query_log = ON;
Query OK, 0 rows affected (0.01 sec)

#로그 위치변경
mysql> set global slow_query_log_file = '/var/log/mysql/slow-mysql.log';
Query OK, 0 rows affected (0.00 sec)
```

<br/>

#### logrotate
logrotate를 사용하지 않으면 로그파일이 무한정 커진다.  
/etc/logrotate.d 폴더의 mysql 파일에 세팅값을 설정한다. (없으면 생성)  
```bash
/var/log/mysql/general-mysql.log {
        create 640 mysql mysql
        notifempty
        daily
        rotate 50
        missingok
        dateext
        postrotate
               # just if mysqld is really running
               if test -x /usr/bin/mysqladmin && \
                  /usr/bin/mysqladmin ping &>/dev/null
               then
                  /usr/bin/mysqladmin flush-logs
               fi
        endscript
}
```