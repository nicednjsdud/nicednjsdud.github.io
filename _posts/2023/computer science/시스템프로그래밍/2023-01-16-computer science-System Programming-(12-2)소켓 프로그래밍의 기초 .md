---
title: (시스템 프로그래밍) 12-2 소켓 프로그래밍의 기초
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 소켓 프로그래밍의 기초
layout: single
tag: Internet
article_tag1: Internet
article_section: Internet
meta_keywords: CS50,computer,cs,시스템 프로그래밍
last_modified_at: "2023-01-16 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# 시스템 프로그래밍 - 소켓 프로그래밍 기초

## 1. 소켓

### 1) 소켓의 종류

- 응용 계층과 전송 계층을 연결 기능 제공
- 네트워크에 대한 사용자 수준의 인터페이스를 제공
- 소켓으느 양방향 통신 방법으로 클라이언트
- 서버 모델을 기반으로 프로세스 사이의 통신에 매우 적합

#### (1) 소켓 인터페이스

![alt](/assets/images/post/ComputerStudy/704.png)

- 응용 프로그램과 TCP 계층을 연결하는 역할
- 네트워크 프로그래밍 작성 용이

#### (2) 종류

##### (2-1) AF_UNIX

- 유닉스 도메인 소켓 (시스템 내부 프로세스간 통신)

##### (2-2) AF_INET

- 인터넷 소켓 (네트워크를 이용한 통신)

### 2) 소켓의 통신 방식

- SOCK_STREAM : TCP 사용
- SOCK_DGRAM : UDP 사용

![alt](/assets/images/post/ComputerStudy/705.png)

## 2. 소켓 프로그래밍

### 1) 소켓 주소 구조체

#### (1) 유닉스 도메인 소켓의 주소 구조체

```c
  struct sockaddr_un {
    sa_family_t sun_family;
    char sun_path[108]
  };
```

- sun_family : AF_UNIX
- sun_path : 통신에 사용할 파일의 경로명

#### (2) 인터넷 소켓의 주소 구조체

```c
  struct sockaddr_in {
    sa_faily_t sin_family;
    in_port_t sin_port;
    struct in_addr sin_addr
  };
  struct in_addr {
   in_addr_t s_addr;
  };
```

- sin_family : 주소 패밀리
- sin_port : 주소 포트 번호
- sin_addr : IP주소

### 2) 바이트 순서 함수

- 정수를 저장하는 방식 : 빅엔디안, 리틀엔디안

#### (1) 빅엔디안 (최상위 바이트 우선)

- 메모리에 낮은 주소에 정수의 첫 바이트를 위치 : 모토로라, 썬

#### (2) 리틀엔디안 (최하위 바이트 우선)

- 메모리에 높은 주소에 정수의 첫 바이트를 위치 : 인텔

![alt](/assets/images/post/ComputerStudy/706.png)

#### (3) TCP/IP 네트워크에서 바이트 순서 표준 : 빅엔디안

- 호스트 바이트 순서(HBO) : 시스템에서 사용하는 바이트 순서
- 네트워크 바이트 순서(NBO) : 네트워크에서 사용하는 바이트 순서

#### (4)

```c
  #include <sys/types.h>
  #include <netinet/in.h>
  #include <inttypes.h>
  uint32_t htonl(unit32_t hostlong);
  uint16_t htons(unit16_t hostshort);
  uint32_t ntohl(unit32_t netlong);
  uint16_t ntons(unit16_t hostshort);
```

- htonl : 32비트 HBO를 32비트 NBO로 변환
- htons : 16비트 HBO를 16비트 NBO로 변환
- ntohl : 32비트 NBO를 32비트 HBO로 변환
- ntons : 16비트 NBO를 16비트 HBO로 변환

### 3) IP주소 변환 함수

#### (1) IP주소의 형태

- 192.168.10.1과 같이 점(.)으로 구분된 형태
- 시스템 내부 저장 방법 : 이진값으로 바꿔서 저장
- 외부적 사용 형태 : 문자열로 사용

#### (2) 문자열 형태의 IP주소를 숫자형태로 변환 : inet_addr(3)

```c
  #include <sys/types.h>
  #include <sys/socket.h>
  #include <netinet/in.h>
  #include <arpa/inet.h>

  in_addr_t inet_addr(const char *cp);
```

#### (3) 구조체 형태의 IP주소를 문자열 형태로 변환 : inet_ntoa(3)

```c
  #include <sys/types.h>
  #include <sys/socket.h>
  #include <netinet/in.h>
  #include <arpa/inet.h>

  char *inet_ntoa(const struct in_addr in);
```

