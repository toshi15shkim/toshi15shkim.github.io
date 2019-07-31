---
layout: post
title: VSCode(Visual Studio Code)로 spring boot 프로젝트 만들기
excerpt: ""
categories: [Development]
comments: true
---

## VSCode(Visual Studio Code)로 spring boot 프로젝트 만들기 (feat.gradle)

상단 메뉴에서 View > Command Pallette를 선택한다. (단축키 Ctrl + Shift + P)  
아래와 같이 목록이 나오는데, Spring Initializr: Generate a Gradle Project 를 선택한다.

  ![Smithsonian Image](/img/2019/190725/1.command_palette.jpg){: width="1000"}

<br/>

Java를 선택한다.

  ![Smithsonian Image](/img/2019/190725/2.java.jpg){: width="1000"}

<br/>

Java 소스의 root 폴더명을 입력한다.

  ![Smithsonian Image](/img/2019/190725/3.name.jpg){: width="1000"}

<br/>

Java 소스의 root 폴더 하위명을 입력한다. (귀찮...)

  ![Smithsonian Image](/img/2019/190725/4.project_name.jpg){: width="1000"}

<br/>

Spring boot 버전을 선택한다. (필자는 2.1.7 SNAPSHOT 선택)

  ![Smithsonian Image](/img/2019/190725/5.boot_version.jpg){: width="1000"}

<br/>

추가할 dependency를 선택한다.  
나는 Spring Web Starter / Spring Boot DevTools 를 추가했다.

  ![Smithsonian Image](/img/2019/190725/6.dependencies.jpg){: width="1000"}

<br/>

Ctrl + E 키를 누르면 파일을 찾는 input 창이 열린다.  
application.properties 파일을 찾고, 확장자를 .yml로 수정한다.  
 > application.properties -> application.yml  

그리고 아래 내용을 입력한다.
```bash
spring:
  mvc:
    view:
      prefix: /WEB-INF/jsp/
      suffix: .jsp
```

<br/>

```xml
plugins {
	id 'org.springframework.boot' version '2.1.7.BUILD-SNAPSHOT'
	id 'java'
}

apply plugin: 'io.spring.dependency-management'

group = 'com.kth'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = '1.8'

configurations {
	developmentOnly
	runtimeClasspath {
		extendsFrom developmentOnly
	}
}

repositories {
	mavenCentral()
	maven { url 'https://repo.spring.io/milestone' }
	maven { url 'https://repo.spring.io/snapshot' }
}

dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-web'
	developmentOnly 'org.springframework.boot:spring-boot-devtools'
	testImplementation 'org.springframework.boot:spring-boot-starter-test'
	implementation 'org.apache.tomcat.embed:tomcat-embed-jasper'
}
```