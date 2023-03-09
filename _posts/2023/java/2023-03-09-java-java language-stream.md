---
published: true
title: (10분 테크톡) Java 51. Stream
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Java
description: Java 51. Stream
tag: java language
article_tag1: Java
article_section: Java
meta_keywords: java
last_modified_at: "2023-03-09 13:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# Stream

1. 스트림이란?
2. 스트림 구조
3. 스트림의 장단점

## 1. 스트림이란?

- 오라클 : 순차 및 벙렬적인 집계연산을 지원하는 연속된 요소
- 모던 자바 인 액션 : 데이터 처리 연산을 지원하도록 소스에서 추출된 요소
- Computer Science : A sequence of data elements made **available over time**
- Common nouns : A continuous flow of things or people

### 1) 요약

- 즉 스트림은 어떠한 요소들이 모인 하나의 고정된 집합이라고 생각하기보단,
- flow, 즉 데이터 흐름이라는 것에 초점을 맞추서 생각하면 이해하기 편함

### 2) 오라클 공식 문서 - 스트림

- Package java.util.stream

![alt](/assets/images/post/ComputerStudy/823.png)

- 오라클 공식문서에서는 스트림 패키지를 요소들의 스트림에 함수형 스타일의 연산을 지원하는 클래스들이라고 묘사
- 스트림 자체는 어떠한 데이터의 흐름이고 우리가 사용하는 자바의 스트림 API는 이 데이터를 어떻게 다룰 것인가를 논하는  
  일종의 파이프라인이라고 생각

## 2. 스트림의 구조

- 크게 세 파트로 구분하면 생성 -> 가공 -> 소비

### 1) 생성

![alt](/assets/images/post/ComputerStudy/824.png)

- 리스트, 맵과 같은 컬렉션으로부터 생성 할 수 있다.
- 이외에도 배열로부터 생성할 수도 있다.
- 또한 파일로부터 생성할 수도 있다.
- 또한 컬렉션과 다르게 무한을 만들 수도 있다.
- 별도의 서드파티 라이브러리를 활용할 수도 있다.

### 2) 가공

![alt](/assets/images/post/ComputerStudy/825.png)

- 중간연산자는 필터, 맵, 리밋 등 소스로 부터 얻어낸 값들을 이제 입맛대로 가공하는 역할을 함
- 결과로는 새로운 스트림을 반환하는데 이는 곧 lazy evaluation을 할 수 있도록 만들어 준다.
- 새로운 스트림 인스턴스를 돌려주기만 할 뿐 어떠한 작업도 하지 않음

#### 2-1) lazy evaluation

- 최종연산이 들어오기 전까지 중간 연산을 실제로 실행되지 않음을 의미

![alt](/assets/images/post/ComputerStudy/826.png)

#### 2-2) 중간 연산자 구분

- 중간연산자는 2개로 구분할 수 있다.
- stateless, stateful

##### 1. stateless

- 특정 행위를 수행할 때 다른 요소에 대해서 독립적으로 처리될 수 있음을 의미
- 맵의 경우 맵 연산을 수행하기 위해서는 내가 현재 바라보고 있는 값에만 신경을 쓰면 됨

##### 2. stateful

- 선행된 연산에 영향을 받음
- sorted, distinct와 같은 중간연산자는 실행되기위해 자기 자신 이외의 값은 무엇이었는지등에 대해서 특정 상태를  
  알고 신경을 써야함

### 3) 소비

![alt](/assets/images/post/ComputerStudy/827.png)

- 결과를 생성하거나 사이드 이펙트를 만들기 위해서 사용
- collect, findAny, findFirst등이 있다.

#### 3-1) collect

- 스트림 패키지 내부에 있는 collectors라는 것을 이용하면 활용성이 다양

#### 3-2) 최종연산자 주의점

##### 1. 첫째

- 최종연산자가 수행되고 나면 스트림 파이프라인은 소비된 것으로 간주된다.
- 즉 다시 사용하려면 새로운 스트림을 만들어야 한다.

![alt](/assets/images/post/ComputerStudy/828.png)

##### 2. 두번째

- foreach는 대게 로그나 디버깅을 위한 출력으로만 사용할 것을 권장
- 이펙티브 자바에서는 foreach가 "덜 스트림스럽다"라고 이야기함
- 첫번째 메서드와 같이 foreach 내부에서 값을 할당하는 식으로 사용할 경우 불필요한 사이드 이펙트롤 만들어 냄
- 두번째 메서드와 같이 병렬 처리가 추가될 경우 올바른 결과값을 기대하기 어렵다.

![alt](/assets/images/post/ComputerStudy/829.png)

##### 3-3) 장점

- 첫번째는 가독성이 좋다는 점
- 코드의 변경이 쉽다.
- 병렬 처리를 간단하게 해결할 수 있다는 점

![alt](/assets/images/post/ComputerStudy/830.png)

##### 3-4) 단점

##### 1. 첫번째

- 컴퓨팅 비용
- 스트림은 내부적으로 다양한 조건과 상황에 따라서 연산을 처리하기 때문에 생성하는데 적지 않은 비용 발생
- 밑에 사진은 for-loop와 스트림에 대해서 성능 비교를 한 자료

![alt](/assets/images/post/ComputerStudy/831.png)

##### 2. 두번째

- 인지에 대한 비용
- 기존 반복문에 경우 우리가 직접 값을 꺼내와서 사용 했고, 반대로 스트림을 사용할 경우 스트림 내부에서 연산이 일어남

![alt](/assets/images/post/ComputerStudy/832.png)

- 밑에 코드에서 왼쪽 코드의 경우 distinct 입장에서 반복해서 들어오는 0과 1이라는 두값은 이미 발견한 적이 있는  
  값이 므로 limit으로 넘겨주지 않는다.

- 오른쪽의 경우 limit으로 먼저 개수의 제한이 걸리기 때문에 다음 distinct로 넘어갈 수 있다.

![alt](/assets/images/post/ComputerStudy/833.png)

## 출처

<a href="https://www.youtube.com/watch?v=rbm87IFpwvQ">차리의 Stream</a>
