---
published: true
title: "⚖️ 로드 밸런싱이란 ?"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: "로드 밸런싱이란 무엇인지, 왜 필요한지, 어떤 방식으로 동작하는지 자세히 알아봅니다. 백엔드 기본기 강화!"
tag: "로드밸런싱, 백엔드, 트래픽분산, 서버인프라"
article_tag1: "로드 밸런서"
article_section: "백엔드 아키텍처"
meta_keywords: "로드밸런싱, Round Robin, Least Connection, IP 해시, L4 L7 차이"
last_modified_at: "2025-05-03 23:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# ⚖️ 로드 밸런싱 완전 정복: 알고리즘부터 실무 적용까지

---

## ✅ 로드 밸런싱이란?

> **들어오는 네트워크 트래픽을 여러 서버로 분산하는 기술**

로드 밸런서는 사용자의 요청을 받아서  
**적절한 서버에게 전달하는 게이트웨이** 역할을 합니다.

### 📍 로드 밸런서를 사용하는 이유

- ✅ 트래픽 분산
- ✅ 고가용성 (서버 장애에도 서비스 유지)
- ✅ 수평 확장 용이 (서버를 추가하면 됨)
- ✅ 클라이언트와 서버 간 분리

---

## 🧠 로드 밸런서가 어디에 있나요?

```
[ Client ] → [ Load Balancer ] → [ Server A / B / C ]
```

- 웹 서버 앞단, API 서버 앞단 등 **모든 트래픽 진입 지점에 위치**

---

## 🧪 주요 로드 밸런싱 알고리즘 정리

| 알고리즘                          | 설명                                   | 특징                             |
| --------------------------------- | -------------------------------------- | -------------------------------- |
| 🎲 **Round Robin**                | 서버들을 **순서대로** 순환             | 단순하고 균등하지만 성능 고려 X  |
| 🎯 **Weighted Round Robin**       | 서버마다 **가중치** 부여하여 순서 배분 | 성능 고려한 순환                 |
| 🧮 **Least Connections**          | **활성 연결 수**가 가장 적은 서버 선택 | 동시 접속 분산                   |
| 🏋️ **Weighted Least Connections** | 연결 수 + 서버 성능 고려               | 더 공정한 분산                   |
| 🕐 **Least Response Time**        | **응답 시간**이 빠른 서버 선택         | 응답 성능 중심                   |
| 🔒 **IP Hash**                    | IP로 **해시 계산 → 서버 매핑**         | 세션 유지 유리, 분산 불균형 위험 |

---

## 🎯 알고리즘별 예시 및 비교

### ✅ Round Robin

```text
요청 순서 → A → B → C → A → B → C ...
```

- 균등하게 순환하나, 서버 상태는 고려하지 않음

---

### ✅ Weighted Round Robin

```text
A: 2, B: 1 → A → A → B → A → A → B ...
```

- 더 강한 서버에 더 많은 요청 할당 가능

---

### ✅ Least Connections

- 현재 연결 수가 가장 적은 서버에 분배

```text
A: 2 connections
B: 0 connections → 여기에 분배
```

---

### ✅ Least Response Time

- 가장 빨리 응답하는 서버를 실시간 모니터링하여 선택

---

### ✅ IP Hash

- 클라이언트 IP → 해시 → 고정 서버 매핑

```text
IP 192.168.0.1 → Server A
IP 192.168.0.2 → Server B
```

- **세션 기반 서비스에 유리**
- 하지만 **부하가 불균형**할 수 있음

---

## 🧱 로드 밸런서 계층: L4 vs L7

| 계층                       | 설명                              | 특징                          |
| -------------------------- | --------------------------------- | ----------------------------- |
| **L4 (Transport Layer)**   | IP + Port 기반 TCP/UDP 로드밸런싱 | 빠르고 단순, 세션 유지 어려움 |
| **L7 (Application Layer)** | HTTP Header, URI, Cookie 기반     | 세밀한 제어, 성능 비용 ↑      |

📌 예시:

- **L4**: 클라우드 Load Balancer, NLB
- **L7**: Nginx, AWS ALB, Istio Ingress

---

## 🛠 실무 적용 예시

### 🔸 Nginx 로드 밸런서

```nginx
upstream backend {
    server backend1.example.com;
    server backend2.example.com;
}

server {
    location / {
        proxy_pass http://backend;
    }
}
```

---

### 🔸 AWS ELB (Elastic Load Balancer)

- ALB (L7): HTTP path 기반 분기
- NLB (L4): TCP 기반 로드밸런싱
- 사용자가 몰려도 안정적인 트래픽 분산

---

### 🔸 Kubernetes Service (ClusterIP / LoadBalancer)

- Kubernetes는 기본적으로 **Round Robin**
- 서비스 뒤에 있는 여러 Pod에 균등 분배

---

## ⚠️ 로드 밸런싱 실무 유의사항

1. **세션을 로컬 서버에 저장하면** → 세션 불일치 발생
   - ✅ 해결: Sticky Session, Redis 세션 저장
2. **실시간 응답 시간 기반 로직은 네트워크 지연 고려**
3. **IP 해시**는 NAT, 프록시, VPN 사용 시 IP 변경 주의!

---

## 🧠 한 줄 요약

> 로드 밸런싱은 **트래픽을 똑똑하게 잘게 쪼개는 기술**이다!

---

## 🎓 마무리 요약

| 항목      | 정리                                      |
| --------- | ----------------------------------------- |
| 목적      | 트래픽 분산, 가용성 향상                  |
| 알고리즘  | Round Robin, Least Connection, IP Hash 등 |
| 계층      | L4(속도), L7(정밀 제어)                   |
| 실무 사용 | Nginx, AWS ELB, Kubernetes 등             |

---
