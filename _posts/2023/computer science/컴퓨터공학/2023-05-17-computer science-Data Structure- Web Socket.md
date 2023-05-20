---
title: (10분 테크톡) Web Socket
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
last_modified_at: "2023-05-17 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 목차

1. 웹 소켓이란?
2. 웹 소켓의 특징
3. 웹 소켓 이전의 실시간 통신
4. 웹 소켓 동작 방법
5. 웹 소켓 프로토콜의 특징
6. 웹 소켓 특이점

## 1. 웹 소켓이란?

* 두 프로그램간의 메세지를 교환하기 위한 통신방법이다.
* W3C와 IETF에 의해 자리잡은 표준 프로토콜 중 하나이다.
* 현재 인터넷 환경(HTML5)에서 많이 사용된다.
* 웹소켓을 지원하는 브라우저의 경우 **웹 소켓 프로토콜을 지원**

![alt](/assets/images/post/ComputerStudy/1017.png)

## 2. 웹 소켓의 특징

### 1) 양방향 통신 ( Full - Duplex )

* 데이터 송수신을 동시에 처리할 수 있는 통신 방법
* 클라이언트와 서버가 서로에게 원할때 데이터를 주고 받을 수 있다.
* **통상적인 Http 통신**은 Client가 요청을 보내는 경우에만 Server가 응답하는 **단방향 통신**

### 2) 실시간 네트워킹 ( Real Time - Networking)

* 웹 환경에서 **연속된 데이터를 빠르게 노출**
* Ex) 채팅, 주식, 비디오 데이터
* 여러 단말기에 빠르게 데이터를 교환

## 3. 웹 소켓 이전의 비슷한 기술

### 1) Polling

![alt](/assets/images/post/ComputerStudy/1018.png)

* 서버로 일정 주기 요청 송신
* real-time 통신에서는 언제 통신이 발생할지 예측이 불가능
* 불필요한 request와 connection 생성
* Real-time 통신이라고 부르기 애매할 정도의 실시간성

### 2) Long Polling

![alt](/assets/images/post/ComputerStudy/1019.png)

* 서버에 요청 보내고 이벤트가 생겨 응답 받을 때 까지 연결 종료 X 
* 응답 받으면 끊고 다시 재요청
* 많은 양의 메세지가 쏟아질 경우 polling과 같다.

### 3) Streaming

![alt](/assets/images/post/ComputerStudy/1020.png)

* 서버에 요청 보내고 끊기지 않은 연결 상태에서 끊임없이 데이터 수신
* 클라이언트에서 서버로의 데이터 송신이 어렵다.

### 정리

* 결과적으로 이 모든 방법이 Http를 통해 통신하기 때문에 Request, Response 둘다 Header가 불필요하게 큼

## 4. 웹 소켓 동작 방법 - 핸드 쉐이킹 

### 1) 요청

![alt](/assets/images/post/ComputerStudy/1021.png)

#### 1-1) Get /chat HTTP/1.1

* 반드시 GET 메서드를 사용해야 한다.

#### 1-2) Host: server.example.com

* 웹 소켓 서버의 주소

#### 1-3) Upgrade: websocket

* 현재 클라이언트, 서버, 전송 프로토콜 연결에서 다른 프로토콜로 업그레이드 또는 변경하기 위한 규칙

#### 1-4) Connection : Upgrade

* Upgrade 헤더 필드가 명시되었을 경우 송신자는 반드시 Upgrade 옵션을 지정한 **Connection 헤더 필드**로 전송

#### 1-5) Sec-WebSocket-key : sfuiodADfjd

* 길이가 16바이트인 임의로 선태고딘 숫자를 base64로 인코딩 한 값

#### 1-6) Origin:http://example.com

* 클라이언트로 웹 브라우저를 사용하는 경우에 필수항목으로 클라이언트의 주소

#### 1-7) Sec-WebSocket-Protocol: chat, superchat

* 클라이언트가 요청하는 여러 서브 프로토콜을 의미
* 공백문자로 구분되며 순서에 따라 우선권이 부여
* 서버에서 여러 프로토콜 혹은 프로토콜 버전을 나눠서 서비스 할 경우 필요한 정보


### 2) 응답

