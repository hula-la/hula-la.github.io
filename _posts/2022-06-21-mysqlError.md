---
layout: single
title: "쿠버네티스, 컨테이너, 도커 개념 정리"
categories: 클라우드
tag: [쿠버네티스, 컨테이너, 도커]
toc: true
toc_sticky: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

# 쿠버네티스 1편

###### 쿠버네티스와 컨테이너, 도커에 대한 기본 개념



##### Q. 쿠버네티스는 컨테이너를 오케스트레이션 하는 도구라는 글을 많이 봤어요. 도커는 컨테이너를 다루는 도구라고 설명하던데, 그렇다면 쿠버네티스는 도커를 다루는 도구인가요?

##### A. 아니요. 쿠버네티스의 역할은 컨테이너를 분산 배치, 상태 관리 및 컨테이너의 구동 환경까지 관리해 주는 도구이고,  도커는 컨테이너를 다루는 도구(컨테이너 런타임) 중 하나이다. 쿠버네티스는 컨테이너를 다루기 위해 도커 이외에도 다양한 컨테이너 런타임 소프트웨어를 사용할 수 있다.



#### 📌 용어에 대한 정리

1. **컨테이너**: 앱이 구동되는 환경까지 감싸서 실행할 수 있도록 하는 격리 기술
2. **컨테이너 런타임**: 컨테이너를 다루는 도구
3. **도커**: 컨테이너를 다루는 도구 중 가장 유명한 것
4. **쿠버네티스**: 컨테이너 런타임을 통해 컨테이너를 오케스트레이션 하는 도구
5. **오케스트레이션**: 여러 서버에 걸친 컨테이너 및 사용하는 환경 설정을 관리하는 행위



### 컨테이너

 **컨테이너란, 우리가 구동하려는 애플리케이션을 실행할 수 있는 환경까지 감싸서, 어디서든 쉽게 실행할 수 있도록 해 주는 기술**이다.

 컨테이너 환경을 묶어서 배포한 컨테이너 이미지라는 프로그램을 내려받아 구동하면 실행되기 때문에, 각종 설정 과정이 줄어 들어서 편하게 사용 가능.

 **컨테이너 런타임이란, 컨테이너를 사용할 때 필요한 도구**이다. 컨테이너를 쉽게 내려받거나 공유하고 구동할 수 있도록 해주는 도구이며, 그 중 **가장 유명한 것이 도커**이다. 도커가 사용하는 컨테이너 규격은 표준화되어 있으므로 도커가 아닌 다른 컨테이너 런타임들도 도커로 만든 컨테이너를 사용할 수 있다.

 **쿠버네티스는 컨테이너 런타임을 통해 컨테이너를 다루는 도구**이다. 쿠버네티스가 해 주는 일은 여러 서버(노드)에 컨테이너를 분산해서 배치하거나, 문제가 생긴 컨테이너를 교체하거나, 컨테이너가 사용할 비밀번호나 환경 설정을 관리하고 주입해 주는 일 등이다.



### 가상환경 vs 컨테이너

![image](https://user-images.githubusercontent.com/88833439/187060805-380585f6-9689-4aee-9e65-81fe4eebe892.png)

#### 1. 전통적 배포 (Traditional Deployment)

 가장 오래되고 단순한 방식이며, 물리적인 컴퓨터 한 대에 하나의 OS (ex. Window)를 깔고 여러 가지 프로그램을 설치하는 방식.



💥 **문제점** 💥

> 한 대의 컴퓨터에서 모든 것을 처리하려고 하면 어떤 프로그램 동작이 다른 프로그램의 동작을 간섭하거나, 특정 프로그램이 성능을 독점할 경우 또 다른 프로그램의 성능이 떨어지는 단점이 있음.
>
> -> 물리적 컴퓨터를 따로 구입해서 사용하는 방법이 있으나, 비용이 큼.
>
> -> 이 문제를 해결하기 위한 해법이 **가상화 배포**

​	

#### 2. 가상화 배포 (Virtualized Deployment)

​	가상 머신을 기반으로 배포를 하는 방법이다. **하이퍼바이저는 하나의 시스템 상에서 가상 컴퓨터를 여러 개 구동할 수 있도록 해주는 중간 계층을 의미**한다. **App은 실행하고자 하는 프로그램, Bin/Library는 프로그램이 실행하는데 필요한 환경과 관련된 파일**이다.

​	가상 머신에는 CPU, 메모리, 저장 장치 등을 개별적으로 할당할 수 있다. 하나의 컴퓨터 안에서 두 개의 가상화된 컴퓨터가 동작하기 때문에 서로 간섭을 일으키지 않게 할 수 있다. 이를 통해, 게임 컴퓨터에는 좀 더 많은 CPU와 메모리를, 인터넷 뱅킹용 컴퓨터에는 적은 CPU와 메모리를 할당하여 사용할 수 있다. 서버와 같이 다중화와 분산 처리가 중요한 시스템이면 시스템 자원 상황에 따라 가상머신 개수를 늘리고 줄이는 것도 좀 더 유연하게 처리 가능하다.



💥 **문제점 💥**

>​	전통적 배포 방식보다는 분명 효율적이지만, 가상머신은 완전한 컴퓨터이고 가상머신에 일일이 운영체제를 설치해야 하기 때문에 **컨테이너 중심의 배포보다는 무거운 편**이다.



#### 3. 컨테이너 중심의 배포 (Container Deployment)

​	가상화 배포와 비교해서 대체된 부분은 다음과 같다.	

- 하이퍼바이저 -> Container Runtime

  - Virtual Machine -> Container

**컨테이너는 가상머신과 달리 프로그램 구동을 위해서 OS를 매번 설치할 필요가 없다.** OS는 하나만 사용한다.

 컨테이너 기반 배포는 물리적인 컴퓨터 상에서만 가능한 것이 아니라, 가상머신 위에 올라간 OS에서도 가능하다.



##### ❓ 컨테이너 중심의 배포방식은 한 프로그램이 다른 프로그램의 성능 저하나 오류를 발생시키는 문제를 어떻게 해결할까?

- 게임과 인터넷 뱅킹 소프트웨어가 각각 컨테이너로 배포된다고 가정
- 두 프로그램은 하나의 OS 상에서 구동
- 컨테이너 중심의 배포는 프로그램이 각각 실행되면서 '이 컴퓨터에서 나만 구동되고 있다'라고 판단할 수 있또록, 실제로 두 프로그램 간에 간섭을 일으킬 수 없는 장벽을 침
- 이러한 장벽을 치는 것과 동시에 OS는 게임과 인터넷 뱅킹이 사용할 수 있는 CPU, 메모리 등의 자원 또한 독립적으로 사용할 수 있도록 할당하고 관리함.
- 이러한 과정을 통해 게임과 인터넷 프로그램은 스스로를 '서로 다른 컴퓨터에서 깔려 있다' 고 생각하게 됨.
- OS 관점에서 보면 둘 다 같은 OS 상에서 구동되는 프로그램
- 컨테이너 중심의 배포방식 == OS 커널을 공유하는 가상화



### 총정리

![image](https://user-images.githubusercontent.com/88833439/187061663-873a45b0-cc96-4111-8389-85e570edf5fc.png)



#### 참조

삼성SDS - [쿠버네티스 알아보기 1편: 쿠버네티스와 컨테이너, 도커에 대한 기본 개념](https://www.samsungsds.com/kr/insights/220222_kubernetes1.html?referrer=https://www.google.com/)

