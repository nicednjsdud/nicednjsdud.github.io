---
title: (10분 테크톡) Web 요청 & 응답과정
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
last_modified_at: "2023-04-17 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 목차

- 웹 요청과 응답 과정을 떠받치는 핵심 개념들
- 웹 요청과 응답 과정

## 1. 인터넷 (Internet)

### 1) Local Area Network (LAN)

- 근거리 통신망
- 구내 정보 통신망은 네트워크 매체를 이용하여 집, 사무실, 학교 등의 건물과 같은 가까운 지역을 한데 묶은 컴퓨터 네트워크

### 2) Internet

- 컴퓨터 네트워크들을 서로 연결지어 주는 범지구적 네트워크
- (= Inter-Network = 컴퓨터 네트워크들의 네트워크)
- 이렇게 구축된 인터넷이라는 거대한 네트워크 위에서 오늘날 우리가 사용하는 다양한 서비스들이 동작

![alt](/assets/images/post/ComputerStudy/953.png)

- 웹도 인터넷 위에서 동작하는 서비스들 중 하나

### 3) 웹 (World Wide Web)

- 당시 빠르게 발전하고 있던 인터넷
- 그리고 HyperText 같은 당시 새롭게 떠오르는 컴퓨터 기술들을 활용하여 이러한 문제점을 해결하고자 했음
- 웹의 존재이유는 정보(자원)의 공유 -> 웹은 수많은 요청과 응답 사이클의 연속으로 이루어짐

### 4) 서버 & 클라이언트

#### 4-1) 서버 (Server)

- 정보, 자원, 서비스를 제공하는 측
- 요청을 받고 응답하는 측

#### 4-2) 클라이언트 (Client)

- 클라이언트는 정보, 자원, 서비스를 사용하는 측
- 요청을 보내는 측

![alt](/assets/images/post/ComputerStudy/954.png)

### 5) HTTP (HyperText Transfer Protocol)

- 웹 요청과 응답에 관한 클라이언트와 서버사이의 규약 (약속)

![alt](/assets/images/post/ComputerStudy/955.png)

### 6) HTTP의 대표적인 특성 (1)

#### 6-1) 비연결성

- 클라이언트의 요청에 대해 서버가 응답을 마치면 연결을 끊어버린다.
- 다음 요청은 새로운 연결을 통해 이루어진다.

#### 6-2) 단점

- 매번 모든 요청에 대해서 새로운 연결/해제 과정을 거치므로 네트워크 비용측면에서 비효율적

#### 6-3) 보완책

- HTTP/1.1 Keep-Alive
- 서버와 클라이언트 사이에서 통신이 없어도 지정된 시간동안 연결을 유지하는 기능

### 7) HTTP의 대표적인 특성 (2)

#### 7-1) 무상태성 (Stateless)

- 서버와 클라이언트는 하나의 요청이 진행되는 동안만 서로를 인지

#### 7-2) 단점

- 클라이언트 인증(로그인)이 필요한 서비스에서 불편함

#### 7-3) 보완책

- 쿠키, 세션, 토큰 (OAuth, JWT) - 상태를 기억하기 위한 기능들

### 8) HTTP Status Code (응답 코드, 상태 코드)

- 클라이언트의 요청에 대해서 서버는 요청에 대한 처리 상태를 숫자 코드로 반환

- 1xx : (정보) 요청을 받았으며 프로세스를 계속한다.

- 2xx : (성공) 요청을 성공적으로 받았으며 인식해서 처리했다.

- 3xx : (리다이렉션) 요청 완료를 위해 추가 작업 조치가 필요하다.

- 4xx : (클라이언트 에러) 요청의 문접이 잘못되었거나 요청을 처리할 수 없다.

- 5xx : (서버 에러) 서버가 명백히 유효한 요청에 대해 충족을 실패했다.

### 9) Http Method(verbs) (Http 메서드)

- 클라이언트가 요청을 보낼때 해당 요청의 목적이 뭔지 HTTP Mehtod를 통해 명시

- **GET** : 서버의 리소스를 조회하고자 할 때 (READ)

- **POST** : 서버에 리소스를 생성하고자 할 때 (CREATE)

- **PUT** : 서버의 리소스를 수정할 때 (UPDATE)

- **DELETE** : 서버의 리소스를 삭제할 때 (DELETE)

- HEAD : GET과 동일하나, 서버에서 Body를 빼고 HEAD로만 응답 (리소스 확인의 용도)

- PATCH : 리소스의 부분만을 수정할 때

- OPTIONS : 지원 가능한 메서드 종류를 알아볼 때

- TRACE : 리소스의 경로를 따라 메세지 loop-back 테스트를 실행

- CONNECT : 리소스로 식별되는 서버로의 터널을 맺을 때

## 2. 웹 요청과 응답 과정

### 1) 티스토리 홈페이지에 대한 요청과 응답

![alt](/assets/images/post/ComputerStudy/956.png)

#### 1-1) URL

- Uniform Resource Locator
- 네트워크상 자원의 위치( 주소 )

![alt](/assets/images/post/ComputerStudy/957.png)

#### 1-2) 홈페이지에 대한 요청을 서버로 전송 (HTTP Request)

![alt](/assets/images/post/ComputerStudy/958.png)

#### 1-3) 서버가 클라이언트로 부터 요청을 받고 처리

- Request Headers 확인

  - 요청에 대한 정보 (URI, Method ..) + 클라이언트에 대한 정보 (accept, user-agent, cookie ...)

- 요청에 상응하는 로직 수행

  - 홈페이지에 해당하는 html 파일을 찾은 후 요청에 대한 응답 생성

#### 1-4) 서버가 클라이언트에게 응답 (HTTP Response)

![alt](/assets/images/post/ComputerStudy/959.png)

#### 1-5) 클라이언트가 응답을 받은 후 필요한 리소스들을 추가 요청 & 응답 받기

- CSS, JavaScript 등등

![alt](/assets/images/post/ComputerStudy/960.png)

#### 1-6) 클라이언트가 모든 리소스 요청에 대한 응답을 받음

![alt](/assets/images/post/ComputerStudy/961.png)

### 2) 티스토리 블로그 글 임시저장 요청과 응답

![alt](/assets/images/post/ComputerStudy/962.png)

![alt](/assets/images/post/ComputerStudy/963.png)

### 3) 티스토리 임시 저장된 글 삭제 요청과 응답

![alt](/assets/images/post/ComputerStudy/964.png)

![alt](/assets/images/post/ComputerStudy/965.png)

<a href="https://www.youtube.com/watch?v=0jV7xOUcKog">삭정의 Web 요청 & 응답과정</a>
