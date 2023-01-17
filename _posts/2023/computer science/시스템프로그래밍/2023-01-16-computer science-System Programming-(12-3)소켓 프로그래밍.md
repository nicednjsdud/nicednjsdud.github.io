---
title: (시스템 프로그래밍) 12-3 소켓 프로그래밍
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: 소켓 프로그래밍
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

# 시스템 프로그래밍 - 소켓 프로그래밍

## 1. 소켓 프로그래밍 함수

### 1) 소켓 인터페이스 함수

#### (1) 함수 종류

- socket : 소켓 파일기술자 생성
- bind : 소켓 파일기술자를 지정된 IP주소/포트번호와 결합
- listen : 클라이언트의 접속 요청 대기
- connect : 클라이언트가 서버에 접속 요청
- accept : 클라이언트의 접속 허용
- recv : 데이터 수신 (SOCK_STREAM)
- send : 데이터 송신 (SOCK_STREAM)
- recvfrom : 데이터 수신 (SOCK_DGRAM)
- sendto : 데이터 송신 (SOCK_DGRAM)
- close : 소켓 파일기술자 종료

#### (2) 소켓 생성하기 : socket

- domain에 지정한 소켓의 형식과 type에 지정한 통신방법을 지원하는 소켓 생성
- 성공 : 소켓 기술자 리턴
- 실패 : -1 리턴

```c
  #include <sys/types.h>
  #include <sys/socket.h>

  int socket(int domain, int type, int protocol);
```

- domain : 소켓 종류 (AF_UNIX, AF_INET)
- type : 통신방식 (TCP, UDP)
- protocol : 소켓에 이용할 프로토콜, 보통 0 지정

```c
  int sd;
  sd = socket(AF_INET, SOCK_STREAM, 0)
```

#### (3) 소켓에 이름 지정하기 : bind

- socket함수가 생성한 소켓 기술자 s에 sockaddr구조체인 name지정한 정보 연결
- 성공 : 0
- 실패 : -1리턴

```c
  #include <sys/types.h>
  #include <sys/socket.h>

  int bind(int s, const struct sockaddr *name, int namelen);
```

- s : socket 함수가 생성한 소켓 기술자
- name : 소켓의 이름을 표현한 기술자
- namelen : 이름의 길이

#### (4) 클라이언트 연결 기다리기 : listen

```c
  #include <sys/types.h>
  #include <sys/socket.h>

  int listen(int s, int backlog);
```

- s : socket 함수가 생성한 소켓 기술자
- backlog : 최대 허용 클라이언트 수
- 예 ) 클라이언트 연결 요청 받아들일 준비 마쳤고 최대 10개까지만 받음

```c
  listen(sd, 10);
```

#### (5) 연결 요청 수락하기 : accept(3) - 서버

- 클라이언트 : 연결 요청 수락
- 서버 : 소켓s를 통해 요청한 클라이언트와의 연결을 수락

```c
  #include <sys/types.h>
  #include <sys/socket.h>
  int accept(int s, struct sockaddr *addr, socklen_t *addrlen);
```

- s : socket함수가 생성한 소켓 기술자
- addr : 접속을 요청한 클라이언트의 IP정보
- addrlen : addr 크기

```c
  int sd, new_sd;
  struct sockaddr_in sin, clisin;
  new_sd = accpet(sd, &clisin, &sizeof(struct sockaddr_in));
```

#### (6) 서버와 연결하기 : connect(3) - 클라이언트

- 클라이언트가 서버에 연결 요청시 사용
- 성공 : 0
- 실패 : -1

```c
  #include <sys/types.h>
  #include <sys/socket.h>

  int connet(int s, const struct sockaddr *name, int namelen);
```

- s: socket 함수가 생성한 소켓 기술자
- name : 접속하려는 서버의 IP정보
- namelen : name의 크기

#### (7) 데이터 보내기 : send(3)

- 소켓 s를 통해 크기가 len인 메세지 msg를 flags에 지정한 방법으로 전송
- 성공 : 실제로 전송한 데이터의 바이트 수 리턴
- 실패 : -1

```c
  #include <sys/types.h>
  #include <sys/socket.h>

  int send(int s, const void *msg, size_t len, int flafs);
```

##### (7-1) flages

- MSG_OOB : 영역밖의 데이터 처리, SOCK_STREAM에서만 사용
- MSG_DONTROUTE : 데이터의 라우팅 설정을 해제

#### (8) 데이터 받기 : recv(3)

- 소켓 s를 통해 전송받은 메세지를 크기가 len인 buf에 저장

```c
  #include <sys/types.h>
  #include <sys/socket.h>

  ssize_t(int s,void *buf,size_t len, int flags);
```

#### (9) UDP 데이터 보내기 : sendto(3)

- UDP 프로토콜 활용 데이터 전송 함수
- 매번 목적지 주소 지정 필요

```c
  #include <sys/types.h>
  #include <sys/socket.h>

  ssize_t sentto(int s, const void *msg, size_t len, int flags,
                const struct sockaddr *to, int tolen);
```

- s : socket 함수가 생성한 소켓 기술자
- msg : 전송할 메세지를 저장한 메모리 주소
- len : 메모리의 크기
- flags: 데이터를 주고받는 방법을 지정한 플래그
- to : 메세지를 받을 호스트의 주소
- tolen : to의 크기
