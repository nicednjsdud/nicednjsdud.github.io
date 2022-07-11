---
title: (Web) 그런 REST API로 괜찮은가? (DEVIEW)
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Mok MVC
tag: Spring Web
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2022-07-01 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 그런 REST API로 괜찮은가? (DEVIEW)

## 0. REST의 역사

- REpresentational State Transfer

### 1) WEB(1991)

- 어떻게 인터넷에서 정보를 공유할 것인가?

```
    A : 정보들을 하이퍼 텍스트로 연결한다.
        표현 형식 : HTML
        식별자    : URI
        전송 방법 : HTTP
```

### 2) HTTP/1.0 (1994- 1996)

Roy T.Fielding : "How do i improve HTTP withdout breaking the Web?"

- 어떻게 하면 웹을 망가뜨리지 않고 HTTP를 증가시킬 수있을가?

#### 해결책 : HTTP Object Model

- 4년후 레스트란 이름으로 발표

### 3) REST (1998)

- Microsoft Research에서 발표

### 4) REST (2000)

- 박사 논문으로 발표

## 1. REST

### 1) REST 구성

- REST API는 다음과 같은 3가지 부분으로 구성된다.

* 자원(Resource) : 자원은 Data, Meta Data, HATEOAS로 나뉩니다.
* 행위(Verb) : HTTP Method로 표현됩니다.
* 표현(Representations)

### 2) REST의 특징

#### 1. Uniform Interface(유니폼 인터페이스)

- 구성 요소(클라이언트, 서버 등) 사이의 인터페이스는 균일(uniform)해야합니다.
- 인터페이스를 일반화함으로써, 전체 시스템 아키텍처가 단순해지고, 상호 작용의 가시성이 개선되며,  
  구현과 서비스가 분리되므로 독립적인 진화가 가능해질 수 있습니다.

#### 2. Stateless (무상태성)

- 클라이언트와 서버의 통신에는 상태가 없어야합니다.
- 모든 요청은 필요한 모든 정보를 담고 있어야합니다.
- 요청 하나만 봐도 바로 뭔지 알 수 있으므로 가시성이 개선되고, task 실패시 복원이 쉬우므로 신뢰성이 개선되며,  
  상태를 저장할 필요가 없으므로 규모 확장성이 개선될 수 있습니다.

#### 3. Cacheable (캐시 가능)

- 캐시가 가능해야합니다. 즉, 모든 서버 응답은 캐시가 가능한지 그렇지 아닌지 알 수 있어야합니다.
- 효율, 규모 확장성, 사용자 입장에서의 성능이 개선됩니다.

#### 4. Self-descriptiveness (자체 표현 구조)

- REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는  
  자체 표현 구조로 되어 있다는 것입니다.

#### 5. Client - Server 구조

- 클라이언트-서버 스타일은 사용자 인터페이스에 대한 관심(concern)을 데이터 저장에  
  대한 관심으로부터 분리함으로써 클라이언트의 이식성과 서버의 규모확장성을 개선할 수 있습니다.

#### 6. Layered System(계층형 구조)

- REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해  
  구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할  
  수 있게 합니다.

## 2. API

### 1) XML-RPC (1998)

- by Microsoft -> SOAP

### 2) Salesforce API (2000.2)

### 3) flicker API (2004)

- SOAP로 만듬 (너무 복잡)

### 4) SOAP과 REST의 느낌적인 비교

| SOAP      | REST      |
| --------- | --------- |
| 복잡하다  | 단순하다  |
| 규칙 많음 | 규칙 적음 |
| 어렵다    | 쉽다      |

- 2006년, AWS가 자사 API의 사용량의 85%가 REST임을 밝힘
- 2010년, Salesforce.com,REST API 추가

### 5) CMIS (2008)

- CMS를 위한 표준
- EMC, IBM, Microsoft등이 함께 작업
- REST 바인딩 지원

## 3. REST API

- REST 아키텍처 스타일을 따르는 API

### 1) REST

- 분산 하이퍼미디어 시스템(ex:웹)을 위한 아키텍처 스타일

#### 아키텍쳐 스타일

- 제약조건의 집합 (모두지켜야 REST를 따른다고 말함)

### 2) REST를 구성하는 스타일

- client-server
- stateless
- cache
- **uniform interface**
- layered system
- code-on-demand (optional) : ex) 자바 스크립트

#### Uniform Interface의 제약조건

- identification of resources
- manipulation of resources through represnetations
- **self-descriptive messages**
  - 메세지는 스스로를 설명해야 한다.
- **hypermedia as the engine of application state(HATEOAS)**
  - 애플리케이션의 상태는 **Hyperlink**를 이용해 전이되어야 한다.

#### 독립적 진화

- 서버와 클라이언트가 각각 독립적으로 진화한다.
- **서버의 기능이 변경되어도 클라이언트를 업데이트 할 필요가 없다.**

### 3) 웹

- 웹 페이지를 변경했다고 웹 브라우저를 업데이트 할 필요는 없다.
- 웹 브라우저를 업데이트했다고 웹 페이지를 변경할 필요도 없다.
- HTTP 명세가 변경되어도 웹은 잘 동작한다.
- HTML 명세가 변경되어도 웹은 잘 동작한다.

### 4) 비교

