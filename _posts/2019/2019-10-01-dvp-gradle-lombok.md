---
layout: post
title: [Gradle+Lombok] 빌드에서 cannot find symbol 에러 날 때
excerpt: "gradle/lombok 빌드시 cannot find symbol 에러 발생"
categories: [Development]
comments: true
---

## [Gradle+Lombok] 빌드에서 cannot find symbol 에러 날 때

<br/>

### build.gradle lombok 부분을 아래 내용으로 치환하고 실행한다.  

```bash
compileOnly 'org.projectlombok:lombok'
annotationProcessor 'org.projectlombok:lombok'
```