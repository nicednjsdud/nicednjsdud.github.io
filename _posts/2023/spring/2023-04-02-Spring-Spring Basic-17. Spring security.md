---
title: (10분 테크톡) (Spring) 17. 인증과 인가
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Spring
description: Spring Web Scope
tag: Spring Basic
article_tag1: Spring Web
article_section: Spring Web
meta_keywords: Spring, backend ,framework
last_modified_at: "2023-04-02 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 인증과 인가

## 개요

### 1) 내용

- 인증과 인가란
- 인증의 방법

### 2) 목표

- 인증과 인가에 대한 지식 습득 및 복습
- 프로젝트에서 선택한 인증 방식에 대한 근거

## 1. 인증과 인가

### 1) 인증이란?

- 닉네임과 사진 같은 정보로 입증하는 과정 예) 출입증
- 즉) (식별가능한 정보로) 서비스에 등록된 유저의 신원을 입증하는 과정

### 2) 인가란?

- 인증된 사용자에 대한 자원 접근 권한 확인

### 3) 웹에서의 인증과 인가

- 웹에서 로그인을 하는 과정을 인증이라고 한다.
- 그러면서 이제 글을 쓸 수 있는 권환도 획득을 하는 인가도 포함되어 있다.
- 다른 사람의 글을 읽을 수 있지만 다른사람의 글을 수정 할 수 없다. (그 권한은 없기 때문에, **인가 적용**)

### 4) 정리

- 자원을 적절한/ 유효한 사용자에게 전달/ 공개 하기 위한 방법을 인증과 인가라고 한다.

## 2. 인증의 방법

1. 인증하기 (Request Header)
2. 인증 유지하기 (Browser)
3. 안전하게 인증하기 (Server)
4. 효율적으로 인증하기 (Token)
5. 다른 채널을 통해 인증하기 (OAuth)

### 1) Request Header 활용하기

![alt](/assets/images/post/ComputerStudy/905.png)

- `http://user:1q2w3e!@www.test.com/login`
- 방금 들어온 url을 Base64 인코더를 이용해서 인코딩을 한 후에 전달하는 방식
- URL에서 `user:1q2w3e!`을 파싱한 후 인코더를 통해서 인코딩한 문자열을 가지고 있다.
- 그 다음 요청 헤더 `Authorization`에 넣어서 보내 주는 개념이다.

![alt](/assets/images/post/ComputerStudy/904.png)

- 서버로 보내면 서버가 DB체킹을 하고 DB에 실제로 값이 있으니깐 OK 사인을 해줌

#### 1-1) Request Header만 활용할 시에 문제점

- 사용자가 매번 로그인을 계속 해줘야 된다는 것이다.

### 2) Browser 활용하기

- 이를 해결하기위해서 브라우저에 있는 storage의 힘을 빌림
- 스토리지는 우리가 알고 있는 로컬 스트리지도 있을수 있고, 세션 스토리지, 쿠키도 될수 있다.

#### 1-1) 쿠키

- 간단하게 그냥 사용자 아이디와 비밀번호를 집어 넣는다.

![alt](/assets/images/post/ComputerStudy/906.png)

- 사용자가 인증이 필요한 요청을 할 때 같이 그냥넣어서 보내준다.
- 다만 해커들에게도 쉽게 노출될 수 있다는 단점이 있다.

### 3) Session 활용하기

- 쿠키의 단점을 해결하기위해서 서버에 도움을 요청한다.
- 세션은 인증된 사용자의 식별자와 랜덤한 문자열로 세션 ID를 만들어서 응답 헤더에 넘겨주고 그 다음에 클라이언트가  
  저장을 할수 있도록 만드는 것

![alt](/assets/images/post/ComputerStudy/907.png)

- 해커들이 정보를 가져가도 크게는 위험하지 않다
- 그리고 세션의 만료기간을 정할 수 있다.
  - 만료기간이 지난후에 정보를 가져가면 유효하지 않아서 안정적이다.
- 세션이라는 것의 관리를 서버 자체에서 하고 있기때문에 탈취가 된 세션을 서버에서 삭제를 해버리면은 이 세션 자체를  
  이용하지 못한다라는 보안사으이 이점도 있다.

#### 3-1) 문제점

- 서버를 여러 개 뒀을때 로드밸런서도 생긴다.
- 한번 세션을 받으면 다음 요청은 이제 세션으로만 이용해서 요청을 하게 된다.

![alt](/assets/images/post/ComputerStudy/908.png)

- 세션을 다시 요청하지만 세번째 서버에 저장이 되어있기때문에 문제가 발생한다.
- 서버 하나하나 자체에서 세션을 관리하고 있어서 발생하는 문제이다.

#### 3-2) 해결 방법

- 세션 DB를 만들어서 관리한다.
- 이렇게 되면 로드밸런서가 요청을 해도 결국에는 한곳으로 요청을 하기 때문에 해결할 수 있다.

![alt](/assets/images/post/ComputerStudy/909.png)

- 클라이언트가 많아질 경우에는 또 문제가 발생 !

#### 3-3) Session DB 문제점

![alt](/assets/images/post/ComputerStudy/910.png)

- 계속 해서 요청하면 디비가 터진다..

#### 3-4) Stateful

![alt](/assets/images/post/ComputerStudy/911.png)

- 클라리언트, 서버, 세션 저장소 를 모두 사용자의 정보를 한 번씩 관리 할 수 있게 했다.
- 문제가 생겼는데 그 이유는 이 세개가 통신을 할때 사용하는 http와 서버 자체가 지향하는 rest api가  
  무상태성을 기초로 하기 때문이다.
- 하지만 실제로 인증과 인가를 구현할 때는 사용자의 정보, 상태를 셋이 다들 가지고 있다.
  - 그말은 상태성을 자기고 있다는 말이다.
  - 이로써 두패러다임이 충돌을 하고 있다.
  - 이 패러다임을 해소해야 문제가 해결된다.

#### 3-5) Stateless

![alt](/assets/images/post/ComputerStudy/912.png)

- 요청과 응답안에 우리 사용자의 상태를 담아보자 그걸로만 사용자의 인증과 인가를 처리하자가
  - 토큰을 활용한 인증과 인증 방법이다.