| --           | 흔한 웹 페이지 | HTTP API  |
| ------------ | -------------- | --------- |
| Protocol     | HTTP           | HTTP      |
| 커뮤니케이션 | 사람-기계      | 기계-기계 |
| Media Type   | HTML           | JSON      |

- HTML JSON 비교

| --               | HTML          | JSON              |
| ---------------- | ------------- | ----------------- |
| Hyperlink        | 됨(a태그 등)  | 정의되어있지 않음 |
| Self-descriptive | 됨(HTML 명세) | 불완전 \*         |

- 문법 해석은 가능하지만, 의미를 해석하려면 별도로 문서가(API 문서 등) 필요하다.

#### Self-descriptive

- 확장 가능한 커뮤니케이션
- 서버나 클라이언트가 변경되더라도 오고가는 메세지는 언제나 self-descriptive하므로  
  언제나 해석이 가능

#### HATEOAS

- 애플리케이션 상태 전이의 late binding
- 어디서 어디로 전이가 가능한지 미리 결정되지 안은다. 어떤 상태로 전이가 완료되고  
  나서야 그 다음 전이될 수 있는 상태가 결정된다.
  - 쉽게 말해서 링크는 동적으로 변경될 수 있다.

## 5. REST API 설계 가이드

### 1) URI는 정보의 자원을 표현해야 합니다.

resource는 동사보다는 명사를, 대문자보다는 소문자를 사용한다.

resource의 도큐먼트 이름으로는 단수 명사를 사용해야 한다.

resource의 컬렉션 이름으로는 복수 명사를 사용해야 한다.

resource의 스토어 이름으로는 복수 명사를 사용해야 한다.

예 : GET /members/1

### 2) 자원에 대한 행위는 HTTP Method (GET, POST, PUT, DELETE)로 표현합니다.

### 3) URI에 HTTP Method가 들어가면 안됩니다.

예) GET /books/delete/1 -> DELETE /books/1

### 4) URI에 행위에 대한 동사 표현이 들어가면 안됩니다.

(즉, CRUD 기능을 나타내는 것은 URI에 사용하지 않습니다.)

예) GET /books/show/1 -> GET /books/1

예) GET /books/insert/2 -> POST /books/2

### 5) 경로 부분 중 변하는 부분은 유일한 값으로 대체합니다.

(즉, id는 하나의 특정 resource를 나타내는 고유값을 의미합니다.)

예) book을 생성하는 URI: POST /students

예) id=10 인 book을 삭제하는 URI: DELETE /students/10

### 6) 슬래시 구분자(/ )는 계층 관계를 나타내는데 사용합니다.

예) http://nicednjsdud.github.io/courses/java

### 7) URI 마지막 문자로 슬래시(/ )를 포함하지 않습니다.

예) http://nicednjsdud.github.io/courses/ (X)

### 8) URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 한다

URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 합니다.

### 9) 하이픈(- )은 URI 가독성을 높이는데 사용할 수 있습니다.

### 10) 밑줄( \_ )은 URI에 사용하지 않습니다.

### 11) URI 경로에는 소문자가 적합합니다.

URI 경로에 대문자 사용은 피하도록 합니다. RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는  
대소문자를 구별하도록 규정하기 때문입니다.

### 12) 파일 확장자는 URI에 포함하지 않습니다. Accept header를 사용하도록 합니다.

예) http://nicednjsdud.github.io/files/java.jpg (X)

예) GET /files/jdk18.exe HTTP/1.1 Host: nicednjsdud.github.io Accept: image/jpg (O)

### 13) 리소스 간에 연관 관계가 있는 경우 다음과 같은 방법으로 표현합니다.

/리소스명/리소스 ID/관계가 있는 다른 리소스명

예) GET : /books/{bookid}/viewers (일반적으로 소유 ‘has’의 관계를 표현할 때)

### 14) 자원을 표현하는 컬렉션(Collection)과 도큐먼트(Document)

컬렉션은 객체의 집합, 도큐먼트는 객체라고 생각하면 됩니다. 컬렉션과 도큐먼트 모두 리소스로  
표현할 수 있으며 URI로 표현할 수 있습니다.

예) http://nicednjsdud.github.io/courses/1

courses는 컬렉션을 나타냅니다. 복수로 표현해야 합니다.  
courses/1 은 courses중에서 id가 1인 도큐먼트를 의미합니다.

## 6. 정리

- 오늘날 대부분의 "REST API"는 사실 REST를 따르지 않고 있다.
- REST의 제약조건 중에서 특히 Self-descriptive와 HATEOAS를 잘 만족하지 못한다.
- REST는 긴 시간에 걸쳐 진화하는 웹 애플리케이션을 위한 것이다.
- REST를 따를것인지는 APi를 설계하는 이들이 스스로 판단하여 결정해야 한다.
  - Self-descriptive는 custom media type이나 profile link relation 등으로  
    만족시킬 수 있다.
  - HATEOAS는 HTTP 헤더나 본문에 링크를 담아 만족시킬 수 있다.
- REST를 따르지 않겠다면, "REST를 만족하지 않은 REST API"를 뭐라고 부를지 결정해야  
  할 것이다.
  - HTTP API라고 부를 수도 있고
  - 그냥 이대로 REST API라고 부를 수도 잇다.

출처 : <a href="https://www.boostcourse.org/web326/lecture/58986?isDesc=false">부스트코스 REST API</a>
