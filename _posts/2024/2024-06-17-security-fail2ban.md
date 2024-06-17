---
layout: post
title: Rocky Linux 9 - Fail2ban 설치하기
excerpt: "Fail2ban"
categories: [Security]
comments: true
---

Fail2ban은 Rocky Linux의 기본 소프트웨어 저장소에서 사용할 수 없다.

그러나 RedHat, Rocky의 타사 패키지에 사용되는 EPEL에서 사용이 가능하다.
<br/>
```bash
# 아래 명령어를 수행하면 fain2ban을 찾을 수 없다는 메시지가 나온다.
$ yum install fail2ban
```

  ![Smithsonian Image](/img/2024/240617/1.rocky9_fail2ban.jpg){: width="650"}

<br/>
<br/>
<br/>

아래 명령어로 epel-release 패키지를 설치한다.
```bash
$ dnf install epel-release -y
```

<br/>
epel-release 패키지 설치가 완료되었다.
<br/>

  ![Smithsonian Image](/img/2024/240617/2.rocky9_fail2ban.jpg){: width="700"}
<br/>
<br/>
<br/>
이제 아래 명령어로 fail2ban 설치가 가능하다.
```bash
$ dnf install fail2ban -y
```

<br/>
<br/>

fail2ban 상태 확인
```bash
$ systemctl status fail2ban.service
```
  ![Smithsonian Image](/img/2024/240617/3.rocky9_fail2ban.jpg){: width="700"}
<br/>
<br/>
<br/>

```bash
# fail2ban 디렉토리로 이동
$ cd /etc/fail2ban

# jail.conf 파일을 복사하여 jail.local 파일을 만든다.
$ cp jail.conf jail.local
```

<br/>

```bash
$ vi /etc/fail2ban/jail.local

# 클라이언트가 올바른 인증을 하지 못할 경우 차단되는 기간 설정. (default 10분)
bantime = 10m


# 10분 이내에 5번 로그인 시도에 실패한 클라이언트 차단.
findtime = 10m
maxretry = 5


[sshd]

# To use more aggressive sshd modes set filter parameter "mode" in jail.local:
# normal (default), ddos, extra or aggressive (combines all).
# See "tests/files/logs/sshd" or "filter.d/sshd.conf" for usage example and details.
#mode   = normal

    enabled = true    #######해당부분 추가 (enabled = true)#######
port    = ssh
logpath = %(sshd_log)s
backend = %(sshd_backend)s

```
<br/>

fail2ban 시작 명령어
```bash
systemctl start fail2ban
```