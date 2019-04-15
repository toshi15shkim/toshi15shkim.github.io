---
layout: post
title: Raspberry Pi 3b+ 외장하드 마운트 하는 방법
excerpt: "라즈베리파이 3b+ 외장하드 마운트"
categories: [Linux]
comments: true
---

## Raspberry Pi 3b+ 외장하드 마운트 하는 방법

라즈베리파이를 개인 Server로 사용하고자 공유기에 연결하고 포트포워딩 작업을 마무리 했다.
하드 용량은 32G로 Server로 사용하기엔 한참 미치지 못하였기에,
남는 외장하드를 연결하면서 있었던 일들과 절차를 기록해본다.

### 시~~작

우선 외장하드를 ntfs로 포맷하고 라즈베리파이에 연결.
그리고 콘솔에 sudo blkid 입력하면
TYPE="ntfs" 기기가 /dev/sda1로 인식되는걸 확인할 수 있다.
> sudo blkid 

![Smithsonian Image](/img/190415/1-sudo blkid.jpg)

ntfs-3g를 설치한다. 
sudo apt-get install ntfs-3g 입력
> sudo apt-get install ntfs-3g 

![Smithsonian Image](/img/190415/2-ntfs3 install err.jpg)

근데..에러가 발생한다.
에러 맨 아래에 보니 apt-get을 업데이트를 하라고 나온다.
업데이트를 해보자.
> sudo apt-get update 

![Smithsonian Image](../img/190415/3-apt-get update.jpg)

업데이트 완료.
다시 ntfs-3g를 설치해보자.
> sudo apt-get install ntfs-3g

![Smithsonian Image](../img/190415/4-re ntfs3 install.jpg)
성공적으로 설치가 되었다. 


마운트가 잘 되었는지 확인해보자.
> df -h

466G 마운트가 되긴 했는데...위치가 좀 이상하다.
![Smithsonian Image](../img/190415/5-auto mount.jpg)

내가 원하는 위치를 잡아줘야 한다.
나의 경우 / 위치에 DATA폴더를 mkdir로 생성했다.
DATA로 마운트를 하기 위한 명령을 입력했다.
> sudo mount /dev/sda1 DATA

![Smithsonian Image](../img/190415/6-auto mount.jpg)
이미 마운트가 되어있다고 나왔다.
/etc/fstab을 수정해보자.

> sudo nano /etc/fstab

![Smithsonian Image](../img/190415/7-nano etc fstab update.jpg)
아래 내용을 추가한다. 간격은 tab이 아닌 space로 띄워줘야 한다.
/dev/sda1     /DATA     ntfs      default     0      0

이제 재부팅을 하고 마운트가 잘 되었나 확인해 보면!
![Smithsonian Image](../img/190415/8-success.jpg)

마운트 성공.



