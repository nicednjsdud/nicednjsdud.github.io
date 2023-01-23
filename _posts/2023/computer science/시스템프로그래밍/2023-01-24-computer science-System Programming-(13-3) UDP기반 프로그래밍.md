---
title: (시스템 프로그래밍) 13-3 UDP 기반 프로그래밍
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: UDP 기반 프로그래밍
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2023-01-24 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - UDP 기반 프로그래밍

## 1. UDP 기반 프로그래밍

### 1) 개념

- 클라이언트로부터 사전에 연결 요청을 받지 않음
- 클라이언트 : connect()함수 사용하지 않음
- 서버 : `bind()` 함수 후 `listen()`함수 사용하지 않음
- 서버 -> 클라이언트 : 클라이언트 주소가 구조체임

#### (1)

- IP를 기반으로 데이터를 전송함 (TCP와 공통점)

#### (2)

- 흐름제어(flow control)을 하지 않기 때문에 데이터 전송을 보장 받지 못함

#### (3)

- 연결설정 및 연결 종료 과정도 존재하지 않음

#### (4)

- 연결 상태가 존재하지 않음

### 2) 특징

- 데이터 경계가 존재하는 UDP 소켓
- UDP소켓은 데이터를 송 수신하는데 필요한 함수 호출의 수를 정확히 일치 시켜야함

![alt](/assets/images/post/ComputerStudy/780.png)

### 3) UDP의 역할

- 포트 정보에 의한 프로세스의 구분
- UDP 패킷 = 데이터 그램 (Datagram)

![alt](/assets/images/post/ComputerStudy/781.png)

- 소켓을 생성하고 `bind`까지만 하면 바로 입출력함수를 사용하면 됨
- socket~bind : 서버
- socket : 클라이언트
- **일반적으로 연결 설정 과정을 거치지 않음**
- 데이터를 주고 받기 위한 소켓은 하나만 생성해도 됨
- UDP는 비연결 프로토콜이기 때문에 주소 정보를 알아야함

### 4) connect 함수 호출을 통한 성능의 향상

#### (1) TCP 소켓에서의 connect함수의 의미

- IP와 포트의 할당
- Three-way handshaking

#### (2) UDP 소켓에서의 connect함수의 의미

- IP와 포트의 할당
- connect함수가 없으면 sendto 함수가 제일 처음 호출되는 시점에 IP와 PORT가 할당됨
- 클라이언트에서 IP와 PORT가 한번 할당되면 `close()`함수 호출시까지 변하지 않음

### 5) TCP/ UDP 소켓에서 공통적으로 가지는 connect의 의미

#### (1) connect함수의 의미

- 커널과 소켓이 논리적으로 연결하고 그것을 유지함

![alt](/assets/images/post/ComputerStudy/782.png)

#### (2) connect함수를 호출하지 않을때 UDP 클라이언트의 데이터 송수신

![alt](/assets/images/post/ComputerStudy/783.png)

- sendto, recvfrom 함수를 호출하면 커널과 소켓이 연결되고 소켓과 호스트와 통신할 준비를 함
- 호출이 끝나면 커널과 소켓의 연결이 해제됨
- 2과정을 반복하는데 많은 시간을 잡아먹고 커널과 소켓을 연결,해체하기 때문에 성능 효율이 떨어짐

#### (3) connect 함수 호출이 주는 이점

- 데이터를 주고 받는 속도가 빨라짐
- TCP 소켓 기반의 데이터 입출력 함수를 그대로 사용할 수 있음

### 6) 데이터 전송 함수

```c
  int sendto(int sock,const void* msg, int len, unsigned flags,
                   const struct sockaddr *addr, int addrlen);
  int sendto(SOCKET s, const xhar FAR *buf, int len, int flags,
                   const struct sockaddr FAR*to,int tolen);
```

- 1 ~ 4 번째 인자는 TCP send함수와 비슷
- addr : 목적지 주소 정보
- addrlen : 목적지 주소 정보 구조체 크기

### 7) 데이터 수신 함수

```c
  int recvfrom(int sock, void *buf, int len, unsigned flags,
                  struct sockaddr * addr, int *addrlen);
  int recvfrom(SOCKET s, char FAR *buf,int len, int flags, struct sockaddr FAR *from,
                  int FAR *fromlen);
```

- 1 ~ 4 번째 인자는 TCP recv함수와 비슷
- addr : 목적지 주소 정보
- addrlen : 목적지 주소 정보 구조체 크기
