---
published: true
title: "🧠 왜 Redis는 단일 스레드일까"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Redis
description: "Redis는 왜 단일 스레드로 작동할까? 그 이유는 동시성 제어를 간소화하고 성능을 극대화하기 위한 전략적인 설계에 있다. 그림과 함께 이해해보자."
tag: "Redis, 싱글 스레드, 성능, 동시성"
article_tag1: "Backend"
article_section: "Redis 아키텍처"
meta_keywords: "Redis 단일 스레드, 이벤트 루프, 멀티스레드, Redis 6.0, 싱글스레드, Redis 성능"
last_modified_at: "2025-05-18 03:10:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

## 🔍 핵심 요약

> Redis는 왜 멀티스레드가 아닌 **단일 스레드(single-threaded)** 로 설계되었을까?  
> 이유는 단순하다: **빠르고 안전하게 동작하기 위해서**다.

---

## 💡 Redis 아키텍처 개요

![alt](/assets/images/post/computer science/4.png)

- 모든 명령은 **하나의 스레드(Event Loop)** 에서 순차적으로 처리됨
- 클라이언트 요청은 **I/O 멀티플렉싱** 으로 비동기 처리
- Redis 6.0부터 **네트워크 I/O는 멀티스레드 지원**, 실행 로직은 여전히 단일 스레드

---

## ✅ 단일 스레드의 장점

### 1️⃣ 동시성 문제 해소

- 멀티스레드 환경에서는 **Race Condition, Deadlock** 등 처리 복잡도 ↑
- 단일 스레드는 이러한 문제에서 **자연스럽게 자유로움**

### 2️⃣ 데이터 일관성 보장

- 모든 명령이 **순차적으로 처리**
- 별도 락 없이도 Atomic(원자성) 보장  
  👉 트랜잭션/복합 연산에서도 안전

### 3️⃣ 성능 최적화

- Redis는 대부분의 작업이 **메모리 내 처리 (RAM)**
- CPU 자원 중 오히려 락과 컨텍스트 스위칭이 **병목 요인**
- 단일 스레드는 **컨텍스트 스위칭 오버헤드 최소화**

---

## ⚙️ Redis의 이벤트 루프(Event Loop)

```text
클라이언트 요청 수신
↓
네트워크 I/O 처리 (epoll/kqueue 등)
↓
요청 큐에 쌓임
↓
단일 스레드가 명령어를 하나씩 순차 처리
↓
결과를 다시 비동기로 응답
```

- 실제로는 하나의 스레드가 수천 개의 클라이언트를 처리 가능
- **동시 접속 수는 많지만, 실제 병렬 작업은 없음**

---

## 🚀 Redis 6.0 이후 - 네트워크 I/O 멀티스레드

- `--io-threads` 옵션 도입
- **클라이언트의 요청 수신/응답 처리**는 병렬화됨
- 하지만, **명령 실행 로직 자체는 여전히 단일 스레드**

```text
🛡️ 결과적으로 여전히 Redis는
데이터 처리에 있어 "Atomic" 을 보장
```

---

## 📌 언제 단일 스레드가 병목이 될 수 있을까?

| 상황 | 대안 |
|------|------|
| 느린 명령이 많을 때 | 명령 최적화, Redis Cluster 사용 |
| 네트워크 병목 시 | `--io-threads`로 I/O 병렬 처리 |
| 데이터 처리량이 매우 높은 경우 | Sharding, Redis Sentinel/Cluster 활용 |

---

## 🧠 마무리 정리

| 항목 | 설명 |
|------|------|
| 설계 목적 | 성능 최적화 + 동시성 단순화 |
| 장점 | 안정성, 예측 가능, 빠름 |
| 단점 | CPU 코어 한계, 느린 명령 병목 |
| Redis 6.0 이후 | 네트워크 I/O는 멀티스레드, 처리 로직은 단일 |

---

