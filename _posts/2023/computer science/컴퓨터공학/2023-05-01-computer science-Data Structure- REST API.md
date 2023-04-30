---
title: (10분 테크톡) REST API
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: Process vs Thread
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,자료구조
last_modified_at: "2023-05-01 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# REST API

## 1. REST API란?

1. URI를 통해 **자원**을 지정
2. HRRP 메서드 : 자원에 대한 **행위** 표현

```sql
  CREATE    POST    /user
  READ      GET     /user/1
  UPDATE    PUT     /user/1
  DELETE    DELETE  /user/1
```

## 2. REST와 HTTP 메서드

- 내 논문 어디에서 CRUD에 대한 내용은 없다.
- HTTP 메서드는 REST가 아니라 웹의 아키텍쳐 스타일의 일부다.
- HTTP에서 정의한 방식대로만 잘 쓴다면 REST는 딱히 할 말이 없다.

## 3. Fielding의 REST API란?

- REST 아키텍쳐 스타일에 부합하는 API

1. Clinet - Server
2. Stateless
3. Cache
4. Uniform Interface
5. Layered System
6. Code-On-Demand

## 4. REST : Uniform Inteface

1. identification of resoruces
2. manipulation of resources through representations
3. self-descriptive mesages
4. HATEOAS (hypermedia as the engine of application state)

### 1) 자원에 대한 식별

#### 1-1) 자원

- 이름을 지닐 수 있는 모든 정보
- 개념적인 대상
- ex) 문서, 이미지, 자원들의 집합, 실존하는 대상 등

#### 1-2) 자원은 객체

- 상태는 변화가능 ! -> 변하지 않는 식별자 필요

![alt](/assets/images/post/ComputerStudy/990.png)

- URI를 통해 자원을 식별해야 한다.

![alt](/assets/images/post/ComputerStudy/991.png)

### 2) 표현을 통한 자원에 대한 조작

- 표현 : 특정한 상태의 자원에 대한 표현
- 자원은 다양한 방식으로 표현 가능
- ex) 문서, 파일 , HTTP 메시지 엔티티 등

![alt](/assets/images/post/ComputerStudy/992.png)

#### 2-1) REST : 자원에 대한 표현 전송

- **REpresentational State Transfer**

- 표현된 (자원의) 상태
- 자원의 현재 상태
- 자원의 기대되는 상태

### 3) 자기 서술적 메시지

- 메세지는 스스로에 대해 설명해야 한다.

![alt](/assets/images/post/ComputerStudy/993.png)

- 클라이언트와 서버 사이의 컴포넌트들은 메시지의 내용을 참고하여 적절한 작업 수행

#### 3-1) Host 헤더

- Host 헤더에 도메인명 기재 필요!

```java
  GET /user/1 HTTP/1.1
  host: example.com
```

- cf) HTTP/1.1부터 Host 헤더 필수화

##### 1) 도메인명 정보의 필요성

- 가상 호스트 문제
- 하나의 IP 주소에 복수의 도메인명 존재 가능
- IP 주소만으로는 요청 대상을 찾아낼 수 없다.

#### 3-2) 캐쉬

- 캐쉬 관련 헤더를 통한 캐쉬 전략 지정
- HTTP/1.1 : Cache - Control, Age, Etag, Vary

![alt](/assets/images/post/ComputerStudy/994.png)

### 4) HATEOAS

![alt](/assets/images/post/ComputerStudy/995.png)

- 하이퍼미디어를 통한 앱상태 변경

![alt](/assets/images/post/ComputerStudy/996.png)

#### 4-1) HATEOAS - 위배 사례

![alt](/assets/images/post/ComputerStudy/997.png)

## 5. REST API여야 하는가?

- 시스템을 통제할 수 있다고 생각한다면 REST에 시간을 낭비하지 말라
- Uniform Interface 제약조건은 비효율적
- 애플리케이션에 필요한 정보가 아니라, 표준화된 형식으로 데이터 전달
- **상황에 따라 최적이 아닐 수 있다.**

## 6. API 설계의 방향성

1. 진짜 REST API 만들기 (aka. RESTful API)
2. REST 스타일의 API 만들기 (aka. HTTP API)
3. 다른 API 표준 서낵하기 (e.g., GraphQL API)

## 7. 정리

1. REST API란 REST 아키텍쳐 스타일에 부합하는 API

- aka. RESTful API

2. REST API의 구현은 가능

- 굳이 필요한가? 어떠한 효용이 있는가?

3. REST API라는 용어를 아무렇게나 쓰지 말자
