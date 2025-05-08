---
published: true
title: "🧱 ACID 트랜잭션 이해하기"
layout: single
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
  - Computer Science
description: "ACID는 트랜잭션의 4대 속성으로, 데이터베이스가 신뢰성 있게 동작하기 위한 핵심 원칙입니다. 실무 상황과 함께 하나씩 깊이 있게 정리해보았습니다."
tag: "ACID, Database, Transaction, 트랜잭션, 일관성"
article_tag1: "트랜잭션 속성"
article_section: "DB 기초"
meta_keywords: "ACID 트랜잭션, 원자성, 일관성, 격리성, 지속성, WAL 로그, Isolation Level"
last_modified_at: "2025-05-08 01:00:00 +0800"
toc: true
toc_sticky: true
toc_label: "목차"
---

## ✅ ACID란 무엇인가?

> ACID는 데이터베이스 트랜잭션이 **정확하고 신뢰성 있게** 처리되도록 보장하는 4가지 핵심 속성입니다.

| 항목        | 설명                                         |
|-------------|----------------------------------------------|
| A - Atomicity  | 트랜잭션은 모두 성공하거나 모두 실패해야 함 |
| C - Consistency | 트랜잭션 후 DB는 항상 유효한 상태여야 함     |
| I - Isolation  | 트랜잭션은 독립적으로 실행되어야 함         |
| D - Durability | 트랜잭션 결과는 영구적으로 보존되어야 함     |

---

## 🧩 1. 원자성 (Atomicity)

> **트랜잭션은 더 이상 나눌 수 없는 최소 단위**  
> 전부 성공하거나, 전부 실패해야 합니다.

### 📌 예시: 계좌 이체

1. A 계좌에서 3000원 출금  
2. B 계좌에 3000원 입금

→ 2번에서 실패하면 1번도 **자동 롤백**되어야 합니다.

### 💡 실제 구현: Undo 로그

- RDBMS는 트랜잭션 시작 전 값을 **Undo 로그**로 저장
- 오류 발생 시, 로그를 기반으로 이전 상태로 **롤백**

---

## 🧩 2. 일관성 (Consistency)

> **트랜잭션 전후로 DB 제약 조건이 항상 유지되어야 함**

### 📌 예시: 제약 조건 위반

- `User` 테이블에 `NOT NULL` 컬럼이 있는데,  
  트랜잭션 중간에 NULL이 삽입되면 → 전체 트랜잭션 **롤백**

### 💡 실제 구현

- 무결성 검사: FK, 제약조건, 트리거 등
- 애플리케이션 → DB로 위임

---

## 🧩 3. 격리성 (Isolation)

> **동시에 실행되는 트랜잭션이 서로 간섭하지 않도록 보장**

### 📌 예시: 중간 결과 노출 방지

- A 계좌 → B 계좌 이체 중에  
  **누군가가 A의 잔고를 조회**하면 안 됨 (중간 상태 노출 방지)

### 💡 트랜잭션 간섭 문제 (Isolation Level)

| 문제 유형          | 설명                                     |
|-------------------|------------------------------------------|
| Dirty Read        | 커밋되지 않은 값 읽기                    |
| Non-repeatable Read | 한 트랜잭션 내에서 값이 바뀜             |
| Phantom Read      | 조건에 맞는 행이 생기거나 사라짐         |

### 💡 실제 제어 방법

- 격리 수준 설정 (Isolation Level)

| Level              | 설명                  |
|-------------------|----------------------|
| READ UNCOMMITTED  | 최소 보장, Dirty Read 가능 |
| READ COMMITTED    | Oracle 기본값         |
| REPEATABLE READ   | MySQL InnoDB 기본값   |
| SERIALIZABLE      | 가장 엄격, 성능 부담 ↑ |

---

## 🧩 4. 지속성 (Durability)

> **성공한 트랜잭션은 시스템이 꺼져도 반드시 저장되어야 함**

### 📌 예시

- 주문 성공 메시지 → DB 반영되었는데  
  서버가 다운되어도 → 재시작 후 데이터는 그대로 있어야 함

### 💡 실제 구현: WAL (Write-Ahead Logging)

- 트랜잭션이 커밋되면 먼저 **로그 파일(WAL)**에 기록  
- 디스크에 쓰기 완료된 후에야 트랜잭션을 성공으로 처리  
- 시스템 장애 시 → WAL을 읽어 상태 복구 가능

---

## 💬 추가로 알아두면 좋은 개념들

| 개념 | 설명 |
|------|------|
| WAL (Write-Ahead Logging) | 로그 우선 기록 → 복구를 위한 핵심 |
| CAP 이론과의 관계 | ACID는 Consistency에 집중, CAP은 분산 시스템의 트레이드오프 |
| 트랜잭션 Savepoint | 트랜잭션 내부에서 특정 지점까지 롤백 가능 |
| Auto Commit | 트랜잭션을 명시하지 않으면 자동 커밋됨 (주의!) |

---

## 🎯 실무에서는 언제 ACID를 활용하나요?

- 계좌 이체, 주문, 재고 감소 등 **절대 실패하면 안 되는 작업**
- 금융/결제/인증 등에서 **일관성과 정확성**이 중요한 경우
- 대체로 RDBMS (MySQL, PostgreSQL 등)가 기본적으로 ACID 보장

---

## 📚 정리 요약

| 속성 | 의미 | 실무 포인트 |
|------|------|--------------|
| A - 원자성 | All or Nothing | 중간 실패 → 전체 롤백 |
| C - 일관성 | 규칙 유지 | FK, 제약조건 유지 |
| I - 격리성 | 독립적 실행 | 중간 값 보지 않게 |
| D - 지속성 | 실패해도 결과 유지 | WAL로 복구 가능 |

---
