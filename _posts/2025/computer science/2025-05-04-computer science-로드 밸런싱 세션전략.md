---
published: true
title: "🛠 Spring Boot + Nginx + AWS에서 로드 밸런싱 적용과 세션 전략"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: "로드 밸런서를 실제 Spring Boot, Nginx, AWS 환경에서 어떻게 설정하고 세션 문제를 해결할 수 있는지 실용 예제 중심으로 설명합니다."
tag: "로드밸런서, 스프링부트, Nginx, AWS, 세션"
article_tag1: "로드밸런싱 실전"
article_section: "Backend Infrastructure"
meta_keywords: "로드밸런싱, 세션 전략, AWS ELB, Spring Boot, Nginx, Sticky Session"
last_modified_at: "2025-05-04 23:20:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🛠 Spring Boot + Nginx + AWS에서 로드 밸런싱 적용과 세션 전략

---

## ✅ 실무 환경에서 왜 세션 전략이 중요할까?

> 서버가 여러 대인 상태에서 로그인한 사용자의 세션이 유지되지 않는 문제 발생 😱

```text
Client → [Load Balancer] → Server A (로그인됨)
       → [Load Balancer] → Server B (세션 없음 → 로그아웃됨)
```

이 문제를 해결하려면 **로드 밸런싱 설정**과 **세션 공유 전략**이 모두 필요합니다.

---

## 1️⃣ Spring Boot + Nginx 환경 설정 예시

### 🔹 기본 구조

```text
Nginx (Reverse Proxy, Load Balancer)
  ↳ Spring Boot App A
  ↳ Spring Boot App B
```

### 🔧 Nginx 설정 (Round Robin + Sticky Session)

```nginx
upstream backend {
    ip_hash;  # Sticky Session 유지
    server 127.0.0.1:8081;
    server 127.0.0.1:8082;
}

server {
    listen 80;
    location / {
        proxy_pass http://backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

📌 `ip_hash;` 설정이 **클라이언트 IP 기반으로 고정 서버 연결**을 유지하게 함 (Sticky Session)

---

## 2️⃣ Spring Boot + Redis (세션 공유 전략)

Spring Boot는 기본적으로 세션을 **메모리(서버 내)**에 저장하기 때문에  
로드 밸런싱 환경에서는 세션 공유가 안 됩니다.

### ✅ Redis로 세션 저장하기

**의존성 추가 (build.gradle)**

```groovy
implementation 'org.springframework.session:spring-session-data-redis'
implementation 'org.springframework.boot:spring-boot-starter-data-redis'
```

**application.yml**

```yaml
spring:
  session:
    store-type: redis
  redis:
    host: localhost
    port: 6379
```

이제 모든 서버가 **동일한 Redis 세션 스토리지**를 사용함 → 세션 불일치 해결

---

## 3️⃣ AWS에서 로드 밸런싱 + 세션 전략

### ✅ AWS ELB 구성 예시

- **ALB (Application Load Balancer)** 사용
- **타겟 그룹**에 Spring Boot 서버들을 추가
- **로드 밸런싱 알고리즘**: 기본은 Round Robin

### 🔐 세션 문제 해결 방법

- **Sticky Session** 사용

  - ALB 설정에서 **고정 세션(Stickiness)** 옵션 ON
  - 쿠키 기반으로 클라이언트 요청을 고정 서버로 연결

- **Redis 세션 저장 (Spring Session)**  
  → EC2 여러 대, ECS 여러 컨테이너 모두 동일 Redis 접근 가능

---

## ✨ 보너스: JWT를 활용한 Stateless 인증

### ✅ 구조

```text
Client <-> Load Balancer <-> Any Server
          ↳ 서버는 세션 상태를 기억하지 않음
```

- 모든 요청에 JWT 포함
- 서버는 토큰만 검증 → **세션 저장소가 필요 없음**
- 수평 확장에 최적

📌 단점: 토큰 탈취 시 위험, 로그아웃 구현 복잡

---

## 🧠 상황별 전략 요약

| 상황                     | 추천 방식                                            |
| ------------------------ | ---------------------------------------------------- |
| 빠른 적용, 소규모        | Sticky Session (Nginx ip_hash or AWS ALB stickiness) |
| 고가용성, 세션 유지 필요 | Redis + Spring Session                               |
| 완전 Stateless 구조      | JWT 인증 방식                                        |

---

## 📚 마무리 요약

- 로드 밸런싱은 **네트워크 분산**의 기본
- 세션을 공유하지 않으면 로그인 유지가 어려움
- Redis, Sticky, JWT 등 **상황에 맞는 전략** 선택이 중요

---
