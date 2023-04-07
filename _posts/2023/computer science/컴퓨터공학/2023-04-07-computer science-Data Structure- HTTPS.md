---
title: (10분 테크톡) HTTPS
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
last_modified_at: "2023-04-07 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 목차

- HTTP VS HTTPS
- SSL / TLS
- SSL 통신 과정

## 1. HTTP VS HTTPS

### 1) HTTP

- Hypertext Transfer Protocol
- 서로 다른 시스템들 사이에서 통신을 주고받게 하는 가장 기본적인 프로토콜
- 서버에서 브라우저로 데이터를 전송하는 용도로 가장 많이 사용함
- HTTP는 서버에서 브라우저로 전송되는 정보가 암호화되지 않는다는 문제점을 가지고 있음
  - **데이터가 쉽게 도난 당할 수 있음**

### 2) HTTPS

- Hypertext Transfer Protocol Secure
- SSL(보안 소켓 계층)사용
- SSL은 서버와 브라우저 사이에 안전하게 암호화된 연결을 만들 수 있게 도와줌
- 서버와 브라우저가 민감한 정보를 주고 받을 때 해당 정보가 도난 당하는것을 막아줌
- HTTP를 사용해서 운반하는 내용, 즉 HTTP Message Body를 암호화함
  - 이때 HTTP헤더는 암호화 되지 않음

### 3) HTTPS를 사용하는 이유

#### 3-1) 보안성

- HTTP로 데이터를 전송하면, 네트워크로 전달되는 데이터는 원본 그 자체

  - 해커가 중간에서 가로챈 후, 이 데이터를 보면 해당 데이터에 어떤 내용이 있는지 바로 알 수 있음

- HTTPS는 전송할 때는 데이터를 암호화해서 전송

  - 해커가 중간에서 가로채도 데이터는 암호화 되어 잇기 때문에 이 데이터가 어떤 내용을 가지고 있는지 알기 어려움

- 그래서, HTTP가 아닌 HTTPS로 데이터로 전송해서 보안성을 확보해야 함

![alt](/assets/images/post/ComputerStudy/916.png)

#### 3-2) SEO (검색 엔진 최적화)

- 검색 엔진 구글은 HTTPS 웹 사이트에 가산점을 줌
- 가속화된 모바일 페이지, 즉 AMP를 만들때는 HTTPS를 사용해야 함
- AMP는 모바일 기기에서 컨텐츠를 훨씬 빠르게 로딩하기 위한 방법으로 구글에서 만듬
- 모바일 친화적인 웹 사이트를 만들고, 모바일 검색 순위를 증가시키기는 게 점점 더 중요해진 요즘에는 HTTPS 전환이 필수적

## 2. SSL / TLS

- SSL의 업그레이드 버전이 TLS

### 1) SSL ?

- Secure Sockets Layer
- Netscape Communications Corporation에서 웹 서버와 웹 브라우저간의 보안을 위해 만든 프로토콜
- 공개키/ 개인키 대칭키 기반으로 사용함

### 2) 대칭키

![alt](/assets/images/post/ComputerStudy/917.png)

- 대칭키 방식은 동일한 키로 암호화와 복호화를 수행하는 방법
- 누구든지 암호화에 이용된 키를 가지고 잇다면, 해당 데이터를 쉽게 복호화 할 수 있다.
- **정리하면, 대칭키 방식은 암호화와 복호화가 쉽다는 장점**
- **키를 배송할 때 문제가 된다는 단점을 가지고 있다.**

### 3) 공개키

![alt](/assets/images/post/ComputerStudy/918.png)

- 공개키 방식은 서로 다른 키로 암호화와 복호화를 수행하는 방법
- **공개키 방식은 비대칭키 방식으로도 불린다.**
- 데이터 암호화 시에는 공개키를 사용하고 데이터 복호화 시에는 개인키를 사용
- 공개키는 단어 그대로 공개키이기 때문에, 해커가 중간에 가로채도 문제가 되지 않음
- **정리하면, 공개키 방법은 무한대로 나눠줘도 괜찮기 때문에 키 배송 문제는 없다.**
- **공개키 방식은 대칭키 방식보다 암호화 연산 시간이 더 소요되어 비용이 크다.**

### 4) SSL이 필요한 이유

- 서버와 브라우저간 전송되는 데이터를 외부의 공격자로부터 보안하기 위해 필요함
- **보안**이 가장 중요한 키워드
- 암호화의 대상은 내용이 유출됐을 때 자칫 악용되어 사용될 수 있는 비밀번호나 개인정보 등이 해당

## 3. SSL 통신 과정

- SSL은 공개키 방식과 대칭키 방식을 적절히 혼합해서 사용한다.
  - SSL은 공개키 방식으로 대칭키를 전달
  - 이 대칭키를 활용해서 암호화와 복호화를 하고, 서버와 브라우저간 통신을 진행
- 데이터 암호화 복호화를 위한 한 쪽의 대칭키를 다른 쪽의 공개키로 암호화하여 전송하면, 반대편에서 자신의 개인 키로  
  복호화하여 그 반대편의 대칭키를 알아내고 이 대칭키를 바탕으로 서로 통신을 하게 된다.

## 출처

<a href="https://www.youtube.com/watch?v=wPdH7lJ8jf0">다니의 HTTPS</a>
