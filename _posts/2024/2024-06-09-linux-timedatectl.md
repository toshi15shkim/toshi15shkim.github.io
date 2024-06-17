---
layout: post
title: Rocky Linux 9 - 한국 시간으로 재설정하기
excerpt: ""
categories: [Linux]
comments: true
---

Rocky Linux에서는 rdate 명령어 대신 timedatectl로 시간을 설정한다.
<br/>
현재 해당 서버는 UST로 설정되어 있다.
<br/>
```bash
$ timedatectl
```

  ![Smithsonian Image](/img/2024/240609/1.timedatectl.jpg){: width="500"}

<br/>
<br/>
<br/>

아래 명령어로 시간을 변경한다.
<br/>
```bash
$ timedatectl set-timezone Asia/Seoul
```

<br/>
timedatectl 명령어로 재확인하면 서울시간으로 변경된 것을 확인할 수 있다.
<br/>

  ![Smithsonian Image](/img/2024/240609/2.timedatectl.jpg){: width="500"}

<br/>