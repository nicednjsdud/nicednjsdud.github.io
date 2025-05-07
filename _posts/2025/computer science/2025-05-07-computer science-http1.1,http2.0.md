---
published: true
title: "🌐 HTTP/1.1 → HTTP/2 전환기: Nginx 설정으로 해결한 실무 장애 경험"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: "HTTP/1.1 환경에서 겪었던 실무 장애를 Nginx HTTP/2 설정으로 해결했던 경험을 바탕으로, HTTP/2의 장점과 적용 방법을 공유합니다."
tag: "HTTP, HTTP2, Nginx, 웹 성능, 실무 트러블슈팅"
article_tag1: "HTTP 프로토콜"
article_section: "웹 인프라"
meta_keywords: "HTTP1.1 문제, HTTP2 장점, Nginx HTTP2 설정, 웹 최적화"
last_modified_at: "2025-05-07 00:25:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🌐 HTTP/1.1 → HTTP/2 전환기: Nginx 설정으로 해결한 실무 장애 경험

---

## 🚨 시작은 갑작스러운 응답 오류

어느 날, 배포 이후 웹 페이지에서 **간헐적인 응답 지연**과  
**504 Gateway Timeout 오류**가 터지기 시작했습니다.

- 페이지는 로딩이 안 되고...
- 콘솔에는 특정 JS/CSS 요청이 계속 대기 상태...
- 서버 로그는 조용한데, 사용자는 계속 에러를 보고 있었습니다.

처음에는 네트워크 문제라고 생각했지만,  
원인은 **HTTP/1.1의 구조적 한계**에 있었습니다.

---

## 🧩 원인 분석: HTTP/1.1의 파이프라이닝 문제

우리는 **HTTP/1.1** 환경에서 서비스를 운영하고 있었고,  
클라이언트는 Nginx를 거쳐 서버에 요청을 보내고 있었습니다.

### 발견된 문제

- 하나의 커넥션에 여러 요청이 순차적으로 쌓이는 구조 (파이프라이닝)
- 첫 번째 JS 요청이 지연되자, 나머지 리소스 요청도 줄줄이 대기
- 결과적으로 **모든 리소스 로딩이 멈추고 504 오류** 발생

### 정리하면…

> 하나의 커넥션에서 **요청은 순차적으로만 응답 가능** →  
> 첫 요청이 느리면 나머지도 줄줄이 묶임 = **HOL Blocking**

---

## 🚀 해결: HTTP/2로 전환

### ✅ 해결 전략

1. 클라이언트 → Nginx → Spring 서버 구조 유지
2. **Nginx에서 HTTP/2 활성화**
3. 테스트 결과: 요청 병렬 처리로 **응답 지연 완전 해결**

---

## 🔧 Nginx에서 HTTP/2 활성화 방법

### 1️⃣ 기존 설정 (HTTP/1.1)

```nginx
server {
    listen 443 ssl;
    server_name example.com;

    ssl_certificate /etc/nginx/certs/fullchain.pem;
    ssl_certificate_key /etc/nginx/certs/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
    }
}
```

### 2️⃣ 수정된 설정 (HTTP/2 적용)

```nginx
server {
    listen 443 ssl http2;  # http2 명시
    server_name example.com;

    ssl_certificate /etc/nginx/certs/fullchain.pem;
    ssl_certificate_key /etc/nginx/certs/privkey.pem;

    location / {
        proxy_pass http://localhost:8080;
    }
}
```

📌 **주의**: HTTP/2는 TLS 기반(HTTPS)에서만 동작하므로 SSL 설정이 필수입니다.

---

## 📈 전환 후 변화

| 항목        | 전 (HTTP/1.1)              | 후 (HTTP/2)            |
| ----------- | -------------------------- | ---------------------- |
| 요청 방식   | 순차 요청/응답             | 병렬 요청/응답         |
| 지연 요소   | 첫 요청이 늦으면 전체 지연 | 요청끼리 독립적 처리   |
| 페이지 로딩 | 느림, 일부 504 오류        | 부드럽고 빠른 로딩     |
| 사용자 경험 | 페이지 깨짐, 대기          | 오류 없음, 반응 속도 ↑ |

---

## 🔍 HTTP/2의 기술적 장점 요약

| 기능                  | 설명                                  |
| --------------------- | ------------------------------------- |
| **멀티플렉싱**        | 하나의 커넥션에서 요청/응답 병렬 처리 |
| **바이너리 프레이밍** | 텍스트 대신 바이너리 처리로 속도 향상 |
| **HPACK 헤더 압축**   | 반복되는 헤더를 압축해 대역폭 절약    |
| **HOL Blocking 해결** | 응답 순서에 얽매이지 않음             |

---

## 💡 정리하며

실제로 경험해 보니, 단순한 프로토콜 차이 하나가  
**서비스 응답성과 사용자 경험에 큰 영향을 미친다**는 걸 체감했습니다.

---
