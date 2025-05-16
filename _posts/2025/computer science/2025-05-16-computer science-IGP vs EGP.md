---
published: true
title: "🌐 IGP vs EGP, 그리고 AS란"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: "IGP와 EGP는 라우팅 프로토콜의 두 축입니다. 각각의 개념과 Autonomous System(AS)의 역할을 이미지와 함께 정리해봅니다."
tag: "IGP, EGP"
article_tag1: "Network"
article_section: "Routing"
meta_keywords: "IGP, EGP, AS, 라우팅 프로토콜, Autonomous System, 네트워크 백엔드"
last_modified_at: "2025-05-16 03:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

# 🌐 IGP vs EGP, 그리고 AS란 무엇인가요?

---

## 🔍 AS(Autonomous System)란?

> Autonomous System(자율 시스템)은 **하나의 네트워크 관리 주체에 의해 운영되는 라우팅 도메인**을 의미합니다.

- 하나의 ISP, 클라우드 사업자, 회사 등에서 관리
- **고유한 AS 번호(ASN)** 를 가지고 있음
- 내부 라우팅은 IGP, 외부와의 라우팅은 EGP를 사용

---

## 🧭 IGP와 EGP란?

| 구분 | 설명 |
|------|------|
| **IGP (Interior Gateway Protocol)** | **하나의 AS 내부**에서 라우팅에 사용되는 프로토콜 |
| **EGP (Exterior Gateway Protocol)** | **AS 간 통신**을 위한 라우팅 프로토콜 |

---

## 🧱 IGP (Interior Gateway Protocol)

> 한 조직 내부(= 하나의 AS 내부)에서 네트워크 경로를 결정하기 위한 프로토콜

### 주요 프로토콜
- RIP (Routing Information Protocol)
- OSPF (Open Shortest Path First)
- IS-IS (Intermediate System to Intermediate System)

### 특징
- 경로 계산이 빠름
- 복잡한 트래픽 정책 반영은 어려움

---

## 🚀 EGP (Exterior Gateway Protocol)

> 서로 다른 AS 간 라우팅 경로를 조율하기 위한 프로토콜

### 대표 프로토콜
- BGP (Border Gateway Protocol) → 유일한 EGP 표준

### 특징
- 전 세계 인터넷을 구성하는 핵심
- 경로 안정성, 정책 기반 라우팅을 중시
- 느리지만 견고한 경로 결정

---

## 🖼 구조 이해: IGP와 EGP, AS

![alt](/assets/images/post/computer science/3.png)

- 파란 원: 각 AS
- 빨간 원: 내부 라우터들 (IGP 사용)
- 두 AS 사이: EGP (BGP로 통신)

---

## 📌 예시로 이해하기

```text
회사 A: AS 65001
회사 B: AS 65002

회사 A 내부: OSPF 사용 (IGP)
회사 B 내부: IS-IS 사용 (IGP)
회사 A ↔ 회사 B: BGP로 라우팅 (EGP)
```

---

## ✅ 마무리 요약

| 개념 | 설명 |
|------|------|
| AS | 하나의 네트워크 도메인, 고유 번호 보유 |
| IGP | AS 내부 라우팅 프로토콜 |
| EGP | AS 간 외부 라우팅 (BGP) |

---