![alt](/assets/images/post/ComputerStudy/1022.png)

#### 2-1) HTTP/1.1 101 Switching Protocols

* 101 Switching Protocols가 Response로 오면 웹소켓이 연결

#### 2-2) Sec-WebSock-Accept : 3f9809sd

* 클라이언트로부터 받은 Sec-WebSocket-Key를 사용하여 계산된 값

## 5. 웹 소켓 동작 방법 - 데이터 전송

![alt](/assets/images/post/ComputerStudy/1023.png)

* 프로토콜이 ws로 변경
* 데이터 보안을 위해 SSL을 적용한 프로그램 (wss)
* Message : 여러 frame이 모여 구성하는 하나의 논리적 매시지 단위
* frame : communication에서 가장 작은 단위의 데이터, **작은 헤더 + payload로 구성**
* 웹소켓 통신에 사용되는 데이터는 UTF8 인코딩
* Ex) 0x00 (보내고 싶은 데이터) 0xff

## 6. 웹 소켓 동작 방법 - 프레임이란?

![alt](/assets/images/post/ComputerStudy/1024.png)

### 1) END 비트

* 이 프렘이 전체 메세지의 끝인지 나타내는 플래그

### 2) Opcode 비트

* Continue (0x0) : 전체 메시지의 일부임을 의미
* Text (0x1) : 포함된 데이터가 UTF-8 텍스트라는 의미
* Binary (0x2) : 포함된 데이터가 이진 데이터라는 의미
* Close (0x8) : Close 핸드쉐이크를 시작한다는 의미

### 3) Length 비트

* 이 프레임에 포함된 데이터의 총길이를 나타내는 단위

## 7. 웹 소켓 동작 방식 - 간단 정리

![alt](/assets/images/post/ComputerStudy/1025.png)

## 8. 웹 소켓 프로토콜 특징

* 최초 접속에서만 http 프로토콜 위에서 handshaking을 하기 때문에 http header를 사용
* 웹소켓을 위한 별도의 포트는 없으며, 기존 포트 (http - 80, https-443)을 사용
* 프레임으로 구성된 메세지라는 논리적 단위로 송수신
* 메세지에 포함될 수 있는 교환 가능한 메시지는 텍스트와 바이너리

## 9. 웹소켓 한계 - Socket.io, SockJS

* HTML5 이전의 기술로 구현된 서비에스에서 웹 소켓처럼 사용할 수 있도록 도와주는 기술
* Javascript를 이요하여 브라우저 종류에 상관없이 실시간 웹을 구현
* WebSocket, FlashSocket, AJAX Long Pilling, AJAX Multi part Streaming, IFrame, JSONP Polling을 하나의 API로 추상화
* **즉, 브라우저와 웹 서버의 종류와 버전을 파악하여 가장 적합한 기술을 선택하여 사용하는 방식**

## 10. 웹소켓 한계 - STOMP

* WebSocket은 문자열들을 주고 받을 수 있게 해줄 뿐 그이상의 일 X
* 주고 받은 문자열의 해독은 온전히 어플리케이션에 맡긴다.
* HTTP는 형식을 정해두었기 때문에 모두가 약속을 따르기만 한다며 해석할 수 있다.
* 하지만 WebSocket은 형식이 정해져 있지 않기 때문에 어플리케이션에서 쉽게 해석하기 힘들다.
* 때문에 WebSocket방식은 Sub-protocols을 사용해서 주고 받는 메시지의 형태를 약속하는 경우가 많다.

### 1) STOMP (Simple Text Oriented Message Protocol)

* STOMP는 채팅 통신을 하기 위한 형식을 정의
* HTTP와 유사하게 간단히 정의되어 해석하기 편한 프로토콜
* 일반적으로 웹소켓 위에서 사용

### 2) 프레임 구조

![alt](/assets/images/post/ComputerStudy/1026.png)

* 프레임 기반의 프로토콜이다
* 프레임은 명령, 헤더, 바디로 구성된다.
* 자주 사용되는 명령은 CONNECT, SED, SUBSCRIBE, DISCONNECT 등이 있다.
* 헤더와 바디는 빈 라인으로 구분하여, 바디의 끝은 NULL 문자로 설정
