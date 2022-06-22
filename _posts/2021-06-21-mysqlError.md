---
layout: single
title: "[MySQL] 에러: Could not acquire management access for administration"
categories: MySQL
tag: [MySQL, Error]
toc: true
toc_sticky: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

MySQL Workbench는 이전까지 잘 쓰고 있었는데

![image-20220621235435082](/images/2021-06-21-mysqlError/image-20220621235435082.png)

이 화면에 들어가기 위해 `Administration>Server Status` 탭을 누르니 아래와 같은 에러가 떴다. 

![image-20220621235235176](/images/2021-06-21-mysqlError/image-20220621235235176.png)

##### 1. ~~환경 변수 추가~~ → **실패**

이 에러창이 말하는대로 PATH 에 변수를 추가하러 갔지만, 이미 `C:\Windows\System32`는 추가가 되어 있었다. 혹시 몰라서 MySQL이 저장경로인 `C:\Program Files\MySQL\MySQL Server 8.0` 도 추가해보고 `C:\Program Files\MySQL\MySQL Server 8.0\bin`도 추가 해봤지만 이 에러는 계속 떴다.



##### 2. 언어 설정 UTF-8로 변경 

https://mondaymonday2.tistory.com/m/488 이 블로그를 참고해서 아래와 같이 언어설정에서 `Unicode UTF-8 사용` 을 체크하고 컴퓨터 재부팅을 하고 나니 에러가 사라졌다.

![image-20220622000209760](/images/2021-06-21-mysqlError/image-20220622000209760.png)
