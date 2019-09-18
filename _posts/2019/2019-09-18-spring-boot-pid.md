---
layout: post
title: Boot로 실행시 pid 자동 생성 방법
excerpt: "프로세스 아이디를 몰라서 grep으로 찾아야 했던 과거를 잊자"
categories: [Spring]
comments: true
---

## Spring Boot로 실행시 pid 자동 생성 방법

스프링 부트를 종료할 때 프로세스 아이디를 몰라서 grep 노가다를 했던 기억이 난다.  

노가다 시간을 줄여서 개발에 집중하도록 하자.

<br/>

```bash
#application.yml에 추가
spring:
  pid:
    file: boot-paas.pid # 파일명은 ***.pid 형식
```

<br/>

### 기존 main은 이렇게 생겼었다.
```java
public class PaaSApplication {
	public static void main(String[] args) {
		SpringApplication.run(PaaSApplication.class, args);
	}
}
```

<br/>

### 아래처럼 변경해준다.
```java
public class PaaSApplication {
	public static void main(String[] args) {
		SpringApplication application = new SpringApplication(PaaSApplication.class);
		application.addListeners(new ApplicationPidFileWriter());
		application.run(args);
	}
}
```

<br/>

### 시작/종료 간단한 shell 작성
```bash
#간단한 shell script 작성
vi start.sh
java -jar 파일명.war &

vi stop.sh
kill -9 `cat boot-paas.pid`
```