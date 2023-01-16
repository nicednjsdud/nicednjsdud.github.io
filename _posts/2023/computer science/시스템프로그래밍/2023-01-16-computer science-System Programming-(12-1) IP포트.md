---
title: (시스템 프로그래밍) 12-1 IP 및 포트
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: IP및 포트
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

# 시스템 프로그래밍 - IP 및 포트

## 1. TCP/IP

### 1) TCP/IP

- Transmission Control Protocol / Internet Protocol
- 인터넷의 표준 프로토콜
- 5계층(4계층)으로 구성

#### (1) TCP/IP 5계층

##### (1-1) 응용 계층 (application layer)

- 사용자에게 서비스를 제공하는 계층

##### (1-2) 전송 계층 (transport layer)

- 패킷 전송 담당 계층
- TCP : Transmission control Protocol
- UDP : User Datagram Protocol

##### (1-3) 네트워크 계층 (network layer)

- 인터넷 계층이라고도 함, 패킷 전달되는 경로 담당
- IP : Internet Protocol
- ICMP : Internet Control Message Protocol, IP 진단이나 제어 및 오류 응답
- IGMP : Internet Group Management Protocol, 호스트 컴퓨터와 주위 라우터 관리용 포르트콜
- ARP : Address Resolution Protocol, IP주소를 물리적 네트워크 주소(MAC Address)로 변환
- RARP : Reverse Address Resolution Protocol. 물리적 네트워크 주소를 IP주소로 변환

##### (1-4) 네크워크 접속 / 하드웨어 계층

- 이더넷 카드/ 카드

![alt](/assets/images/post/ComputerStudy/703.png)

#### (2) TCP와 UDP의 차이

##### (2-1) TCP

- 연결 지향형
- **신뢰성 보장**
- 흐름제어 기능 보장
- 순서 보장

##### (2-2) UDP

- 비연결형
- 신뢰성을 보장하지 않음
- 흐름 제어 기능 없음
- 순서를 보장하지 않음

#### (3) port number

- 전송되어오는 데이터를 어떤 프로세스가 수신해 서비스를 제공할 지 미리 알려주는 번호
- 2byte : 1 ~ 65535
- 일반 프로그램 : 1024 ~ 65535 포트 번호 사용

#### (4) well-known port

- 인터넷 서비스는 0 ~ 1023번 사용
- 이미 정해지고 알려진 번호를 well-known port라고함

```c
  서비스 명     |      포트 번호
  ftp                   21
  telnet                23
  SMTP                  25
  DNS                   53
  HTTP                  80
  POP3                  110
```

## 2. IP Address

### 1) IP주소와 호스트명

#### (1) IP 주소

- 인터넷을 이용할 때 사용하는 주소로 점(.)으로 구분된 32비트 숫자
- A,B,C,D,E 클래스 중 A,B,C 클래스만 사용중

#### (2) 호스트명

- 시스템에 부여된 이름
- 호스트명(도메인명)과 IP주소를 관리하는 서비스

#### (3) IPv4주소 및 IPv6주소 비교

##### (3-1) IPv4

- 32비트
- 8비트씩 4부분으로 10진수로 표시
- 약 43억개의 주소 개수
- 주소할당 : A,B,C 클래스 단위의 비순차적 할당
- 품질제어 : 지원 수단 없음
- 보안기능 : IPsec 프로토콜 별도 설치
- 플러그 앤드 플레이 : 지원수단 없음
- 모바일 IP : 상당히 곤란
- 웹개스팅 : 곤란

##### (3-2) IPv6

- 128비트
- 16비트씩 8부분으로 16진수로 표시
- 약 43억 X 43억 X 43억 X 43억개의 주소 개수
- 주소할당 : 네트워크 규모 및 단말기 수에 따른 순차적 할당
- 품질제어 : 등급별, 서비스별로 패킷을 구분할 수 있어 품질 보장이 용이
- 보안기능 : 확장기능에서 기본으로 제공
- 플러그 앤드 플레이 : 지원 수단 있음
- 모바일 IP : 용이
- 웹개스팅 : 용이

### 2) 호스트명과 IP주소 변환

#### (1) 호스트명과 IP주소 변환

- `/etc/hosts` 파일 또는 DNS, NIS 등
- `/etc/nsswitch.conf`파일에 주소변환을 누가 할것인지 지정

#### (2) 호스트명과 주소 읽어오기

```c
  #include <netdb.h>

  struct hostent *gethostent(void);
  int sethostent(int stayopne);
  int endhostent(void);
```

- stayopne : IP주소 DB를 열어둘지 여부를 나타내는 값

#### (3) IP주소와 호스트명

##### (3-1) gethostent

- 호스트명과 IP주소를 읽어 hostent 구조체에 저장

##### (3-2) sethostent

- 데이터베이스의 읽기 위치를 시작위치로 재설정

##### (3-3) endhostent

- 데이터베이스를 닫음

#### (4) 호스트명으로 정보 검색 : gethostbyname(3)

```c
  #include <netdb.h>

  struct hostent *gethostbyname(const char *name)
```

- name : 검색하려는 호스트명

#### (5) IP주소로 정보 검색 : gethostbyaddr(3)

```c
  #include <netdb.h>

  struct hostent *gethostbyaddr(const char *addr, int len, int type);
```

- addr : 검색하려는 IP주소
- len : addr길이
- type : IP주소 형식

### 3) 포트 정보 읽어오기

#### (1) getservent

- 포트 정보를 읽어 servent 구조체로 리턴

#### (2) serservent

- 읽기 위치를 시작으로 재설정

#### (3) endservent

- 데이터베이스 닫기

```c
  #include <netdb.h>

  struct servent *getservnet(void);
  int setservent(int seayopen);
  int endservent(void);
```

- stayopen : 포트 정보 데이터베이스를 열어둘지 여부를 나타내는 값

### 4) 서비스명으로 정보 검색

#### (1) getservbyname(3)

- 포트명을 인자로 받아 데이터베이스에서 해당 항목을 검색해 servent 구조체에 저장하고 그 주소를 리턴

```c
  #include <netdb.h>

  struct servnet *getservbyname(const char *name, const chat *proto);
```

- name : 검색할 포트명
- proto : tcp 또는 udp 또는 Null

#### (2) 포트 번호로 정보 검색 : getservbyport(3)

- 포트명을 인자로 받아 데이터베이스에서 해당 항목을 검색해 servent 구조체에 저장하고 그 주소를 리턴

```c
  #include <netdb.h>

  struct servent *getservbyport(int port, const char *proto);
```

- proto : tcp 또는 udp 또는 null
