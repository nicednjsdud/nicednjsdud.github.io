---
title: (10분 테크톡) TCP / IP
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
last_modified_at: "2023-05-04 14:00:00 +0800"
toc: true
toc_sticky: true
toc_label: 목차
---

# TCP/IP

## 목차

1. 인터넷
2. TCP/IP 계층
3. TCP/IP 흐름
4. 신롸할 수 있는 TCP

## 1. 인터넷

- 전 세계에 걸쳐 파일 전송 등의 데이터 통신 서비스를 받을 수 있는 컴퓨터 네트워크 시스템

## 2. TCP / IP

- 인터넷에서 컴퓨터들이 서로 정보를 주고 받는데 쓰이는 프로토콜의 집합

## 3. TCP / IP의 계층

![alt](/assets/images/post/ComputerStudy/998.png)

### 1) Application Layer

- 특정 서비스를 제공하기 위해 애플리케이션 끼리 정보를 주고 받을 수 있음
- FTP, HTTP, SSH, Telnet, DNS, SMTP

### 2) Transport Layer

- 송신된 데이터를 수신측 애플리케이션에 확실히 전달하게 함
- TCP, UDP, RTP, RTCP

### 3) Internet Layer

- 수신 측까지 데이터를 전달하기 위해 사용됨
- IP, ARP, ICMP, RARP, OSPF

### 4) Network Access Layer

- 네트워크에 직접 연결된 기기 간 전송을 할 수 있도록 해줌
- Ethernet, PPP, Token Ring

## 4. TCP / IP의 흐름

- "www.google.com"을 웹브라우저에 입력하면 무슨일 일어날까?

### 1) Application Layer (HTTP)

- (http) www.google.com(:80)
- HTTP로 작성된 해당 요청 처리 부탁해요
- 아래와 같은 HTTP Request 메세지를 구글 80포트로 보냄

![alt](/assets/images/post/ComputerStudy/999.png)

### 2) Transport Layer (TCP)

![alt](/assets/images/post/ComputerStudy/1000.png)

- SP : 시작 포트 번호
- DP : 목적지 포트 번호

### 3) Internet Layer (IP)

![alt](/assets/images/post/ComputerStudy/1001.png)

- SA : 시작 IP 주소
- DA : 목적지 IP 주소
- 지금은 www.google.com이라는 도메인 정보만 알고 있음
- DNS 프로토콜을 통해서 도메인 정보로 IP주소를 알아낼 수 있음

#### 3-1) DNS

![alt](/assets/images/post/ComputerStudy/1002.png)

- DNS에게 domain에 대한 IP주소를 알고 싶다고 요청
- 그러면 OS에서 DNS서버로 요청을 보내게 됨

  - DNS서버 주소는 이미 컴퓨터에 등록이 되어있음

- DNS 또한 HTTP와 같은 애플리케이션 계층 프로토콜이다. (53번 포트)

![alt](/assets/images/post/ComputerStudy/1003.png)

- DNS도 HTTP Request로 도메인이 담긴 쿼리를 도메인 서버로 보냄
- Transport Layer에서 UDP라는 프로토콜을 사용
- UDP는 TCP와는 다르게 헤더가 간단
  - UDP는 비연결지향형 프로토콜이기 때문이다.

### 4) Network Access Layer

![alt](/assets/images/post/ComputerStudy/1004.png)

- 물리적으로 연결된 공유기의 MAC 주소가 필요하다.

![alt](/assets/images/post/ComputerStudy/1005.png)

- 이공유기를 통해 다른 네트워크와 연결이 가능
- 게이트웨이라고 부르기도 함

![alt](/assets/images/post/ComputerStudy/1006.png)

- netstat -rn 명령어를 통해 게이트웨이 IP를 알 수 있음
- IP주소로 MAC주소를 알아내기 위해 ARP 프로토콜을 사용

#### 4-1) ARP

- IP주소를 MAC주소로 바꾸어주는 주소해석 프르토콜

### 5) 3 - way - Handshaking

- TCP는 연결 지향형 프로토콜이기 때문에 송신측과 수신측이 서로 연결되는 작업이 필요하다.

![alt](/assets/images/post/ComputerStudy/1007.png)

- 3-way-Handshaking을 사용하기위해 TCP 헤더에 표시한 플래그들이 사용됨

  - 이러한 플래그들을 컨트롤 비트하고 부름

- SYN, ACK 플래그가 사용됨

![alt](/assets/images/post/ComputerStudy/1008.png)

