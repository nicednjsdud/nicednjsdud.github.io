---
published: true
title: "🌐 REST API란 무엇인가 그리고 SOAP, Modbus와의 비교"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: "REST의 기본 개념부터 장단점, 실무에서 어떻게 사용되는지 그리고 SOAP, GraphQL, Modbus와 어떤 차이가 있는지를 쉽게 정리했습니다."
tag: "REST, API, SOAP, Modbus, 통신 프로토콜"
article_tag1: "REST API"
article_section: "웹 통신"
meta_keywords: "REST, API 비교, SOAP, GraphQL, Modbus, JSON, HTTP"
last_modified_at: "2025-05-13 01:10:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

## ✅ REST란?

> REST(Representational State Transfer)란 **자원의 표현을 이용해 상태를 주고받는 아키텍처 스타일**입니다.

- **자원(Resource)**: 서버가 관리하는 모든 것 (예: user, order, product)
- **표현(Representation)**: 자원을 표현하는 방식 (보통 JSON, XML)
- **전송(Transfer)**: HTTP를 통해 상태 변화 정보 전송

---

## 🧪 REST의 동작 방식

| 구성 요소 | 역할 |
|-----------|------|
| URI       | 자원을 식별 (`/orders/1`) |
| HTTP METHOD | 행위를 표현 (`GET`, `POST`, `PUT`, `DELETE`) |
| JSON       | 메시지 포맷 (요청/응답에 사용) |

---

## 🎯 REST API 예시

```
GET    /orders       → 주문 목록 조회
GET    /orders/1     → 특정 주문 조회
POST   /orders       → 주문 생성
PUT    /orders/1     → 주문 수정
DELETE /orders/1     → 주문 삭제
```

---

## ⚖️ REST의 장단점

### ✅ 장점

- 🌍 **플랫폼 독립성**: 브라우저, 앱, 서버 등 어디서든 사용 가능
- 🔗 **HTTP 기반**: 표준 프로토콜 → 테스트와 연동 용이 (CURL, Postman)
- 🎯 **자원 중심 설계**: URI로 명확하게 표현
- 🔄 **하위 호환성 우수**: JSON은 자기서술적 구조

### ❌ 단점

- ⛓ **복잡한 요청 구성 어려움**: 1 요청에 여러 자원 동시 처리 불가
- 🔂 **오버페치/언더페치 문제**: 필요한 데이터만 가져오기 어려움
- 🧱 **메시지 오버헤드**: JSON은 가볍지만 **텍스트 기반이라 무거울 수 있음**

---

## 📦 다른 API/통신 방식들과의 비교

### 🧼 SOAP (Simple Object Access Protocol)

- XML 기반의 **엄격한 메시지 구조**
- **HTTP 외에도 SMTP, FTP 등 다양한 전송 가능**
- 계약 기반 (WSDL 사용)
- ✅ 장점: 보안, 트랜잭션 처리 강력  
- ❌ 단점: 복잡함, 무겁고 느림 (XML 사용)

### 🧪 GraphQL

- **1 요청에 여러 자원 요청 가능**
- 원하는 필드만 선택해 가져올 수 있음 → Overfetch 문제 해결
- 단일 Endpoint(`/graphql`)
- ✅ 장점: 클라이언트 맞춤형 응답
- ❌ 단점: 캐싱 어렵고 학습 난이도 있음

### ⚙️ Modbus

- 산업 제어 시스템(PLC 등)에서 사용되는 **직렬/이더넷 통신 프로토콜**
- 명령어 단위로 데이터 주고받음 (읽기/쓰기)
- 매우 가볍고 실시간 처리에 적합
- ✅ 장점: 임베디드/공정 시스템에서 빠르고 효율적
- ❌ 단점: 보안 없음, REST처럼 구조화된 API 아님

---

## 🔍 요약 비교표

| 프로토콜 | 전송 방식 | 포맷 | 장점 | 단점 |
|----------|-----------|------|------|------|
| REST     | HTTP      | JSON | 단순, 표준화 | 복잡한 요청 어렵 |
| SOAP     | HTTP, SMTP 등 | XML | 보안, 트랜잭션 | 무거움, 복잡함 |
| GraphQL  | HTTP      | JSON | 필요한 데이터만 선택 | 캐싱 어려움 |
| Modbus   | TCP/Serial | 바이너리 | 빠르고 단순 | 보안 취약, 범용 아님 |

---

## 📌 실무에서 선택 기준은?

| 상황 | 추천 방식 |
|------|------------|
| 간단한 CRUD + 범용 API | REST |
| 엄격한 계약, 보안, 트랜잭션 | SOAP |
| 모바일/프론트에서 요청 최적화 | GraphQL |
| 공장 자동화, IoT 센서 통신 | Modbus |

---

## 🧠 추가로 알아두면 좋은 것

- REST는 아키텍처 스타일일 뿐, 표준은 아님
- RESTful하지 않은 REST API도 많음 (ex: `/getUserList`)
- REST가 불편할 땐 GraphQL이나 gRPC도 고려

---

## ✅ 마무리 정리

REST는 지금도 가장 널리 쓰이는 API 설계 방식입니다.  
하지만, 목적과 상황에 따라 SOAP, GraphQL, gRPC, Modbus 등 **다양한 통신 방식**이 존재합니다.

> REST가 만능은 아니며, **각 방식은 목적에 따라 선택되어야 합니다.**

---