---
published: true
title: "⏱ 동시성과 병렬성"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Backend
  - System
  - Spring
description: "동시성과 병렬성의 개념을 쉽게 정리하고, Spring에서 비동기/병렬 아키텍처를 실제로 어떻게 구성하는지 도식과 함께 정리했습니다."
tag: "동시성, 병렬성, 비동기, 병렬 처리, 스프링"
article_tag1: "Concurrency vs Parallelism"
article_section: "Backend Architecture"
meta_keywords: "동시성 병렬성 차이, Spring Async Parallel, 스레드, WebFlux, Executor"
last_modified_at: "2025-05-05 23:55:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# ⏱ 동시성과 병렬성 완전 정복 + Spring 실무 아키텍처 비교

---

## ✅ 동시성 (Concurrency)이란?

> **논리적으로 동시에 처리되도록 보이게 만드는 기술**  
> 하나의 CPU(코어)가 작업을 빠르게 **번갈아가며 처리**하는 구조입니다.

📌 대표 예시:

- 웹 서버가 여러 요청을 동시에 처리하는 것처럼 보이지만, 사실은 빠르게 번갈아 처리
- `@Async`, `CompletableFuture` 등은 이 구조 기반

---

## ✅ 병렬성 (Parallelism)이란?

> **물리적으로 여러 코어가 동시에 작업을 처리하는 것**

📌 대표 예시:

- CPU 코어 4개 → 각각 별도의 계산을 동시에 처리
- Java `parallelStream()`, `ForkJoinPool` 등이 여기에 해당

---

## 🎯 동시성과 병렬성 비교

| 항목         | 동시성                   | 병렬성                  |
| ------------ | ------------------------ | ----------------------- |
| 실행 방식    | 교대로 처리              | 동시에 처리             |
| 자원         | CPU 시간                 | CPU 코어                |
| 주로 쓰는 곳 | I/O 중심 서버, 요청 분산 | 계산, 이미지 처리, 분석 |
| 장점         | 응답성 향상              | 성능 극대화             |
| 단점         | 동기화 복잡성            | 자원 경합, 오버헤드     |

---

## 🧪 실무 예시 비교

### 🔸 동시성 (Spring @Async)

```java
@Async
public CompletableFuture<User> findUserAsync() {
    return CompletableFuture.supplyAsync(() -> userRepository.findById(1L));
}
```

- **논리적 동시 실행**
- I/O 동안 다른 요청 처리 가능

---

### 🔸 병렬성 (Java Parallel Stream)

```java
List<Integer> input = List.of(1,2,3,4);
input.parallelStream().map(this::processHeavyTask).collect(Collectors.toList());
```

- **물리적으로 병렬 실행 (멀티코어 분산)**

---

## 🧠 Spring 비동기 처리 vs 병렬 처리 아키텍처 비교

### ✅ 비동기 처리 (I/O 중심)

```text
[Client]
   ↓
[Controller] ---(@Async)---> [Service (Thread)]
   ↓                        ↘
응답 먼저 반환             [DB/API 요청 → 대기]
                             ↘
                          [결과 처리 후 Callback]
```

- `@Async`, `CompletableFuture` 기반
- Thread Pool(`TaskExecutor`) 활용
- 응답성을 높이는 데 적합 (I/O가 많을 때)

---

### ✅ 병렬 처리 (CPU 중심)

```text
[Controller]
   ↓
[Service]
   ├── process1() ─▶ Core 1
   ├── process2() ─▶ Core 2
   └── process3() ─▶ Core 3
```

- `parallelStream()`, `ForkJoinPool` 등 사용
- **동시에 계산 처리**
- 대량 연산, 이미지 처리 등에 적합

---

## 🔍 도식 요약

| 항목    | 비동기 처리 (@Async 등) | 병렬 처리 (parallelStream 등)   |
| ------- | ----------------------- | ------------------------------- |
| 목적    | I/O 대기 해소           | CPU 계산 분산                   |
| 대상    | DB/API 등 외부 호출     | 계산, 변환, 압축                |
| 방식    | Thread → Callback       | 멀티코어 병렬 처리              |
| 실무 예 | 알림, 로그, 이메일      | 추천 시스템, 대용량 데이터 변환 |
| 장점    | 응답 속도 향상          | 처리 속도 향상                  |
| 단점    | 콜백 구조 복잡          | 동기화 비용, 공유자원 문제      |

---

## 🚨 실무 팁

- ✅ I/O 작업은 비동기로, 계산/변환은 병렬로
- ✅ 공유 리소스는 최소화 or 동기화 처리 필수
- ✅ 병렬이 항상 빠르지 않다: 스레드 전환, 동기화 비용 주의
- ✅ 스레드 풀 크기와 코어 수 튜닝 중요

---

## 🧠 추가로 알아두면 좋은 개념

- **Context Switching**: CPU가 다른 스레드로 바뀔 때 → 오버헤드
- **Race Condition**: 두 스레드가 동시에 변수 접근 → 예외
- **Deadlock**: 서로 락 걸고 기다리다 무한 대기
- **ThreadLocal**: 스레드마다 고유 데이터를 보관할 때 사용

---

## ✅ 마무리 정리

| 개념               | 요약                              |
| ------------------ | --------------------------------- |
| 동시성             | 스레드를 빠르게 전환하여 I/O 대응 |
| 병렬성             | 물리적으로 동시에 계산 수행       |
| Spring 비동기 처리 | 응답 우선 처리, I/O 효율화        |
| Spring 병렬 처리   | 계산 작업을 빠르게 분산           |

---
