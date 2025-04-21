---
published: true
title: "🔐 HTTPS란? 백엔드를 위한 암호화 통신의 기본 개념과 원리"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Backend
  - Network
  - Security
description: "HTTP와 HTTPS의 차이, 그리고 HTTPS가 어떻게 동작하는지 백엔드 개발자 시선에서 정리합니다."
tag: "HTTPS, TLS, 보안, 백엔드, 암호화 통신"
article_tag1: "HTTPS"
article_section: "백엔드"
meta_keywords: "HTTPS란, HTTPS 동작 원리, TLS, SSL, 백엔드 보안, 인증서"
last_modified_at: "2025-04-19 21:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🔐 HTTPS란? 백엔드를 위한 암호화 통신의 기본 개념과 원리

---

## 🌐 HTTP란?

> **HTTP (Hypertext Transfer Protocol)**  
> 웹에서 데이터를 주고받기 위한 **비암호화 통신 프로토콜**입니다.

하지만 문제는...

- **데이터가 평문(Plain Text)으로 전송됨**
- **중간자(MITM)에 의해 탈취될 위험**
- **민감한 정보(로그인, 결제 등)는 쉽게 노출될 수 있음**

👉 그래서 등장한 것이 바로 **HTTPS**입니다.

---

## 🔒 HTTPS란?

> **HTTPS (Hypertext Transfer Protocol Secure)**  
> HTTP 위에 **암호화(SSL/TLS)** 계층이 추가된 보안 프로토콜입니다.

📦 HTTPS는 세 가지를 보장합니다:

1. **기밀성** – 데이터를 암호화해서 외부 노출 차단
2. **무결성** – 데이터가 도중에 변경되지 않도록 검증
3. **인증** – 통신 대상이 진짜 서버인지 확인

---

## 📜 HTTPS를 사용하려면?

1. **SSL 인증서(Certificate)**를 구매하거나 무료로 발급 받기 (ex: Let's Encrypt)
2. 서버에 설치하고 포트 443을 통해 HTTPS 요청을 수신
3. HTTPS를 통해 암호화 통신 시작

> 인증서는 **CA(Certificate Authority)** 라는 신뢰기관에서 발급합니다.  
> 예: Digicert, GlobalSign, Let's Encrypt 등

---

## 🔁 HTTPS 동작 원리 (TLS Handshake)

### 1. 클라이언트 → 서버

- 지원하는 암호화 알고리즘 목록
- TLS 버전
- 랜덤한 값 (Client Random)

### 2. 서버 → 클라이언트

- 서버 인증서 (CA로부터 발급받은 것)
- 서버 랜덤 값 (Server Random)
- 선택된 암호화 알고리즘

### 3. 인증서 검증

- 클라이언트는 서버 인증서를 받아 **CA의 공개키**로 복호화하여 진위 확인
- 만약 신뢰할 수 없는 인증서라면 연결 실패

### 4. Pre-Master Secret 생성

- 클라이언트는 새로운 Pre Master Secret 값을 만들어 서버의 공개키로 암호화해 전송

### 5. 서버는 개인키로 복호화

- 서버는 Pre Master Secret 값을 받아 복호화
- 클라이언트와 서버는 이를 바탕으로 **같은 Master Secret**을 생성

### 6. 세션 키 생성

- Master Secret을 기반으로 **대칭키(세션 키)**를 만들고
- 이후 통신은 이 세션 키로 암호화하여 주고받음 (빠르고 안전함)

---

## 🔐 암호화 알고리즘 방식 요약

| 단계       | 방식                   | 설명                           |
| ---------- | ---------------------- | ------------------------------ |
| 핸드쉐이크 | 공개키 암호화 (비대칭) | 안전한 키 교환용               |
| 본격 통신  | 대칭키 암호화          | 빠른 속도로 실제 데이터 암호화 |

---

## 📌 정리하면?

| 항목        | HTTP    | HTTPS                 |
| ----------- | ------- | --------------------- |
| 암호화      | ❌ 없음 | ✅ 있음 (TLS)         |
| 인증서 사용 | ❌ 없음 | ✅ 필요               |
| 보안성      | 낮음    | 높음 (도청/위조 방지) |
| 사용 포트   | 80      | 443                   |

---

## 🚀 실무에서 HTTPS를 적용하려면?

1. SSL 인증서 발급받기 (무료: Let’s Encrypt, 유료 CA)
2. Nginx 또는 Spring Boot에서 HTTPS 설정
3. 도메인 연결 시, HTTP → HTTPS 리다이렉트도 함께 설정

---
