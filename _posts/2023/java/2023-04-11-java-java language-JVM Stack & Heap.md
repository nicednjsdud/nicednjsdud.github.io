---
published: true
title: (10분 테크톡) Java 55. JVM Stack & Heap
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: JVM Stack & Heap
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-04-11 15:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# JVM Stack & Heap

## 목차

1. JVM?
2. JVM 내부 구조
3. Bytecode 실행 예제

## 1. JVM

- 자바 바이트코드는 타겟 플램폼에 상관 없이 JVM 위에서 동작한다.
- 물론, JVM은 타겟 플랫폼에 의존한다.

![alt](/assets/images/post/ComputerStudy/919.png)

### 1) WORA

- Write Once, Run Anywhere - Sun Microsystems
- 해석) 네가 짠 자바 코드를 컴파일해서 배포하면, 어떤 플랫폼이든 다시 컴파일 할 필요 없이 실행시킬 수 있어!  
  근데 실행하려면 그 플랫폼에 맞는 JVM이 설치되어 있어야 해!

### 2) 굳이 JVM?

- C/C++도 크로스 컴파일해서 배포하면 되는데, 굳이 JVM을 사용해야 하나?
- 자바는 네트워크에 연결된 모든 디바이스에서 작동하는 것이 목적
- 디바이스마다 운영체제나 하드웨어가 다르기 때문에, 자연스럽게 플랫폼에 의존하지 않도록 언어를 설계
- 그 결과가 Java Bytecode, JVM

## 2. JVM 내부 구조

### 1) Runtime Data Areas

![alt](/assets/images/post/ComputerStudy/920.png)

#### 1-1) Per JVM

![alt](/assets/images/post/ComputerStudy/921.png)

- mehtod area와 heap은 모든 쓰레드가 공유하는 area

#### 1-2) Mehtod Area

![alt](/assets/images/post/ComputerStudy/922.png)

- 클래스 로더가 클래스 파일을 읽어오면, 클래스 정보를 파싱해서 Mehtod Area에 저장

#### 1-3) Heap

![alt](/assets/images/post/ComputerStudy/923.png)

- 프로그램을 실행하면서 생성한 모든 객체를 Heap에 저장

#### 1-4) Program Counter

![alt](/assets/images/post/ComputerStudy/924.png)

- 각 스레드는 메서드를 싱행하고 있고, pc는 그 메서드안에서 몇번째 줄을 실행해야 하는지 나타내는 역할

#### 1-5) Stack

![alt](/assets/images/post/ComputerStudy/925.png)

- 자바 스택은 스레드 별로 1개만 존재하고, 스택 프레임은 메서드가 호출 될때마다 생성된다.
- 메서드 실행이 끝나면 스택 프레임은 pop되어 스택에서 제거

#### 1-6) Stack Frame

- 스택 프레임은 메서드가 호출될 때마다 새로 생겨 스택에 push 된다.
- 스택 프레임은 Local variables array, Operand stack, Frame Data를 갖는다.
- Frame Data는 Constant Pool, 이전 스택 프레임에 대한 정보, 현재 메서드가 속한 클래스/ 객체에 대한 참조 등의  
  정보를 갖는다.

#### 1-7) Native Method Stack

![alt](/assets/images/post/ComputerStudy/926.png)

- Native Method는 Java Bytecode가 아닌 다른 언어로 작성된 메서드를 의미

## 3. Bytecode 실행 예제

```java
  public class main{
    public static void main(String[] args){
      double position = 1.0;
      double initial = 1.0;
      double rate = 1.0;

      position = initial + rate * 60;
    }
  }
```

### 1) Local Variable Array

![alt](/assets/images/post/ComputerStudy/927.png)

## 출처

<a href="https://www.youtube.com/watch?v=UzaGOXKVhwU">무민의 JVM Stack & Heap</a>
