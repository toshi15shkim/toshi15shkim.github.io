---
layout: post
title: Java 현재 시간 + 랜덤 문자로 고유한 Unique 값 만들기
excerpt: "SimpleDateFormat + Calendar + RandomStringUtils"
categories: [Java]]
comments: true
---

## Java 현재 시간 + 랜덤 문자로 고유한 Unique 값 만들기

### RandomStringUtils 을 사용하기 위해서는 commons-lang3이 필요하다.   
### build.gradle 에 아래 항목을 추가한다.

```bash
compile 'org.apache.commons:commons-lang3:3.0'
```

<br/>

### yyyyMMddHHmmssSSS_랜덤문자6개 생성

```java
import java.text.SimpleDateFormat;
import java.util.Calendar;

import org.apache.commons.lang3.RandomStringUtils;

public class CommonUtils {
    //고유 아이디 만들기 (yyyyMMddHHmmssSSS_랜덤문자6개)
    public static String getUniqueId() {
        String uniqueId = "";
        SimpleDateFormat sdf = new SimpleDateFormat("yyyyMMddHHmmssSSS");
        Calendar dateTime = Calendar.getInstance();
        uniqueId = sdf.format(dateTime.getTime());
            
        //yyyymmddhh24missSSS_랜덤문자6개
        uniqueId = uniqueId+"_"+RandomStringUtils.randomAlphanumeric(6);

        return uniqueId;
    }
}
```

<br/>

### 메소드를 실행하면 고유값을 리턴한다.

```bash

20191008102330130_EiHRzo
```