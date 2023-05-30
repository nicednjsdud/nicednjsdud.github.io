---
published: true
title: (10분 테코톡) Java 59. Java에서 Kotlin으로
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: OOP
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-05-29 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Java에서 Koltlin으로

## 목차

1. 혜성처럼 등장한 Kotlin
2. Kotlin의 장점
3. Kotlin과 Java의 상호 운용

## 1. 혜성처럼 등장한 Kotlin

### 1) 속도

- Java를 대안하기 위해서 만든 언어이다
- (최소한 Java보다는 빨라야 된다라는 것에 관심을 가짐)

### 2) 상호 운용

- 기존의 코드를 그대로 사용할 수 있으면서 꾸준히 개발할 수 잇는 그런 언어를 필요로 함

### 3) 간결성

- 세미콜론이나 간단한 기능을 구현할 때도 라인 수가 너무 많아지는 것을 조금 피해보자 조금 간결하게 해보자라는 것을 중점으로 개발

## 2. Kotlin의 장점

### 1) 정적 타입 지정 언어

- Kotlin은 정적 타입 지정 언어이다.
- 컴파일러가 코드를 검증하고 컴파일 하기 때문에 런타임 오류를 줄일 수 있다.

### 2) 타입 추론

* 변수 선언시 타입을 작성하지 않아도 val, var 키워드만으로도 가능하다.

![alt](/assets/images/post/ComputerStudy/1027.png)

### 3) Null Safety

* Kotlin은 Null을 다루는 방식이 명확하게 정해져 있기 때문에 Null Safety를 보장

### 4) Elvis 연산자 [ ?: ]

* nullable한 값에 대해서 만약에 이값이 null인 경우에 default값을 정함

![alt](/assets/images/post/ComputerStudy/1028.png)

### 5) 간결하고 명확하다.

* Kotlin은 Java에 비해 코드를 간결하고 명확하게 작성할 수 있다.
* 그렇기 때문에 비교적 코드를 파악하기 쉽다는 장점이 있다.

### 6) Coroutine

* Kotlin은 비동기적 코드를 쉽게 작성할 수 있도록 Coroutine을 제공
* 코루틴은 Kolitn의 고유의 개념은 아니다.
* Coroutine은 Thread에서 실행되는 단위이며, 경량 Thread라고 불릴 만큼 훨씬 가볍다.

## 3. Kotlin과 Java의 상호 운용

* Kotlin은 Java와 100% 상호 운용이 가능하다.
* Kotlin 코드를 컴파일 하면 Java와 동일한 바이트 코드가 생성된다.

![alt](/assets/images/post/ComputerStudy/1029.png)

## 출처

<a href="https://www.youtube.com/watch?v=eA8e18ddSms">부나의 Java에서 Kotlin으로</a>


