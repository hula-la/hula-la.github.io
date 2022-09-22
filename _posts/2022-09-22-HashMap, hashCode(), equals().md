---
layout: single
title: "String vs StringBuffer vs StringBuilder"
categories: Java
tag: [Java, String, StringBuffer, StringBuilder]
toc: true
toc_sticky: true
author_profile: false
sidebar:
  nav: "docs"
# search: false
---

## String vs StringBuffer vs StringBuilder

#### 🍺 String vs StringBuffer/StringBuilder

> String과 StringBuffer/StringBuilder 클래스의 가장 큰 차이점은 String은 **불변**의 속성을 가지다는 것.

```java
String str = "String";
str = str + "Builder";
```

- 위의 예제에서 str이 데이터만 바꼈다고 착각할 수 있음.
- "String" 값이 들어가있던 String 클래스의 참조변수 str이 "StringBuilder"라는 값을 가지고 있는 **새로운 메모리영역을 가리키게 변경**되고 처음 선언햇던 "String"로 값이 할당되어 있던 메모리 영역은 Garbage로 남아있다가 Garbage Collector에 의해 사라지게 됨.
- String 클래스는 불변하기 때문에 문자열을 수정하는 시점에 **새로운 String 인스턴스가 생성된 것**

##### 주의

- 문자열 추가, 수정, 삭제 등의 연산이 빈번하게 발생하는 알고리즘에 String 클래스를 사용하면 힙 메모리에 많은 임시 가비지가 생성되어 힙메모리가 부족

#### 🥨 StringBuffer vs StringBuilder

> 가장 큰 차이점은 **동기화의 유무**

- StringBuffer는 동기화 키워드를 지원하여 멀티쓰레드 환경에서 안전 (thread-safe)
- 반대로, StringBuilder는 동기화를 지원하지 않기 때문에 멀티쓰레드 환경에서 사용하는 것은 적합하지 않지만, 동기화를 고려하지 않는 만큼 단일쓰레드에서의 성능은 StringBuffer보다 뛰어남.



#### 📌 결론

- `String`: 문자열 연산이 적고 멀티쓰레드 환경일 경우
- `StringBuffer`: 문자열 연산이 많고 멀티쓰레드 환경일 경우 (동기화)
- `StringBuilder`: 문자열 연산이 많고 단일쓰레드이거나 동기화를 고려하지 않아도 되는 경우
