---
published: true
title: "운영체제의 CPU 스케줄링"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Backend
description: "운영체제의 핵심 기능인 CPU 스케줄링. 선점형과 비선점형 스케줄링의 차이와 다양한 스케줄링 알고리즘을 정리합니다."
tag: [OS, CPU 스케줄링, 선점형, 비선점형, 알고리즘]
article_section: "OS"
meta_keywords: "CPU Scheduling, Preemptive, Non-preemptive, FCFS, SJF, RR, SRT, Multilevel Queue, Aging"
last_modified_at: "2025-06-03 22:00:00 +0900"
toc: true
toc_sticky: true
toc_label: "목차"
---

## 🧠 CPU 스케줄링이란?

CPU 스케줄링은 운영체제가 여러 프로세스에게 CPU 자원을 효율적이고 공정하게 분배하는 작업입니다. 효율적인 스케줄링이 없으면, 긴 작업만 우선되거나 중요한 작업이 영원히 실행되지 않는 등의 문제가 생깁니다.

---

## 🔄 선점형 vs 비선점형

| 구분 | 선점형 (Preemptive) | 비선점형 (Non-preemptive) |
|------|----------------------|-----------------------------|
| 특징 | 운영체제가 CPU를 강제로 회수 가능 | 프로세스가 스스로 CPU를 반납해야 교체됨 |
| 장점 | 응답 시간 짧음, 상호작용성 좋음 | 컨텍스트 스위칭 비용 적음 |
| 단점 | 오버헤드 발생, 동기화 어려움 | 응답 시간 길 수 있음 |

---

## ⏱ 주요 CPU 스케줄링 알고리즘

### 1. FCFS (First Come First Serve)
- **비선점형**
- 큐에 들어온 순서대로 실행
- 공정하지만 긴 작업이 먼저 오면 짧은 작업은 오래 기다림 (Convoy Effect)

### 2. SJF (Shortest Job First)
- **비선점형**
- 실행 시간이 가장 짧은 프로세스 우선
- 평균 대기시간 최소화
- 단점: 긴 작업이 기아 상태에 빠질 수 있음

### 3. Round Robin (RR)
- **선점형**
- 각 프로세스는 정해진 시간만큼 실행 (타임 슬라이스)
- 짧은 응답 시간 보장
- 타임 슬라이스 선택이 중요

### 4. SRT (Shortest Remaining Time)
- **선점형**
- 실행 중에도 더 짧은 프로세스가 들어오면 CPU를 양보
- 평균 대기시간 최소화
- 기아 현상 발생 가능

### 5. Multilevel Queue
- **비선점/선점 혼합 가능**
- 우선순위 별 큐 분리
- 각각의 큐에 서로 다른 스케줄링 알고리즘 사용 가능
- 단점: 우선순위 낮은 큐에 기아 현상 발생 가능

### 6. Multilevel Feedback Queue
- **선점형**
- Multilevel Queue + Aging
- 오래 대기 중인 프로세스는 우선순위를 상승시킴

---

## 🧓 Aging 기법이란?

기아(Starvation)를 막기 위한 방식. 오래 기다린 프로세스의 우선순위를 점점 높이는 기법입니다.

---

## ✅ 추가로 알아두면 좋은 개념들

- **Context Switching**: CPU를 다른 프로세스에 넘길 때의 오버헤드
- **Burst Time**: 프로세스가 CPU를 사용하는 데 걸리는 시간
- **Turnaround Time**: 프로세스 생성부터 완료까지 걸리는 시간
- **Waiting Time**: 프로세스가 큐에서 기다리는 시간

---

## 📌 결론

- CPU 스케줄링은 운영체제의 핵심 기능
- 다양한 알고리즘은 각각의 목적과 특성이 있음
- 기아 현상, 응답 시간, 효율성 등을 고려해 스케줄링 방식을 설계해야 함
