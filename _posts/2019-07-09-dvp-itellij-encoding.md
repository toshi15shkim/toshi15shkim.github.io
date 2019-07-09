---
layout: post
title: 인텔리J UTF-8 인코딩
excerpt: ""
categories: [Development]
comments: true
---

## 인텔리J UTF-8 인코딩

File > Settings > Editor > File Encodings  
UTF-8로 설정

  ![Smithsonian Image](/img/190709/1.settings.jpg){: width="1000"}

<br/>

Run > Edit Configurations  
VM options : -Dfile.encoding=UTF-8 입력

  ![Smithsonian Image](/img/190709/2.Run.jpg){: width="1000"}

<br/>

JetBrains > 인텔리J폴더 > bin  
idea64.exe.vmoptions 파일 내용 편집  
맨 밑에 추가  

> -Dfile.encoding=UTF-8