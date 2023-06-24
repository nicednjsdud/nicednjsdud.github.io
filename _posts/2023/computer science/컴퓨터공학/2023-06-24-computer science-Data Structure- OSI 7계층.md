---
title: (10분 테크톡) OSI 7 계층
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
last_modified_at: "2023-06-24 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 목차

1. OSI 7계층은 왜 만들어졌을까?
2. OSI 7계층은 어떻게 동작할까?
3. 왜 우리는 OSI 7계층을 알아야 할까?

## 1. OSI 7계층은 왜 만들어졌을까?

### 1) Open System Interconnection

- 국제표준화기구(ISO)가 1977년에 정의한 국제 통신 표준 규약.
- 통신의 접속에서부터 완료까지의 과정을 7단계로 구분 정의
- **서로 다른 컴퓨터들이 데이터를 주고 받을수 있도록 표준화된 규칙**

### 2) Intro

#### 2-1) 네트워크의 시작

- 서로 다른 컴퓨터 사이에 정보를 주고 받을 수 있게 됨

#### 2-2) 프로토콜의 발전

- 여러 회사에서 각각의 프로토콜을 개발함
- 통일된 규정이 없어 문제 발생

![alt](/assets/images/post/ComputerStudy/1055.png)

#### 2-3) 표준의 탄생

- 국제 표준기구에서 표준 네트워크 프로토콜, OSI 를 발표함

![alt](/assets/images/post/ComputerStudy/1056.png)

## 2. OSI 7계층은 어떻게 동작할까?

### 1) OSI

![alt](/assets/images/post/ComputerStudy/1057.png)

#### 1-1) Application Layer (응용 계층)

- 사용자와 직접 연결되어 네트워크 접근을 돕는 계층
- 데이터 전송을 위한 인터페이스 제공
- 사용자로부터 입력 받은 정보를 하위계층에 전달함

#### 1-2) Presentation Layer (표현 계층)

- 데이터를 응용계층에서 사용하는 표현으로 변환해주는 계층
- 데이터의 인코딩과 디코딩이 이루어진다.
- 문자열을 ASCII 코드로 변환

#### 1-3) Session Layer (세션 계층)

- 컴퓨터간 연결인 세션의 생성과 유지를 관리하는 계층
- 오류 발생시 복구 역할을 한다.

##### 1) Session

- 프로세스들 사이에 통신을 하기 위해 메시지 교환을 통해 서로를 인식한 후 이후부터 통신을 마칠 때까지의 기간

#### 1-4) Transport Layer (전송 계층)

- 데이터를 신뢰성 있게 전송하기 위한 계층
- 패킷을 나누어 전송하고, 실패할 경우 다시 패킷을 보내는 역할을 수행한다.
- TCP (Transmission Control Protocol)
- UDP (User Datagram Protocol)

#### 1-5) Network Layer (네트워크 계층)

- 데이터 전송 경로, 순서 등을 결정하는 계층
- 데이터를 Packet 단위로 분할하여 전송하고, 수신시 합치는 역할을 한다.
- IP 주소를 사용하여 데이터를 전송

#### 1-6) Data Link Layer (데이터 링크 계층)

- 물리적인 기기들 사이에서 데이터를 전송하는 계층
- 패킷을 프레임으로 구성하고, 각 프레임에 대한 에러 검사와 수정을 수행
- MAC를 사용하여 데이터를 전송

#### 1-7) Physical Layer (물리 계층)

- 데이터를 물리적인 신호로 변환하는 계층
- 단순 전달만 수행하며, 데이터를 검증하지 않음
- 비트 단위의 전기 신호를 전달한다.

![alt](/assets/images/post/ComputerStudy/1058.png)

## 3. 왜 우리는 OSI 7계층을 알아야 할까?

### 1) OSI 7 계층의 특징

- 네트워크 프로토콜을 나타내는 표준 규약이다.
- 네트워크 과정이 7개의 계층으로 모듈화 되어있다.
- 각 계층은 특정한 역할과 기능을 수행한다.
- 각 계층은 다른 계층과 독립적으로 동작한다.
- 각 계층은 인접한 계층과만 통신하며, 다른 계층에 미치는 영향을 최소화한다.

### 2) 이유

- 데이터 전송 과정을 단계적으로 이해함으로써, 네트워크 기반 서비스를 설계할 수 있다.
- 각 계층의 역할과 발생할 수 있는 문제를 이해함으로써, 네트워크 문제를 빠르게 추적하고 해결할 수 있다.

## 출처

<a href="https://www.youtube.com/watch?v=wuOzMvNEzAg">이오의 OSI 7계층</a>