- 클라이언트는 서버에게 접속을 요청하는 SYN 패킷을 보냄
- 서버는 SYN 요청을 받고, 클라이언트에게 요청을 수락한다는 ACK, SYN 플래그가 설정된 패킷을 보냄
- 클라이언트는 서버에게 다시 ACK를 보냄
- 이제부터 연결이 이루어지고 데이터가 오가게 됨

### 6) NAT (Network Address Translation)

![alt](/assets/images/post/ComputerStudy/1009.png)

- 내가 사용하는 컴퓨터는 Private IP를 사용하고 있다.
- Private IP는 외부에서 사용하는 IP주소를 찾지 못한다.
- 그래서 공유기를 통해 나갈때 public ip로 주소를 변환하여 나가는 작업이 필요
- 이러한 작업을 NAT 이라고 함

### 7) Routing

![alt](/assets/images/post/ComputerStudy/1010.png)

- 구글 서버에 도착하기 위해 여러 라우터를 거쳐가야 함

### 8) ARP

![alt](/assets/images/post/ComputerStudy/1011.png)

- 라우팅을 거쳐 구글 서버가 있는 곳까지 도달하게 되면
- 패킷의 IP헤더에 기록된 구글 서버 IP 주소를 통해 MAC주소를 얻어와야 함
- 라우터가 연결된 네트워크에 브로드캐스팅이 됨

![alt](/assets/images/post/ComputerStudy/1012.png)

- 목적지 구글서버가 자신의 IP로 온 ARP 요청을 받고 MAC주소를 응답해줌
- MAC주소를 알았으니 데이터가 물리적으로 전달 될 수 있음

### 9) Transport Layer (Server)

- 포트번호 80이 적혀있다.
- 이것을 보고 80번 포트를 사용하고 있는 애플리케이션에게 데이터를 전달해줘야 하는 것을 알 수 있음

### 10) Application Layer (Server)

- 웹 서버가 사용될 HTTP Request 데이터를 얻을 수 있음

### 11) Routing (to Client)

- HTTP Request를 받고 응답을 돌려보냄
- `"/"`에 매핑된 GET요청을 처리해서 적절한 HTML을 응답해줌

### 12) 4 - Way - Handshaking

![alt](/assets/images/post/ComputerStudy/1013.png)

- HTTP의 요청과 응답과정이 끝나면 연결을 종료해야 함
- 여기서도 TCP 컨트롤 비트가 사용됨
- ACK, FIN 플래그 사용

![alt](/assets/images/post/ComputerStudy/1014.png)

- 클라이언트가 서버로 연결을 종료 하겠다는 FIN 플래그를 전송
- 서버는 클라이언트에게 ACK 메세지를 보내고 자신의 통신이 끝날 때 까지 기다림
- 서버가 통신이 끝나면 클라이언트로 FIN을 보냄
- 클라이언트는 확인했다는 의미로 서버에게 ACK을 보내면 연결이 종료됨

![alt](/assets/images/post/ComputerStudy/1015.png)

- 서버가 FIN을 보내는 과정에서 한가지 문제가 발생할 수 있음
  - 서버가 FIN을 보내기 전에 보냈던 데이터가 FIN보다 늦게 도착할 경우 서버에게 FIN을 받았다고 클라이언트가 바로 연결된 소켓을 닫아버리면  
    FIN을 보내기전에 보낸 패킷은 영영 클라이언트가 받을 수 없게 됨
  - 그래서 클라이언트는 서버로부터 FIN 요청을 받더라도 일정시간동안 소켓을 닫지 않고 혹시나 아직 도착하지 않은 잉여 패킷을 기다림

## 5. 신뢰할 수 있는 TCP

![alt](/assets/images/post/ComputerStudy/1016.png)

- 요즘 세상에 우리는 엄청나게 큰 데이터를 주고 받음
- 그래서 한개의 패킷으로만 주고 받기에는 상당한 무리가 있음

- 그래서 데이터를 잘게 쪼개서 보내게 되고 많은 패킷을 보내게 됨
- 그리고 이많은 패킷은 엄청 복잡한 인터넷을 통해 목적지로 이동하게 됨
- 이것을 가능하개 해주는게 신뢰할 수 잇는 프로토콜인 TCP 이다.

- TCP는 흐름제어, 오류제어, 혼잡제어를 통해 신뢰성있는 데이터 전송을 보장

## 출처

<a href="https://www.youtube.com/watch?v=BEK354TRgZ8">수리의 TCP/IP</a>
