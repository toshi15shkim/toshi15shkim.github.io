---
layout: post
title: Window에 kafka 설치하기
excerpt: ""
categories: [Window]
comments: true
---

## Window에 kafka 설치하기

1. https://kafka.apache.org/downloads 접속  
(저는 Scala 2.11  - kafka_2.11-2.3.0.tgz 를 받았습니다.)

2. 적당한 위치에 압출을 풀고, config 폴더에 들어간다.

3. bin폴더에 sh파일들만 있는데, 윈도우 실행용 bat파일은 windows 폴더안에 들어있다.

4. 한가지 알아둬야 할 점은, kafka는 zookeeper와 함께 작동되기 때문에 kafka 소스에 zookeeper도 포함되어 있다.  
kafka는 broker를 기준으로 클러스터링 되어 topic을 관리하는데 zookeeper가 분산 처리 및 kafka의 노드를 관리해준다.  

5. 반드시 zookeeper를 먼저 실행 후 kafka를 실행해야 한다.  
zookeeper-server-start.bat 뒤에 zookeeper.properties를 붙여준다.  

```bash
##예시
%KAFKA_HOME%\bin\windows\zookeeper-server-start.bat %KAFKA_HOME%\config\zookeeper.properties

##필자가 실행한 구문
D:\develop\kafka_2.11-2.3.0\bin\windows\zookeeper-server-start.bat D:\develop\kafka_2.11-2.3.0\config\zookeeper.properties
```

6. kafka를 실행한다.

```bash
%KAFKA_HOME%\bin\windows\kafka-server-start.bat %KAFKA_HOME%\config\server.properties

D:\develop\kafka_2.11-2.3.0\bin\windows\kafka-server-start.bat D:\develop\kafka_2.11-2.3.0\config\server.properties
```

