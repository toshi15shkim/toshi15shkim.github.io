---
layout: post
title: FTP(File Transfer Protocol) 2가지 mode
excerpt: "FTP"
categories: [Security]
comments: true
---

## FTP(File Transfer Protocol) 2가지 mode

> FTP는 TCP/IP에 의해 제공되는 파일 전송 표준 프로토콜이다.  
제어 접속 포트와 데이터 접속 포트가 분리되어 있다.  
Active Mode와 Passive Mode가 있는데, 사용 여부는 클라이언트가 결정한다.
   
<br/>

### __Active Mode__
- FTP의 기본 설정 값이다.
- 서버에서는 20, 21 두 개의 포트만 오픈하면 된다.  
  
  ![Smithsonian Image](/img/190520/active_mode.jpg)

1. 클라이언트에서 서버 21번 포트로 접속을 시도하며 클라이언트의 데이터 포트 5151를 알려준다.
2. 서버는 연결을 확인한다.
3. 서버의 20번 데이터 포트가 클라이언트의 5151포트에 데이터 전송을 요청한다.
4. 연결 완료.

<br/>
<br/>

### __Passive Mode__
- 서버에서 클라이언트로 접근해야 하는 모순을 해결하기 위한 방식이다.
- 서버는 데이터 전송을 위해 1024 이후의 모든 포트를 오픈해야 한다.  
 
  ![Smithsonian Image](/img/190520/passive_mode.jpg)

1. 클라이언트에서 서버의 21번 포트로 접속한다.
2. 서버는 접근가능한 데이터 포트 3267을 클라이언트에 알려준다.
3. 클라이언트는 전달 받은 데이터 포트로 접속을 시도한다.
4. 연결 완료.