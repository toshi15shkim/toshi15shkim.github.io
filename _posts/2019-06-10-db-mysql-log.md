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

#### general_log
Mysql에서 실행되는 모든 쿼리를 저장  
default는 OFF로 설정되어 있음  
ON으로 설정해야 로그를 기록함  

```bash
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
mysql> set global general_log_file = '/var/log/mysql/general_mysql.log';
Query OK, 0 rows affected (0.00 sec)

mysql> set global general_log = ON;
Query OK, 0 rows affected (0.00 sec)

```
데이터가 굉장히 빨리 쌓이므로 용량관리에 주의해야 함

slow_query_log
오래걸리는 쿼리에 대한 정보
얼마나 오래 걸리는지에 대해서는 long_query_time 에서 설정하기 나름
```bash
mysql> show variables like 'long_query%';
+-----------------+-----------+
| Variable_name   | Value     |
+-----------------+-----------+
| long_query_time | 10.000000 |
+-----------------+-----------+
1 row in set (0.00 sec)
```

```bash
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
mysql> set global slow_query_log = ON;
Query OK, 0 rows affected (0.01 sec)

mysql> set global slow_query_log_file = '/var/log/mysql/slow-mysql.log';
Query OK, 0 rows affected (0.00 sec)
```

/etc/logrotate.d 를 통해